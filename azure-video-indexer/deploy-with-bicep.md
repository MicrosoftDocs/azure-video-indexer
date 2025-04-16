---
title:  Deploy Azure AI Video Indexer by using Bicep
description: Learn how to create an Azure AI Video Indexer account by using a Bicep file.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/09/2024
ms.service: azure-video-indexer
ms.topic: quickstart
---

# Quickstart: Deploy Azure AI Video Indexer (VI) by using Bicep

Using this quickstart, you can create an Azure AI Video Indexer (VI) account by using [Bicep](/azure/azure-resource-manager/bicep/overview).

The following resources are installed using the Bicep template:

- Azure Storage account. *Storage accounts for VI must be a Standard general-purpose v2 storage account*.
- VI account with a connection to the storage account using a system assigned managed identity
- The Storage Blob Data Contributor role assignment for the VI account on the storage account

## Prerequisites

- An Azure subscription with permission to create resources.
- The latest version of the [Azure CLI](/cli/azure/install-azure-cli).
- Recommended: Bicep tools.

## Review the Bicep file

The code that accompanies this quickstart can be found in the [Official Azure AI Video Indexer Samples](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/Deploy-Samples/bicep).

The `main.bicep` file orchestrates the installation of two modules:

- The VI module that deploys the VI account with its dependent Azure Storage account resource.
- The Role Permission module that grants the VI identity the Azure Blob Storage Data Owner permission on the storage account.

> [!NOTE]
> It's a good practice to separate Azure resources to multiple Bicep modules. For a comprehensive understanding of how Bicep modules work, see [Bicep modules - Azure Resource Manager](/azure/azure-resource-manager/bicep/modules).

## Create the Bicep file

1. Copy and paste the following content to a file called *main.bicep* in your working directory.

    ```cli
    param location string = resourceGroup().location 
    @description('Storage Account Name') 
    param storageAccountName string = “<add_your_storage_account_name” 
    @description('Video Indexer Account Name') 
    param videoIndexerAccountName string = = “<add_your_videoindexer_account_name>” 
    
    module videoIndexer 'videoIndexer.bicep' = { 
      name: 'videoIndexer.bicep' 
      params: { 
        location: location 
        storageAccountName: storageAccountName 
        videoIndexerAccountName: videoIndexerAccountName 
      } 
    } 
    
    // Role Assignment must be on a separate resource  
    
    module roleAssignment 'role-assignment.bicep' = { 
      name: 'grant-storage-blob-data-contributor' 
      params: { 
        servicePrincipalObjectId: videoIndexer.outputs.servicePrincipalId 
        storageAccountName: storageAccountName 
      } 
      dependsOn: [ 
        videoIndexer 
      ] 
    } 
    
    ```

1. Edit the `main.bicep` file by filling in the missing parameters:
    
    - *storageAccountName* - the name of the storage account you want connected to the Azure AI Video Indexer account
    - *videoIndexerAccountName* - the VI account name

## Create a Video AI Indexer Bicep module

Copy and paste the following content to a file called *videoindexer.bicep* in your working directory. The file deploys the storage account along with a VI account with a system assigned identity.

```cli

param location string = resourceGroup().location 
@description('Storage Account Name') 
param storageAccountName string 
@description('Video Indexer Account Name') 
param videoIndexerAccountName string 
@description('Storage Account Kind') 
var storageKind = 'StorageV2' 
@description('Storage Account Sku') 
var storageSku = 'Standard_LRS' 
resource storageAccount 'Microsoft.Storage/storageAccounts@2021-04-01' = { 
  name: storageAccountName 
  location: location 
  kind: storageKind 
  properties: { 
    minimumTlsVersion: 'TLS1_2' 
  } 
  sku: { 
    name: storageSku 
  }
} 

resource videoIndexer 'Microsoft.VideoIndexer/accounts@2024-01-01' = { 
  name: videoIndexerAccountName 
  location: location 
  identity: { 
    type: 'SystemAssigned' 
  } 

  properties: { 
    storageServices: { 
      resourceId: storageAccount.id 
    } 
  } 
} 

output storageAccountName string = storageAccount.name 
output accountName string = videoIndexer.name 
output servicePrincipalId string = videoIndexer.identity.principalId 

```

## Create a role assignment Bicep module

Copy and paste the following content to a file called `role-assignment.bicep` in your working directory. The module grants the system assigned identity the role of Storage Blob Data Contributor on the storage account of the VI account.

```cli

@secure() 
param servicePrincipalObjectId string 
param storageAccountName string
@description('Storage Blob Data Contributor Role Id') 
var storageBlobDataContributorRoleId = 'ba92f5b4-2d11-453d-a403-e96b0029c9fe' 
resource storageAccount 'Microsoft.Storage/storageAccounts@2021-04-01' existing= { 
  name: storageAccountName 
} 

resource roleAssignment 'Microsoft.Authorization/roleAssignments@2020-04-01-preview' = { 
  name: guid(storageAccount.id, servicePrincipalObjectId, 'Storage Blob Data Contributor')  
  scope: storageAccount  
  properties: { 
    roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', storageBlobDataContributorRoleId)  
    principalId: servicePrincipalObjectId 
    principalType: 'ServicePrincipal'
  }
} 

```

## Deploy the Bicep files

1. Open a terminal and ensure that you're signed in to your Azure subscription.
    
    `az login`
    
    `az account set --subscription <your-subscription-name>`

1. Create a resource group.

    `az group create -n <your-resource-group-name> -l eastus`

1. Deploy the template to the resource group.

    `az deployment group create --resource-group <your-resource-group-name> --template-file .\main.template.json`

1. Wait for the deployment to finish and inspect the created resource on Azure portal. 

## Related articles

If you're new to Azure AI Video Indexer, see:

- The [Azure AI Video Indexer documentation](/azure/azure-video-indexer/)
- The [Azure AI Video Indexer developer portal](https://api-portal.videoindexer.ai/)
- The [Official Azure AI Video Indexer Samples](https://github.com/Azure-Samples/media-services-video-indexer/blob/master/README.md)

If you're new to Bicep deployment, see:

- [Azure Resource Manager documentation](/azure/azure-resource-manager/)
- [Deploy Resources with Bicep and Azure PowerShell](/azure/azure-resource-manager/bicep/deploy-powershell)
- [Deploy Resources with Bicep and Azure CLI](/azure/azure-resource-manager/bicep/deploy-cli)
