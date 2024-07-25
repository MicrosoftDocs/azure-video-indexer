---
title: Face detection decription
ms.service: azure-video-indexer
ms.topic: include
ms.date: 07/25/2024
ms.author: inhenkel
---

Face detection detects faces in a media file, and then aggregates instances of similar faces into groups.

Face detection insights are generated as a categorized list in a JSON file that includes a thumbnail and either a name or an ID for each face. In the web portal, selecting a face’s thumbnail displays information like the name of the person (if they were recognized), the percentage of the video that the person appears, and the person's biography, if they're a celebrity. You can also scroll between instances in the video where the person appears.