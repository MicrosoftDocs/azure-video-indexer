---
title: Create an Azure AI Video Indexer account with an Azure OpenAI connection
description: This article explains how to create an Azure AI Video Indexer account with an Azure OpenAI connection.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 05/28/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
---

# Create or update an Azure AI Video Indexer account with an Azure OpenAI connection

You can use Azure AI Video Indexer with Azure OpenAI deployments by creating or updating an Azure AI Video Indexer account to connect with an Azure OpenAI in the Azure portal. This article explains how to connect Azure OpenAI to Azure AI Video Indexer, but doesn't cover use cases for Azure OpenAI or combining the two services. For more information about Azure OpenAI deployments, see the [Azure OpenAI Service documentation](/azure/ai-services/openai/).

## Prerequisites

- An Azure subscription

> [!NOTE]
> We recommended that you create resources in the same region to avoid performance issues.

## Create an Azure OpenAI account

1. From the Azure portal home page, select **Create a resource**.
1. Enter *OpenAI* in the search bar.
1. Under the **Azure OpenAI**, select **Create** and then **Azure OpenAI**.
1. Select the resource group you want to use from the **Resource group** list or create a new one.
1. Select the region (location) from the **Region** list.
1. Enter a name for the Azure OpenAI resource.
1. Select a tier from the **Pricing tier** list.
1. Select **Next**.
1. Next to **Type**, select the **Disabled** option unless you want to configure network access. Additionally, you can configure a private endpoint.
1. Select **Next**.
1. Select **Create**.
1. Wait for the deployment to finish.

## Create an Azure AI Video Indexer account with a connection to Azure OpenAI

1. Navigate to the resource group you're currently working with. 
1. Select **Create**.
1. Search for and select *Azure AI Video Indexer.* The Create a Video Indexer resource page appears.
1. Create a resource group and select a region.
1. Give the account a name in the **Resource name** field.
1. Connect the account to storage. Either…
    1. Select an existing storage account from the **Storage account** dropdown or
    1. Create a new storage account. For more information about creating a storage account, see [Create a storage account](/azure/storage/common/storage-account-create?tabs=azure-portal). *Storage accounts for VI must be a Standard general-purpose v2 storage account*.
1. Select the Azure OpenAI account you want to work with from the **Azure OpenAI Resource** dropdown list.
1. Select **system assigned managed identity**.
1. Select the **I have all the rights to use the content/file, and agree that it will be handled per the Online Services Terms  and the Microsoft Privacy Statement** checkbox.
1. Select **Review + create**. Validation of the configuration starts.
1. When validation is complete, select **Create**.
1. When the deployment is complete, select **Go to resource**. The Azure AI Video Indexer overview page opens.  
1. Notifications on the page appear that say you must select a managed identity role assignment. Select the **Assign role** buttons. The Azure AI Video Indexer and Azure OpenAI accounts are now connected.

## Update an existing Azure AI Video Indexer account to connect to Azure OpenAI

1. In the Azure portal, navigate to the existing Azure AI Video Indexer account and select **Overview**.
1. Select the **connect** or **change** link next to the Azure OpenAI item.
1. Select the Azure OpenAI resource you want to use from the Azure OpenAI dropdown list.
1. Select **Update**.
1. Select **Assign roles** in the error message.
