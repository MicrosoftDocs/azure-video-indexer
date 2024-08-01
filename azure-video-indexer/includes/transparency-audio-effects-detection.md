---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 07/25/2024
ms.author: inhenkel
title: transparency audio effects detection
---

## Audio effects detection transparency notes

- Avoid use of short or low-quality audio, audio effects detection provides probabilistic and partial data on detected nonspeech audio events. For accuracy, audio effects detection requires at least 2 seconds of clear nonspeech audio. Voice commands or singing aren't supported.   
- Avoid use of audio with loud background music or music with repetitive and/or linearly scanned frequency, audio effects detection is designed for nonspeech audio only and therefore can't classify events in loud music. Music with repetitive and/or linearly scanned frequency many be incorrectly classified as an alarm or siren. 
- Carefully consider the methods of usage in law enforcement and similar institutions. To promote more accurate probabilistic data, ensure that: 

    - Audio effects can be detected in nonspeech segments only. 
    - The duration of a nonspeech section should be at least 2 seconds. 
    - Low quality audio might affect the detection results.  
    - Events in loud background music aren't classified.  
    - Music with repetitive and/or linearly scanned frequency might be incorrectly classified as an alarm or siren. 
    - Knocking on a door or slamming a door might be labeled as a gunshot or explosion. 
    - Prolonged shouting or sounds of physical human effort might be incorrectly classified. 
    - A group of people laughing might be classified as both laughter and crowd. 
    - Natural and nonsynthetic gunshot and explosions sounds are supported.

##  Audio effects detection components

During the audio effects detection procedure, audio in a media file is processed, as follows:

|Component|Definition|
|---|---|
|Source file |	The user uploads the source file for indexing. |
|Segmentation|  	The audio is analyzed, nonspeech audio is identified and then split into short overlapping internals. |
|Classification| 	An AI process analyzes each segment and classifies its contents into event categories such as crowd reaction or laughter. A probability list is then created for each event category according to department-specific rules. |
|Confidence level|	The estimated confidence level of each audio effect is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|