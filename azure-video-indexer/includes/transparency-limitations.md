---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.collection: ce-skilling-ai-copilot,rai-skilling-ai-copilot
ms.date: 10/09/2024
ms.author: inhenkel
title: transparency characteristics and limitations
---

## Characteristics and limitations of Video Indexer

The intended use of Azure AI Video Indexer is to generate insights from recorded media and entertainment content. Extracted insights are created in a JSON file that lists the insights in categories. Each insight holds a list of unique elements, and each element has its own metadata and a list of its instances. For example, a face might have an ID, a name, a thumbnail, other metadata, and a list of its temporal instances. The output of some insights may also display a confidence score to indicate its accuracy level.

A JSON file can be accessed in three ways:

- Azure AI Video Indexer portal, an easy-to-use solution that lets you evaluate the product, manage the account, and customize models.  
- API integration, via a REST API, which lets you integrate the solution into your apps and infrastructure.  
- Embeddable widget, which lets you embed the Azure AI Video Indexer insights, player, and editor experiences into your app to customize the insights displayed in a web interface. For example, the list can be customized to display insights only about people appearing in a video. To find videos that include a specific celebrity, a content editor can implement a deep search using the name appearing in the Face or People insights categories.