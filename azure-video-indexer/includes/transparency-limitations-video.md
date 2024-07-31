---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 07/25/2024
ms.author: inhenkel
title: transparency imitations - video
---

### Video
- Azure AI Video Indexer only supports the processing of recorded footage, with a storage limit of 30GB and 4 hours for uploaded videos.
- When uploading a file always use high-quality video content. The recommended maximum frame size is HD and frame rate is 30 FPS. A frame should contain no more than 10 people. When outputting frames from videos to AI models, only send around 2 or 3 frames per second. Processing 10 or more frames might delay the AI result.
- People and faces in videos recorded by cameras that are high-mounted, down-angled or with a wide field of view (FOV) may have fewer pixels which may result in lower accuracy of the generated insights.
- When uploading a file always use high quality audio content. At least 1 minute of spontaneous conversational speech is required to perform analysis. Audio effects are detected in non-speech segments only. The minimal duration of a non-speech section is 2 seconds. Voice commands and singing are not supported.
- Typically, small people or objects under 200 pixels and people who are seated may not be detected. People wearing similar clothes or uniforms might be detected as being the same person and will be given the same ID number. People or objects that are obstructed may not be detected. Tracks of people with front and back poses may be split into different instances.
- An observed person must first be detected and appear in the People category before they are matched. Tracks are optimized to handle observed people who frequently appear in the foreground. Obstructions like overlapping people or faces may cause mismatches between matched people and observed people. Mismatching may occur when different people appear in the same relative spatial position in the frame within a short period.
- When detecting clothing, dresses and skirts are categorized as Dresses or Skirts, clothing the same color as a person’s skin is not detected, and a full view of the person is required. To optimize detection, both the upper and lower body should be included in the frame.
- When extracting handwritten text, avoid using the OCR results of signatures which are hard to read for both humans and machines. A better way to use OCR is to use it for detecting the presence of a signature for further analysis.
- Named entities only detects insights in audio and images. Logos in a brand name may not be detected.
- Detectors may misclassify objects in videos that are in a "birds-eye" view as there were trained witha a frontal view of objects.
