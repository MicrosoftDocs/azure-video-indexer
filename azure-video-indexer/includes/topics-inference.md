---
title: Topic inference
ms.service: azure-video-indexer
ms.topic: include
ms.date: 07/09/2024
ms.author: inhenkel
---

## Topics inference

Topics inference creates inferred insights derived from the transcribed audio, OCR content in visual text, and celebrities recognized in the video using the Video Indexer facial recognition model. 

In the web portal, the extracted Topics and categories (when available) are listed in the Insights tab. To jump to the topic in the media file, click a Topic -> Play Previous or Play Next.

## Topics inference use cases 

- Personalization using topics inference to match customer interests, for example websites about England posting promotions about English movies or festivals.
- Deep-searching archives for insights on specific topics to create feature stories about companies, personas or technologies, for example by a news agency. 
- Monetization, increasing the worth of extracted insights. For example, industries like the news or social media that rely on ad revenue can deliver relevant ads by using the extracted insights as additional signals to the ad server.

[!INCLUDE [Insights introductory paragraph](insights-intro-paragraph.md)]

### [Example response](#tab/topicsinferenceresponse)
     
```json
    "topics": [
      {
        "id": 1,
        "name": "Pens",
        "referenceId": "Category:Pens",
        "referenceUrl": "https://en.wikipedia.org/wiki/Category:Pens",
        "referenceType": "Wikipedia",
        "confidence": 0.6833,
        "iabName": null,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:00:30",
            "adjustedEnd": "0:01:17.5",
            "start": "0:00:30",
            "end": "0:01:17.5"
          }
        ]
      },
      {
        "id": 2,
        "name": "Musical groups",
        "referenceId": "Category:Musical_groups",
        "referenceUrl": "https://en.wikipedia.org/wiki/Category:Musical_groups",
        "referenceType": "Wikipedia",
        "confidence": 0.6812,
        "iabName": null,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:01:10",
            "adjustedEnd": "0:01:17.5",
            "start": "0:01:10",
            "end": "0:01:17.5"
          }
        ]
      },
```
    
### [Components](#tab/topicsinferencecomponents)
 
|Component|Definition|
|---|---|
|Source language	|The user uploads the source file for indexing.|
|Pre-processing|Transcription, OCR and facial recognition AIs extract insights from the media file.|
|Insights processing|	Topics AI analyzes the transcription, OCR and facial recognition insights extracted during pre-processing: <br/>-	Transcribed text, each line of transcribed text insight is examined using ontology-based AI technologies. <br/>-	OCR and Facial Recognition insights are examined together using ontology-based AI technologies.  |
|Post-processing	|- Transcribed text, insights are extracted and tied to a Topic category together with the line number of the transcribed text. For example, Politics in line 7.<br/>- OCR and Facial Recognition, each insight is tied to a Topic category together with the time of the topic’s instance in the media file. For example, Freddie Mercury in the People and Music categories at 20.00. |
|Confidence value	|The estimated confidence level of each topic is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|

### [Transparency notes](#tab/namedentitiestransnote)

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

Below are some considerations to keep in mind when using topics:

- When uploading a file always use high-quality video content. The recommended maximum frame size is HD and frame rate is 30 FPS. A frame should contain no more than 10 people. When outputting frames from videos to AI models, only send around 2 or 3 frames per second. Processing 10 and more frames might delay the AI result.  
- When uploading a file always use high quality audio and video content. At least 1 minute of spontaneous conversational speech is required to perform analysis. Audio effects are detected in non-speech segments only. The minimal duration of a non-speech section is 2 seconds. Voice commands and singing aren't supported. 
- Typically, small people or objects under 200 pixels and people who are seated may not be detected. People wearing similar clothes or uniforms might be detected as being the same person and will be given the same ID number. People or objects that are obstructed may not be detected. Tracks of people with front and back poses may be split into different instances. 

### [Sample code](#tab/namedentitiessamplecode)

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

---