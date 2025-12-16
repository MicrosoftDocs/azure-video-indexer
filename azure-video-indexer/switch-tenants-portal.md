---
title: Switch between tenants on the Azure AI Video Indexer website
description: This article shows how to switch between tenants in the Azure AI Video Indexer website. 
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/06/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
ms.custom: sfi-image-nochange
appliesto:
  - Cloud-based Azure AI Video Indexer
---

# Switch between multiple tenants

When working with multiple tenants/directories in the Azure environment, you might need to switch between the different directories. 

When logging in the Azure AI Video Indexer website, a default directory loads the relevant accounts and lists them in the **Account list**.

> [!Note]
> Trial accounts are global and not tenant-specific. Hence, the tenant switching described in this article only applies to your ARM accounts.
>
> The option to switch directories is available only for users using Entra ID to log in. 

This article shows two options to solve the same problem - how to switch tenants:

- When starting [in the website](#switch-tenants-in-the-website).
- When starting [outside the website](#switch-tenants-outside-the-website).

## Switch tenants in the website

1. To switch between directories in the [Azure AI Video Indexer](https://www.videoindexer.ai/), open the **User menu** > select **Switch directory**.  
    :::image type="content" source="./media/switch-directory/avi-user-switch.png" border="true" alt-text="Screenshot showing how to switch directory." lightbox="./media/switch-directory/avi-user-switch.png" :::

There you can view all detected directories listed. The current directory is marked. When you select a different directory, **Switch directory** becomes available.

When selected, the authenticated credentials get used to sign in again to the Azure AI Video Indexer website with the new directory.

## Switch tenants outside the website

This section shows how to get the domain name from the Azure portal. You can then sign in with it into th the [Azure AI Video Indexer](https://www.videoindexer.ai/) website.

### Get the domain name

1. Sign in to the [Azure portal](https://portal.azure.com) using the same subscription tenant in which your Azure AI Video Indexer Azure Resource Manager (ARM) account was created. 
1. Hover over your account name (in the right-top corner).  
    :::image type="content" source="./media//switch-directory/account-attributes.png" border="true" alt-text="Screenshot showing where to select account." lightbox="./media//switch-directory/account-attributes.png" :::
2. Get the domain name of the current Azure subscription. You need it for the last step in the next.

If you want to see domains for all of your directories and switch between them, see [Switch and manage directories with the Azure portal](/azure/azure-portal/set-preferences#switch-and-manage-directories).

### Sign in with the correct domain name on the VI website

1. Go to the [Azure AI Video Indexer](https://www.videoindexer.ai/) website.
1. Select **Sign out** after pressing the button in the top-right corner.
1. On the VI website, press **Sign in** and choose the Microsoft Entra ID account.
1. Select **Use another account**.
1. Choose **Sign-in with other options**.
1. Select **Sign in to an organization**.
1. Enter the domain name you copied in the [Get the domain name from the Azure portal](#get-the-domain-name) section.