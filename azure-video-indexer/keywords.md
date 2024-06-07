---
title: Azure AI Video Indexer keywords extraction overview 
description: An introduction to Azure AI Video Indexer keywords extraction component responsibly.
ms.date: 06/06/2024
ms.topic: article
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Keywords extraction

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

Keywords extraction is an Azure AI Video Indexer AI feature that automatically detects insights on the different keywords discussed in media files. Keywords extraction can extract insights in both single language and multi-language media files. The total number of extracted keywords and their categories are listed in the Insights tab, where clicking a Keyword and then clicking Play Previous or Play Next jumps to the keyword in the media file.  

## Prerequisites  

Review [Transparency Note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context) 

## View the insight

When working on the website the insights are displayed in the **Insights** tab. They can also be generated in a categorized list in a JSON file which includes the Keyword’s ID, text, together with each keyword’s specific start and end time and confidence score.  

To display the instances in a JSON file, do the following: 

1. Click Download and then Insights (JSON).  
1. Copy the text and paste it into your Online JSON Viewer. 
    
    ```json
    "keywords": [
      {
        "id": 1,
        "text": "office insider",
        "confidence": 1,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:00:00",
            "adjustedEnd": "0:00:05.75",
            "start": "0:00:00",
            "end": "0:00:05.75"
          },
          {
            "adjustedStart": "0:01:21.82",
            "adjustedEnd": "0:01:24.7",
            "start": "0:01:21.82",
            "end": "0:01:24.7"
          },
          {
            "adjustedStart": "0:01:31.32",
            "adjustedEnd": "0:01:32.76",
            "start": "0:01:31.32",
            "end": "0:01:32.76"
          },
          {
            "adjustedStart": "0:01:35.8",
            "adjustedEnd": "0:01:37.84",
            "start": "0:01:35.8",
            "end": "0:01:37.84"
          }
        ]
      },
      {
        "id": 2,
        "text": "insider tip",
        "confidence": 0.9975,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:01:14.91",
            "adjustedEnd": "0:01:19.51",
            "start": "0:01:14.91",
            "end": "0:01:19.51"
          }
        ]
      },

    ```
    
To download the JSON file via the API, use the [Azure AI Video Indexer developer portal](https://api-portal.videoindexer.ai/). 

> [!NOTE]
> Keywords extraction is language independent. 

## Keywords components

During the Keywords procedure, audio and images in a media file are processed, as follows:

|Component|Definition|
|---|---|
|Source language |	The user uploads the source file for indexing. |
|Transcription API	|The audio file is sent to Azure AI services and the translated transcribed output is returned. If a language has been specified it is processed.| 
|OCR of video	|Images in a media file are processed using the Azure AI Vision Read API to extract text, its location, and other insights.  |
|Keywords extraction	|An extraction algorithm processes the transcribed audio. The results are then combined with the insights detected in the video during the OCR process. The keywords and where they appear in the media and then detected and identified. |
|Confidence level|	The estimated confidence level of each keyword is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty will be represented as an 0.82 score.|

## Example use cases 

- Personalization of keywords to match customer interests, for example websites about England posting promotions about English movies or festivals. 
- Deep-searching archives for insights on specific keywords to create feature stories about companies, personas or technologies, for example by a news agency.  

## Considerations and limitations when choosing a use case 

Below are some considerations to keep in mind when using keywords extraction: 

- When uploading a file always use high-quality video content. The recommended maximum frame size is HD and frame rate is 30 FPS. A frame should contain no more than 10 people. When outputting frames from videos to AI models, only send around 2 or 3 frames per second. Processing 10 and more frames might delay the AI result.   
- When uploading a file always use high quality audio and video content. At least 1 minute of spontaneous conversational speech is required to perform analysis. Audio effects are detected in non-speech segments only. The minimal duration of a non-speech section is 2 seconds. Voice commands and singing aren't supported.
