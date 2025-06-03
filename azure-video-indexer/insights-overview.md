---
title:  Azure AI Video Indexer insights overview
description: This article gives a brief overview of Azure AI Video Indexer insights.
ms.topic: conceptual
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/03/2025
ms.service: azure-video-indexer
---

# Azure AI Video Indexer insights

When a video is indexed, Azure AI Video Indexer analyzes the video and audio content by running 30+ AI models. It generates JSON containing the video insights including transcripts, optical character recognition elements (OCRs), face, topics, emotions, and so on. Each insight type includes instances of time ranges that show when the insight appears in the video. 

Follow the links in the insights table to learn how to get each insight JSON response in the web portal and using the API.

## Insights

| Insight | Description |
| ------- | ----------- |
| [Face detection](face-detection-insight.md) | Face detection finds faces in a media file and groups similar faces. The system generates face detection insights as a categorized list in a JSON file. Each entry includes a thumbnail and either a name or an ID for each face. In the web portal, when you select a face’s thumbnail, you see details like the person’s name (if recognized), the percentage of the video where the person appears, and the person's biography if they're a celebrity. You can scroll through instances in the video where the person appears. |
| [Labels identification](labels-identification-insight.md) | Labels identification is an Azure AI Video Indexer feature that identifies visual objects, like sunglasses, or actions, like swimming, in the video footage of a media file. The feature includes many label categories. After extraction, you see label instances in the Insights tab, and you can translate them into over 50 languages. Select a label to open the instance in the media file. Select **Play Previous** or **Play Next** to see more instances. |
| [Object detection](object-detection-insight.md)| [!INCLUDE [object detection description](./includes/object-detection-description.md)] |
|[Observed people detection](observed-matched-people-insight.md) | Observed people detection and matched faces automatically detect and match people in media files. Observed people detection and matched faces can be set to display insights on people, their clothing, and the exact timeframe of their appearance. |
| [OCR](ocr-insight.md) | [!INCLUDE [ocr description](./includes/ocr-description.md)] |
| [Post-production: clapper board detection](clapper-board-insight.md) | Clapper board detection finds clapper boards used during filming and gives you the information on the clapper board as metadata, like *production*, *roll*, *scene*, and *take*. Clapper board is part of post-production insights that you select in the web portal [advanced settings](../indexing-configuration-guide.md?#advanced-settings) when you upload and index the file. |
| [Post-production: digital patterns](digital-patterns-color-bars-insight.md) | Digital patterns detection finds [color bars](https://en.wikipedia.org/wiki/SMPTE_color_bars) used during filming. Digital patterns are part of post-production insights that you select in the web portal [advanced settings](../indexing-configuration-guide.md?#advanced-settings) when you upload and index the file. |
| [Scenes, shots, and keyframes](scene-shot-keyframe-detection-insight.md) | [!INCLUDE [Scenes, shots detection and keyframes description](./includes/scene-shot-keyframe-detection-description.md)] |

## Audio insights
| Insight | Description |
| ------- | ----------- |
| [Audio effects detection](audio-effects-detection-insight.md) | Audio effects detection detects acoustic events and classifies them into categories like laughter, crowd reactions, alarms, or sirens. |
| [Keywords extraction](keywords-insight.md) | Keyword extraction finds important keywords in media files and provides insights in both single-language and multi-language media files. |
| [Named entities](named-entities-insight.md) | [!INCLUDE [Named entities description](./includes/named-entities-description.md)] |
| [Text-based emotion detection](text-based-emotions-detection-insight.md) | [!INCLUDE [Emotions detection description](./includes/text-based-emotions-detection-description.md)] |
| [Topics inference](topics-inference-insight.md) | [!INCLUDE [topics inference description](./includes/topics-inference-description.md)] |
| [Transcription, translation, and language identification](transcription-translation-lid-insight.md) | [!INCLUDE [transcription description](./includes/transcription-translation-lid-description.md)] |
