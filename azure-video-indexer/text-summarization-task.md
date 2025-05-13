---
title: Use textual summarization
description: This article explains how to use Azure OpenAI textual summarization with Azure AI Video Indexer.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 3/24/2025
ms.service: azure-video-indexer
ms.topic: how-to
---

# Use textual summarization

This article shows you how to use textual summarization with Azure AI Video Indexer. This example uses Azure OpenAI model deployments.

> [!NOTE]
> This feature only works with a paid account. Create a [paid account](create-account.md).

## Prerequisites

Review the [overview of textual summarization](text-summarization-overview.md) and the following prerequisites.

### Cloud

- An [Azure AI Video Indexer paid account](connect-azure-open-ai-task.md) connected to an Azure OpenAI account.
- Access granted to Azure OpenAI in the desired Azure subscription. Currently, access to this service gets granted by application. For more information about how to apply for access to Azure OpenAI, see [Limited access for Azure OpenAI Service](https://aka.ms/oai/access).
- An Azure OpenAI [GPT-35-Turbo, GPT-4, GPT-4o, or GPT-4O-mini](/azure/ai-services/openai/how-to/working-with-models?tabs=powershell) deployment. To benefit from keyframes based summaries, you must select an Azure OpenAI model that accepts visual input. For more information, see [Azure OpenAI Service models](/azure/ai-services/openai/concepts/models?tabs=python-secure%2Cglobal-standard%2Cstandard-chat-completions). 
- The Prompt Shields for direct attacks (jailbreak) filter should be added to the deployment. Read more here: [Use content filters (preview) with Azure OpenAI Service](/azure/ai-services/openai/how-to/content-filters#understand-other-filters).
- We recommended that you configure harmful content filters for categories such as “Violence,” “Hate,” “Sexual,” and “Self-harm.” While these filters aren't mandatory, you should set them to either "Medium" or "Low" to filter out content of at least the Medium level of harmfulness. This setting ensures that content with a harmfulness rating of medium or higher is blocked. For increased safety, you can opt for a stricter setting. Once configured, save the content filter settings.  

- A video uploaded to your Azure AI Video Indexer library.

> [!NOTE]
> Azure AI Video Indexer is unable to connect to fine-tuned models.

### Edge devices

Azure AI Video Indexer enabled by Arc allows you to use Azure AI Video Indexer on edge devices. The following are the technical requirements for this use case:

- Video Indexer Enabled by Arc of version number 1.1.23 or higher.
- Hardware requirements: GPU or Intel CPUs. We don't recommend running on CPUs due to slow speed. We recommend using Nvidia V100 or higher GPUs. If there are multiple GPU nodes, you can add a node selector to select the desired node.
- Using [keyframes](text-summarization-overview.md#textual-summarization-with-keyframes) as part of the summary requires Nvidia A100 or higher.
- Textual Video Summarization on the edge uses the Phi3.5 model only. For more hardware information, refer to the Phi 3.5 official release information.

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

## [Web](#tab/web)

## Generate a text summary with or without keyframes

You can use the Azure AI Video Indexer web portal to summarize text.

1. If you don't have the web portal open already, open the [Azure AI Video Indexer web portal](https://api-portal.videoindexer.ai/).
1. Upload a file and wait for it to index.
1. Select the video to navigate to the media page.
1. If you want to use keyframes to produce the summary, select the **Include visual keyframe insights to get better quality summary** option.
1. Select **Generate summary**. The textual summary is generated.

> [!NOTE]
> If you aren't seeing the **Generate summary** button, you might be using a trial account. To use this feature, create a [standard account](create-account.md).

## Summary customizations

Once the summary is generated, you can make adjustments to it by customizing the summary style or changing the model deployment.

### Customize summary style
You can also customize the summary by selecting the **Customize summary** icon. You can choose from **Short**, **Medium**, or **Long** summary lengths, and you can choose **Neutral**, **Casual**, or **Formal** as a summary style. Once you make your choices, select **Generate again**.

### Change model deployment

1. Select the **Customize summary** icon.
1. Select the model deployment you want to use from the **Model deployment** dropdown list.
1. Select **Generate again**.

> [!NOTE]
> Remember that the model deployment is a combination of the model and the filters. Additionally, every time you customize the text summary it represents an API PUT request.

## [API](#tab/api)

## Create a video summary

### Generate an access token

Generate an access token in the Azure portal:

1. Navigate to your Azure AI Video Indexer account.
1. From the menu, select **Management** then **Management API**.
1. From the **Permission** type dropdown, select **Contributor**.
1. From the **Scope** dropdown, select **Account**.
1. Select **Generate**. The access token is generated.
1. Copy the access token to your clipboard.

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

## Customize a textual video summary

Customize textual summarization with the optional `addToEndOfSummaryInstructions` parameter to the [Create Video Summary API](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Video-Summary). Use this parameter to enhance the textual summary of your video by including additional information in natural language. For example, you can use it to include information about the people appearing, general topics discussed, and brands mentioned in the video.

Customizing your summary ensures that your video summary is comprehensive and tailored to your needs.

To customize a summary:

1. Access the Video Indexer API. You need to make a POST call to the [Create Video Summary API](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Video-Summary).
2. Add the `addToEndOfSummaryInstructions` parameter. Include the `&addToEndOfSummaryInstructions=["Your prompt"]` parameter in the URL when making the POST call. This parameter is optional and can be used to add additional information to the summary. "Your prompt" is the additional information you want to include in the summary.
3.	URL encode the parameter. Make sure the additional information is URL encoded. For example, if you want to add "the known people or celebrities appearing in the video, the general topics of the video, and all of the brands mentioned in it", use: `&addToEndOfSummaryInstructions=the+known+people+or+celebrities+appearing+in+the+video,+the+general+topics+of+the+video+and+all+of+the+brands+mentioned+in+it`.

Here's an example of how to use the `addToEndOfSummaryInstructions` parameter:

```http
POST
https://api.videoindexer.ai/{location}/Accounts/{accountId}/Videos/{videoId}/Summaries/Textual?deploymentName={deploymentName}&includedFrames={None/Keyframes}&addToEndOfSummaryInstructions=the+known+people+or+celebrities+appearing+in+the+video,+the+general+topics+of+the+video+and+all+of+the+brands+mentioned+in+it
```

The example post call results in a summary that ends with content like:

```
Known people or celebrities appearing in the video: Satya Nadella
General topics: Technology, Microsoft Build Keynotes, AI, GenAI
Brands mentioned: Microsoft, Phi Models.
```

## Get a video summary

First, check on the summary status. Until the summary job is finished, the state value shows "Processing," but there's no summary in the response. When the summary job is finished, the summary is displayed in the response.

1. Select **GET Video Summary**.
1. Enter the account ID, the video ID, the summary ID, and the access token into the appropriate fields.
1. Select **Send**.

> [!NOTE]
> There's always a disclaimer available in the response about the summary. Also, there's a link to the job status API in the *Location* header.

## List video summaries

You can list the video summaries by page. Select **GET List Video Summaries** and use the same parameters already described. If there's a large list of summaries, use the page parameters to return the response in pages. Use the summary ID for the GET Video Summary request.

## Delete a video summary

Deleting the video summary is as simple as selecting DEL Delete Video Summary, using the same parameters, and selecting **Send**.

## Error codes

| Request | Status code | Error Message | Error Type | Reason | Mitigation |
|---|--|--|--|--|--|
|  |  |  |  |  |  |
| Create-Video-Summary | 400 | Account isn't connected to Azure OpenAI | INVALID_INPUT |  | Go to the Azure portal and connect an Account. |
| Create-Video-Summary | 400 | No deployment found with this name: {deploymentName} | INVALID_INPUT |  | Check the deployment name string. |
| Create-Video-Summary | 400 | This model doesn't support generating summaries. | INVALID_INPUT |  | Choose a different model  |
| Create-Video-Summary | 400 | Couldn’t generate a summary because the AI model must have content filters added to avoid showing harmful content. " +  \$"Add the following policies: {string.Join(",", Enum.GetValues\<FilterType\>().Where(type =\> type != FilterType.JailBreak))}." +  \$"Set the AllowedContentLevel to at least {AllowedContentLevel.Medium} for both sources {FilterSource.Prompt} and {FilterSource.Completion} | SUMMARY_FILTERS_NOT_FOUND |  | See error message. |
| Create-Video-Summary | 400 | Video not found | VIDEO_NOT_FOUND |  |  |
| Create-Video-Summary | 400 | Video indexing hasn't finished successfully yet | VIDEO_ALREADY_IN_PROGRESS |  |  |
| Create-Video-Summary | 400 | Invalid summary length value '{length}' | INVALID_INPUT |  |  |
| Create-Video-Summary | 400 | Invalid summary style value '{style} | INVALID_INPUT |  |  |
| Get-Video-Summary | 200 | NA | NA |  |  |
| Get-Video-Summary | 404 | Summary '{summaryId}' not found for video '{videoId}' | NOT_FOUND |  |  |
| Get-Video-Summary | 200 | Couldn’t generate a summary because the video content was flagged as harmful. For details, see [Content filters](/azure/ai-services/openai/concepts/content-filter). | NA | All sections in the video have triggered the content filter. | There's no solution for the specific video. |
| Get-Video-Summary | 200 | Not enough information in order to generate summary. | NA | The video insights don't contain enough information in order to create prompts for Azure OpenAI | If the preset of the video doesn't contain all the models, then reindexing with a more advanced preset that contains audio might help. |
| Get-Video-Summary | 200 | Couldn't get Azure OpenAI deployments for resource {_resourceName} |  |  |  |
| Get-Video-Summary | 200 | Deployment {DeploymentName} doesn't exist |  |  |  |
| Get-Video-Summary | 200 | Azure OpenAI couldn't be reached. Try running the summary again later. |  |  | Try summarization job again later. |
| Create-Video-Summary |  |  |  | No role assignment |  |
| Get-Video-Summary |  |  |  | No role assignment |  |

---

## Troubleshooting

Before looking for specific solutions, be sure that you created the resources in the [Prerequisites](#prerequisites) section of the document.

### Generate summary doesn't appear

Your Azure OpenAI account might be connected to your Azure AI Video Indexer account incorrectly.

### Couldn't generate summary

- You need to add content filters to the deployment to avoid showing harmful content. Go back to the Azure OpenAI studio and add filters to your deployment.
- You created a permissive content filter for content that has sensitive or harmful content. The content filter needs to be at least Medium. If you set the content filter to Medium AND harmful content remains in the video, the filter is triggered. In this case, there's no solution.
- You didn't request a transcript or there might not be enough information generated during the indexing process.
- You might be using an advanced preset.
- The video might not have enough audio in it to create a transform.

### Unable to use a model deployment or deployment missing

- You didn't create a deployment.
- Someone changed or deleted the deployed model.

### Throttling

There might be too many requests being sent to VI. Wait for a few minutes and try again.

### You receive the error "filter not found"

If you get a filter not found error, you get a detailed error describing what is missing. The error might resemble the following example, but might have details about other missing things:

<pre>
ErrorType":"SUMMARY_FILTERS_NOT_FOUND","Message":"Couldn't generate a summary because the model needs to be set with the right content filters to avoid showing harmful content. Input filter 'Jailbreak' must be enabled with action set to 'Annotate and block'. Trace id: '00000000-0000-0000-0000-000000000000'.
</pre>

> [!NOTE]
> The jailbreak filter is only required when using a keyframes based summary or a regular summary, as of November 1, 2024.

To resolve the jailbreak issue:

1. Select **Go to Azure Open AI studio**.
1. Select **Deployments**.
1. Select the deployment you're working with.
1. Select **Edit**.
1. Configure the filters to have at least Medium level for each category.
1. Apply [prompt shields for jailbreak attacks](/azure/ai-services/openai/concepts/content-filter?tabs=warning%2Cuser-prompt%2Cpython#prompt-shield-content).
1. Select **Create** filter.

## Other considerations

We recommend creating the Azure AI Video Indexer and Azure OpenAI accounts in the same region or you might experience performance issues.
