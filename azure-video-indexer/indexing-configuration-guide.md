---
title: Indexing configuration guide
description: This article explains each of the indexing options. The same options apply when using the Azure AI Video Indexer website as for using the API.
ms.topic: conceptual
ms.date: 10/08/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# The indexing configuration guide

You can use the default indexing settings or adjust them. You can choose language, indexing, custom models, and streaming settings that have implications on the insights generated, cost, and performance.

This article explains each of the options. The same options apply when using the [Azure AI Video Indexer website](https://www.videoindexer.ai/) as for using the API (see the [API guide](video-indexer-use-apis.md)). When indexing large volumes, follow the [at-scale guide](considerations-when-use-at-scale.md).

## Default settings 

By default, Azure AI Video Indexer is configured as:

- Source language: English
- Privacy: private
- Audio and video setting: standard
- Streaming quality: single bitrate
  

## Video source language 

If you're aware of the language spoken in the video, select the language from the video source language list. If you're unsure of the language of the video, choose **Auto-detect single language**. Azure AI Video Indexer uses language identification (LID) to detect the videos language and generate transcription and insights with the detected language. 

If the video contains multiple languages and you aren't sure which ones, select **Auto-detect multi-language**. In this case, multi-language (MLID) detection is applied when uploading and indexing your video. 

While autodetect is a great option when the language in your videos varies, there are two points to consider when using LID or MLID: 

- LID/MLID don't support all the languages supported by Azure AI Video Indexer.
- The transcription is of a higher quality when you preselect the video’s appropriate language.

Learn more about [language support and supported languages](language-support.md). 

## Privacy 

This option allows you to determine if the insights should only be accessible to users in your Azure AI Video Indexer account or to anyone with a link. 

## Indexing options 

Each of the audio and video indexing options might be priced differently when you use the default indexing settings. See [Azure AI Video Indexer pricing](https://azure.microsoft.com/pricing/details/video-indexer/) for details. 

The following are the indexing type options with details of their insights provided. To modify the indexing type, select **Advanced settings**.

> [!NOTE] 
> Optical Character Recognition (OCR) is used with several insight types.

## Advanced settings

### Audio only  

- **Basic**: Indexes and extract insights by using audio only (ignoring video) and provides the following insights: transcription, translation, formatting of output captions and subtitles (closed captions).
- **Standard**: Indexes and extract insights by using audio only (ignoring video) and provides the following insights: transcription, translation, formatting of output captions and subtitles (closed captions), automatic language detection, emotions, keywords, named entities (brands, locations, people), sentiments, speakers, topic extraction, and textual content moderation.   
- **Advanced**: Indexes and extract insights by using audio only (ignoring video) and provides the following insights: transcription, translation, formatting of output captions and subtitles (closed captions), automatic language detection, audio event detection, emotions, keywords, named entities (brands, locations, people), sentiments, speakers, topic extraction, and textual content moderation.   

### Video only 

- **Basic**: Indexes and extract insights by using video only (ignoring audio) and provides the following insights: labels, object detection, OCR, scenes (keyframes and shots), and black frame detection.
- **Standard**: Indexes and extract insights by using video only (ignoring audio) and provides the following insights: labels (OCR), named entities (OCR - brands, locations, people), OCR, people, scenes (keyframes and shots), black frames, visual content moderation, and topic extraction (OCR). 
- **Advanced**: Indexes and extract insights by using video only (ignoring audio) and provides the following insights: labels (OCR), matched person, named entities (OCR - brands, locations, people), OCR, observed people, people, scenes (keyframes and shots), clapper board detection, digital pattern detection, featured clothing insight, textless slate detection, textual logo detection, black frames, visual content moderation, and topic extraction (OCR). 

### Audio and Video   

- **Basic**: Indexes and extract insights by using audio and video and provides the following insights: transcription, translation, formatting of output captions and subtitles (closed captions), object detection, OCR, scenes (keyframes and shots), and black frames.
- **Standard**: Indexes and extract insights by using audio and video and provides the following insights: transcription, translation, formatting of output captions and subtitles (closed captions), automatic language detection, emotions, keywords, named entities (brands, locations, people), OCR, scenes (keyframes and shots), black frames, visual content moderation, people, sentiments, speakers, topic extraction, and textual content moderation.   
- **Advanced**: Indexes and extract insights by using audio and video and provides the following insights: transcription, translation, formatting of output captions and subtitles (closed captions), automatic language detection, textual content moderation, audio event detection, emotions, keywords, matched person, named entities (brands, locations, people), OCR, observed people, people, clapper board detection, digital pattern detection, featured clothing insight, textless slate detection, sentiments, speakers, scenes (keyframes and shots), textual logo detection, black frames, visual content moderation, and topic extraction.   

### Streaming quality options 

There are two options for streaming indexed videos: 

- **Single bitrate**: If the video height is greater than or equal to 720p HD, Azure AI Video Indexer encodes it with a resolution of 1280 x 720. Otherwise, it's encoded as 640 x 468.
- **No streaming**: Insights are generated but no streaming operation is performed and the video isn't available on the Azure AI Video Indexer website. When No streaming is selected, you aren't billed for encoding.

## Customizing content models 

Azure AI Video Indexer allows you to customize some of its models to be adapted to your specific use case. These models include [brands](customize-brands-model-how-to.md), [language](customize-language-model-how-to.md), [person](customize-person-model-how-to.md), and [speech](customize-speech-model-how-to.md).

## Insights and media storage

### Insight storage

All indexing insights and metadata are kept in storage accounts managed by VI and you aren't charged for this storage.

### Media storage
Your VI account is connected to an Azure Storage account. You control and pay for the usage of this storage account. The following files are stored in this account when a video is indexed:

- The source file. It's kept in case you want to reindex the video in the future.
- A new encoded file when the streaming quality is set to single bitrate.

### Deleting media

Indexed media and all its associated files and insights can be deleted in three ways:

1. Delete the files with the [Video Indexer portal](https://www.videoindexer.ai/).
1. Use the [Delete Video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Video) or [Delete Video Source File](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Video-Source-File) request. 
1. If you don't need to keep the original media file in storage, when using the API, set the `retentionPeriod` parameter to between 1-7. The indexed video and everything related to it, the source file, insights, etc. are deleted 1-7 days after indexing.
