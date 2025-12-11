---
title: Azure AI Video Indexer release notes and updates
description: Stay updated on the latest features, bug fixes, and known issues. Explore new capabilities and enhancements now.
author: cwatson-cat
ms.author: cwatson
ms.collection: ce-skilling-ai-copilot
ms.date: 12/10/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ai-usage: ai-assisted
ms.topic: release-notes
#customer intent: As a video content manager, I want to track the latest Azure AI Video Indexer features and updates so that I can use new capabilities and plan my workflows.
---

# Azure AI Video Indexer release notes

Revisit this page to view the latest updates.

To stay up-to-date with the most recent Azure AI Video Indexer developments, this article provides you with information about:

* The latest releases
* Known issues
* Bug fixes
* Deprecated functionality

## November 2025

### Real-time analysis (Preview) for Azure AI Video Indexer enabled by Azure Arc

Azure AI Video Indexer enabled by Azure Arc introduces real-time analysis, enabling real-time video intelligence at the edge. Extract actionable insights from live video streams with ultra-low latency and complete data privacy, keeping all video data on-premises. Azure Arc provides centralized management and scalability.

For more information, see [Live video analysis overview](live-analysis.md).

New capabilities in real-time analysis:

- **Agentic intelligence:** Modular, agent-based architecture with specialized AI agents trained to detect specific events. Prebuilt agents support detections such as safety hazards, customer experience issues, or operational anomalies. Use the API to trigger an agent and provide instructions for the events you want to detect. You don’t need to know which agent is best for the task - VI routes the queries to the appropriate agent. 

- **Custom AI insights with natural language:** Define custom detection logic using natural language to monitor specific objects or situations. No technical expertise required. Describe what you want to detect and upload supporting images or negative examples to fine-tune detection. Available through both API and portal.

- **Event summarization:** Generate end-of-shift summaries with your own focus, to get a textual summary from your video footage. Help teams quickly review key events and operational outcomes.

- **Area of interest:** Define specific regions within the video frame where you want to focus on the analysis.

For more information, see the following articles:

