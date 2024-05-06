---
title: Use Azure AI Video Indexer to create prompt content 
description: This article shows you how to use Azure AI Video Indexer to create prompt content. 
ms.topic: how-to
ms.date: 05/06/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Use Azure AI Video Indexer to create prompt content

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

This article shows you how to Use Azure AI Video Indexer to create prompt content.

## Prerequisites

- An [Azure AI Video Indexer account](/azure/azure-video-indexer/create-account?tabs=portal).

## Open web pages in your browser

It's easier to follow these instructions if you already have the needed web pages open. Copy and paste the following parameters to your favorite text editor. Here's a list to get you started:

- VI account ID:
- video file ID: 
- deployment name:
- access token:

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

## Create prompt content

You should have all of the parameters needed to create a video summary ready to go in your text editor.

1. On the Azure AI Video Indexer API page, search for *prompt*. 
1. Select the **Try it** button next to *Create Prompt Content*. The API parameters pane opens.
1. Select the location from the **location** dropdown list.
1. Copy and paste the VI account ID in the **accountId** field.
1. Copy the video file ID and paste it into the **videoId** field.
1. Choose the language model you want to use, *LLama2*, *Phi2*, *GPT3_5Turbo*, or *GPT4* from the **modelName** dropdown list.
1. Choose the prompt style, *Full* or *Summarized*, from the **style** dropdown list.
1. Paste the access token on your clipboard into the **accessToken** field.
1. Select **Send**.

If there aren't any issues with the request, the response shows *HTTP/1.1 202 Accepted*.

### Check job status

It takes a few minutes for the prompt job to complete. If you would like to check on the job status, you can use the **Job Status** request by using all of the same parameters for the Create Prompt Content request. Find the Job Status request by using the search field as you did before.

## Get prompt content

1. Select **Get Prompt Content**.
1. Enter the account ID, the video ID, the summary ID, and the access token into the appropriate fields.
1. Select **Send**.

The prompt content will be in the response.

### Sample response

```json

TTP/1.1 200 OK

cache-control: max-age=18000, private
content-type: application/json; charset=utf-8
expires: Tue, 07 May 2024 03:23:26 GMT

{
    "partition": null,
    "name": "portlandia",
    "sections": [{
        "id": 0,
        "start": "0:00:00",
        "end": "0:00:10.966667",
        "content": "[Video title] portlandia\n[Known people] Fred Armisen, Carrie Brownstein\n[Detected objects] cell phone,
        dining table, laptop\n[Visual labels] human face, electronics, clothing, person, indoor, wall, glasses, laptop\n[OCR] 
        GADGETS, BUZZ, CELEBS, TECH, ENTERTAINMENT, WORLD, THE PUFFINGTON HOST, TOP TEN FAMILY PHOTOS, playlist, Fri 5:30a, 2hr. 
        33 min HD, \"Finding Mr. Write\", 2011. Woman searches for romance online., My Playlist, Search, Finding Mr. Write, 
        Juggling World, Soccer Cousins, Hide and Seek Championships, Mind-fi Update, IFC\n[Transcript] Top Ten family photos.\nCan 
        you send one more text?\nMP3's I want to just my DVR Oh please.\nGo check my Facebook update.\nI can Tumblr, Fred.\nSweet, 
        please, I'm checking my."
    }]
}

```
