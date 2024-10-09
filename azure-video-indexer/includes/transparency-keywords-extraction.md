---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.collection: ce-skilling-ai-copilot,rai-skilling-ai-copilot
ms.date: 10/09/2024
ms.author: inhenkel
title: transparency Keywords extraction
---

## Keywords extraction notes

Always upload a high-quality audio and video content. The recommended maximum frame size is HD and frame rate is 30 FPS. A frame should contain no more than 10 people. When outputting frames from videos to AI models, only send around 2 or 3 frames per second. Processing 10 and more frames might delay the AI result. At least 1 minute of spontaneous conversational speech is required to perform analysis. Audio effects are detected in nonspeech segments only. The minimal duration of a nonspeech section is 2 seconds. Voice commands and singing aren't supported.

## Keywords extraction components

During the Keywords procedure, audio and images in a media file are processed, as follows:

|Component|Definition|
|---|---|
|Source language |	The user uploads the source file for indexing. |
|Transcription API	|The audio file is sent to Azure AI services and the translated transcribed output is returned. If a language has been specified, it's processed.| 
|OCR of video	|Images in a media file are processed using the Azure AI Vision Read API to extract text, its location, and other insights.  |
|Keywords extraction	|An extraction algorithm processes the transcribed audio. The results are then combined with the insights detected in the video during the OCR process. The keywords and where they appear in the media and then detected and identified. |
|Confidence level|	The estimated confidence level of each keyword is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|
