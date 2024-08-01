---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 07/25/2024
ms.author: inhenkel
title: transparency scene shot keyframe detection
---

## Scene, shot, and keyframe transparency notes

- The algorithm works best on media files that have shots and scenes within them.  
- If the video is filmed with one camera that never moves, the shot segmentation will work poorly, and the keyframes might not be representative. 
- Keyframes are selected by taking into account the blurriness level of the frames. If most of the shot is blurry, for example with motion, the keyframe might also be blurry. 
- Videos with poor visual quality won't work as well. 
- The time of each shot/scene/keyframe may shift (less than a second).

## Scene, shot, and keyframe components

No components defined.