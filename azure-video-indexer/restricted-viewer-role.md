---
title: Manage access to an Azure AI Video Indexer account
description: This article talks about Video Indexer restricted viewer built-in role. This role is an account level permission, which allows users to grant restricted access to a specific user or security group. 
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/09/2024
ms.service: azure-video-indexer
ms.topic: how-to
---

# Manage access to an Azure AI Video Indexer account

In this article, you'll learn how to manage access (authorization) to an Azure AI Video Indexer account.

To see your accounts, select **User Accounts** at the top-right of the [Azure AI Video Indexer website](https://videoindexer.ai/). Trial accounts will have a label with the account type to the right of the account name.

## User management of ARM accounts

[Azure role-based access control (Azure RBAC)](/azure/role-based-access-control/overview) is used to manage access to Azure resources, such as the ability to create new resources or use existing ones. Using Azure RBAC, you can segregate duties within your team and users by granting only the amount of access that is appropriate. Users in Entra ID are assigned specific roles, which grant access to resources. 

Users with owner or administrator Entra ID permissions can assign roles to users or security groups for an account. For information on how to assign roles, see [Assign Azure roles using the Azure portal](/azure/role-based-access-control/role-assignments-portal). 

Azure AI Video Indexer provides three built-in roles. You can learn more about [Azure built-in roles](/azure/role-based-access-control/built-in-roles). Azure AI Video Indexer doesn't support the creation of custom roles. 

**Owner** - This role grants full access to manage all resources, including the ability to assign roles to determine who has access to resources.  
**Contributor** - This role has permissions to everything an owner does except it can't control who has access to resources.  
**Video Indexer Restricted Viewer** - This role is unique to Azure AI Video Indexer and has permissions to view videos and their insights but can't perform edits or changes or user management operations. This role enables collaboration and user access to insights through the Video Indexer website while limiting their ability to make changes to the environment.  

Users with this role can perform the following tasks: 

- View and play videos.  
- View and search insights and translate a videos insights and transcript.

Users with this role are unable to perform the following tasks: 

- Upload/index/re-index a video. 
- Download/embed video/insights.
- Change account settings.
- Edit insights.
- Create/update customized models.
- Assign roles.
- Generate an access token.

Disabled features will appear to users with the **Restricted Viewer** access as greyed out. When a user navigates to an unauthorized page, they receive a pop-up message that they don't have access. 

> [!Important]
> The Restricted Viewer role is only available in Azure AI Video Indexer ARM accounts. 
>

### Manage account access

If you're an account owner, you can add and remove roles for the account. You can also assign roles to users. Use the following links to discover how to manage access: 

- [Azure portal UI](/azure/role-based-access-control/role-assignments-portal)
- [PowerShell](/azure/role-based-access-control/role-assignments-powershell) 
- [Azure CLI](/azure/role-based-access-control/role-assignments-cli) 
- [REST API](/azure/role-based-access-control/role-assignments-rest) 
- [Azure Resource Manager templates](/azure/role-based-access-control/role-assignments-template) 

## Manager trial account users  

User management of trial accounts, including the creation of new users, is performed in the Account settings section of the Video Indexer website. This can be accessed by either: 

- Selecting the **User accounts** icon and then settings. 
- Selecting the **Account settings** icon.

### Share the account

1. In the **Account setting** section, select **Manage Roles** to view all the account users and people with pending invites. 
1. To add users, select **Invite more people to this account**. Users can receive an invitation but you also have the option to copy the invite link to share it directly. Once the invitation is accepted, you can define their role as either **Owner** or **Contributor**. See the [ARM Account user management](#user-management-of-arm-accounts) section for a description of the **Owner** and **Contributor** roles.

## Troubleshooting

If you see the following error message when you log in to the Azure portal, you must ask for a **Contributor** or **Restricted Viewer** role from the account owner to get access.

:::image type="content" source="media/common/you-need-permission-to-view-content.png" alt-text="An error message that states that you don't have permission to access the account."::: 
