---
title: Tutorial - Azure AI Video Indexer enabled by Arc
description: This tutorial shows you how to deploy Azure Video Indexer with Arc.
ms.topic: tutorial
ms.service: azure-video-indexer
ms.date: 10/30/2023
ms.author: inhenkel
author: IngridAtMicrosoft
---

# Tutorial: Try Azure Video Indexer enabled by Arc

Azure Video Indexer enabled by Arc ([!INCLUDE [variable-edge-product-name](includes/variable-edge-product-name.md)]) is an Azure Arc Extension Enabled Service that runs video and audio analysis on edge devices. The solution is designed to run on Azure Stack Edge Profile, a heavy edge device, and supports many video formats, including MP4 and other common formats. The solution supports several languages in all basic audio-related models. It assumes that one Video Indexer resource is mapped to one extension.

This tutorial walks you through the steps required to enable Video Indexer as an Arc extension on your current infrastructure.

## Prerequisites

> [!IMPORTANT]
> To successfully deploy the Azure Video Indexer extension, it is **mandatory** that your Azure subscription id is approved in advance. You must first sign up using [this form](https://aka.ms/vi-register).

- Review the [!INCLUDE [variable-edge-product-name](includes/variable-edge-product-name.md)][ overview](azure-video-indexer-enabled-by-arc-overview.md).
- Set up the following things before you attempt the rest of this tutorial:
    - Create an Azure subscription with permissions to create Azure resources.
    - Create an Azure Video Indexer Account. Use the [Create Video Indexer account](create-account-portal.md) tutorial.
    - Install the latest version of the [Azure CLI](/cli/azure/install-azure-cli). (You can skip this step if you're using Cloud Shell.)
    - **If not using Cloud Shell**, install the latest version of *connectedk8s* Azure CLI extension. Use the following command.
    
        ```bash
        az extension add --name connectedk8s
        ```

> [!IMPORTANT]
> The AKS cluster contains the Video Indexer extension must be in the East US region.

## Minimum hardware requirements

The following list is the minimum and recommended requirements if the extension contains single language support. If you install multiple speech and translation containers with several languages, increase the hardware requirements accordingly.

| Component | Minimum Requirements | Recommended Requirements
| --- | --- | --- |
| VM Count | 1 | 2
| CPU (Per Cluster)| 16 cores | 32 cores | 
| RAM (Per Cluster)| 32 GB | 64 GB |
| Storage | 30 GB | 50 GB |

> [!Note] 
> At least a 2-node cluster is recommended for high availability and scalability. The recommended settings refer to cluster wide settings, so for example, if you have 2 nodes, each node should have 16 cores and 32 GB of RAM.

> [!TIP] 
> We recommend creating a dedicate node-pool / auto-scaling groups to host the VI Solution

### Minimum software requirements

| Component |  Minimum Requirements |
| --- | --- |
| Operating System | Ubuntu 20.04 LTS or any Linux Compatible OS |
| Kubernetes | 1.24 |
| Azure CLI | 2.4.0 |

## Prepare for deployment

During the deployment, the script asks for environment specific values. Have these values ready so you can copy and paste them when the script asks for them. 

| Question | Value | Details
| --- | --- | --- |
| What is the Video Indexer account ID during deployment? | GUID | Your Video Indexer Account ID |
| What is the Azure subscription ID during deployment? | GUID | Your Azure Subscription ID |
| What is the name of the Video Indexer resource group during deployment? | string | The Resource Group Name of your Video Indexer Account |
| What is the name of the Video Indexer account during deployment? | string | Your Video Indexer Account name |

> [!WARNING]
> This sample environment is **NOT** meant to be used in production and only provided to quickly test functionality. Be certain to restrict access to the IP addresses in the environment to prevent security issues.

## [One-click deployment](#tab/oneclick)

## One-Click Deploy Sample to Azure

If you would like to test the extension on a sample edge device, this deployment script can be used to quickly set up a K8S cluster and all pods to run Azure Video Indexer. This script does the following things:

- Creates a small two node AKS Cluster (costs are ~$0.80/hour)
- Enables ARC Extension on top of the cluster
- Adds Video Indexer Arc Extension
- Adds Video Indexer and Cognitive Services Speech + Translation containers
- Exposes the Video Indexer Swagger API for data plane operations

You can read more on how to set up your Cloud Shell environment [here](/azure/cloud-shell/quickstart?tabs=azurecli).

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://shell.azure.com/bash?url=)

In Cloud Shell execute these two commands:

```bash
curl -sSL https://github.com/Azure-Samples/media-services-video-indexer/blob/master/AVIenabledbyArc/vi-edge-deployment-script.sh -o install_vi_arc.sh
```

```bash
sh install_vi_arc.sh
```

When finished, you can use the URL of the new Video Indexer extension running on the AKS cluster to perform test Video Indexer on Edge.

## [Manual deployment](#tab/manual)

## Manual deployment

Follow these steps to deploy the Video Indexer Arc Extension to your Arc K8S Enabled cluster. 

### Step 1 - Create Azure Arc Kubernetes Cluster and connect it to your cluster

> [!Note] 
> The following command assumes you have a Kubernetes cluster and that the current context on your ./kube/config file points to it.

Run the following command to connect your cluster. This command deploys the Azure Arc agents to the cluster and installs Helm v. 3.6.3 to the *.azure* folder of the deployment machine. This Helm 3 installation is only used for Azure Arc, and it doesn't remove or change any previously installed versions of Helm on the machine.

```bash
az connectedk8s connect --name myAKSCluster --resource-group myResourceGroup
```

> [!TIP] 
> Follow the article [how to connect your cluster to Azure Arc](/azure/azure-arc/kubernetes/quickstart-connect-cluster?tabs=azure-cli) on Azure Docs for a complete walkthrough of this process.

### Step 2 - Create Cognitive Services Resources for the extension

> [!NOTE] 
> The resources are created once per each subscription, and used by all the extensions under that subscription. 

One of the prerequisites of installing an Azure Video Indexer Arc extension are speech and translator resources. Once the resources are created, their key and endpoint need to be provided during the installation process. The resources are created once per subscription.

Run the following commands:

```bash
$Subscription="<your subscription ID>"
$ResourceGroup="<your resource group name"
$AccountName="<your account name>"
az rest --method post --verbose --uri https://management.azure.com/subscriptions/${Subscription}/resourceGroups/${ResourceGroup}/providers/Microsoft.VideoIndexer/accounts/${AccountName}/CreateExtensionDependencies?api-version=2023-06-02-preview
```

If the response is "accepted" (202), the resources are being created. You can track their provisioning state by polling the location header returned in the response from the previous call. Alternatively, you can wait for one minute, and proceed to the next step.

```bash
az rest --method get --uri <the uri from the location response header>
```

If the response is "conflict" (409), it means the resources already exist for your subscription and you can proceed to the below command without waiting. Once the resources have been created, get their data using this command: 

```bash
az rest --method post --uri  https://management.azure.com/subscriptions/${Subscription}/resourceGroups/${ResourceGroup}/providers/Microsoft.VideoIndexer/accounts/${AccountName}/ListExtensionDependenciesData?api-version=2023-06-02-preview
```

The response comes in the following format:
 
```json
{
    "speechCognitiveServicesPrimaryKey": "<key>",
    "speechCognitiveServicesSecondaryKey": "<key>",
    "translatorCognitiveServicesPrimaryKey": "<key>",
    "translatorCognitiveServicesSecondaryKey": "<key>",
    "speechCognitiveServicesEndpoint": "<uri>",
    "translatorCognitiveServicesEndpoint": "<uri>"
}
```
Use this data in the next step. 

### Step 3 - Create Azure Arc Video Indexer Extension

The following parameters are used as input to the extension creation command: 

| Parameter | Default | Description |
|-----------|---------|-------------|
| release-namespace | yes | The Kubernetes namespace that the extension is installed into | 
| cluster-name | | The Kubernetes Azure Arc instance name |
| resource-group | | The Kubernetes Azure Arc resource group name |
| version | latest | Video Indexer Extension version |
| speech.endpointUri |  | Speech Service Url Endpoint |
| speech.secret |  | Speech Instance secret |
| translate.endpointUri |  | Translation Service Url Endpoint  |
| translate.secret |  | Translation Service secret |
| videoIndexer.accountId |  | Video Indexer Account ID |
| frontend.endpointUri |  | Video Indexer Dns Name to be used as the Portal endpoint |

```bash
az k8s-extension create --name videoindexer \
    --extension-type Microsoft.videoindexer \
    --scope cluster \
    --release-namespace ${namespace} \
    --cluster-name ${connectedClusterName} \
    --resource-group ${connectedClusterRg} \
    --cluster-type connectedClusters \
    --release-train viextensiondemo  \
    --version ${version} \
    --auto-upgrade-minor-version false \
    --config-protected-settings "speech.endpointUri=${speechUri}" \
    --config-protected-settings "speech.secret=${speechSecret}" \
    --config-protected-settings "translate.endpointUri=${translateUri}" \
    --config-protected-settings "translate.secret=${translateSecret}" \
    --config "videoIndexer.accountId=${viAccountId}" \
    --config "frontend.endpointUri=${dnsName}" \
    --config "storage.storageClass=azurefile-csi"
```

There are other parameters that can be used to have a more fine grained control on the extension creation:

| Parameter | Default | Description |
|-----------|---------|-------------|
| AI.nodeSelector | - | The node Selector label on which the AI Pods (speech and translate) are assigned to | 
| speech.resource.requests.cpu | 1 | The requested number of cores for the speech pod |
| speech.resource.requests.mem | 2Gi | The requested memory capacity for the speech pod |
| speech.resource.limits.cpu | 2 | The limits number of cores for the speech pod. must be > speech.resource.requests.cpu  |
| speech.resource.limits.mem | 3Gi | The limits memory capacity for the speech pod. must be > speech.resource.requests.mem  |
| translate.resource.requests.cpu | 1 | The requested number of cores for the translate pod |
| translate.resource.requests.mem | 16Gi | The requested memory capacity for the translate pod |
| translate.resource.limits.cpu | -- | The limits number of cores for the translate pod. must be > translate.resource.requests.cpu  |
| translate.resource.limits.mem | -- | The limits memory capacity for the translate pod. must be > translate.resource.requests.mem  |
| videoIndexer.webapi.resources.requests.cpu | 0.5 | The request number of cores for the web api pod  |
| videoIndexer.webapi.resources.requests.mem | 4Gi | The request memory capacity for the web api pod  |
| videoIndexer.webapi.resources.limits.cpu | 1 | The limits number of cores for the web api pod  |
| videoIndexer.webapi.resources.limits.mem | 6Gi | The limits memory capacity for the web api pod  |
| videoIndexer.webapi.resources.limits.mem | 6Gi | The limits memory capacity for the web api pod  |
| storage.storageClass | "" | The storage class to be used |
| storage.useExternalPvc | false | determines whether an external PVC is used. if true, the VideoIndexer PVC isn't installed |

Here's an example deployment script: 

```bash
az k8s-extension create --name videoindexer \
    --extension-type Microsoft.videoindexer \
    .......
    --config AI.nodeSelector."beta\\.kubernetes\\.io/os"=linux
    --config "speech.resource.requests.cpu=500m" \
    --config "speech.resource.requests.mem=2Gi" \
    --config "speech.resource.limits.cpu=1" \
    --config "speech.resource.limits.mem=4Gi" \
    --config "videoIndexer.webapi.resources.requests.mem=4Gi"\
    --config "videoIndexer.webapi.resources.limits.mem=8Gi"\
    --config "videoIndexer.webapi.resources.limits.cpu=1"\ 
```

### Step 4 - Verify Deployment

```bash
kubectl get pods -n video-indexer
```

## Updating the extension

The following command can be used to update the extension with either another version or with different configuration parameters, if needed. You must specify the cluster name and resource group name.

```bash
az k8s-extension update --name videoindexer \
    --cluster-name ${connectedClusterName} \
    --resource-group ${connectedClusterRg} \
    --cluster-type connectedClusters \
    --release-train ${releaseTrain}  \
    --version ${version} \
    --config "speech.resource.requests.cpu=500m"                        
```
---

[!INCLUDE [footer](includes/footer.md)]