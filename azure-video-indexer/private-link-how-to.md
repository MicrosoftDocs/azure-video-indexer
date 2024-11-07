---
title: How to use private endpoints with Azure AI Video Indexer
description: This article is an overview of using Private Endpoints with Azure AI Video Indexer.
author: IngridAtMicrosoft
ms.author: inhenkel
ms.collection: ce-skilling-ai-copilot
ms.date: 11/07/2024
ms.service: azure-video-indexer
ms.topic: article
---

# How to use private endpoints with Azure AI Video Indexer (private preview)

This article shows you how to use a private endpoints with Azure AI Video Indexer. See the [use cases for private endpoints with Azure AI Video Indexer](private-link-overview.md) for a quick overview.

## Prerequisistes

None.

## Enable the private endpoint on the Azure AI Video Indexer account

When you [create the Azure AI Video Indexer account](create-account.md), you might not have configured networking. This is fine. You can configure networking after the account is created:

1. Sign in to the Azure portal.
1. Navigate to the Azure AI Video Indexer account you want to work with and select **Settings**, then **Networking**. The Public access screen appears.
1. If you have not completed the form for accessing this feature, the Disabled ratdio button is disabled and the message "The private endpoints feature is currently in private preview, so if you'd like to disable public access, fill out this form to join the preview." appears. Fill out [the form](https://aka.ms/vi-enable-private-endpoint) to join the private preview.
1. Once you have access, select the **Disable** radio button.
1. Select **+ Create a private endpoint**. The Create private endpoint blade appears.
1. Select the subscription you want to work with.
1. Select the resource group you want to work with or create a new one.
1. Enter a name for the endpoint in the **Name** field.
1. Select the virtual network and the subnet from the dropdowns.
1. Select the private DNS integration checkbox. The fields are autopopulated by the selections you chose earlier.
1. Select **Add**.
1. Select **Review + create**.
1. Wait for the validation.
1. Select **Create**.
    1. If you are doing this at the same time you are creating a Azure AI Video Indexer account, Wait for the additional validation.
    1. Select **Create** again.
1. Wait for the deployment.
