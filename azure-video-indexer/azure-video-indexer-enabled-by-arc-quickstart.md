---
title: Try Azure Video Indexer enabled by Arc
description: This article walks you through the steps required to enable Video Indexer as an Arc extension on your current infrastructure.
ms.topic: quickstart
ms.service: azure-video-indexer
ms.date: 1/2/2024
ms.author: inhenkel
author: IngridAtMicrosoft
---

# Try Azure Video Indexer enabled by Arc

Azure Video Indexer enabled by Arc ([!INCLUDE [variable-edge-product-name](includes/variable-edge-product-name.md)]) is an Azure Arc Extension Enabled Service that runs video and audio analysis on edge devices. The solution is designed to run on Azure Stack Edge Profile, a heavy edge device, and supports many video formats, including MP4 and other common formats. The solution supports several languages in all basic audio-related models. It assumes that one Video Indexer resource is mapped to one extension.

This article walks you through the steps required to enable Video Indexer as an Arc extension on your current infrastructure.

## Prerequisites

> [!IMPORTANT]
> To successfully deploy the Azure Video Indexer extension, it is **mandatory** that your Azure subscription id is approved in advance. You must first sign up using [this form](https://aka.ms/vi-register).

- Create an Azure subscription with permissions to create Azure resources.
- Create an Azure Video Indexer Account. Use the [Create Video Indexer account](create-account-portal.md) tutorial.

To use the Video Indexer extension, you need to have an externally facing endpoint, which can be either a DNS name or IP. The endpoint should be set as a secure transfer protocol (`https:\\`) and is used as the extension API endpoint, formatted as `https:\\{endpointUri}/swagger/index.html`. It is also used by the Video Indexer web portal to communicate with the extension. It is recommended that you use an ingress control to manage the endpoint. 

> [!NOTE]
> If the endpoint is not publicly accessible, you will not be able to perform actions on the extension from the web portal.

> [!IMPORTANT]
> The AKS cluster contains the Video Indexer extension must be in the East US region.

## Minimum hardware requirements

The following list is the minimum and recommended requirements if the extension contains single language support. If you install multiple speech and translation containers with several languages, increase the hardware requirements accordingly.

| Configuration | VM Count | Node CPU Cores Count  | Node Ram | Node Storage | Remarks
| --- | --- | --- | --- | --- | --- |
| Minimum | 1 | 32 Cores | 64 GB | 50 GB | Storage needs to support `ReadWriteMany` Storage Class |
| Recommended | 2 | 48-64 Cores | 256 GB | 100 GB | Storage needs to support `ReadWriteMany` Storage Class |

> [!Note] 
> At least a 2-node cluster is recommended for high availability and scalability. The recommended settings refer to cluster wide settings, so for example, if you have 2 nodes, each node should have 16 cores and 32 GB of RAM.

> [!TIP] 
> We recommend creating a dedicated node-pool / auto-scaling groups to host the VI Solution

### Minimum software requirements

| Component |  Minimum Requirements |
| --- | --- |
| Operating System | Ubuntu 22.04 LTS or any Linux Compatible OS |
| Kubernetes | 1.26 |
| Azure CLI | 2.48.0 |

## Parameter definitions

| Parameter | Default | Description |
| --------- | ------- | ----------- |
| release-namespace | yes | The Kubernetes namespace that the extension is installed into |
| cluster-name |  | The Kubernetes Azure Arc instance name
| resource-group |  | The Kubernetes Azure Arc resource group name
| version | yes | Video Indexer Extension version, leave empty for latest |
| speech.endpointUri |  | Speech Service Url Endpoint (link)
| speech.secret |  | Speech Instance secret (link) |
| translate.endpointUri |  | Translation Service Url Endpoint (link)
| translate.secret |  | Translation Service secret (link)
| ocr.endpointUri |  | OCR Service Url Endpoint (link)
| ocr.secret |  |OCR Service secret (link) |
| videoIndexer.accountId |  | Video Indexer Account ID |
| videoIndexer.endpointUri |  | Dns Name or IP to be used as the extension external endpoint.|

## Prepare for deployment

During the deployment, the script asks for environment specific values. Have these values ready so you can copy and paste them when the script asks for them. 

| Question | Value | Details
| --- | --- | --- |
| What is the Video Indexer account ID during deployment? | GUID | Your Video Indexer Account ID |
| What is the Azure subscription ID during deployment? | GUID | Your Azure Subscription ID |
| What is the name of the Video Indexer resource group during deployment? | string | The Resource Group Name of your Video Indexer Account |
| What is the name of the Video Indexer account during deployment? | string | Your Video Indexer Account name | 

## [Deploy in Azure Portal](#tab/portal)

1. In the Azure portal, navigate to your Azure Arc-connected cluster.
1. From the menu, select **Extensions** > **+ Add** > **Azure Video Indexer Arc Extension**.
1. Select **Create**. The *Create an AI Video Indexer extension* screen will appear.
1. Configure the extension in *Instance details*:
    1. Select the **subscription** and **resource group** for your extension.
    1. Select the **region and connected** k8 cluster.
    1. Enter a **name** for your extension.
    1. Select the **Azure Video Indexer Account** that the extension will be connected to.
    1. Enter the **cluster endpoint**, either an IP or DNS Name to be used as the API endpoint.
    1. Provide the **storage class** you want to use for the extension that's supported by your Kubernetes distribution. For example, if you're using AKS, you could use `azurefile-cli`. For more information on predefined storage classes supported by AKS, see [Storage Classes in AKS](/azure/aks/concepts-storage#storage-classes). If you're using other Kubernetes distributions, see your Kubernetes distribution documentation for predefined storage classes supported or the way you can provide your own.
1. Select **Review + create** and then **Create**.

<!------------------------------------------------------>

## [Manual deployment](#tab/manual)

## Manual deployment

Follow these steps to deploy the Video Indexer Arc Extension to your Arc K8S Enabled cluster. Before you get started here are some things to keep in mind:

- **Storage class** - Video Indexer extension requires that a storage volume must be available on the Kubernetes cluster. The storage class needs to support `ReadWriteMany`. It's important to note that the indexing process is IO intensive, so the IOPS (input/output operations per second) of the storage volume will have a significant impact on the duration of the process.
- **Managed AI resources** - Some Azure AI resources (Translator, Transcription and OCR) will be created on the Microsoft tenant. These resources are for your subscription only and are under a pay-as-you-go model. If you already have an AI Video Indexer Arc-enabled resource in your subscription, it will be associated with existing Azure AI resources.

### Step 1 - Create Azure Arc Kubernetes Cluster and connect it to your cluster

> [!Note] 
> The following command assumes you have a Kubernetes cluster and that the current context on your ./kube/config file points to it.

Run the following command to connect your cluster. This command deploys the Azure Arc agents to the cluster and installs Helm v. 3.6.3 to the *.azure* folder of the deployment machine. This Helm 3 installation is only used for Azure Arc, and it doesn't remove or change any previously installed versions of Helm on the machine.

```bash
az connectedk8s connect --name myAKSCluster --resource-group myResourceGroup
```

> [!TIP] 
> Follow the article [how to connect your cluster to Azure Arc](/azure/azure-arc/kubernetes/quickstart-connect-cluster?tabs=azure-cli) on Azure Docs for a complete walkthrough of this process.

### Step 2 - Create Azure Arc Video Indexer Extension

```bash
az k8s-extension create --name videoindexer \
    --extension-type Microsoft.videoindexer \
    --scope cluster \
    --release-namespace ${namespace} \
    --cluster-name ${connectedClusterName} \
    --resource-group ${connectedClusterRg} \
    --cluster-type connectedClusters \
    --version ${version} \
    --auto-upgrade-minor-version false \
    --config-protected-settings "speech.endpointUri=${speechUri}" \
    --config-protected-settings "speech.secret=${speechSecret}" \
    --config-protected-settings "translate.endpointUri=${translateUri}" \
    --config-protected-settings "translate.secret=${translateSecret}" \
    --config-protected-settings "ocr.endpointUri=$($csResourcesData.ocrCognitiveServicesEndpoint)" `
    --config-protected-settings "ocr.secret=$($csResourcesData.ocrCognitiveServicesPrimaryKey)" `
    --config "videoIndexer.accountId=${viAccountId}" \
    --config "frontend.endpointUri=${dnsName}" \
    --config "storage.storageClass=azurefile-csi"
```

## Create and get resource keys

### Create AI resources keys 

```
$Subscription="<your subscription ID>"
$ResourceGroup="<your resource group name"
$AccountName="<your account name>"

az rest --method post --verbose --uri https://management.azure.com/subscriptions/${Subscription}/resourceGroups/${ResourceGroup}/providers/Microsoft.VideoIndexer/accounts/${AccountName}/CreateExtensionDependencies?api-version=2023-06-02-preview

```

When the response to a request is "accepted" (202), it means that the resources are currently being created. To track the provisioning state of these resources, you can poll the location header that was returned in the response from the previous call. Typically, this process requires waiting for approximately one minute.

A response of type "conflict" (409) means the resources already exist for the subscription, use the get command to retrive the keys.  

### Get AI resources keys

```
$Subscription="<your subscription ID>"
$ResourceGroup="<your resource group name"
$AccountName="<your account name>" 

az rest --method post --uri  https://management.azure.com/subscriptions/${Subscription}/resourceGroups/${ResourceGroup}/providers/Microsoft.VideoIndexer/accounts/${AccountName}/ListExtensionDependenciesData?api-version=2023-06-02-preview
```
 
Response format:
```json
{
    "speechCognitiveServicesPrimaryKey": "<key>",
    "speechCognitiveServicesSecondaryKey": "<key>",
    "translatorCognitiveServicesPrimaryKey": "<key>",
    "translatorCognitiveServicesSecondaryKey": "<key>",
    "speechCognitiveServicesEndpoint": "<uri>",
    "translatorCognitiveServicesEndpoint": "<uri>",
    "ocrCognitiveServicesPrimaryKey": "<key>",
    "ocrCognitiveServicesSecondaryKey": "<key>",
    "ocrCognitiveServicesEndpoint": "<uri>"
}
```

## Optional configuration

The extension default settings are set to handle the common workloads, for specific cases, the following parameters can be used to configure the resource allocation:

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

## Example deployment script

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
    --version ${version} \                        
```
---

## Sample
[Sample script to deploy Arc enabled AKS cluster with Video Indexer extension](https://github.com/Azure-Samples/media-services-video-indexer/blob/master/AVIenabledbyArc/vi-edge-deployment-script.sh)
