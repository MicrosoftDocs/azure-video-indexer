---
title:  Azure AI Video Indexer insights overview
description: This article gives a brief overview of Azure AI Video Indexer insights.
ms.topic: conceptual
ms.date: 07/09/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Azure AI Video Indexer insights

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

When a video is indexed, Azure AI Video Indexer analyzes the video and audio content by running 30+ AI models, generating insights.  Use the links in the insights table to learn how to view each insight JSON response.

## Insights

| Insight | Description |
| ------- | ----------- |
| [Audio effects detection](audio-effects-detection-insight.md) | [!INCLUDE [Audio effects detection description](audio-effects-detection-description.md)] |
| [Face detection](face-detection-insight.md) | [!INCLUDE [Face detection description](face-detection-description.md)] |
| [Keywords extraction](keywords-insight.md) | [!INCLUDE [keywords-descritpion](keywords-description.md)] |
| [Labels identification]() | [!INCLUDE [labels identification description](labels-identification-description.md)] |
| [Media transcription, translation, and language identification](transcription-translation-lid-insight.md) | [!INCLUDE [transcription description](transcription-translation-lid-description.md)] |
| [Named entities](named-entities-insight.md) | [!INCLUDE [Named entities description](named-entities-description.md)] |
| [Object detection](object-detection-insight.md)| [!INCLUDE [object detection description](object-detection-description.md)] |
| [OCR](ocr-insight.md) | [!INCLUDE [ocr description](ocr-description.md)] |
| [Post-production: clapper board detection](clapper-board-insight.md) | [!INCLUDE [clapper board description](clapperboard-description.md)] |
| [Post-production: digital patterns](digital-patterns-color-bars-insight.md) | [!INCLUDE [digital patterns description](digital-patterns-description.md)] |
| [Text-based emotion detection](emotions-detection-insight.md) | [!INCLUDE [Emotions detection description](emotions-detection-description.md)] |
| [Topics inference](topics-inference-insight.md) | [!INCLUDE [topics inference description](topics-inference-description.md)] |

## Insights JSON

Insights contain an aggregated view of the data: transcripts, optical character recognition elements (OCRs), face, topics, emotions, etc. Once the video is indexed and analyzed, Azure AI Video Indexer create JSON of the details of the video insights. For example, each insight type includes instances of time ranges that show when the insight appears in the video.
