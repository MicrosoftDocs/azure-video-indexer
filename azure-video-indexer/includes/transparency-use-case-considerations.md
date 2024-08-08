---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 07/25/2024
ms.author: inhenkel
title: transparency use case considerations
---

## Use case considerations

- Avoid using Video Indexer for decisions that may have serious adverse impacts. Decisions based on incorrect output could have serious adverse impacts. Additionally, it is advisable to include human review of decisions that have the potential for serious impacts on individuals.
- The Video Indexer text-based emotion detection was not designed to assess employee performance or the emotional state of an individual.
- Bring Your Own Model
    - Azure AI Video Indexer isn't responsible for the way you use an external AI model. It is your responsibility to ensure that your external AI models are compliant with Responsible Artifical Intelligence standards.
    - Azure AI Video Indexer isn't responsible for the custom insights you create while using the Bring Your Own Model feature as they are not generated by Azure Video Indexer models.