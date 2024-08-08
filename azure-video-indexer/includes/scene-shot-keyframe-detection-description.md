---
title: Scene detection description
services: azure-video-indexer
ms.service: azure-video-indexer
ms.topic: include
ms.date: 07/25/2024
ms.author: inhenkel
---

Scene detection detects when a scene changes in a video based on visual cues. 

A **scene** depicts a single event and is composed of a series of shots, which are related.

**Shots** are a series of frames distinguished by visual cues such as abrupt and gradual transitions in color scheme of adjacent frames. The shot's metadata includes start and end time, as well as a list of keyframes included in the shot.

A **keyframe** is a frame from a shot that best represents a shot.