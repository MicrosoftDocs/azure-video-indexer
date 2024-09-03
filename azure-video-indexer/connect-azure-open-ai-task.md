---
title: Create an Azure AI Video Indexer account with an Azure OpenAI connection
description: This article shows you how to create an Azure AI Video Indexer account with an Azure OpenAI connection. 
ms.topic: how-to
ms.date: 09/03/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Create or update an Azure AI Video Indexer account with an Azure OpenAI connection

You can create an Azure AI Video Indexer account with an Azure OpenAI connection in the Azure portal. This article shows you how to connect Azure Open AI to Azure AI Video Indexer.

## Prerequisites

- An Azure subscription

> [!NOTE]
> It is recommended that you create resources in the same region to avoid performance issues.

## Create an Azure OpenAI account

1. From the Azure portal home page, select **Create a resource**.
1. Enter *OpenAI* in the search bar.
1. Select the Azure OpenAI card or **Create** and then **Azure OpenAI**.
1. Select the resource group you want to use from the **Resource group** drowpdown list or create a new one.
1. Select the region (location) from the **Region** dropdown** list.
1. Give the Azure OpenAI resource a name.
1. Select a tier from the **Pricing tier** dropdown list.
1. Select **Next**.
1. Select the **Disabled, no networks can access this resource. You could configure private endpoint connections that will be the exclusive way to access this resource** button unless you want to configure network access. Additionally, you can configure a private endpoint.
1. Select **Next**.
1. Select **Create**.
1. Wait for the deployment to finish.

## Create an Azure AI Video Indexer account with a connection to Azure OpenAI

1. Navigate to the resource group you are currently working with. 
1. Select **Create**.
1. Search for and select *Azure AI Video Indexer.* The Create a Video Indexer resource page appears.
1. Create a resource group and selecting the region.
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
