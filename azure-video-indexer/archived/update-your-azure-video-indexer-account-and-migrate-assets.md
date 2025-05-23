---
title: Update your Azure AI Video Indexer account and migrate assets  
description: Azure AI Video Indexer (VI) used Azure Media Services (AMS) for encoding, packaging, and streaming of media assets. AMS announced that it's retiring on June 30, 2024. Therefore, VI is removing the dependency on AMS. As described in the update and migration guide azure-video-indexer-retirement-guide.md, your Azure AI Video Indexer account needs to be updated. During the update, you have the opportunity to opt in to having the VI product team migrate your assets for you. If you don’t opt in during the update process, your assets won’t be migrated.
author: bandersmsft
ms.author: banders
ms.date: 10/09/2024
ms.service: azure-video-indexer
ms.topic: conceptual
---

# Update your Azure AI Video Indexer account and migrate assets

[!INCLUDE [AMS VI retirement announcement](../includes/important-ams-retirement-avi-announcement.md)]

Azure AI Video Indexer (VI) used Azure Media Services (AMS) for encoding, packaging, and streaming of media assets. AMS announced that it's retiring on June 30, 2024. Therefore, VI is removing the dependency on AMS.

As described in the [VI update and migration guide](azure-video-indexer-ams-retirement-guide.md), your Azure AI Video Indexer account needs to be updated. During the update, you have the opportunity to opt in to having the VI product team migrate your assets for you. If you don’t opt in during the update process, your assets won’t be migrated.

You can opt in to VI migration using either the Azure portal or the API during the account update process.

> [!IMPORTANT] 
> Until June 30 you can still opt in to migration performed by VI or choose not to migrate your assets. After June 30, there will be no option to migrate your assets at all.

## Update an existing ARM account

Update an existing Azure Resource Manager (ARM) account.

### Permissions

The following permissions are required to update an existing ARM account:

- A **Contributor** role on the Azure AI Video Indexer account
- An **Owner** role or both **Contributor** and **User Access Administrator** roles on the linked storage account
- A **Reader** role for the Azure AI Video Indexer resource on the AMS resource.

If the AMS linked storage account is behind a firewall, VI needs to be assigned the following managed identity - Storage Blob Data Owner. To learn more, see [Use Video Indexer with storage behind firewall](/azure/azure-video-indexer/storage-behind-firewall).

### [Update existing account in Azure portal](#tab/updateexistingportal)

1.  In the Azure portal, navigate to the VI ARM account you want to work with.
1.  Select **Update account**. The Update account pane appears.
1.  Connect the account to storage. Either…
    1.  Select an existing storage account from the **Storage account** dropdown or
    1.  Create a new storage account. *Storage accounts linked to VI must be a Standard general-purpose v2 storage account or Standard general-purpose v1 storage account. It can't be a Premium block blob, Premium file share, or Premium page blob account*. For more information about creating a storage account, see [Create a storage account](/azure/storage/common/storage-account-create?tabs=azure-portal). 
1.  Select the **Request to migrate** checkbox.
1.  Once the storage is created, a notification appears that says that you must select a managed identity role assignment. Select the **Assign role** button.
1.  If you didn’t opt in to the migration process during storage creation, you can opt in by selecting the **Migrate content** tab. The migration prompt appears.
1.  Select **Request migration** to continue. When the migration request has been received, a success notification appears, the Migrate content tab disappears, and the banner disappears.

### [Update existing account with the API](#tab/updateexsitingapi)

1.  Invoke Create or Update Account ARM API for your account. In the request body, Set the *storageServices* properties (`resourceId` and `userAssignedIdentity`) with the storage account that will be linked to the VI account.

    ```REST API
    PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VideoIndexer/accounts/{accountName}?api-version=2024-01-01
    ```
    See [Accounts - Create Or Update - REST API (Azure Azure AI Video Indexer)](/rest/api/videoindexer/accounts/create-or-update?view=rest-videoindexer-2024-01-01&tabs=HTTP&preserve-view=true) for more information
    
1.  Opt in to migration process by invoking Start Account Migration API
    
    ```REST API
    POST https://api.videoindexer.ai/{location}/Accounts/{accountId}/AMSAssetsMigration[?accessToken]
    ```
    
    See [APIs: Details - Microsoft Azure API Management - developer portal (videoindexer.ai)](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Start-Account-Migration)

---

## Connect a classic account to a new ARM based account

If your account is a classic account, you're required to connect the classic account to an ARM account before the classic account is retired. Doing so creates the VI account as an ARM resource and the ARM VI resource must be in the same Azure subscription as the VI Classic account and its AMS asset.

### Transition state

Connecting a classic account to be ARM-based triggers a 30 days of a transition state. In the transition state, an existing account can be accessed by generating an access token using both the:

- Access token generated through API Management(classic way)
- Access token generated through ARM

The transition state moves all account management functionality to be managed by ARM and will be handled by [Azure Role Based Access Control (RBAC)](/azure/role-based-access-control/overview).

