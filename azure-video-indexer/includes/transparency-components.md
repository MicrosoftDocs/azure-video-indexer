---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.collection: ce-skilling-ai-copilot,rai-skilling-ai-copilot
ms.date: 10/09/2024
ms.author: inhenkel
title: transparency components
---

## Components of Azure AI Video Indexer

During the Azure AI Video Indexer procedure, a media file is processed using Azure APIs to extract different types of insights, as follows:

| Component | Definition |
|--|--|
| Video uploader | The user uploads a media file to be processed by Azure AI Video Indexer. |
| Insights generation | *Azure services APIs such as Azure AI services OCR and Transcription, extract insights.* <br/> Internal AI models are run to generate insights like Detected Audio Events, Observed People, Detected Clothing, and Topics. |
| Insights processing | Additional logic such as confidence level threshold filtering is applied to the output of Insights generation to create the final insights that are then displayed in the Azure AI Video Indexer portal and in the JSON file that can be downloaded from the portal. |
| Storage | Output from the processed media file is saved in: <br/><br/> • Azure Storage <br/> • Azure Search, where users can search for videos using specific insights like an actor’s name, a location, or a brand. <br/><br/> |
| Notification | The user receives notification that the indexing process has been completed. |