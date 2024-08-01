---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 07/25/2024
ms.author: inhenkel
title: transparency Labels identification
---

## Labels identification transparency notes

- Carefully consider the accuracy of the results, to promote more accurate detections, check the quality of the video, low quality video might affect the detected insights. 
- Carefully consider when using for law enforcement that Labels potentially can't detect parts of the video. To ensure fair and high-quality decisions, combine Labels with human oversight. 
- Don't use labels identification for decisions that might have serious adverse impacts. Machine learning models can result in undetected or incorrect classification output. Decisions based on incorrect output could have serious adverse impacts. Additionally, it's advisable to include human review of decisions that have the potential for serious impacts on individuals.

## Labels identification components 

During the Labels procedure, objects in a media file are processed, as follows:

|Component|Definition|
|---|---|
|Source	|The user uploads the source file for indexing. |
|Tagging|	Images are tagged and labeled. For example, door, chair, woman, headphones, jeans. |
|Filtering and aggregation	|Tags are filtered according to their confidence level and aggregated according to their category.|
|Confidence level|	The estimated confidence level of each label is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|