The invite users feature in the Azure AI Video Indexer website gets disabled. The invited users on this account lose their access to the Azure AI Video Indexer account Media in the portal. However, this can be resolved by assigning the right role-assignment to these users through RBAC, see [How to assign RBAC](/azure/role-based-access-control/role-assignments-steps).

Only the account owner, who performed the connect action, is automatically assigned as the owner on the connected account. When [Azure policies](/azure/governance/policy/overview) are enforced, they override the settings on the account.

If users aren't added through Azure RBAC to the account after 30 days, they'll lose access through API and the Azure AI Video Indexer website.

After the transition state ends, users will only be able to generate a valid access token through ARM, making Azure RBAC the exclusive way to manage role-based access control on the account.

> [!Note]
> If there are invited users you wish to remove access from, do it before connecting the account to ARM.

Before the end of the 30 days of transition state, you can remove access from users through the Azure AI Video Indexer website account settings page.

The following steps walk you through creating a new ARM based account.

### Permissions

You must have the following permissions to update an existing ARM account and to opt in and complete the VI AMS resource migration:

- **Owner** permission on the classic account
- **Contributor** permission on the subscription
- **Owner** or both **Contributor** and **User Access Administrator** roles on the VI linked storage account
- A **Reader** role for the Azure AI Video Indexer resource on the AMS resource.

If the AMS linked storage account is behind a firewall, VI needs to be assigned the following managed identity - Storage Blob Data Owner. To learn more, see [Use Video Indexer with storage behind firewall](/azure/azure-video-indexer/storage-behind-firewall).

### [Connect a classic account in the Azure portal](#tab/connectclassicportal)

[!INCLUDE [migrate-important](../includes/migrate-important.md)]

1.  In the Azure portal, select **+ Create a resource.**
1.  Search for and select *Azure AI Video Indexer.* The Create a Video Indexer resource page appears.
1.  **Skip** creating a resource group and selecting the region sections. They're auto populated by the following steps.
1.  Select the Connect all content from an existing classic account button.
1.  Select the classic account from the **Available classic accounts dropdown** list.
1.  Give the account a name in the **Resource name** field.
1.  Connect the account to storage. Either…
    1.  Select an existing storage account from the **Storage account** dropdown or
    1.  Create a new storage account. For more information about creating a storage account, see [Create a storage account](/azure/storage/common/storage-account-create?tabs=azure-portal).

> [!NOTE]
> If you attempt to link the account to the storage account that is associated with an AMS account, you'll receive an error.

1.  Select or create a **user assigned managed identity**. (If you forget, a prompt in the storage overview page appears later in the process.)
1.  Select **Review + create**. Validation of the configuration starts.
1.  When validation is complete, select **Create**.
1.  When the deployment is complete, select **Go to resource**. The storage resource overview page appears.
1.  If you assigned a system assigned managed identity during the storage creation process, a notification on the page says that you must select a managed identity role assignment. Select the **Assign role** button.
1.  You can opt in to VI migration by selecting the **Migrate content** tab. The migration prompt appears.
1.  Select **Request migration** to continue. When the migration request is received, a success notification appears, the Migrate content tab disappears, and the banner disappears.

### [Connect a classic account with the API](#tab/connectapi)

1.  Invoke Create or Update Account ARM API for your account. In the request body, set the *storageServices* properties (`resourceId` and `userAssignedIdentity`) with the new storage account you’ve created, and set the *accountId* property with the account ID of the VI Classic account.

    ```REST API
    PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.VideoIndexer/accounts/{accountName}?api-version=2024-01-01    
    ```

    See [Accounts - Create Or Update - REST API (Azure Azure AI Video Indexer)](/rest/api/videoindexer/accounts/create-or-update?view=rest-videoindexer-2024-01-01&tabs=HTTP&preserve-view=true) for more information.
  
1.  Opt in to migration process by invoking Start Account Migration API

    ```REST API
    POST https://api.videoindexer.ai/{location}/Accounts/{accountId}/AMSAssetsMigration[?accessToken]
    ```

    See [APIs: Details - Microsoft Azure API Management - developer portal (videoindexer.ai)](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Start-Account-Migration) for more information.

---

## Opt in to VI migration of an already updated account

To opt in to VI migration of an already updated account, you can use either the Azure portal or the API.

### Permissions

You must have a **Contributor** role on the Azure AI Video Indexer account.

### [Opt in in the Azure portal](#tab/optinportal)

1.  You can opt in to VI migration by selecting the **Migrate content** tab. The migration prompt appears.
2.  Select **Request migration** to continue. When the migration request is received, a success notification appears, the Migrate content tab disappears, and the banner disappears.

### [Opt in with the API](#tab/optinapi)

Include the access token in the request.

```REST API
POST https://api.videoindexer.ai/{location}/Accounts/{accountId}/AMSAssetsMigration[?accessToken]
```

See [APIs: Details - Microsoft Azure API Management - developer portal (videoindexer.ai)](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Start-Account-Migration) for more information.

---