- [Real-time video analysis overview](https://aka.ms/VI-LiveAnalysis-Overview)
- [Manage real-time analysis extensions](https://aka.ms/VI-LiveAnalysis-QuickStart)
- [Create custom insights](live-ai-insights-catalog.md)
- [Create an event summary for camera footage](live-event-summary.md)

- [https://review.learn.microsoft.com/en-us/azure/azure-video-indexer/live-area-interest?branch=main](/azure/azure-video-indexer/live-area-interest?branch=main)

## May 2025

### Added support to customize textual summarization

Added support to customize textual summarization with the optional `addToEndOfSummaryInstructions` parameter to the [Create Video Summary API](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Video-Summary). This parameter lets you enhance the textual summary of your video by including additional information using natural language. For example, you can use it to include information about the people appearing, general topics discussed, and brands mentioned in the video.

For more information, see [Customize a textual video summary](text-summarization-task.md?tabs=api#customize-a-textual-video-summary).

## April 2025

### Improved error messaging

When you try to index an unsupported file type, the response returns an `UnsupportedFileType` error. For more information about supported file types, see [Supported file formats](avi-support-matrix.md#supported-file-formats).

## March 2025

### General availability of Azure AI Video Indexer enabled by Arc

Azure AI Video Indexer enabled by Arc is now generally available. Now, you can run Video Indexer in your edge environment to generate audio and video insights and textual summaries on videos in more than 30 source languages. For more information, see [Azure AI Video Indexer enabled by Arc](arc/azure-video-indexer-enabled-by-arc-overview.md).

### Azure AI Video Indexer support for private endpoints

Azure AI Video Indexer support for private endpoints is now generally available. Now, organizations can enhance security by using private endpoints to allow clients on a virtual network to securely access data over a Private Link. It ensures data traffic travels privately via Microsoft's backbone network, instead of using public endpoints. For more information, see [Private endpoints with Azure AI Video Indexer](private-endpoint-overview.md).

## February 2025

### Added Indonesian and Lithuanian as source languages

We added support for videos using the Indonesian and Lithuanian source languages. For a list of supported languages, see [Language support in Azure Video Indexer](language-support.md).

### URL change for widget mediator.js file

Azure AI Video Indexer changed the URL to access the mediator.js file, which enables the embedded video player and insight widgets to interact. If your website uses the mediator.js file, update the URL before May 1. The old URL stops working on May 1, after which the player and insight widgets won't be able to interact.

Old mediator.js URL: ```https://breakdown.blob.core.windows.net/public/vb.widgets.mediator.js```

New mediator.js URL: ```https://aka.ms/vi-mediator-file```

For more info, see [Embed widgets in your app or blog](video-indexer-embed-widgets.md#embed-widgets-in-your-app-or-blog-recommended).

### Multi-modal video summarization now generally available

Multi-Modal Video Summarization is now generally available for Azure Video Indexer. This feature uses the latest LLM and SLM technology such as Azure OpenAI and Phi models to provide comprehensive summaries of video content by combining insights from multiple modalities, including audio, visual, and text.

## January 2025

### Multimodal Video Summarization with GPT-4o

Our Multimodal Video Summarization now supports GPT-4o, generating more accurate summaries. To use Multimodal Video Summarization, see [Use textual summarization](text-summarization-task.md).

### Enhanced Multimodal Textual Video Summarization with Keyframes

We added improvements to our Multimodal Textual Video Summarization feature. The updated logic now better captures video content by integrating more relevant keyframes, resulting in more accurate summaries.

### Added Filipino as a source language

We added support for videos using the Filipino source language. For a list of supported languages, see [Language support in Azure Video Indexer](language-support.md).

### Added option to recognize spoken punctuation marks in audio

We added a new optional parameter, PunctuationMode, to our Upload and Reindex APIs. This parameter controls whether to recognize explicitly spoken punctuation marks when transcribing audio. For example, a spoken "period" is transcribed as a period `.`, and `dot dot dot` as an ellipsis `...`. For more information, see our [developer portal](https://api-portal.videoindexer.ai).

## December 2024

### Filters Policy updates to Multimodal Video Summarization with Azure OpenAI

We updated our policy for harmful content filters in Multimodal Textual Video Summarization. These filters aren't mandatory anymore, but we still recommend configuring them to help ensure that harmful content is blocked. If you want to completely disable the harmful content filters, sign up in the following form: [Azure OpenAI Limited Access Review: Modified Content Filtering](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR7en2Ais5pxKtso_Pz4b1_xUMlBQNkZMR0lFRldORTdVQzQ0TEI5Q1ExOSQlQCN0PWcu).

Additionally, textual video summarization now supports the Prompt Shields for direct attacks (jailbreak) filter. We recommend adding this filter to your deployment.

For details about the filters required to benefit from Multimodal Video Summarization with Azure OpenAI, see [Use textual summarization](text-summarization-task.md).

## November 2024

### Multimodal Video Summarization - Cloud and edge

We're excited to introduce Multimodal Video Summarization, which enhances our textual video summarization by analyzing keyframes along with audio and video insights. This feature is available both in the cloud, powered by Azure OpenAI, and on the edge as part of VI enabled by ARC. It utilizes the latest Phi3.5 visual model, which you can configure to run with GPUs for improved performance.

### Enhanced Prompt Content API

Our Video-to-Text API, also known as the [Prompt Content](./prompt-overview.md) API, now supports more models: Llama2, Phi3, Phi3.5, GPT-4O, and GPT-4O Mini. This enhancement provides you with greater flexibility when converting video content to text and opens up more opportunities for you when using Azure Video Indexer. You can gather information from Azure Video Indexer in a prompt format that you can customize by selecting the model name and adjusting the prompt style. The "Summarized" style is ideal for tasks like video summaries, naming videos, and describing main events, while the "Full" style is more suited for Q&A, RAG, and search use cases. For more information about this API, see [Azure Video Indexer Operations and Prompt Content](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Prompt-Content).

## October 2024

### New sample code

We added [new sample code](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/ExportVideoDataToADX) for exporting Azure AI Video Indexer data to Azure Data Explorer using Logic Apps.

## August 2024

### Enhanced security for Textual Video Summarization

Textual Video Summarization now includes support for preventing jailbreak attack risks. You must add this new security filter to your AOAI in order to benefit from the language model based Textual Video Summarization. For more information, see [Textual Video Summary with Azure OpenAI](/azure/azure-video-indexer/text-summarization-task?tabs=web#prerequisites).

### Textual video summary on an edge device

We released the blog post [Azure AI Video Indexer & Phi-3 introduce Textual Video Summary on the edge: Better Together story](https://techcommunity.microsoft.com/t5/ai-azure-ai-services-blog/azure-video-indexer-amp-phi-3-introduce-textual-video-summary-on/ba-p/4190931).

<!-- Removed 9/25/24 not released
### Shot detection algorithm update

We enhanced shot detection by integrating a neural network that significantly improves the service's ability to detect shot transitions, especially gradual ones. This update also has a positive impact on other features like scene detection and summarization.
-->

## July 2024

### Textual summarization on VI enabled by Arc

The textual summarization capability is now available on the VI enabled by Arc extension by using the latest Phi 3 model. You can benefit from the same functionality as in the cloud, including customizing the summary with several settings: Formal, Casual, Short, and Long.

### Language identification improvements

- Turnover time and quality of single language identification improved.
- If there are multiple languages in the file (and you asked for a single language identification):
    - The most dominant language, the language that appears for the longest duration, is returned.
    - The artifact contains all the languages identified by speech in the original video.
- The transcript includes only the lines of the most dominant language and excludes lines containing different languages.

### Player and accessibility improvements

The website player was updated to the latest version of the Shaka base. The player is also included in the widgets.

Accessibility improvements were implemented for the website.

## June 2024

### Code samples

- To make finding relevant video content easier for learners and trainers, use Azure AI Video indexer with Microsoft Azure OpenAI. See the blog post [Enhancing Training Search Experience using Azure AI Video Indexer](https://techcommunity.microsoft.com/t5/ai-azure-ai-services-blog/enhancing-training-search-experience-using-azure-ai-video/ba-p/4160409) and the [source code](https://github.com/Azure-Samples/azure-video-indexer-samples/blob/master/VideoQnA-Demo/README.md).
- Use Azure LogicApps to classify cars detected in a video. The sample uses Video Indexer's Bring Your Own capability to detect objects and Azure OpenAI's GPT-4 for enhanced classification. See the [YouTube demo](https://www.youtube.com/watch?v=yMqJufR9Rfs) and the [sample code](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/LogicApp-Samples).

### Increased file duration limit

All presets now support the indexing of files up to six hours in length (the previous limit was four hours) and the Basic Audio preset supports indexing of files up to 12 hours in length.

## May 2024

### Textual summarization

Azure AI Video Indexer now provides a brief summary of what a video is about without having to watch the entire video. It can save you time by digesting long videos and giving you the gist in a shorter format. It distills lengthy videos into concise, digestible summaries.

It uses summarization algorithms to identify the most relevant insights for the video. It involves scoring insights based on their importance and relevance to the overall theme. A user-friendly interface allows you to input videos and customize the type of summary you need.

You can customize the summary by selecting Short, Longer, Formal, or Casual and specify the specific model deployment.

For more information about textual summarization, see [Textual Summarization Overview](text-summarization-overview.md).

### Azure OpenAI integration

Azure AI Video Indexer now offers an integration with Azure OpenAI. You can connect your Azure OpenAI resource when creating a new Azure Video Indexer account or add it to your existing Azure Video Indexer account. When you connect VI with Azure OpenAI, you can use the Textual summary capability, available from the API and from the portal.

For more information about connecting Azure OpenAI to your VI account, see [Create or update an Azure AI Video Indexer account with an Azure OpenAI connection](connect-azure-open-ai-task.md).

### Expansion of Prompt Content API

Azure AI Video Indexer's Prompt Content API now supports more language models: Phi 2, Llama, and GPT 4V. When you use the Prompt Content API with GPT 4V, it outputs the keyframes that the language model can analyze, along with the other insights.

## April 2024

### Exclude models

You can now exclude models when indexing through both the VI Website and API. When uploading a video to index, select **Advanced settings** > **Indexing presets** and then select the AI models to exclude from the indexing results. This feature enables more efficient indexing and VI results only containing the insights you're interested in.

### New availability region

Azure AI Video Indexer is now available in Germany West Central region.

## February 2024

### AMS-less accounts and migration guidance

- All new VI account video packaging, streaming, and encoding is performed by VI. Now you can't create AMS-based VI accounts. See the [new account create guide](create-account.md).
- VI encoding and packaging is billed at a flat rate of one cent per minute with free streaming.
- You can update your VI accounts from AMS-based to the new AMS-less account type.
- You can opt in to have your AMS VI assets reprocessed and migrated by VI, so you can continue to access your videos and insights. The migration begins in late March.
- Video Indexer webapp and widgets use a new media player that is highly performant and no longer use Azure Media Player.

The following documentation guides you through the account and asset migration process:

- See the new [API version](/rest/api/videoindexer/accounts?view=rest-videoindexer-2024-01-01&preserve-view=true).

### TLS 1.3 support

We support TLS 1.3, the latest version of the Transport Layer Security (TLS) protocol. TLS 1.3 encrypts data to provide a secure communication channel between two endpoints.

### Azure AI Video Indexer deployed in the Sweden Central and US West3

You can now create an Azure AI Video Indexer paid account in the Sweden Central and US West3 regions.

## January 2024

### New LLM prompt content

You can now connect your video insights to Large Language Model (LLMs) for tasks like summarization and question answering. The API converts your video insights into a "prompt-ready" text format for use with LLMs. For more information, see [Azure AI Video Indexer with LLM prompts](prompt-overview.md).

## December 2023

### New preset option - Basic Video

Video Indexer added a new indexing preset option, Basic Video. It's also available on the VI enabled by Arc extension. It's a low-cost indexing option that includes many useful AI insights, including OCR, object detection, and visual labels. Basic Video can be used to generate insights together with Basic Audio (Basic Audio and Video) or on its own (Basic Video only). To learn more about your indexing options, see the [Indexing configuration guide](indexing-configuration-guide.md#indexing-options).

### Get Frames API

You can now extract frames from an indexed video for a selected video section by making a `FramesSasUrls` request. For more information, see [FrameSelection](azure-video-indexer-enabled-by-arc-bring-your-own-model-overview.md#frame-selection).

### Bring Your Own Model (Preview) updates

- Added UI support for custom insights.
- Added search support for custom insights.

For more information, see [Bring Your Own AI Model](azure-video-indexer-enabled-by-arc-bring-your-own-model-overview.md).

### Search by object on the Azure AI Video Indexer website and API

You can now use the search feature to find videos with specific objects, such as cars or motorcycles, on the [Azure AI Video Indexer website](https://www.videoindexer.ai/) or by using a [search](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Search-Videos) request.

## November 2023

In November, Video Indexer released the following features:

### Azure AI Video Indexer enabled by Arc (Preview)

You can use Video Indexer for your hybrid scenarios by hosting it on-premises in a Kubernetes cluster. For more information, see the [Azure AI Video Indexer enabled by Arc overview](azure-video-indexer-enabled-by-arc-overview.md). You can also try out the extension by following the [tutorial](azure-video-indexer-enabled-by-arc-quickstart.md).

### Bring Your Own Model (Preview)

You can use your own customized AI model and integrate the data with Video Indexer models. For more information, see [Bring Your Own AI model](azure-video-indexer-enabled-by-arc-bring-your-own-model-overview.md).

### Custom tags and free text per video (Preview)

You can add custom tags and free text as video metadata to any video in your Video Indexer account. This feature enables you to categorize and annotate your videos with any information that's relevant to you and your business. For example, you can add tags such as `product demo`, `customer testimonial`, or `internal training` or free text such as `This video shows how to use our new feature X` or `This video was recorded at our annual conference in Y`. You can add these tags and text to the area below the video once the video is indexed.

### Search based on custom tags and free text (Preview)

You can search for videos based on their custom tags and free text. This feature makes it easier and faster to find videos that match your criteria. You can search by using custom tags and free text in all supported languages. You can also combine these search options with other search filters, such as keywords, faces, labels, and emotions. To perform more complex queries, use the advanced search syntax. For example, you can search for videos that have the tag `product demo` and the free text `feature X`.

We added many improvements to the customized people model, which enhance the overall experience and accuracy. People models are gated AI models that you can train to recognize specific people in your videos. The new additions are:

### Indication on the quality of people model (Preview)

You can get an indication of the quality of your customized People model (poor, fair, good). The quality depends on the number of images used for labeling. The more images you use to label a person, the higher the probability of correctly identifying the person. For example, the probability of identifying a person with 24 labeled images is higher than the probability of identifying a person with two labeled images. You can see the number of images used for labeling each person in your customized People model page.

### Choose a custom people model as default (Preview)

You can now choose a customized People model as the default on the VI account user level. With this option, you don't have to select the model name for every video upload. It saves time and effort when you upload videos that you want to analyze with your customized People model.

### Grouping of unknown people in the video (Preview)

You can see the unknown people in your videos grouped by their appearance similarity. This feature helps you label the unknown people more easily and quickly, and it improves the accuracy of your customized People model. You can see the grouping of unknown people in your customization page. Choose **people**, then navigate to the **unknown people** tab. This feature could, for example, help you label a local celebrity or a local politician.

### Search results with max confidence score for identified person name (Preview)

You can search for the name of an identified person and get the times when the person appears in the video, with the maximum confidence score. This feature helps you decide which videos are the most relevant to explore. For example, you can search for "John Smith" and get the videos where John Smith gets recognized by your customized People model, along with the confidence score for each video.

### Avoid duplicate indexing uploads

Occasionally, you might unintentionally submit the same indexing job multiple times. To avoid this situation, a new optional query parameter was added: `preventDuplicates`. When set to `true`, the service rejects a file upload and returns a conflict if it was already indexed.

The Upload URL MD5 duplicate checks rely on the server response [Content-md5 header if exist RFC 1864: The Content-MD5 Header Field](https://www.rfc-editor.org/info/rfc1864). Storage providers commonly use it.

If you want to upload the same video repeatedly, set the parameter to `false`.

## October 2023

### New insight - Object detection

Video Indexer added a new insight, object detection, to both the standard and advanced video preset. Use this insight to identify and track a wide range of objects that appear in your videos. For more information, see [Azure AI Video Indexer object detection overview](object-detection.md).

## September 2023

### Changes related to AMS retirement

As a result of the June 30, 2024 [retirement of Azure Media Services (AMS)](/azure/media-services/latest/azure-media-services-retirement), Video Indexer announced many related retirements. They include the June 30, 2024 retirement of Video Indexer Classic accounts, API changes, and no longer supporting adaptive bitrate. For full details, see[Changes related to Azure Media Service (AMS) retirement](https://aka.ms/vi-ams-related-changes).

## July 2023

### Redact faces with Azure AI Video Indexer API

You can now redact faces with Azure AI Video Indexer API. For more information, see [Redact faces with Azure AI Video Indexer API](face-redaction-with-api.md).

### API request limit increase

Video Indexer increased the API request limit from 60 requests per minute to 120.

## June 2023

Azure Media Services retirement was announced.

<!-- Content archived 9/3/2024
### FAQ - following the Azure Media Services retirement announcement 

For more information, see [AMS deprecation FAQ](./retirement/ams-deprecation-faq.yml).
-->

## May 2023

### API updates

We're introducing a change in behavior that might require a change to your existing query logic. The change is in the **List** and **Search** APIs. The following table shows a detailed comparison between the current and the new behavior. You might need to update your code to use the [new APIs](https://api-portal.videoindexer.ai/).

|API	|Current|New|The update|
|---|---|---|---|
|List Videos|•	List all videos and projects according to the `IsBase` boolean parameter. If `IsBase` isn't defined, list both.<br/>•	Returns videos in all states (In progress/Processed/Failed).	|•	List Videos API returns only videos (with paging) in all states.<br/>•	List Projects API returns only projects (with paging).|• List Videos API is divided into two new APIs: **List Videos** and **List Projects**.<br/>•	The `IsBase` parameter no longer has a meaning. |
|Search Videos|•	Search all videos and projects according to the `IsBase` boolean parameter. If `IsBase` isn't defined, search both. <br/>•	Search videos in all states (In progress/Processed/Failed). |Search only processed videos.|•	Search Videos API only searches videos and not projects.<br/>•	The `IsBase` parameter no longer has a meaning.<br/>•	Search Videos API only searches processed videos (and not failed or in-progress ones).|

### Support for HTTP/2

We added support for HTTP/2 for our [Data Plane API](https://api-portal.videoindexer.ai/). [HTTP/2](https://en.wikipedia.org/wiki/HTTP/2) offers several benefits over HTTP/1.1, which continues to be supported for backwards compatibility. One of the main benefits of HTTP/2 is increased performance, better reliability, and reduced system resource requirements over HTTP/1.1. With this change, HTTP/2 is supported for both the Video Indexer [Portal](https://videoindexer.ai/) and our Data Plane API. Update your code to take advantage of this change.

### Topics insight improvements

We now support all five levels of IPTC ontology.

## April 2023

### Resource Health support

Azure AI Video Indexer is now integrated with Azure Resource Health. You can see the health and availability of each of your Azure AI Video Indexer resources. Azure Resource Health also helps with diagnosing and solving problems. You can set alerts to be notified whenever your resources are affected. For more information, see [Azure Resource Health overview](/azure/service-health/resource-health-overview).

### The animation character recognition model is retired

The **animation character recognition** model retired on March 1, 2023. For any related issues, [open a support ticket via the Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).

### Excluding sensitive AI models

Following the Microsoft Responsible AI agenda, Azure AI Video Indexer now allows you to exclude specific AI models when indexing media files. The list of sensitive AI models includes:

- Face detection
- Observed people
- Emotions
- Labels identification

This feature is currently available through the API, and is available in all presets except the Advanced preset.

### Observed people detection improvements  

For more information, see [Get observed people detection and matched faces insights](observed-matched-people-insight.md).

## March 2023

### Support for storage behind firewall

It's good practice to lock storage accounts and disable public access to enhance or comply with enterprise security policy. Video Indexer can now access nonpublic accessible storage accounts by using the [Azure Trusted Service](/azure/storage/common/storage-network-security?tabs=azure-portal#trusted-access-based-on-a-managed-identity) exception with Managed Identities. You can read more about how to set it up in our [how-to](storage-behind-firewall.md).

### New custom speech and pronunciation training

Azure AI Video Indexer added a new custom speech model experience. The experience includes the ability to use custom pronunciation datasets to improve recognition of mispronounced words, phrases, or names. Use the custom models to improve the transcription quality of content with industry specific terminology. To learn more, see [Customize speech model overview](customize-speech-model-overview.md).

### Observed people quality improvements

The observed people feature now supports people who are sitting. This support is in addition to the existing support for people who are standing or walking. This improvement makes the observed people model more versatile and suitable for a wider range of use cases. We also improved the model re-identification and grouping algorithms by 50%. The model can now more accurately track and group people across multiple camera views.

### Observed people indexing duration optimization

We optimized the memory usage of the observed people model, resulting in a 60% reduction in indexing duration when using the advanced video analysis preset. You can now process your video footage more efficiently and get results faster.

## February 2023

### Pricing

On January 1, 2023, we introduced the Advanced Audio and Video version for Advanced presets. With this version, you can report the use of each preset - Basic, Standard, and Advanced - with their own distinct meter on the Azure Billing statement. You can also see it in Cost analysis reports.

Starting February 1, we're excited to announce a 40% price reduction on the Basic Audio Analysis, Audio Analysis, and Video Analysis versions. We took into consideration feedback from our customers and market trends to make changes that benefit them. By reducing prices and introducing a new Advanced version, we're providing competitive pricing and more options for customers to balance costs and features. Additionally, we continue to improve and add more AI capabilities. You can take advantage of these cost savings when performing new or reindexing operations.

This change was implemented automatically. Customers who already have Azure discounts continue to receive them in addition to the new pricing.

|**Charge** | **Basic Audio Analysis** | **Standard Audio Analysis** | **Advanced Audio Analysis** | **Standard Video Analysis** | **Advanced Video Analysis** |
|--------------------- | ------------ | ---------------- | --------------------------- | --------------------------- | --------------------------- |
| Per input minute     | $0.0126      | $0.024           | $0.04                       | $0.09                       | $0.15               |

### Network Service Tag

Video Indexer supports the use of Network Security Tag to allow network traffic from Video Indexer IPs into your network. Starting January 22, we renamed our Network Security Service tag from `AzureVideoAnalyzerForMedia` to `VideoIndexer`. This change requires you to update your deployment scripts and/or existing configuration. See our [Network Security Documentation](network-security.md) for more info.

## January 2023

### Notification experience

The [Azure AI Video Indexer website](https://www.videoindexer.ai/) now has a notification panel where you can stay informed of important product updates, such as service impacting events, new releases, and more.

### Textual logo detection

**Textual logo detection** enables you to customize text logos to be detected within videos. For more information, see [Detect textual logo](detect-textual-logo.md).

### Switching directories

You can now switch Microsoft Entra ID directories and manage Azure AI Video Indexer accounts across tenants by using the [Azure AI Video Indexer website](https://www.videoindexer.ai/).

### Language support

* New languages are now supported: Irish, Bulgarian, Catalan, Greek, Estonian, Croatian, Latvian, Romanian, Slovak, Slovenian, Telugu, Malayalam, Kannada, Icelandic,  Armenian, Gujarati, Malay, and Tamil.
* Use an API to get all supported languages: [Get Supported Languages](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Supported-Languages).

For more information, see [supported languages](language-support.md).

### Face grouping

We reduced the number of low-quality face detection occurrences in the UI and insights.json. Enhancing the quality and usability through improved grouping algorithm.

## November 2022

### Edit speakers' names from the Azure AI Video Indexer website

You can now add new speakers, rename identified speakers, and modify speakers assigned to a particular transcript line by using the [Azure AI Video Indexer website](https://www.videoindexer.ai/). For details on how to edit speakers from the **Timeline** pane, see [Edit speakers with the Azure AI Video Indexer website](edit-speakers.md).

The Azure AI Video Indexer [upload video index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Video-Index) API provides the same capabilities.

## October 2022

### A new built-in role: Video Indexer Restricted Viewer

The limited access **Video Indexer Restricted Viewer** role is intended for the [Azure AI Video Indexer website](https://www.videoindexer.ai/) users. The role's permitted actions relate to the [Azure AI Video Indexer website](https://www.videoindexer.ai/) experience.

For more information, see [Manage access with the Video Indexer Restricted Viewer role](restricted-viewer-role.md).

### Slate detection insights (preview)

The following slate detection (a movie postproduction) insights are automatically identified when indexing a video by using the advanced indexing option:

* Clapperboard detection with metadata extraction.
* Digital patterns detection, including color bars.
* Textless slate detection, including scene matching.

For details, see [Slate detection](slate-detection-insight.md).

### New source languages support for STT, translation, and search

Now supporting source languages for STT (speech-to-text), translation, and search in Ukrainian and Vietnamese. It means transcription, translation, and search features are also supported for these languages in the [Azure AI Video Indexer](https://www.videoindexer.ai/) website, widgets, and APIs.

For more information, see [supported languages](language-support.md).

### Edit a speaker's name in the transcription through the API

You can now edit the name of the speakers in the transcription by using the Azure AI Video Indexer API.

### Word level time annotation with confidence score

Now supporting word level time annotation with confidence score.

An annotation is any type of additional information that you add to an existing text, such as a transcription of an audio file or an original text file.

For more information, see [Examine word-level transcription information](edit-transcript-lines-portal.md#examine-word-level-transcription-information).

### Azure Monitor integration enabling indexing logs

The new set of logs, described in the following section, enables you to better monitor your indexing pipeline.

Azure AI Video Indexer now supports Diagnostics settings for indexing events. You can now export logs monitoring upload, and reindexing of media files through diagnostics settings to Azure Log Analytics, Storage, Event Hubs, or a third-party solution.

### Expanded supported languages in LID and MLID through Azure AI Video Indexer API

Expanded the languages supported in LID (language identification) and MLID (multilanguage identification) using the Azure AI Video Indexer API.

The API now supports the following languages:

- Arabic (United Arab Emirates)
- Arabic Modern Standard
- Arabic Egypt
- Arabic (Iraq)
- Arabic (Jordan)
- Arabic (Kuwait)
- Arabic (Oman)
- Arabic (Qatar)
- Arabic (Saudi Arabia)
- Arabic Syrian Arab Republic
- Czech
- Danish
- German
- English Australia
- English United Kingdom
- English United States
- Spanish
- Spanish (Mexico)
- Finnish
- French (Canada)
- French
- Hebrew
- Hindi
- Italian
- Japanese
- Korean
- Norwegian
- Dutch
- Polish
- Portuguese
- Portuguese (Portugal)
- Russian
- Swedish
- Thai
- Turkish
- Ukrainian
- Vietnamese
- Chinese (Simplified)
- Chinese (Cantonese and Traditional)

To specify the list of languages to identify with LID or MLID when autodetecting, call [upload a video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video) API and set the `customLanguages` parameter to include up to 10 languages from the supported languages listed previously. The API compares the languages specified in the `customLanguages` parameter at a language level, so include only one locale per language.

For more information, see [supported languages](language-support.md).

### Configure confidence level in a person model with an API

Use the [Patch person model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Patch-Person-Model) API to set the confidence level for face recognition within a person model.

### View speakers in closed captions

You can now view speakers in closed captions of the Azure AI Video Indexer media player. For more information, see [View closed captions in the Azure AI Video Indexer website](view-closed-captions.md).

### Control face and people bounding boxes using parameters

The new `boundingBoxes` URL parameter controls the option to set bounding boxes on or off when embedding a player. For more information, see [Embed widgets](video-indexer-embed-widgets.md#player-widget).

### Control autoplay from the account settings

Control whether a media file autoplays when opened by using the webapp through the user settings. Go to the [Azure AI Video Indexer website](https://www.videoindexer.ai/) -> the **Gear** icon (the top-right corner) -> **User settings** -> **Auto-play media files**.

### Copy video ID from the player view

**Copy video ID** is available when you select the video in the [Azure AI Video Indexer website](https://www.videoindexer.ai/).

### New dark theme in native Azure colors

Select the desired theme in the [Azure AI Video Indexer website](https://www.videoindexer.ai/). Select the **Gear** icon (the top-right corner) -> **User settings**.

### Search or filter the account list

You can search or filter the account list by using the account name or region. Select **User accounts** in the top-right corner of the [Azure AI Video Indexer website](https://www.videoindexer.ai/).

## September 2022

### General availability of ARM-based accounts

With an Azure Resource Management (ARM) based [paid (unlimited)](accounts-overview.md) account, you can use:

- [Azure role-based access control (RBAC)](/azure/role-based-access-control/overview).
- Managed Identity to better secure the communication between your Azure Media Services and Azure AI Video Indexer account, Network Service Tags, and native integration with Azure Monitor to monitor your account (audit and indexing logs).
- Scale and automate your [deployment with ARM-template](deploy-with-arm-template.md), [bicep](deploy-with-bicep.md), or terraform.
- [Create logic apps connector for ARM-based accounts](logic-apps-connector-arm-accounts.md).

To create an ARM-based account, see [create an account](create-account-portal.md).

## August 2022

### Update topic inferencing model

The Azure AI Video Indexer topic inferencing model was updated and now extracts more than 6.5 million topics, such as the Covid virus. To benefit from recent model updates, you need to reindex your video files.

### Topic inferencing model is now available on Azure Government

You can now use the topic inferencing model in your Azure AI Video Indexer paid account on [Azure Government](/azure/azure-government/documentation-government-welcome) in Virginia and Arizona regions. With this release, we completed the AI parity between Azure global and Azure Government. To benefit from the model updates, you need to reindex your video files.

### Session length is now 30 days in the Azure AI Video Indexer website

The [Azure AI Video Indexer website](https://vi.microsoft.com) session length was extended to 30 days. You can preserve your session without having to sign in again every hour.

## July 2022

### The featured clothing insight (preview)

The featured clothing insight enables more targeted ad placement.

The insight provides information about key items worn by individuals within a video and the timestamp when the clothing appears. It allows high-quality in-video contextual advertising, where relevant clothing ads match with the specific time within the video when they're viewed.

To view the featured clothing of an observed person, you need to index the video by using Azure AI Video Indexer advanced video settings. For details on how featured clothing images are ranked and how to view this insight, see [featured clothing](observed-people-featured-clothing.md).

## June 2022

### Create Video Indexer improvements in the Azure portal

Azure AI Video Indexer now supports the creation of new resources by using system-assigned managed identity or system and user assigned managed identity for the same resource.

You can also change the primary managed identity by using the **Identity** tab in the [Azure portal](https://portal.azure.com/#home).

### Limited access of celebrity recognition and face identification features

As part of Microsoft's commitment to responsible AI, we're designing and releasing Azure AI Video Indexer identification and celebrity recognition features. These features are designed to protect the rights of individuals and society and foster transparent human-computer interaction. Thus, there's limited access and use of Azure AI Video Indexer identification and celebrity recognition features.

Identification and celebrity recognition features require registration and are only available to Microsoft managed customers and partners.
Customers who want to use this feature must apply and submit an [intake form](https://aka.ms/facerecognition). For more information, read [Azure AI Video Indexer limited access](limited-access-features.md).

For more information, see [announcement blog post](https://aka.ms/AAh91ff) and [investment and safeguard for facial recognition](https://aka.ms/AAh9oye).

## May 2022

### Line breaking in transcripts

Improved line break logic to better split transcript into sentences. New editing capabilities are now available through the Azure AI Video Indexer website, such as adding a new line and editing the line's timestamp. For more information, see [Insert or remove transcript lines](edit-transcript-lines-portal.md).

### Azure Monitor integration

Azure AI Video Indexer now supports Diagnostics settings for Audit events. You can now export logs of Audit events through diagnostics settings to Azure Log Analytics, Storage, Event Hubs, or a third-party solution.

These additions enable easier access to analyze the data, monitor resource operation, and create automatic flows to act on an event. For more information, see [Monitor Azure AI Video Indexer](monitor-video-indexer.md).

### Video Insights improvements

Object Character Reader (OCR) improved 60%. Face Detection improved 20%. Label accuracy improved 30% over a wide variety of videos. These improvements are available immediately in all regions and don't require any changes by the customer.

### Service tag

Azure AI Video Indexer is now part of [Network Service Tags](network-security.md). Video Indexer often needs to access other Azure resources (for example, Storage). If you secure your inbound traffic to your resources with a Network Security Group, you can now select Video Indexer as part of the built-in Service Tags. It simplifies security management as we populate the Service Tag with our public IPs.

### Celebrity recognition toggle

You can now enable or disable the celebrity recognition model on the account level (on classic account only). To turn on or off the model, go to the **Model customization** > toggle on/off the model. Once you disable the model, Video Indexer insights don't include the output of celebrity model and doesn't run the celebrity model pipeline.

### Azure AI Video Indexer repository name

As of May 1, our new updated repository of Azure AI Video Indexer widget was renamed. Use https://www.npmjs.com/package/@azure/video-indexer-widgets instead.

## April 2022

### Renamed **Azure Video Analyzer for Media** back to **Azure AI Video Indexer**

As of today, the Azure Video Analyzer for Media product name is **Azure AI Video Indexer**. All product-related assets, such as the web portal and marketing materials, reflect this change. This backward-compatible change has no effect on APIs and links. **Azure AI Video Indexer**'s new logo:

:::image type="content" source="./media/video-indexer.svg" alt-text="Symbol that represents Azure AI Video Indexer.":::

## March 2022

### Closed captioning files now support including speakers' attributes

Azure AI Video Indexer enables you to include speakers' characteristics based on a closed captioning file that you choose to download. To include the speakers' attributes, select **Downloads** -> **Closed Captions** -> choose the closed captioning downloadable file format (SRT, VTT, TTML, TXT, or CSV) and check **Include speakers** checkbox.

### Improvements to the widget offering

The following improvements were made:

* Azure AI Video Indexer widgets support more than one locale in a widget's parameter.
* The Insights widgets support initial search parameters and multiple sorting options.
* The Insights widgets also include a confirmation step before deleting a face to avoid mistakes.
* The widget customization now supports width as strings (for example 100%, 100vw).

## February 2022

### Public preview of Azure AI Video Indexer account management based on ARM in Government cloud

Azure AI Video Indexer website now supports account management based on ARM in public preview (see, [November 2021 release note](#november-2021)).

### Use open-source code to create ARM based account

Added new code samples including HTTP calls to use Azure AI Video Indexer create, read, update, and delete (CRUD) ARM API for solution developers.

## January 2022

### Improved audio effects detection

The audio effects detection capability was improved to have a better detection rate over the following classes:

* Crowd reactions (cheering, clapping, and booing)
* Gunshot or explosion
* Laughter

For more information, see [Audio effects detection](audio-effects-detection-insight.md).

### New source languages support for STT, translation, and search on the website

Azure AI Video Indexer introduces source language support for STT (speech-to-text), translation, and search for the following languages on the [Azure AI Video Indexer](https://www.videoindexer.ai/) website:

- Hebrew `he-IL`
- Portuguese `pt-PT`
- Persian `fa-IR`

It means transcription, translation, and search features are also supported for these languages in the [Azure AI Video Indexer](https://www.videoindexer.ai/) website and widgets.

## December 2021

### The projects feature is now GA

The projects feature is now GA and ready for productive use. There's no pricing change related to the "Preview to GA" transition. See [Add video clips to your projects](use-editor-create-project.md).

### New source languages support for STT, translation, and search on API level

Azure AI Video Indexer introduces source languages support for STT (speech-to-text), translation, and search in Hebrew `he-IL`, Portuguese `pt-PT`, and Persian `fa-IR` on the API level.

### Matched person detection capability

When indexing a video with Azure AI Video Indexer advanced video settings, you can view the new matched person detection capability. If the media file contains people, you can view the specific person who matched each of them through the media player.

## November 2021

### Public preview of Azure AI Video Indexer account management based on ARM

Azure AI Video Indexer introduces a public preview of Azure Resource Manager (ARM) based account management. You can use ARM-based Azure AI Video Indexer APIs to create, edit, and delete an account from the [Azure portal](https://portal.azure.com/#home).

> [!NOTE]
> The Government cloud includes support for CRUD ARM based accounts from Azure AI Video Indexer API and from the Azure portal.
>
> There's currently no support from the Azure AI Video Indexer [website](https://www.videoindexer.ai).

For more information, go to [create an Azure AI Video Indexer account](https://techcommunity.microsoft.com/t5/azure-ai/azure-video-analyzer-for-media-is-now-available-as-an-azure/ba-p/2912422).

### People's clothing detection

When indexing a video with Azure AI Video Indexer advanced video settings, you can view the new people's clothing detection capability. If the media file contains people, you can view the clothing type they're wearing through the media player.

### Face bounding box (preview)

You can turn on a bounding box for detected faces during indexing of the media file. The face bounding box feature is available when indexing your file by choosing the **standard**, **basic**, or **advanced** indexing presets.

You can enable the bounding boxes through the player.

## October 2021

### Embed widgets in your app using Azure AI Video Indexer package

Use the new Azure AI Video Indexer (AVAM) `@azure/video-analyzer-for-media-widgets` npm package to add `insights` widgets to your app and customize it according to your needs.

The new AVAM package enables you to easily embed and communicate between our widgets and your app, instead of adding an `iframe` element to embed the insights widget. Learn more in [Embed and customize Azure AI Video Indexer widgets in your app](https://techcommunity.microsoft.com/t5/azure-media-services/embed-and-customize-azure-video-analyzer-for-media-widgets-in/ba-p/2847063). 

## August 2021

### Reindex video or audio files

You can now reindex video or audio files that failed during the indexing process.

### Improve accessibility support

Fixed bugs related to CSS, theming, and accessibility issues:

* high contrast
* account settings and insights views in the [portal](https://www.videoindexer.ai).

## July 2021

### Automatic scaling of media reserved units

On August 1, 2021, Azure AI Video Indexer enabled [Media Reserved Units (MRUs)](/azure/media-services/latest/concept-media-reserved-units) auto scaling by [Azure Media Services](/azure/media-services/latest/media-services-overview). As a result, you don't need to manage them through Azure AI Video Indexer. This feature optimizes pricing, such as by reducing prices in many cases, based on your business needs as it autoscales.

## June 2021

### Azure AI Video Indexer deployed in six new regions

You can now create an Azure AI Video Indexer paid account in France Central, Central US, Brazil South, West Central US, Korea Central, and Japan West regions.

## May 2021

### New source languages support for speech-to-text (STT), translation, and search

Azure AI Video Indexer now supports STT, translation, and search in:

- Chinese (Cantonese) `zh-HK`
- Dutch (Netherlands) `Nl-NL`
- Czech `Cs-CZ`
- Polish `Pl-PL`
- Swedish (Sweden) `Sv-SE`
- Norwegian `nb-NO`
- Finnish `fi-FI`
- Canadian French `fr-CA`
- Thai `th-TH`
- Arabic: 
  - United Arab Emirates `ar-AE` and `ar-EG`
  - Iraq `ar-IQ`
  - Jordan `ar-JO`
  - Kuwait `ar-KW`
  - Lebanon `ar-LB`
  - Oman `ar-OM`
  - Qatar `ar-QA`
  - Palestinian Authority `ar-PS`
  - Syria `ar-SY`
  - Turkish `tr-TR`

You can use these languages in both the API and the Azure AI Video Indexer website. Select the language from the combobox under **Video source language**.

### New theme for Azure AI Video Indexer

The new theme 'Azure' is available along with the 'light' and 'dark' themes. To select a theme, select the gear icon in the top-right corner of the website, then find themes under **User settings**.

### New open-source code you can use

Three new GitHub projects are available at our [GitHub repository](https://github.com/Azure-Samples/media-services-video-indexer):

* Code to help you use the newly added [widget customization](https://github.com/Azure-Samples/media-services-video-indexer/tree/master/Embedding%20widgets).

* Solution to help you add [deduplication](https://github.com/Azure-Samples/azure-video-indexer-samples/commit/6b828f598f5bf61ce1b6dbcbea9e8b87ba11c7b1) to your video libraries.

### New option to toggle bounding boxes (for observed people) on the player

When indexing a video through our advanced video settings, you can view our new observed people capabilities. If the service detects people in your media file, you can enable a bounding box on the detected person through the media player.

## April 2021

The Video Indexer service was renamed to Azure AI Video Indexer.

### Improved upload experience in the portal

Azure AI Video Indexer has a new upload experience in the [website](https://www.videoindexer.ai). To upload your media file, press the **Upload** button from the **Media files** tab.

### New developer portal in available in gov-cloud

The [Azure AI Video Indexer API developer portal](https://api-portal.videoindexer.ai) is now also available in Azure for US Government.

### Observed people detection (preview)

Azure AI Video Indexer now detects observed people in videos. It provides information such as the location of the person in the video frame and the exact timestamp (start, end) when a person appears. The API returns the bounding box coordinates (in pixels) for each person instance detected, including its confidence.

For example, if a video contains a person, the detection operation lists the person appearances together with their coordinates in the video frames. You can use this functionality to determine the person path in a video. It also lets you determine whether there are multiple instances of the same person in a video.

The newly added observed people detection feature is available when indexing your file by choosing the **Advanced option** -> **Advanced video** or **Advanced video + audio** preset (under Video + audio indexing). Standard  and basic indexing presets don't include this new advanced model.

When you choose to see Insights of your video on the Azure AI Video Indexer website, the Observed People detection shows up on the page with all detected people thumbnails. You can choose a thumbnail of a person and see where the person appears in the video player.

The feature is also available in the JSON file generated by Azure AI Video Indexer. For more information, see [Observed people in a video](observed-matched-people-insight.md).

### Detected acoustic events with **Audio Effects Detection** (preview)

You can now see the detected acoustic events in the closed captions file. You can download the file from the Azure AI Video Indexer website, and it's available as an artifact in the GetArtifact API.

**Audio Effects Detection** (preview) component detects various acoustics events and classifies them into different acoustic categories (such as Gunshot, Screaming, Crowd Reaction, and more). For more information, see [Audio effects detection](audio-effects-detection-insight.md).

## March 2021

### Audio analysis

Audio analysis is now available in a new bundle of audio features at a different price point. The new **Basic Audio** analysis preset provides a low-cost option to only extract speech transcription, translation, and format output captions and subtitles. The **Basic Audio** preset produces two separate meters on your bill, including a line for transcription and a separate line for caption and subtitle formatting. For more information on the pricing, see the [Media Services pricing](https://azure.microsoft.com/pricing/details/media-services/) page.

The newly added bundle is available when indexing or reindexing your file by choosing the **Advanced option** -> **Basic Audio** preset (under the **Video + audio indexing** drop-down box).

### New developer portal

Azure AI Video Indexer has a new [developer portal](https://api-portal.videoindexer.ai/). Try out the new Azure AI Video Indexer APIs and find all the relevant resources in one place:

- [GitHub repository](https://github.com/Azure-Samples/media-services-video-indexer)
- [Stack overflow](https://stackoverflow.com/questions/tagged/video-indexer)
- [Azure AI Video Indexer tech community](https://techcommunity.microsoft.com/blog/azure-ai-services-blog/new-name-and-a-wealth-of-new-capabilities-in-video-indexer-now-ava-for-media/2305908) with relevant blog posts
- [Azure AI Video Indexer FAQs](faq.yml)
- [User Voice](https://feedback.azure.com/d365community/forum/09041fae-0b25-ec11-b6e6-000d3a4f0858) to provide your feedback and suggest features
- ['CodePen' link](https://codepen.io/videoindexer) with widgets code samples

### Advanced customization capabilities for insight widget

The SDK is now available to embed Azure AI Video Indexer's insights widget in your own service and customize its style and data. The SDK supports the standard Azure AI Video Indexer insights widget and a fully customizable insights widget. A code sample is available in the [Azure AI Video Indexer GitHub repository](https://github.com/Azure-Samples/media-services-video-indexer/tree/master/Embedding%20widgets/widget-customization). With these advanced customization capabilities, solution developers can apply custom styling and bring their own AI data to present in the insight widget (with or without Azure AI Video Indexer insights).

### Azure AI Video Indexer deployed in the US North Central, US West, and Canada Central

You can now create an Azure AI Video Indexer paid account in the US North Central, US West, and Canada Central regions.

### New source languages support for speech-to-text (STT), translation, and search

Azure AI Video Indexer now supports STT, translation, and search in:

- Danish `da-DK`
- Norwegian `nb-NO`
- Swedish `sv-SE`
- Finnish `fi-FI`
- Canadian French `fr-CA`
- Thai `th-TH`
- Arabic `ar-BH`, `ar-EG`, `ar-IQ`, `ar-JO`, `ar-KW`, `ar-LB`, `ar-OM`, `ar-QA`, `ar-S`, and `ar-SY`), and Turkish `tr-TR`.

You can use these languages in the API and the Azure AI Video Indexer website.

### Search by Topic in Azure AI Video Indexer Website

You can now use the search feature, at the top of  the [Azure AI Video Indexer website](https://www.videoindexer.ai/account/login) page, to search for videos with specific topics.

## February 2021

### Multiple account owners

Azure AI Video Indexer adds the account owner role. You can add, change, and remove users. You can also change their role. For details on how to share an account, see [Invite users](restricted-viewer-role.md#share-the-account).

### Audio event detection (public preview)

> [!NOTE]
> This feature is only available in trial accounts.

Azure AI Video Indexer now detects the following audio effects in the nonspeech segments of the content: gunshot, glass shatter, alarm, siren, explosion, dog bark, screaming, laughter, crowd reactions (cheering, clapping, and booing), and silence.

The newly added audio effects feature is available when indexing your file by choosing the **Advanced option** -> **Advanced audio** preset (under Video + audio indexing). Standard indexing only includes **silence** and **crowd reaction**.

The **clapping** event type that was included in the previous audio effects model is now extracted as part of the **crowd reaction** event type.

When you choose to see **Insights** of your video on the [Azure AI Video Indexer](https://www.videoindexer.ai/) website, the Audio Effects show up on the page.

### Named entities enhancement

The extracted list of people and locations was extended and updated in general.

In addition, the model now includes people and locations in context that aren't famous, like a ‘Sam' or ‘Home' in the video.

## January 2021

### Azure AI Video Indexer is deployed on US Government cloud

You can now create an Azure AI Video Indexer paid account on US government cloud in Virginia and Arizona regions.
Azure AI Video Indexer trial offering isn't available in the mentioned region. For more information, go to Azure AI Video Indexer Documentation.

### Azure AI Video Indexer deployed in the India Central region

You can now create an Azure AI Video Indexer paid account in the India Central region.

### New dark mode for the Azure AI Video Indexer website experience

The Azure AI Video Indexer website experience is now available in dark mode. To enable the dark mode, open the settings panel and toggle on the **Dark Mode** option.

## December 2020

### Azure AI Video Indexer deployed in the Switzerland West and Switzerland North

You can now create an Azure AI Video Indexer paid account in the Switzerland West and Switzerland North regions.

## October 2020

### Planned Azure AI Video Indexer website authentication changes

Starting March 1, 2021, you can't register or sign in to the [Azure AI Video Indexer website](https://www.videoindexer.ai/) [developer portal](video-indexer-use-apis.md) by using Facebook or LinkedIn.

You can register and sign in by using one of these providers: Microsoft Entra ID, Microsoft, and Google.

> [!NOTE]
> The Azure AI Video Indexer accounts connected to LinkedIn and Facebook aren't accessible after March 1, 2021.
>
> To maintain access, [invite](restricted-viewer-role.md#share-the-account) your own Microsoft Entra ID, Microsoft, or Google email address to the Azure AI Video Indexer account. You can add another owner of supported providers, as described in the [invite](restricted-viewer-role.md#share-the-account) section.
> Alternatively, you can create a paid account and migrate the data.

## August 2020

### Mobile design for the Azure AI Video Indexer website

The Azure AI Video Indexer website experience now supports mobile devices. The user experience is responsive to adapt to your mobile screen size (excluding customization UIs).

### Accessibility improvements and bug fixes

As part of WCAG (Web Content Accessibility guidelines), the Azure AI Video Indexer website experience aligns with grade C, as part of Microsoft Accessibility standards. The team resolved several bugs and made improvements related to keyboard navigation, programmatic access, and screen reader support.

## July 2020

### GA for multi-language identification

Multi-language identification moves from preview to GA and is ready for productive use.

There's no pricing change related to the "Preview to GA" transition.

### Azure AI Video Indexer website improvements

#### Adjustments in the video gallery

The team added a new search bar for deep insights search with extra filtering capabilities. They also enhanced search results.

The team added a new list view with the ability to sort and manage the video archive with multiple files.

#### New panel for easy selection and configuration

The team added a side panel for easy selection and user configuration, allowing simple and quick account creation and sharing, and configuring settings.

The side panel is also used to access user preferences and help.

## June 2020

### Search by topics

You can now use the search API to search for videos with specific topics (API only).

The `topics` parameter is part of the `textScope` parameter (optional). For more information, see [API](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Search-Videos).

### Labels enhancement

The label tagger was upgraded and now includes more visual labels that it can identify.

## May 2020

### Azure AI Video Indexer deployed in the East US

You can now create an Azure AI Video Indexer paid account in the East US region.

### Azure AI Video Indexer URL

All Azure AI Video Indexer regional endpoints now start with **www**. No action is required.

From now on, you reach **www.videoindexer.ai** whether it's for embedding widgets or signing in to the [Azure AI Video Indexer](https://www.videoindexer.ai/) website.

Also, **wus.videoindexer.ai** redirects to **www**. For more information, see [Embed Azure AI Video Indexer widgets in your apps](video-indexer-embed-widgets.md).

## April 2020

### New widget parameters capabilities

The **Insights** widget includes new parameters: `language` and `control`.

The **Player** widget has a new `locale` parameter. Both `locale` and `language` parameters control the player's language.

For more information, see the [widget types](video-indexer-embed-widgets.md#widget-types) section.

### New player skin

A new player skin launched with updated design.

### Prepare for upcoming changes

* Today, the following APIs return an account object:

    * [Create-Paid-Account](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Paid-Account)
    * [Get-Account](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Account)
    * [Get-Accounts-Authorization](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Accounts-Authorization)
    * [Get-Accounts-With-Token](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Accounts-With-Token)

    The Account object has a `Url` field that points to the location of the [Azure AI Video Indexer website](https://www.videoindexer.ai/).
For paid accounts, the `Url` field currently points to an internal URL instead of the public website.
In the coming weeks, we'll update it and return the [Azure AI Video Indexer website](https://www.videoindexer.ai/) URL for all accounts (trial and paid).

    Don't use the internal URLs. Use the [Azure AI Video Indexer public APIs](https://api-portal.videoindexer.ai/).
* If you're embedding Azure AI Video Indexer URLs in your applications and the URLs don't point to the [Azure AI Video Indexer website](https://www.videoindexer.ai/) or the Azure AI Video Indexer API endpoint (`https://api.videoindexer.ai`) but rather to a regional endpoint (for example, `https://wus2.videoindexer.ai`), regenerate the URLs.

   You can do it by either:

    * Replacing the URL with a URL that points to the Azure AI Video Indexer widget APIs (for example, the [insights widget](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Insights-Widget))
    * Using the Azure AI Video Indexer website to generate a new embedded URL:

         Press **Play** to get to your video's page -> select the **&lt;/&gt; Embed** button -> copy the URL into your application:

    The regional URLs aren't supported. They'll get blocked in the coming weeks.

## January 2020

### Custom language support for more languages

Azure AI Video Indexer now supports custom language models for `ar-SY` , `en-UK`, and `en-AU` (API only).

### Delete account timeframe action update

Delete account action now deletes the account within 90 days instead of 48 hours.

### New Azure AI Video Indexer GitHub repository

A new Azure AI Video Indexer GitHub with different projects, getting started guides, and code samples is now available:
https://github.com/Azure-Samples/media-services-video-indexer

### Swagger update

Azure AI Video Indexer unified **authentications** and **operations** into a single [Azure AI Video Indexer OpenAPI Specification (swagger)](https://api-portal.videoindexer.ai/api-details#api=Operations&operation). Developers can find the APIs in the [Azure AI Video Indexer developer portal](https://api-portal.videoindexer.ai/).

## December 2019

### Update transcript with the new API

Update a specific section in the transcript by using the [Update-Video-Index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Video-Index) API.

### Fix account configuration from the Azure AI Video Indexer website

You can now update Media Services connection configuration to resolve issues like:

* Incorrect Azure Media Services resource
* Password changes
* Media Services resources moved between subscriptions

To fix the account configuration, in the Azure AI Video Indexer website, navigate to **Settings > Account** tab (as owner).

### Configure the custom vision account

Configure the custom vision account on paid accounts by using the Azure AI Video Indexer website (previously, only the API supported it). To do that, sign in to the Azure AI Video Indexer website, choose **Model Customization > <*model*> > Configure**.

### Scenes, shots, and keyframes – now in one insight pane

Scenes, shots, and keyframes are now merged into one insight for easier consumption and navigation. When you select the desired scene, you can see what shots and keyframes it consists of.

### Notification about a long video name

When a video name is longer than 80 characters, Azure AI Video Indexer shows a descriptive error on upload.

### Streaming endpoint is disabled notification

When streaming endpoint is disabled, Azure AI Video Indexer shows a descriptive error on the player page.

### Error handling improvement

Status code 409 is now returned from [Re-Index Video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Re-Index-Video) and [Update Video Index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Video-Index) APIs when a video is actively indexed. It prevents overriding the current reindex changes by accident.

## November 2019

* Korean custom language models support

    Azure AI Video Indexer now supports custom language models in Korean (`ko-KR`) in both the API and portal.
* New languages supported for speech-to-text (STT)

    Azure AI Video Indexer APIs now supports STT in Arabic Levantine (ar-SY), English UK regional language (en-GB), and English Australian regional language (en-AU).

    For video upload, we replaced zh-HANS to zh-CN. Both are supported but zh-CN is recommended and more accurate.

## October 2019

* Search for animated characters in the gallery

    When indexing animated characters, you can now search for them in the account's video galley.

## September 2019

At IBC 2019, we announced several advancements:

* Animated character recognition  (public preview)

    Detect and recognize groups of characters in animated content through integration with custom vision.
* Multilanguage identification (public preview)

    Detect segments in multiple languages in the audio track and create a multilingual transcript based on them. Initial support: English, Spanish, German, and French. For more information, see [Transcribe multi-language content](transcription-translation-lid-insight.md).
* Named entity extraction for people and location

    Extract brands, locations, and people from speech and visual text through natural language processing (NLP).
* Editorial shot type classification

    Tag shots with editorial types such as close up, medium shot, two shot, indoor, and outdoor. For more information, see [Editorial shot type detection](scene-shot-keyframe-detection-insight.md#keyframe-editorial-shot-type-detection).
* Topic inferencing enhancement - now covering level 2

    The topic inferencing model now supports deeper granularity of the IPTC taxonomy. For more information, see [Azure Media Services new AI-powered innovation](https://azure.microsoft.com/blog/azure-media-services-new-ai-powered-innovation/).

## August 2019

### Azure AI Video Indexer deployed in UK South

You can now create an Azure AI Video Indexer paid account in the UK South region.

### New editorial shot type insights available

New tags added to video shots provide editorial "shot types" to identify them with common editorial phrases used in the content creation workflow such as: extreme closeup, closeup, wide, medium, two shot, outdoor, indoor, left face, and right face (Available in the JSON).

### New People and Locations entities extraction available

Azure AI Video Indexer identifies named locations and people through natural language processing (NLP) from the video's OCR and transcription. Azure AI Video Indexer uses machine learning algorithms to recognize when specific locations (for example, the Eiffel Tower) or people (for example, John Doe) are mentioned in a video.

### Keyframes extraction in native resolution

Keyframes extracted by Azure AI Video Indexer are available in the original resolution of the video.

### GA for training custom face models from images

Training faces from images moved from preview to GA (available via API and in the portal).

> [!NOTE]
> There's no pricing change related to the "Preview to GA" transition.

### Hide gallery toggle option

You can choose to hide the gallery tab from the portal (similar to hiding the samples tab).

### Maximum URL size increased

Support for URL query string of 4,096 (instead of 2,048) on indexing a video.

### Support for multilingual projects

You can now create projects based on videos indexed in different languages (API only).

## July 2019

### Editor as a widget

The Azure AI Video Indexer AI-editor is now available as a widget to embed in your applications.

### Update custom language model from closed caption file from the portal

You can provide VTT, SRT, and TTML file formats as input for language models in the customization page of the portal.

## June 2019

### Azure AI Video Indexer deployed to Japan East

You can now create an Azure AI Video Indexer paid account in the Japan East region.

### Create and repair account API (Preview)

Added a new API that enables you to [update the Azure Media Service connection endpoint or key](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Paid-Account-Azure-Media-Services).

### Improve error handling on upload

A descriptive message is returned if there's misconfiguration of the underlying Azure Media Services account.

### Player timeline keyframes preview

You can now see an image preview for each time on the player's timeline.

### Editor semi-select

You can now see a preview of all the insights that are selected as a result of choosing a specific insight timeframe in the editor.

## May 2019

### Update custom language model from closed caption file

The [Create custom language model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Language-Model) and [Update custom language models](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Language-Model) APIs now support VTT, SRT, and TTML file formats as input for language models.

When you call the [Update Video transcript API](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Video-Transcript), the transcript is added automatically. The training model associated with the video is updated automatically as well. For information on how to customize and train your language models, see [Customize a Language model with Azure AI Video Indexer](customize-language-model-overview.md).

### New download transcript formats – TXT and CSV

In addition to the closed captioning format already supported (SRT, VTT, and TTML), Azure AI Video Indexer now supports downloading the transcript in TXT and CSV formats.

## Related content

- [Azure AI Video Indexer documentation](index.yml)