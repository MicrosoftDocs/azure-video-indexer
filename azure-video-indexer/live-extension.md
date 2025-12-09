---
title: Manage real-time analysis extensions for Azure AI Video Indexer
description: Learn how to create, update, or delete an Azure AI Video Indexer extension that supports real-time analysis.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 11/05/2025
ms.service: azure-video-indexer
ms.topic: how-to
#customer intent: As a user of Azure AI Video Indexer, I want to manage real-time analysis extensions so that I can enable real-time video analysis capabilities.
---

# Manage real-time analysis extensions - Preview

To use real-time analysis, you must create and manage Azure AI Video Indexer extensions that support it. Use the following instructions to create, update, or delete a Video Indexer extension for real-time analysis.

>[!IMPORTANT]
> - Before you begin, ensure that you meet all prerequisites documented in the [Real-time video analysis in Azure AI Video Indexer](live-analysis.md) article.
> - After you create the extension using the information in this article, you connect cameras to it for real-time video analysis. For more information, see [Manage cameras with the Azure AI Video Indexer live extension](live-add-remove-camera.md).

## [Create in Azure portal](#tab/portal)

To create a Video Indexer extension that supports real-time analysis in the Azure portal, follow these steps:

1.  In the Azure portal, navigate to your Azure Arc-connected cluster.
2.  From the menu, select **Extensions** > **+ Add** > **Azure AI Video Indexer Arc Extension**.
3.  Select **Create**. The *Create an AI Video Indexer extension* page appears.
4.  Configure the extension in the **Basics** area:
    1.  Select the **subscription** for your extension.
    2.  Select the **region and connected** k8 cluster.
    3.  Enter a **name** for your extension.
    4.  Select the **Azure AI Video Indexer Account** that the extension connects to.
    5.  Enter the **Ingress endpoint**, either an IP address or DNS name to use as the API endpoint.
    6.  Provide the **storage class name** as configured in the cluster. If you're using AKS, you could use the predefined storage class named `azurefile-cli`. For more information about predefined storage classes supported by AKS, see [Storage Classes in AKS](/azure/aks/concepts-storage#storage-classes). If you're using other Kubernetes distributions, see your Kubernetes distribution documentation about supported predefined storage classes or for the way you can provide your own.
    7.  Select the **Live video stream** option in the **Content type** field. You can choose to mark also:
        - **Media uploads** – to allow upload media files to the extension.
        - **Include event summary** – to allow generating textual summaries for recording files. For more information, see [Event summary for media files](live-event-summary.md).
5.  Continue to configure the extension *Generative AI:*
    1.  Select the **Processor type (CPU or GPU)** to run the AI features you selected in the previous step.
      - For **Live video stream**, **GPU** is mandatory (there's no option to choose).
      - For **Media uploads** choose **GPU** or **CPU**.
    2.  Enter the **Toleration Key for GPU**.
    3.  Optionally, fill **Node selector**. Use if there are multiple GPUs nodes in the cluster. You can add a node selector to select the desired node for media uploads, live video, and event summary.
6.  Select **Review + create** and then select **Create**.  
    :::image type="content" source="./media/live-extension/create-video-indexer-extension.png" border="true" alt-text="Screenshot of the Create an AI Video Indexer extension Basics page." lightbox="./media/live-extension/create-video-indexer-extension.png" :::

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

To create a VI live extension, run the following command with your parameters:

```azurecli
az deployment group create -g \<resource group\> --template-file \<template file\>
```

## [Create with CLI](#tab/cli)

Use the Azure CLI to create a Video Indexer extension that supports real-time analysis. The following parameters are used as input to the extension creation command:

| **Parameter**                                    | **Type** | **Default value** | **Description**                                             |
|--------------------------------------------------|----------|-------------------|-------------------------------------------------------------|
| \<extension_name\>                               | String   |                   | Give a name to your VI live extension                       |
| \<release-namespace\>                            | String   | default           | The Kubernetes namespace where the extension gets installed |
| \<cluster-name\>                                 | String   |                   | The Kubernetes Azure arc instance name                      |
| \<resource-group\>                               | String   |                   | The Kubernetes Azure arc resource group name                |
| \<account_Id\>                                   | String   |                   | Video Indexer Account ID                                    |
| \<endpoint\>                                     | String   |                   | Video Indexer DNS Name to be used as the portal endpoint    |
| ViAi.gpu.tolerations.key                         | String   |                   | the default toleration in which GPU                         |
| videoIndexer.mediaFilesEnabled                   | Boolean  | true              | Enable media files upload                                   |
| ViAi.gpu.nodeSelector.workload                   | String   |                   | The GPU for media files summarization                       |
| videoIndexer.liveStreamEnabled                   | Boolean  | false             | Enable live streaming                                       |
| ViAi.LiveSummarization.enabled                   | Boolean  | false             | Enable live summarization on the recordings                 |
| ViAi.LiveSummarization.gpu.nodeSelector.workload | String   |                   | The node selector for live summarization                    |

To create a VI live extension, run the following command with your parameters as explained in the previous table.

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

## [Update with CLI](#tab/updatecli)

### Update Azure Arc Video Indexer extension using CLI

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

## [Delete with CLI](#tab/deletecli)

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

Run the following command to delete a VI live extension:

```azurecli
az k8s-extension delete --cluster-name <cluster-name> --cluster-type connectedclusters --resource-group <resource-group> --name <extension-name> --yes
```

---

## Related content

- [Real-time video analysis in Azure AI Video Indexer](live-analysis.md)
- [Add or remove cameras with the Azure AI Video Indexer live extension](live-add-remove-camera.md)