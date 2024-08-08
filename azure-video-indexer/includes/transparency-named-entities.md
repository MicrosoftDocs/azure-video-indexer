---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 07/25/2024
ms.author: inhenkel
title: transparency Named entities
---

## Named entities

-	Carefully consider the accuracy of the results, to promote more accurate detections, check the quality of the audio and images, low quality audio and images might impact the detected insights. 
-	Named entities only detect insights in audio and images. Logos in a brand name may not be detected.
-	Carefully consider that when using for law enforcement named entities may not always detect parts of the audio. To ensure fair and high-quality decisions, combine named entities with human oversight. 
-	Don't use named entities for decisions that may have serious adverse impacts. Machine learning models that extract text can result in undetected or incorrect text output. Decisions based on incorrect output could have serious adverse impacts. Additionally, it's advisable to include human review of decisions that have the potential for serious impacts on individuals.

## Components 

During the named entities extraction procedure, the media file is processed, as follows:   

|Component|Definition|
|---|---|
| Source file | 	The user uploads the source file for indexing. |
| Text extraction |- The audio file is sent to Speech Services API to extract the transcription.<br/>- Sampled frames are sent to the Azure AI Vision API to extract OCR. |
| Analytics	|The insights are then sent to the Text Analytics API to extract the entities. For example, Microsoft, Paris or a person’s name like Paul or Sarah.
| Processing and consolidation |	The results are then processed. Where applicable, Wikipedia links are added and brands are identified via the Video Indexer built-in and customizable branding lists.
| Confidence value | The estimated confidence level of each named entity is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|
