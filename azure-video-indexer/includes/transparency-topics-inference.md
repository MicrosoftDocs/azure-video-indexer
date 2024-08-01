---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 07/25/2024
ms.author: inhenkel
title: transparency topics inference
---

## Topics inference transparency notes

- When uploading a file, always use high-quality video content. The recommended maximum frame size is HD and frame rate is 30 FPS. A frame should contain no more than 10 people. When outputting frames from videos to AI models, only send around two or three frames per second. Processing 10 and more frames might delay the AI result.  
- When uploading a file always use high quality audio and video content. At least 1 minute of spontaneous conversational speech is required to perform analysis. Audio effects are detected in nonspeech segments only. The minimal duration of a nonspeech section is 2 seconds. Voice commands and singing aren't supported. 
- Typically, small people or objects under 200 pixels and people who are seated might not be detected. People wearing similar clothes or uniforms might be detected as being the same person and are given the same ID number. People or objects that are obstructed might not be detected. Tracks of people with front and back poses might be split into different instances.

## Topics inference components
 
|Component|Definition|
|---|---|
|Source language	|The user uploads the source file for indexing.|
|Preprocessing|Transcription, OCR, and facial recognition AIs extract insights from the media file.|
|Insights processing|	Topics AI analyzes the transcription, OCR, and facial recognition insights extracted during preprocessing: <br/>-	Transcribed text, each line of transcribed text insight is examined using ontology-based AI technologies. <br/>-	OCR and Facial Recognition insights are examined together using ontology-based AI technologies.  |
|Post-processing	|- Transcribed text, insights are extracted and tied to a Topic category together with the line number of the transcribed text. For example, Politics in line 7.<br/>- OCR and Facial Recognition, each insight is tied to a Topic category together with the time of the topic’s instance in the media file. For example, Freddie Mercury in the People and Music categories at 20.00. |
|Confidence value	|The estimated confidence level of each topic is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|
