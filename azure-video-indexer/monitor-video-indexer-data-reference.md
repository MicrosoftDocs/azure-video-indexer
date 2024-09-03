---
title: Monitoring Azure AI Video Indexer data reference
description: Azure Monitor reference material for Azure AI Video Indexer 
ms.topic: reference
ms.custom: subject-monitoring
ms.date: 09/03/2024
ms.author: inhenkel
author: itnorman
ms.service: azure-video-indexer
---

# Monitor Azure AI Video Indexer data reference

See [Monitoring Azure AI Video Indexer](monitor-video-indexer.md) for details on collecting and analyzing monitoring data for Azure AI Video Indexer.

## Metrics

Azure AI Video Indexer currently does not support any metrics monitoring.

For more information, see a list of [all platform metrics supported in Azure Monitor](/azure/azure-monitor/platform/metrics-supported).

## Metric dimensions

Azure AI Video Indexer currently does not support any metrics monitoring.

Azure AI Video Indexer has the following dimensions associated with its metrics.

## Resource logs

This section lists the types of resource logs you can collect for Azure AI Video Indexer.  

For reference, see a list of [all resource logs category types supported in Azure Monitor](/azure/azure-monitor/platform/resource-logs-schema).

### Azure AI Video Indexer

Resource Provider and Type: [Microsoft.VideoIndexer/accounts](/azure/azure-monitor/platform/resource-logs-categories#microsoftvideoindexeraccounts)

| Category | Display Name | Additional information |
|:---------|:-------------|------------------|
| VIAudit   | Azure AI Video Indexer Audit Logs | Logs are produced from both the [Azure AI Video Indexer website](https://www.videoindexer.ai/) and the REST API. |
| IndexingLogs | Indexing Logs | Azure AI Video Indexer indexing logs to monitor all files uploads, indexing and reindexing jobs. |

## Azure Monitor Logs tables

This section refers to all of the Azure Monitor Logs Kusto tables relevant to Azure AI Video Indexer and available for query by Log Analytics.

|Resource Type | Notes |
|-------|-----|
| [Azure AI Video Indexer](/azure/azure-monitor/reference/tables/tables-resourcetype#azure-video-indexer) | |

### Azure AI Video Indexer

| Table |  Description | Additional information  |
|:---------|:-------------|------------------|
| [VIAudit](/azure/azure-monitor/reference/tables/tables-resourcetype#azure-video-indexer)<!-- (S/azure/azure-monitor/reference/tables/viaudit)-->   | <!-- description copied from previous link --> Events produced using the Azure AI Video Indexer [website](https://aka.ms/VIportal) or the [REST API portal](https://aka.ms/vi-dev-portal). |  |
|VIIndexing| Events produced using the Azure AI Video Indexer [upload](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video) and [re-index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Re-Index-Video) APIs. |

For a reference of all Azure Monitor Logs / Log Analytics tables, see the [Azure Monitor Log Table Reference](/azure/azure-monitor/reference/tables/tables-resourcetype).

## Activity log

The following table lists the operations related to Azure AI Video Indexer that may be created in the Activity log.

| Operation | Description |
|:---|:---|
|Generate_AccessToken | |
|Accounts_Update | |
|Write tags | |
|Create or update resource diagnostic setting| |
|Delete resource diagnostic setting|

For more information on the schema of Activity Log entries, see [Activity  Log schema](/azure/azure-monitor/essentials/activity-log-schema). 

## Schemas

The following schemas are in use by Azure AI Video Indexer:

#### Audit schema

```json
{
    "time": "2022-03-22T10:59:39.5596929Z",
    "resourceId": "/SUBSCRIPTIONS/602a61eb-c111-43c0-8323-74825230a47d/RESOURCEGROUPS/VI-RESOURCEGROUP/PROVIDERS/MICROSOFT.VIDEOINDEXER/ACCOUNTS/VIDEOINDEXERACCOUNT",
    "operationName": "Get-Video-Thumbnail",
    "category": "Audit",
    "location": "westus2",
    "durationMs": "192",
    "resultSignature": "200",
    "resultType": "Success",
    "resultDescription": "Get Video Thumbnail",
    "correlationId": "33473fc3-bcbc-4d47-84cc-9fba2f3e9faa",
    "callerIpAddress": "46.*****",
    "operationVersion": "Operations",
    "identity": {
      "externalUserId": "4704F34286364F2*****",
      "upn": "alias@outlook.com",
      "claims": { "permission": "Reader", "scope": "Account" }
    },
    "properties": {
      "accountName": "videoIndexerAccoount",
      "accountId": "8878b584-d8a0-4752-908c-00d6e5597f55",
      "videoId": "1e2ddfdd77"
    }
  }
  ```

#### Indexing schema

```json
{
    "time": "2022-09-28T09:41:08.6216252Z",
    "resourceId": "/SUBSCRIPTIONS/{SubscriptionId}/RESOURCEGROUPS/{ResourceGroup}/PROVIDERS/MICROSOFT.VIDEOINDEXER/ACCOUNTS/MY-VI-ACCOUNT",
    "operationName": "UploadStarted",
    "category": "IndexingLogs",
    "correlationId": "5cc9a3ea-126b-4f53-a4b5-24b1a5fb9736",
    "resultType": "Success",
    "location": "eastus",
    "operationVersion": "2.0",
    "durationMs": "0",
    "identity": {
        "upn": "my-email@microsoft.com",
        "claims": null
    },
    "properties": {
        "accountName": "my-vi-account",
        "accountId": "6961331d-16d3-413a-8f90-f86a5cabf3ef",
        "videoId": "46b91bc012",
        "indexing": {
            "Language": "en-US",
            "Privacy": "Private",
            "Partition": null,
            "PersonModelId": null,
            "LinguisticModelId": null,
            "AssetId": null,
            "IndexingPreset": "Default",
            "StreamingPreset": "Default",
            "Description": null,
            "Priority": null,
            "ExternalId": null,
            "Filename": "1 Second Video 1.mp4",
            "AnimationModelId": null,
            "BrandsCategories": null,
            "CustomLanguages": "en-US,ar-BH,hi-IN,es-MX",
            "ExcludedAIs": "Faces",
            "LogoGroupId": "ea9d154d-0845-456c-857e-1c9d5d925d95"
        }
    }
}
  ```

## Related articles

- See [Monitoring Azure AI Video Indexer](monitor-video-indexer.md) for a description of monitoring Azure AI Video Indexer.
- See [Monitoring Azure resources with Azure Monitor](/azure/azure-monitor/essentials/monitor-azure-resource) for details on monitoring Azure resources.
