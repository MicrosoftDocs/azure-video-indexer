---
title: Use Azure OpenAI text summarization with Azure AI Video Indexer
description: In this article, you'll learn how to use Azure OpenAI text summarization with Azure AI Video Indexer. 
ms.topic: how-to
ms.date: 04/27/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Use Azure OpenAI text summarization with Azure AI Video Indexer

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

In this article, you'll learn how to use Azure OpenAI text summarization with Azure AI Video Indexer.

## Prerequisites

- An [Azure AI Video Indexer account](/azure/azure-video-indexer/create-account?tabs=portal).
- Access granted to Azure OpenAI in the desired Azure subscription. Currently, access to this service is granted only by application. You can apply for access to Azure OpenAI by completing the [form](https://aka.ms/oai/access).
- An [Azure OpenAI *gpt-35-turbo* or *gpt-4* deployment](/azure/ai-services/openai/how-to/working-with-models?tabs=powershell).
- A video uploaded to your Azure AI Video Indexer library.

## Open web pages in your browser

It's easier to follow these instructions if you already have the needed web pages open. Copy and paste the following parameters to your favorite text editor. Here's a list to get you started.

- VI account ID:
- video file ID: 
- deployment name:
- 

1. Open the [Azure portal](https://portal.azure.com) in one tab or window, and sign in.
    1. Navigate to the Azure AI Video Indexer account page for the account ID.
    1. Navigate to the Azure OpenAI account page
        1. From the menu, select Model deployments, then select Manage deployments. The Azure OpenAI Studio opens. Copy the Deployment Name you want to use. 
1. Open the [Azure AI Video Indexer web portal](https://www.videoindexer.ai) in another tab or window and sign in.
    1. Navigate to the library page, choose a video, then right-click on it for the video file ID.
1. Open the [Azure AI Video Indexer API](https://api-portal.videoindexer.ai/) in another tab or window and sign in.

## Generate an access token

Generate an access token in the Azure portal:

1. Navigate to your Azure AI Video Indexer account.
1. From the menu, select **Management** then **Management API**.
1. From the **Permission** type dropdown, select **Contributor**.
1. From the **Scope** dropdown, select **Account**.
1. Select **Generate**. The access token is generated.
1. Copy the access token to your clipboard.

## Create a video summary

You should have all of the parameters needed to create a video summary ready to go in your text editor.

1. On the Azure AI Video Indexer API page, search for *summarization*. 
1. Select the **Try it** button next to *Create Video Summary*. The API parameters pane opens.
1. Paste the access token on your clipboard into the **accessToken** field.
1. Select the location from the **location** dropdown list.
1. Copy and paste the VI account ID in the **accountId** field.
1. Copy the video file ID and paste it into the **videoId** field.
1. Choose the length of the summary, medium, short or long, from the **length** dropdown list.
1. Choose the style, neutral, casual, or formal, from the **style** dropdown list.
1. Select **Send**.

In the response, there's a summary ID. Copy that ID to your clipboard.

## Get a video summary

First, check on the summary status. Until the summary job is finished, the state value shows "Processing," but there's no summary in the response. When the summary job is finished, the summary is displayed in the response.

1. Select **GET Video Summary**.
1. Enter the account ID, the video ID, the summary ID, and the access token into the appropriate fields.
1. Select **Send**.

> [!NOTE]
> There is always a disclaimer available in the response about the summary.

## List video summaries

You can list the video summaries by page. Select **GET List Video Summaries** and use the same parameters already described. If there's a large list of summaries, use the page parameters to return the response in pages.

## Delete a video summary

Deleting the video summary is as simple as selecting DEL Delete Video Summary, using the same parameters, and selecting **Send**.


 


