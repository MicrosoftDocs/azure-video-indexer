---
title:  Azure AI Video Indexer insights overview
description: This article gives a brief overview of Azure AI Video Indexer insights.
ms.topic: conceptual
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/09/2024
ms.service: azure-video-indexer
---

# Azure AI Video Indexer insights

When a video is indexed, Azure AI Video Indexer analyzes the video and audio content by running 30+ AI models. It generates JSON containing the video insights including transcripts, optical character recognition elements (OCRs), face, topics, emotions, and so on. Each insight type includes instances of time ranges that show when the insight appears in the video. 

Use the links in the insights table to learn how to get each insight JSON response in the web portal and using the API.

## Insights

| Insight | Description |
| ------- | ----------- |
| [Face detection](face-detection-insight.md) | [!INCLUDE [Face detection description](./includes/face-detection-description.md)] |
| [Labels identification](labels-identification-insight.md) | [!INCLUDE [labels identification description](./includes/labels-identification-description.md)] |
| [Object detection](object-detection-insight.md)| [!INCLUDE [object detection description](./includes/object-detection-description.md)] |
|[Observed people detection](observed-matched-people-insight.md) | Observed people detection and matched faces automatically detect and match people in media files. Observed people detection and matched faces can be set to display insights on people, their clothing, and the exact timeframe of their appearance. |
| [OCR](ocr-insight.md) | [!INCLUDE [ocr description](./includes/ocr-description.md)] |
| [Post-production: clapper board detection](clapper-board-insight.md) | [!INCLUDE [clapper board description](./includes/clapperboard-description.md)] |
| [Post-production: digital patterns](digital-patterns-color-bars-insight.md) | [!INCLUDE [digital patterns description](./includes/digital-patterns-description.md)] |
| [Scenes, shots, and keyframes](scene-shot-keyframe-detection-insight.md) | [!INCLUDE [Scenes, shots detection and keyframes description](./includes/scene-shot-keyframe-detection-description.md)] |

## Audio insights
| Insight | Description |
| ------- | ----------- |
| [Audio effects detection](audio-effects-detection-insight.md) | [!INCLUDE [Audio effects detection description](./includes/audio-effects-detection-description.md)] |
| [Keywords extraction](keywords-insight.md) | [!INCLUDE [keywords-descritpion](./includes/keywords-description.md)] |
| [Named entities](named-entities-insight.md) | [!INCLUDE [Named entities description](./includes/named-entities-description.md)] |
| [Text-based emotion detection](text-based-emotions-detection-insight.md) | [!INCLUDE [Emotions detection description](./includes/text-based-emotions-detection-description.md)] |
| [Topics inference](topics-inference-insight.md) | [!INCLUDE [topics inference description](./includes/topics-inference-description.md)] |
| [Transcription, translation, and language identification](transcription-translation-lid-insight.md) | [!INCLUDE [transcription description](./includes/transcription-translation-lid-description.md)] |
