---
title: Audio effects detection
titleSuffix: Azure AI Video Indexer
services: azure-video-indexer
ms.service: azure-video-indexer
ms.topic: include
ms.date: 06/26/2024
ms.author: inhenkel
---

## Audio effects detection

Audio effects detection detects insights on acoustic events and classifies them into categories such as laughter, crowd reactions, alarms and/or sirens.

### Use cases

- Companies with a large video archive can improve accessibility by offering more context for a hearing- impaired audience by transcription of nonspeech effects. 
- Improved efficiency when creating raw data for content creators. Important moments in promos and trailers such as laughter, crowd reactions, gunshots, or explosions can be identified, for example,  in Media and Entertainment. 
- Detecting and classifying gunshots, explosions, and glass shattering in a smart-city system or in other public environments that include cameras and microphones to offer fast and accurate detection of violence incidents.

### [Example response](#tab/audioeffectsresponse)

```json
    "audioEffects": [
      {
        "id": 1,
        "type": "Silence",
        "instances": [
          {
            "confidence": 0,
            "adjustedStart": "0:01:46.243",
            "adjustedEnd": "0:01:50.434",
            "start": "0:01:46.243",
            "end": "0:01:50.434"
          }
        ]
      },
      {
        "id": 2,
        "type": "Speech",
        "instances": [
          {
            "confidence": 0,
            "adjustedStart": "0:00:00",
            "adjustedEnd": "0:01:43.06",
            "start": "0:00:00",
            "end": "0:01:43.06"
          }
        ]
      }
    ]
```

### [Components](#tab/audioeffectscomponents)

During the audio effects detection procedure, audio in a media file is processed, as follows:

|Component|Definition|
|---|---|
|Source file |	The user uploads the source file for indexing. |
|Segmentation|  	The audio is analyzed, nonspeech audio is identified and then split into short overlapping internals. |
|Classification| 	An AI process analyzes each segment and classifies its contents into event categories such as crowd reaction or laughter. A probability list is then created for each event category according to department-specific rules. |
|Confidence level|	The estimated confidence level of each audio effect is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|

### [Transparency notes](#tab/audioeffectstransnote)

- Avoid use of short or low-quality audio, audio effects detection provides probabilistic and partial data on detected nonspeech audio events. For accuracy, audio effects detection requires at least 2 seconds of clear nonspeech audio. Voice commands or singing aren't supported.   
- Avoid use of audio with loud background music or music with repetitive and/or linearly scanned frequency, audio effects detection is designed for nonspeech audio only and therefore can't classify events in loud music. Music with repetitive and/or linearly scanned frequency many be incorrectly classified as an alarm or siren. 
- Carefully consider the methods of usage in law enforcement and similar institutions, to promote more accurate probabilistic data, carefully review the following: 

    - Audio effects can be detected in nonspeech segments only. 
    - The duration of a nonspeech section should be at least 2 seconds. 
    - Low quality audio might impact the detection results.  
    - Events in loud background music aren't classified.  
    - Music with repetitive and/or linearly scanned frequency might be incorrectly classified as an alarm or siren. 
    - Knocking on a door or slamming a door might be labeled as a gunshot or explosion. 
    - Prolonged shouting or sounds of physical human effort might be incorrectly classified. 
    - A group of people laughing might be classified as both laughter and crowd. 
    - Natural and nonsynthetic gunshot and explosions sounds are supported.

### [Sample code](#tab/audioeffectssamplecode)

[Link to sample code that uses the insight](#)

---