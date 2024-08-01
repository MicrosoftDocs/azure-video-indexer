---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 07/25/2024
ms.author: inhenkel
title: Transparency imitations - video
---

### Video
- Azure AI Video Indexer has a storage limit of 30 GB and 4 hours for uploaded, previously recorded videos.
- Always upload high-quality video and audio content. The recommended maximum frame size is HD and frame rate is 30 FPS. A frame should contain no more than 10 people. When outputting frames from videos to AI models, only send around two or three frames per second. Processing 10 or more frames might delay the AI result. At least 1 minute of spontaneous conversational speech is required to perform analysis. Audio effects are detected in nonspeech segments only. The minimal duration of a nonspeech section is 2 seconds. Voice commands and singing aren't supported.
- Lower accuracy of the generated insights might occur when people and faces recorded by cameras that are high-mounted, down-angled or with a wide field of view (FOV) might have fewer pixels.
- Typically, small people or objects under 200 pixels and people who are seated might not be detected. People wearing similar clothes or uniforms might be detected as being the same person and are given the same ID number. People or objects that are obstructed might not be detected. Tracks of people with front and back poses might be split into different instances.
- An observed person must first be detected and appear in the People category before they're matched. Tracks are optimized to handle observed people who frequently appear in the foreground. Obstructions like overlapping people or faces might cause mismatches between matched people and observed people. Mismatching might occur when different people appear in the same relative spatial position in the frame within a short period.
- Dresses and skirts are categorized as Dresses or Skirts. Clothing the same color as a person’s skin isn't detected. A full view of the person is required. To optimize detection, both the upper and lower body should be included in the frame.
- Avoid using the OCR results of signatures that are hard to read for both humans and machines. A better way to use OCR is to use it for detecting the presence of a signature for further analysis.
- Named entities only detects insights in audio and images. Logos in a brand name might not be detected.
- Detectors might misclassify objects in videos that are in a "birds-eye" view as there were trained with a frontal view of objects.
