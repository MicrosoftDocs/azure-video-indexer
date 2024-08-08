---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 08/08/2024
ms.author: inhenkel
title: transparency observed people tracking and matched faces
---

## Observed people tracking and matched faces notes

- People are generally not detected if they appear small (minimum person height is 100 pixels).
- Maximum frame size is FHD
- Low quality video (for example, dark lighting conditions) may impact the detection results.
- The recommended frame rate at least 30 FPS.
- Recommended video input should contain up to 10 people in a single frame. The feature could work with more people in a single frame, but the detection result retrieves up to 10 people in a frame with the detection highest confidence.
- People with similar clothes: (for example, people wear uniforms, players in sport games) could be detected as the same person with the same ID number.
- Obstruction – there maybe errors where there are obstructions (scene/self or obstructions by other people).
- Pose: The tracks may be split due to different poses (back/front)
- As clothing detection is dependent on the visibility of the person’s body, the accuracy is higher if a person is fully visible. There might be errors when a person is without clothing. In this scenario or others of poor visibility, results may be given such as long pants and skirt or dress.

## Observed people tracking and matched faces components

|Component|Definition|
|---|---|
| Source file |    The user uploads the source file for indexing.   |
| Detection |    The media file is tracked to detect observed people and their clothing. For example, shirt with long sleeves, dress or long pants. Note that to be detected, the full upper body of the person must appear in the media.|
| Local grouping    |The identified observed faces are filtered into local groups. If a person is detected more than once, additional observed faces instances are created for this person. |
| Matching and classification    |The observed people instances are matched to faces. If there is a known celebrity, the observed person will be given their name. Any number of observed people instances can be matched to the same face.  |
| Confidence value|    The estimated confidence level of each observed person is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|
