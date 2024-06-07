---
title: Azure AI Video Indexer named entities extraction overview 
description: An introduction to Azure AI Video Indexer named entities extraction component responsibly.
ms.date: 06/06/2024
ms.topic: article
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Named entities extraction

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

Named entities extraction is an Azure AI Video Indexer AI feature that uses Natural Language Processing (NLP) to extract insights on the locations, people and brands appearing in audio and images in media files. Named entities extraction is automatically used with Transcription and OCR and its insights are based on those extracted during these processes. The resulting insights are displayed in the **Insights** tab and are filtered into locations, people and brand categories. Clicking a named entity, displays its instance in the media file. It also displays a description of the entity and a Find on Bing link of recognizable entities.   

## Prerequisites  

Review [Transparency Note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context)

## View the insight

To see the insights in the website, do the following:

1. Go to View and check Named Entities.
1. Go to Insights and scroll to named entities.

To display named entities extraction insights in a JSON file, do the following: 

1. Click Download and then Insights (JSON).
2. Named entities are divided into three:

    * Brands
    * Location
    * People
3. Copy the text and paste it into your JSON Viewer.
    
    ```json
    namedPeople: [
    {
    referenceId: "Satya_Nadella",
    referenceUrl: "https://en.wikipedia.org/wiki/Satya_Nadella",
    confidence: 1,
    description: "CEO of Microsoft Corporation",
    seenDuration: 33.2,
    id: 2,
    name: "Satya Nadella",
    appearances: [
    {
    startTime: "0:01:11.04",
    endTime: "0:01:17.36",
    startSeconds: 71,
    endSeconds: 77.4
    },
    {
    startTime: "0:01:31.83",
    endTime: "0:01:37.1303666",
    startSeconds: 91.8,
    endSeconds: 97.1
    },
    ```
    
To download the JSON file via the API, use the [Azure AI Video Indexer developer portal](https://api-portal.videoindexer.ai/). 

## Named entities extraction components 

During the named entities extraction procedure, the media file is processed, as follows:   

|Component|Definition|
|---|---|
|Source file | 	The user uploads the source file for indexing. |
|Text extraction |- The audio file is sent to Speech Services API to extract the transcription.<br/>- Sampled frames are sent to the Azure AI Vision API to extract OCR. |
|Analytics	|The insights are then sent to the Text Analytics API to extract the entities. For example, Microsoft, Paris or a person’s name like Paul or Sarah.
|Processing and consolidation |	The results are then processed. Where applicable, Wikipedia links are added and brands are identified via the Video Indexer built-in and customizable branding lists.
Confidence value	The estimated confidence level of each named entity is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|

## Example use cases 

-	Contextual advertising, for example, placing an ad for a Pizza chain following footage on Italy.
- Deep searching media archives for insights on people or locations to create feature stories for the news.
-	Creating a verbal description of footage via OCR processing to enhance accessibility for the visually impaired, for example a background storyteller in movies. 
-	Extracting insights on brand na

## Considerations and limitations when choosing a use case 

-	Carefully consider the accuracy of the results, to promote more accurate detections, check the quality of the audio and images, low quality audio and images might impact the detected insights. 
-	Named entities only detect insights in audio and images. Logos in a brand name may not be detected.
-	Carefully consider that when using for law enforcement named entities may not always detect parts of the audio. To ensure fair and high-quality decisions, combine named entities with human oversight. 
-	Don't use named entities for decisions that may have serious adverse impacts. Machine learning models that extract text can result in undetected or incorrect text output. Decisions based on incorrect output could have serious adverse impacts. Additionally, it's advisable to include human review of decisions that have the potential for serious impacts on individuals. 
 