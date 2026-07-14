---
title: Indexing configuration options in Azure AI Video Indexer
description: This article explains each indexing option. The same options apply when you use the Azure AI Video Indexer website and the API.
author: cwatson-cat
ms.author: cwatson
ms.date: 07/13/2026
ai-usage: ai-assisted
ms.service: azure-video-indexer
ms.topic: concept-article
# customer intent: As a user of Azure AI Video Indexer, I want to understand the indexing configuration options available so that I can optimize my video indexing process.
appliesto:
  - Cloud-based Azure AI Video Indexer
---

# Indexing configuration options

You can use the default indexing settings or adjust them. You can choose language, indexing, custom models, and streaming settings, which affect generated insights, cost, and performance.

This article explains each option. The same options apply when you use the [Azure AI Video Indexer website](https://www.videoindexer.ai/) and the API (see the [API guide](video-indexer-use-apis.md)). For large-volume indexing, see the [at-scale guide](considerations-when-use-at-scale.md).

## Default settings

By default, Azure AI Video Indexer uses the following settings:

- Source language: English
- Privacy: Private
- Audio and video setting: Standard
- Streaming quality: Single bitrate

## Video source language

If you know the language spoken in the video, select it from the video source language list. If you're not sure, choose **Auto-detect single language**. Azure AI Video Indexer uses language identification (LID) to detect the video's language and generate transcription and insights in that language.

If the video contains multiple languages and you're not sure which ones, select **Auto-detect multi-language**. In this case, multi-language identification (MLID) runs during upload and indexing.

When the language in your videos varies, auto-detect can help. Consider the following points when using LID or MLID:

- LID and MLID don't support every language that Azure AI Video Indexer supports.
- Transcription quality is higher when you preselect the correct video language.

Learn more about [language support and supported languages](language-support.md).

## Privacy

This option determines whether only users in your Azure AI Video Indexer account can access insights or if anyone with a link can access them.

## Indexing options

Audio and video indexing options can have different pricing. For more information, see [Azure AI Video Indexer pricing](https://azure.microsoft.com/pricing/details/video-indexer/).

The following indexing options describe the insights each option provides. To change the indexing type, select **Advanced settings**.

> [!NOTE]
> Optical Character Recognition (OCR) is used with several insight types.

## Advanced settings

When you select **Advanced settings**, you can choose the following options:

### Audio only

- **Basic**: Indexes and extracts insights by using audio only (ignoring video) and provides the following insights:
  - Transcription
  - Translation
  - Formatting of output captions and subtitles (closed captions)
- **Standard**: Indexes and extracts insights by using audio only (ignoring video) and provides the following insights:
  - Transcription
  - Translation
  - Formatting of output captions and subtitles (closed captions)
  - Automatic language detection
  - Emotions
  - Keywords
  - Named entities (brands, locations, people)
  - Sentiments
  - Speakers
  - Topic extraction
  - Textual content moderation
- **Advanced**: Indexes and extracts insights by using audio only (ignoring video) and provides the following insights:
  - Transcription
  - Translation
  - Formatting of output captions and subtitles (closed captions)
  - Automatic language detection
  - Audio event detection
  - Emotions
  - Keywords
  - Named entities (brands, locations, people)
  - Sentiments
  - Speakers
  - Topic extraction
  - Textual content moderation

### Video only

- **Basic**: Indexes and extracts insights by using video only (ignoring audio) and provides the following insights:
  - Labels
  - Object detection
  - OCR
  - Scenes (keyframes and shots)
  - Black frame detection
- **Standard**: Indexes and extracts insights by using video only (ignoring audio) and provides the following insights:
  - Labels (OCR)
  - Named entities (OCR - brands, locations, people)
  - OCR
  - People
  - Scenes (keyframes and shots)
  - Black frames
  - Visual content moderation
  - Topic extraction (OCR)
- **Advanced**: Indexes and extracts insights by using video only (ignoring audio) and provides the following insights:
  - Labels (OCR)
  - Matched person
  - Named entities (OCR - brands, locations, people)
  - OCR
  - Observed people
  - People
  - Scenes (keyframes and shots)
  - Clapper board detection
  - Digital pattern detection
  - Featured clothing insight
  - Textless slate detection
  - Textual logo detection
  - Black frames
  - Visual content moderation
  - Topic extraction (OCR)

### Audio and video

- **Basic**: Indexes and extracts insights from audio and video. It provides the following insights:
  - Transcription
  - Translation
  - Formatting of output captions and subtitles (closed captions)
  - Object detection
  - OCR
  - Scenes (keyframes and shots)
  - Black frames
- **Standard**: Indexes and extracts insights from audio and video. It provides the following insights:
  - Transcription
  - Translation
  - Formatting of output captions and subtitles (closed captions)
  - Automatic language detection
  - Emotions
  - Keywords
  - Named entities (brands, locations, people)
  - OCR
  - Scenes (keyframes and shots)
  - Black frames
  - Visual content moderation
  - People
  - Sentiments
  - Speakers
  - Topic extraction
  - Textual content moderation
- **Advanced**: Indexes and extracts insights from audio and video. It provides the following insights:
  - Transcription
  - Translation
  - Formatting of output captions and subtitles (closed captions)
  - Automatic language detection
  - Textual content moderation
  - Audio event detection
  - Emotions
  - Keywords
  - Matched person
  - Named entities (brands, locations, people)
  - OCR
  - Observed people
  - People
  - Clapper board detection
  - Digital pattern detection
  - Featured clothing insight
  - Textless slate detection
  - Sentiments
  - Speakers
  - Scenes (keyframes and shots)
  - Textual logo detection
  - Black frames
  - Visual content moderation
  - Topic extraction

### Streaming quality options

There are two options for streaming indexed videos:

- **Single bitrate**: If the video height is greater than or equal to 720p HD, Azure AI Video Indexer encodes it with a resolution of 1280 x 720. Otherwise, it's encoded as 640 x 468.
- **No streaming**: Azure AI Video Indexer generates insights but doesn't perform any streaming operation. The video isn't available on the Azure AI Video Indexer website. When you select **No streaming**, you aren't billed for encoding.

## Exclude models

You can exclude models when indexing through the Azure AI Video Indexer website and API. When you upload a video in the website, select **Advanced settings** > **Indexing presets**, and then select the AI models to exclude from indexing results. This setting can improve indexing efficiency and help ensure results include only the insights you need.

## Customizing content models

Azure AI Video Indexer lets you customize some models for your use case. These models include [brands](customize-brands-model-how-to.md), [language](customize-language-model-how-to.md), [person](customize-person-model-how-to.md), and [speech](customize-speech-model-how-to.md).

## Insights and media storage

The following sections explain how insights and media are stored in Azure AI Video Indexer.

### Insight storage

Azure AI Video Indexer stores indexing insights and metadata in Microsoft-managed storage accounts. You aren't charged for this storage.

### Media storage
Your Azure AI Video Indexer account connects to an Azure Storage account. You control and pay for the usage of this storage account. When you index a video, the following files are stored in this account:

- The source file. It's kept in case you want to reindex the video later.
- A new encoded file when the streaming quality is set to single bitrate.

### Delete media

Indexed media and all its associated files and insights can be deleted in three ways:

- Delete files in the [Azure AI Video Indexer website](https://www.videoindexer.ai/).
- Use a [Delete Video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Video) or a [Delete Video Source File](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Video-Source-File) API request.
- If you don't need to keep the original media file in storage, set the API `retentionPeriod` parameter to a value between 1 and 7. The indexed video and related assets (source file, insights, and more) are deleted 1 to 7 days after indexing.

## Related content

- [Azure AI Video Indexer documentation](index.yml)