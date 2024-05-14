---
title: Use Azure OpenAI text summarization with Azure AI Video Indexer
description: This article shows you how to use Azure OpenAI text summarization with Azure AI Video Indexer. 
ms.topic: how-to
ms.date: 04/27/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Use text summarization with Azure AI Video Indexer

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

This article shows you how to use text summarization with Azure AI Video Indexer. This example uses Azure OpenAI deployments.

## Prerequisites

- Review the overview of [texual summarization](text-summarization-overview.md).
- An [Azure OpenAI *gpt-35-turbo* or *gpt-4* deployment](/azure/ai-services/openai/how-to/working-with-models?tabs=powershell).
- Content filters at or above Medium set on the deployment. For more information about to use content filters, see [Content filtering](/azure/ai-services/openai/how-to/content-filters).
- An [Azure AI Video Indexer account](connect-azure-open-ai-task.md) connected to an Azure OpenAI account.
- Access granted to Azure OpenAI in the desired Azure subscription. Currently, access to this service is granted only by application. You can apply for access to Azure OpenAI by completing the [form](https://aka.ms/oai/access).
- A video uploaded to your Azure AI Video Indexer library.

> [!NOTE]
> Azure AI Video Indexer is unable to connect to fine-tuned models.

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

## [Web](#tab/web)

## Generate a text summary

You can use the Azure AI Video Indexer web portal to summarize text.

1. If you don't have the web portal open already open the [Azure AI Video Indexer web portal](https://api-portal.videoindexer.ai/).
1. Upload a file and wait for it to index.
1. Select **Generate summary**. The textual summary is generated.

## Summary customizations

Once the summary has been generated, you can make adjustments to it by customizing the summary style or changing the model deployment.

### Customize summary style
You can also customize the summary by selecting the **Customize summary** icon. You can choose from **Short**, **Medium** or **Long** summary lengths, and you can choose **Neutral**, **Casual**, or **Formal** as a summary style. Once you have made your choices, select **Generate again**.

### Change model deployment

1. Select the **Customize summary** icon.
1. Select the model deployment you want to use from the **Model deployment** dropdown list.
1. Select **Generate again**.

> [!NOTE]
> Remember that the model deployment is a combination of the model and the filters. Additionally, every time you customize the text summary it represents an API PUT request.

## [API](#tab/api)

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
> There is always a disclaimer available in the response about the summary. Also, there is a link to the job status API in the *Location* header.

## List video summaries

You can list the video summaries by page. Select **GET List Video Summaries** and use the same parameters already described. If there's a large list of summaries, use the page parameters to return the response in pages.

## Delete a video summary

Deleting the video summary is as simple as selecting DEL Delete Video Summary, using the same parameters, and selecting **Send**.

---

## Troubleshooting

Before looking for specific solutions, be sure that you created the resources in the [Prerequisites](#prerequisites) section of the document.

### Generate summary doesn't appear

You might not have connected your Azure OpenAI account to the Azure AI Video Indexer account correctly.

### Couldn't generate summary

- You need to add content filters to the deployment to avoid showing harmful content. Go back to the Azure OpenAI studio and add filters to your deployment.
- If you created a permissive content filter for content that has sensitive or harmful content, edit the sensitive content out of the video and try again.
- You might not have asked for a transcript or there might not be enough information generated during the indexing process.
- You may be using an advanced preset.
- The video may not have enough audio in it to create a transform.

### Unable to use a model deployment or deployment missing

- You might not have created a deployment.
- Someone may have changed or deleted the deployed model.

### Throttling 

There may be too many requests being sent to VI. Wait for a few minutes and try again.
