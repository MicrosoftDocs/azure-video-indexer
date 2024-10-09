---
title: Named entities
ms.service: azure-video-indexer
ms.topic: include
ms.date: 10/09/2024
ms.author: inhenkel
---

## Named entities extraction

[!INCLUDE [Named entities description](named-entities-description.md)]

## Named entities use cases 

-	Contextual advertising, for example, placing an ad for a Pizza chain following footage on Italy.
- Deep searching media archives for insights on people or locations to create feature stories for the news.
-	Creating a verbal description of footage via OCR processing to enhance accessibility for the visually impaired, for example a background storyteller in movies. 
-	Extracting insights on brand names.

[!INCLUDE [get insights with the web portal](get-insights-web-portal.md)]
[!INCLUDE [get insights with the API](get-insights-api.md)]

## Example response
    
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

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

[!INCLUDE [transparency-named-entities](transparency-named-entities.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)
