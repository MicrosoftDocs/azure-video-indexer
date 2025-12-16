---
title: Manage Azure AI Video Indexer extensions for real-time analysis
description: Learn how to create, update, or delete an Azure AI Video Indexer extension that supports real-time analysis.
author: cwatson-cat
ms.author: cwatson
ms.collection: ce-skilling-ai-copilot
ms.date: 12/16/2025
ms.service: azure-video-indexer
ms.topic: how-to
ai-usage: ai-assisted
appliesto: 
- Azure AI Video Indexer enabled by Azure Arc
#customer intent: As a user of Azure AI Video Indexer, I want to manage real-time analysis extensions so that I can enable real-time video analysis capabilities.
---

# Manage Azure AI Video Indexer extensions for real-time analysis - Preview

To use real-time analysis, you must create and manage Azure AI Video Indexer (VI) extensions that support it. Use the following instructions to create, update, or delete a Video Indexer extension for real-time analysis.

After you create the extension by using the information in this article, connect cameras to it for real-time video analysis. For more information, see [Add or remove cameras for use with the VI extension for real-time analysis](live-add-remove-camera.md).

## Prerequisites

Before you begin, review the following prerequisites to ensure that you meet them.

- You must have an **Azure AI Video Indexer** account. For more information, see the [Create Video Indexer account](create-account.md) tutorial.
- You must have a running **Kubernetes (K8s) cluster connected to Azure Arc**. For more information, see [Connect an existing Kubernetes cluster](/azure/azure-arc/kubernetes/quickstart-connect-cluster?tabs=azure-cli#connect-an-existing-kubernetes-cluster). Real-time analysis was validated on Azure Local but is compatible with any Kubernetes infrastructure that supports the following requirements.
  - Read-write-many (RWX) storage class.
  - The ingress controller must allow outside clients to connect to the application.
  - At least one NVIDIA GPU enabled node in the cluster.
  - Requirements for supported Kubernetes (K8s) distributions include:
    - [AKS on Azure Local enabled by Arc](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/VideoIndexerEnabledByArc/AzureLocal)
    - [K8s on a Linux machine](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/VideoIndexerEnabledByArc)
    - [AKS on cloud](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/VideoIndexerEnabledByArc/aks)
- Make sure you have a valid **RTSP stream**. You need the RTSP URL.
- Optionally, you can have an **Azure IoT for Operations extension** deployed to an Azure Arc Kubernetes cluster. The installation of both AIO and VI extensions must be in the same cluster.
- You must have the latest version of Azure CLI. However, you can skip this requirement if you're using Azure cloud shell.
- As noted previously, your **Azure subscription ID** must already be approved. If not already approved, you can sign up at [Application for Azure AI Video Indexer Enabled by Arc - real-time video analysis](https://aka.ms/vi-live-register).

We recommend enabling automatic version upgrade for your Arc-enabled Kubernetes cluster extension, so that you always have the latest security patches and new capabilities. For more information, see [Deploy and manage an Azure Arc-enabled Kubernetes cluster extension](/azure/azure-arc/kubernetes/extensions#optional-parameters).

## Deploy the Azure AI Video Indexer extension

Choose the method you want to use to create the Azure AI Video Indexer extension. Create the extension by using the Azure portal, with Azure CLI, or by using a Bicep template, depending on your preference and environment.

## [Create in Azure portal](#tab/portal)

To create a Video Indexer extension that supports real-time analysis in the Azure portal, complete the following steps:

1. In the [Azure portal](https://portal.azure.com/), go to your Azure Arc-connected Kubernetes cluster.
1. On the Kubernetes cluster, under **Settings**, select **Extensions**.
1. Select **Add** > **Azure AI Video Indexer Arc Extension**.
1. Select **Create**.
1. On the **Basic** tab, provide the following information:

    | Field | Value     |
    |------------------------|--------|
    | Subscription     | Select the subscription for your extension.    |
    | Resource group         | Select the resource group for your extension.                                                      |
    | Region    | Select the region to create the extension.   |
    | Connected K8S cluster     | Select the Azure Arc connected Kubernetes cluster.   |
    | Extension name                   | Enter a name for your extension.  |
    | Video indexer account ID | Select the Azure AI Video Indexer account that the extension connects to.   |
    | Ingress endpoint       | Enter the cluster endpoint, either an IP address or DNS name, to use as the API endpoint.                                               |
    | Storage class name | Provide the storage class supported by your Kubernetes distribution. For example, use `azurefile-cli` for AKS. See [Storage Classes in AKS](/azure/aks/concepts-storage#storage-classes) for more info. For other distributions, see your Kubernetes documentation. |
    | Content type | Select the following options: </br>•  **Live video** to enable real-time analysis<br>•  **Media uploads** to allow upload media files to the extension |

   :::image type="content" source="media/live-extension/create-video-indexer-extension-basics.png" alt-text="Screenshot of the basics tab for the Azure AI Video Indexer extension that shows fields in sections for project details, instance details, and additional settings." lightbox="media/live-extension/create-video-indexer-extension-basics.png":::

1. Select **Next**.
1. On the **Processing + AI** tab, provide the following information:

   | Field                        | Description |
   |------------------------------|-------------|
   | Agentic capabilities         | Includes advanced video investigation capabilities. Requires two dedicated H100 GPUs. Toggle to enable or disable. |
   | Summarization capabilities   | Includes advanced vision event summary capabilities. Requires a dedicated H100 GPU. Toggle to enable or disable. |
   | Processing                   | <ul><li>**Live video** requires four GPU units: one dedicated to live streaming, two for agentic capabilities, and one for summarization capabilities.</li><li>**Media uploads** requires one GPU unit for summarization capabilities.</li></ul> |
   | Toleration Key for GPU       | Enter the toleration key for GPU nodes (for example, `nvidia.com/gpu`). Required for GPU workloads. |
   | Node selector (optional)     | If there are multiple GPU node types, you can add a node selector to select the desired node. Specify the node name and value for each of the following (optional): <ul><li>Live video stream</li><li>Agentic capabilities</li><li>Summarization capabilities</li></ul> |

   :::image type="content" source="./media/live-extension/create-video-indexer-extension-processing.png" border="true" alt-text="Screenshot of the Create an AI Video Indexer extension generative AI page." lightbox="./media/live-extension/create-video-indexer-extension-processing.png" :::

1. Select **Review + create** > **Create**.

## [Create with Bicep](#tab/bicep)

Use the following Bicep template to create a Video Indexer extension that supports real-time analysis. The template includes all the necessary parameters and configurations to deploy the extension on your Azure Arc connected Kubernetes cluster. Name the file `vi.arcextension.template.bicep`.

```bicep
param accountId string = '<enter_vi_account_id>'
param videoIndexerEndpointUri string = '<enter_endpoint_uri>'
param arcConnectedClusterName string = '<enter_arc_cluster_name>'
param extensionName string = '<extension_name>'
param releaseTrain string = 'preview'
param version string = '1.2.53'
param useGpuForSummarization bool = false
param nodeSelectorForSummarization object = { }
param nodeSelectorForLiveSummarization object = { }
param deepstreamNodeSelector string = ''
param tolerationsKeyForGpu string = 'nvidia.com/gpu'
param liveSummarizationEnabled bool = true

var storageClass = '<storage_class_name>'

var baseConfigProperties = {
  'videoIndexer.endpointUri': videoIndexerEndpointUri
  'videoIndexer.accountId': accountId
  'videoIndexer.mediaFilesEnabled': string(true)
  'videoIndexer.liveStreamEnabled': string(true)
  'mediaServerStreams.enabled': string(true)
  'storage.storageClass': storageClass
  'storage.accessMode': 'ReadWriteMany'
  'ViAi.gpu.enabled': string(useGpuForSummarization)
  'ViAi.gpu.tolerations.key': tolerationsKeyForGpu
  'ViAi.LiveSummarization.enabled': string(liveSummarizationEnabled)
}

var summarizationNodeSelectorProps = reduce(
  items(nodeSelectorForSummarization),
  {},
  (cur, next) => union(cur, {'ViAi.gpu.nodeSelector.${next.key}': next.value})
)

var liveSummarizationNodeSelectorProps = reduce(
  items(nodeSelectorForLiveSummarization),
  {},
  (cur, next) => union(cur, {'ViAi.LiveSummarization.gpu.nodeSelector.${next.key}': next.value})
)

var deepstreamNodeSelectorProps = !empty(deepstreamNodeSelector) && deepstreamNodeSelector != ' ' ? {
  'viai.deepstream.nodeselector': deepstreamNodeSelector
} : {}

var extensionConfigPropertiesWithSelector = union(
  baseConfigProperties,
  summarizationNodeSelectorProps,
  liveSummarizationNodeSelectorProps,
  deepstreamNodeSelectorProps
)
resource connectedCluster 'Microsoft.Kubernetes/connectedClusters@2024-01-01' existing = {
  name: arcConnectedClusterName

}
resource extension 'Microsoft.KubernetesConfiguration/extensions@2022-11-01' = {
  name: extensionName
  scope: connectedCluster
  identity: {
    type: 'SystemAssigned'
  }
  properties: {
    extensionType: 'microsoft.videoindexer'
    autoUpgradeMinorVersion: false
    releaseTrain: releaseTrain
    version: version
    scope: {
      cluster: {}
    }
    configurationSettings: extensionConfigPropertiesWithSelector
  }
}

output result string = extension.properties.provisioningState
```

### Edit parameters

After you save the Bicep file, edit the following parameters:

| **Parameter**      | **Type** | **Description**                                                  |
|--------------------|----------|------------------------------------------------------------------|
| \<account ID\>     | string   | Enter your video indexer account ID                              |
| \<endpoint uri\>   | string   | Enter the Kubernetes cluster connected to Azure Arc endpoint URL |
| \<cluster name\>   | string   | Enter the Arc connected cluster name                             |
| \<extension name\> | string   | Give a name to the new extension created                         |

Use the following parameters as input for the extension creation command:

| **Parameter**      | **Type** | **Description**                                                    |
|--------------------|----------|--------------------------------------------------------------------|
| \<resource group\> | String   | Enter the name of the resource group                               |
| \<template-file\>  | String   | Enter the full path to the template file location in your computer |

### Create the extension

To create a VI extension for real-time analysis, run the following command with your parameters:

```azurecli
az deployment group create -g \<resource group\> --template-file \<template file\>
```

## [Create with CLI](#tab/cli)

Use the Azure CLI to create a Video Indexer extension that supports real-time analysis. The following parameters are input to the extension creation command:

| **Parameter**                                    | **Type** | **Default value** | **Description**                                             |
|--------------------------------------------------|----------|-------------------|-------------------------------------------------------------|
| \<extension_name\>                               | String   |                   | Name for your Video Indexer extension                        |
| \<release-namespace\>                            | String   | default           | The Kubernetes namespace where the extension is installed   |
| \<cluster-name\>                                 | String   |                   | The Kubernetes Azure Arc instance name                       |
| \<resource-group\>                               | String   |                   | The Kubernetes Azure Arc resource group name                 |
| \<account_Id\>                                   | String   |                   | Video Indexer Account ID                                    |
| \<endpoint\>                                     | String   |                   | Video Indexer DNS Name to be used as the portal endpoint    |
| ViAi.gpu.tolerations.key                         | String   |                   | The default toleration for GPU                               |
| videoIndexer.mediaFilesEnabled                   | Boolean  | true              | Enable media files upload                                   |
| ViAi.gpu.nodeSelector.workload                   | String   |                   | The GPU for media files summarization                       |
| videoIndexer.liveStreamEnabled                   | Boolean  | false             | Enable live streaming                                       |
| ViAi.LiveSummarization.enabled                   | Boolean  | false             | Enable live summarization on the recordings                 |
| ViAi.LiveSummarization.gpu.nodeSelector.workload | String   |                   | The node selector for live summarization                    |

To create a Video Indexer extension for real-time analysis, run the following command with your parameters as explained in the previous table.

```azurecli
az k8s-extension create
--name <extension_name>
--extension-type "Microsoft.videoIndexer"
--scope cluster
--release-namespace "video-indexer"
--cluster-name <cluster_name>
--resource-group <cluster_resource_group>
--cluster-type "connectedClusters"
--version "1.2.0"
--release-train "preview"
--auto-upgrade-minor-version "false"
--config "videoIndexer.accountId=<account_id>"
--config "videoIndexer.endpointUri=<endpoint>"
--config AI.nodeSelector."beta\.kubernetes\.io/os"=linux
--config "storage.storageClass=azurefile-csi"
--config "storage.accessMode=ReadWriteMany"
--config "ViAi.gpu.enabled=true"
--config "ViAi.gpu.tolerations.key=nvidia.com/gpu"
--config videoIndexer.liveStreamEnabled=true
--config videoIndexer.mediaFilesEnabled=true
--config "ViAi.LiveSummarization.enabled=true"
--config "ViAi.LiveSummarization.gpu.nodeSelector.workload=summarization"
--config "ViAi.gpu.nodeSelector.workload=summarization"
```

### Other parameters

Here are some other parameters that can be used in order to have a fine grain control on the extension creation:

| Parameter | Default | Description |
|-----------|---------|-------------|
| AI.nodeSelector | - | The node Selector label on which the AI Pods (speech and translate) get assigned to resource.requests.mem |
| videoIndexer.webapi.resources.requests.cpu | 0.5 | The request number of cores for the web API pod |
| videoIndexer.webapi.resources.requests.mem | 4Gi | The request memory capacity for the web API pod |
| videoIndexer.webapi.resources.limits.cpu | 1 | The limits number of cores for the web API pod |
| videoIndexer.webapi.resources.limits.mem | 6Gi | The limits memory capacity for the web API pod |
| videoIndexer.webapi.resources.limits.mem | 6Gi | The limits memory capacity for the web API pod |
| storage.storageClass | "" | The storage class to be used |
| storage.useExternalPvc | false | determines whether an external PVC is used. If true, the VideoIndexer PVC doesn't get installed |

### Example deployment script

```bash
az k8s-extension create --name videoindexer \
    --extension-type Microsoft.videoindexer \
    .......

    --config AI.nodeSelector."beta\\.kubernetes\\.io/os"=linux
    --config "videoIndexer.webapi.resources.requests.mem=4Gi"\
    --config "videoIndexer.webapi.resources.limits.mem=8Gi"\
    --config "videoIndexer.webapi.resources.limits.cpu=1"\
    --config "storage.storageClass=azurefile-csi" 
```

---

## Update VI extension using CLI

To update your extension, add any of the parameters from the **Create with CLI** tab with their new values if you want to change them in the following example.

In this example, it updates the extension endpoint.

```bash
az k8s-extension update --name $extension_name --extension-type "Microsoft.videoIndexer" --scope cluster \
  --release-namespace "video-indexer" \
  --cluster-name $cluster_name \
  --resource-group $cluster_resource_group \
  --cluster-type "connectedClusters" \
  --version $version \
  --release-train "preview" \
  --config "videoIndexer.endpointUri=$endpoint"
```

## Delete VI extension using CLI

Use the following parameters as input to the extension delete command:

| **Parameter**      | **Type** | **Description**                                      |
|--------------------|----------|------------------------------------------------------|
| \<cluster-name\>   | String   | The Kubernetes Azure arc instance name               |
| \<resource-group\> | String   | The Kubernetes Azure arc resource group name         |
| \<extension-name\> | String   | Enter the VI extension name you would like to delete |

To get your extension name, run the following command:

```azurecli
az k8s-extension list --cluster-name <cluster-name>
 --cluster-type connectedClusters --resource-group  <resource-group> --query "[?extensionType == 'microsoft.videoindexer'] | [0]"
```

Run the following command to delete a VI extension:

```azurecli
az k8s-extension delete --cluster-name <cluster-name> --cluster-type connectedclusters --resource-group <resource-group> --name <extension-name> --yes
```

## Related content

- [Add or remove cameras for use with the VI extension for real-time analysis](live-add-remove-camera.md).
- [Real-time video analysis in Azure AI Video Indexer](live-analysis.md)