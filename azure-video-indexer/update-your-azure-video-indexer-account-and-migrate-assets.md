---
title: Update your Azure Video Indexer account and migrate assets  
description: Azure Video Indexer (AVI) used Azure Media Services (AMS) for encoding, packaging and streaming of media assets. AMS announced that it's retiring on June 30, 2024. Therefore, AVI is removing the dependency on AMS. As described in the update and migration guide azure-video-indexer-retirement-guide.md, your Azure Video Indexer account needs to be updated. During the update, you'll have the opportunity to opt in to having the AVI product team migrate your assets for you. If you don’t opt in during the update process, your assets won’t be migrated.
ms.topic: conceptual
ms.service: azure-video-indexer
ms.date: 01/22/2024
ms.author: inhenkel
author: IngridAtMicrosoft
---

# Update your Azure Video Indexer account and migrate assets

Azure Video Indexer (AVI) used Azure Media Services (AMS) for encoding, packaging and streaming of media assets. AMS announced that it's retiring on June 30, 2024. Therefore, AVI is removing the dependency on AMS.

As described in the [AVI update and migration guide](azure-video-indexer-retirement-guide.md), your Azure Video Indexer account needs to be updated. During the update, you'll have the opportunity to opt in to having the AVI product team migrate your assets for you. If you don’t opt in during the update process, your assets won’t be migrated.

You can opt in to AVI migration using either the Azure portal or the API during the account update process.

> [!IMPORTANT] 
> Until June 30th you can still opt in to migration performed by AVI or choose not to migrate your assets. After June 30th, there will be no option to migrate your assets at all.

## Update an existing ARM account

Update an existing ARM account.

### [Update existing account in Azure portal](#tab/updateexistingportal)

1.  In the Azure portal, navigate to the AVI ARM account you want to work with.
1.  Select **Update account**. The Update account pane appears.
1.  Connect the account to storage. Either…
    1.  Select an existing storage account from the **Storage account** dropdown or
    1.  Create a new storage account. For more information about creating a storage account, see Create a storage account](/azure/storage/common/storage-account-create?tabs=azure-portal).
1.  Select the **Request to migrate** checkbox.
1.  Once the storage is created, a notification appears that says that you must select a managed identity role assignment. Select the **Assign role** button.
1.  If you didn’t opt in to the migration process during storage creation, you can opt in by selecting the **Migrate content** tab. The migration prompt appears.
1.  Select **Request migration** to continue. When the migration request has been received, a success notification appears, the Migrate content tab disappears, and the banner disappears.

### [Update existing account with the API](#tab/updateexsitingapi)

1.  Invoke Create or Update Account ARM API for your account. In the request body, Set the *storageServices* properties (`resourceId` and `userAssignedIdentity`) with the storage account that will be linked to the AVI account.

    ```REST API
    PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VideoIndexer/accounts/{accountName}?api-version=2024-01-01
    ```
    See [Accounts - Create Or Update - REST API (Azure Azure Video Indexer)](/rest/api/videoindexer/accounts/create-or-update?view=rest-videoindexer-2024-01-01&tabs=HTTP&preserve-view=true) for more information
    
1.  Opt in to migration process by invoking Start Account Migration API
    
    ```REST API
    POST https://api.videoindexer.ai/{location}/Accounts/{accountId}/AMSAssetsMigration[?accessToken]
    ```
    
    See [APIs: Details - Microsoft Azure API Management - developer portal (videoindexer.ai)](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Start-Account-Migration)

---

## Connect a classic account to a new ARM based account

If your account is a classic account, you are required to connect the classic account to an ARM account before the classic account is retired. The following steps walk you through creating a new ARM based account.

### [Connect a classic account in the Azure portal](#tab/connectclassicportal)

1.  In the Azure portal, select **+ Create a resource.**
1.  Search for and select *Azure AI Video Indexer.* The Create a Video Indexer resource page appears.
1.  **Skip** creating a resource group and selecting the region sections. The are auto populated by the following steps.
1.  Select the Connect all content from an existing classic account button.
1.  Select the classic account from the **Available classic accounts dropdown** list.
1.  Give the account a name in the **Resource name** field.
1.  Connect the account to storage. Either…
    1.  Select an existing storage account from the **Storage account** dropdown or
    1.  Create a new storage account. For more information about creating a storage account, see [Create a storage account](/azure/storage/common/storage-account-create?tabs=azure-portal).

> [!NOTE]
> If you attempt to link the account to the storage account that is associated with an AMS account, you will receive an error.

1.  Select or create a **user assigned managed identity**. (If you forget, a prompt in the storage overview page appears later in the process.)
1.  Select **Review + create**. Validation of the configuration starts.
1.  When validation is complete, select **Create**.
1.  When the deployment is complete, select **Go to resource**. The storage resource overview page appears.
1.  If you assigned a system assigned managed identity during the storage creation process, a notification on the page says that you must select a managed identity role assignment. Select the **Assign role** button.
1.  You can opt in to AVI migration by selecting the **Migrate content** tab. The migration prompt appears.
1.  Select **Request migration** to continue. When the migration request is received, a success notification appears, the Migrate content tab disappears, and the banner disappears.

### [Connect a classic account with the API](#tab/connectapi)

1.  Invoke Create or Update Account ARM API for your account. In the request body, set the *storageServices* properties (`resourceId` and `userAssignedIdentity`) with the new storage account you’ve created, and set the *accountId* property with the account ID of the AVI Classic account.

    ```REST API
    PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VideoIndexer/accounts/{accountName}?api-version=2024-01-01    
    ```

    See [Accounts - Create Or Update - REST API (Azure Azure Video Indexer)](/rest/api/videoindexer/accounts/create-or-update?view=rest-videoindexer-2024-01-01&tabs=HTTP&preserve-view=true) for more information.
  
1.  Opt in to migration process by invoking Start Account Migration API

    ```REST API
    POST https://api.videoindexer.ai/{location}/Accounts/{accountId}/AMSAssetsMigration[?accessToken]
    ```

    See [APIs: Details - Microsoft Azure API Management - developer portal (videoindexer.ai)](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Start-Account-Migration) for more information.

---

## Opt in to AVI migration of an already updated account

To opt in to AVI migration of an already updated account, you can use either the Azure portal or the API.

### [Opt in in the Azure portal](#tab/optinportal)

1.  You can opt in to AVI migration by selecting the **Migrate content** tab. The migration prompt appears.
2.  Select **Request migration** to continue. When the migration request is received, a success notification appears, the Migrate content tab disappears, and the banner disappears.

### [Opt in with the API](#tab/optinapi)

Include the access token in the request.

```REST API
POST https://api.videoindexer.ai/{location}/Accounts/{accountId}/AMSAssetsMigration[?accessToken]
```

See [APIs: Details - Microsoft Azure API Management - developer portal (videoindexer.ai)](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Start-Account-Migration) for more information.

---
