---
title:  Azure AI Video Indexer insights overview
description: This article gives a brief overview of Azure AI Video Indexer insights. It includes links to articles that describe how to get each insight in the web portal and using the API.
ms.topic: concept-article
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/06/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
# customer intent: As a user of Azure AI Video Indexer, I want to understand the different insights that can be generated from my video content, so that I can use the insights for better content analysis and decision-making.
---

# Azure AI Video Indexer insights

When a video is indexed, Azure AI Video Indexer analyzes the video and audio content by running 30+ AI models. It generates JSON containing the video insights including transcripts, optical character recognition elements (OCRs), face, topics, emotions, and so on. Each insight type includes instances of time ranges that show when the insight appears in the video. 

Follow the links in the insights table to learn how to get each insight JSON response in the web portal and using the API.

## Insights

| Insight | Description |
| ------- | ----------- |
| [Face detection](face-detection-insight.md) | Face detection finds faces in a media file and groups similar faces. The system generates face detection insights as a categorized list in a JSON file. Each entry includes a thumbnail and either a name or an ID for each face. In the web portal, when you select a face’s thumbnail, you see details like the person’s name (if recognized), the percentage of the video where the person appears, and the person's biography if they're a celebrity. You can scroll through instances in the video where the person appears. |
| [Labels identification](labels-identification-insight.md) | Labels identification is an Azure AI Video Indexer feature that identifies visual objects, like sunglasses, or actions, like swimming, in the video footage of a media file. The feature includes many label categories. After extraction, you see label instances in the Insights tab, and you can translate them into over 50 languages. Select a label to open the instance in the media file. Select **Play Previous** or **Play Next** to see more instances. |
| [Object detection](object-detection-insight.md)| Azure AI Video Indexer detects objects in videos like cars, handbags, backpacks, and laptops. |
|[Observed people detection](observed-matched-people-insight.md) | Observed people detection and matched faces automatically detect and match people in media files. Observed people detection and matched faces can be set to display insights on people, their clothing, and the exact timeframe of their appearance. |
| [OCR](ocr-insight.md) | Optical character recognition (OCR) extracts text from images, such as pictures, street signs, and products in media files to create insights. |
| [Post-production: clapper board detection](clapper-board-insight.md) | Clapper board detection finds clapper boards used during filming and gives you the information on the clapper board as metadata, like *production*, *roll*, *scene*, and *take*. Clapper board is part of post-production insights that you select in the web portal [advanced settings](indexing-configuration-guide.md?#advanced-settings) when you upload and index the file. |
| [Post-production: digital patterns](digital-patterns-color-bars-insight.md) | Digital patterns detection finds [color bars](https://en.wikipedia.org/wiki/SMPTE_color_bars) used during filming. Digital patterns are part of post-production insights that you select in the web portal [advanced settings](indexing-configuration-guide.md?#advanced-settings) when you upload and index the file. |
| [Scenes, shots, and keyframes](scene-shot-keyframe-detection-insight.md) | Scene detection finds when a scene changes in a video based on visual cues. A **scene** shows a single event and has a series of related shots. **Shots** are a series of frames that differ by visual cues, like abrupt or gradual changes in the color scheme of adjacent frames. Shot metadata includes the start time, end time, and a list of keyframes in the shot. A **keyframe** is a frame from a shot that best represents the shot. |

## Audio insights

| Insight | Description |
| ------- | ----------- |
| [Audio effects detection](audio-effects-detection-insight.md) | Audio effects detection detects acoustic events and classifies them into categories like laughter, crowd reactions, alarms, or sirens. |
| [Keywords extraction](keywords-insight.md) | Keyword extraction finds important keywords in media files and provides insights in both single-language and multi-language media files. |
| [Named entities](named-entities-insight.md) | Named entities extraction uses natural language processing (NLP) to find locations, people, and brands in audio and images in media files. Named entities extraction uses transcription and optical character recognition (OCR). |
| [Text-based emotion detection](text-based-emotions-detection-insight.md) | Emotion detection finds emotions in a video's transcript lines. Each sentence is detected as *anger*, *fear*, *joy*, *sad*, or *none* if no other emotion is found. |
| [Topics inference](topics-inference-insight.md) | Topics inference creates inferred insights from transcribed audio, OCR content in visual text, and celebrities the Video Indexer facial recognition model recognizes in the video. |
| [Transcription, translation, and language identification](transcription-translation-lid-insight.md) | The transcription, translation, and language identification features detect, transcribe, and translate speech in media files into more than 50 languages. |

## Related content

- [Azure AI Video Indexer documentation](index.yml)