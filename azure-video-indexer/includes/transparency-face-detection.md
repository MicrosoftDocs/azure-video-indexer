---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 07/25/2024
ms.author: inhenkel
title: Transparency Face detection
---

## Face detection transparency notes

Face detection is a valuable tool for many industries when it's used responsibly and carefully. To respect the privacy and safety of others, and to comply with local and global regulations, we recommend that you follow these use guidelines:

- Carefully consider the accuracy of the results. To promote more accurate detection, check the quality of the video. Low-quality video might affect the insights that are presented.
- Carefully review results if you use face detection for law enforcement. People might not be detected if they're small, sitting, crouching, or obstructed by objects or other people. To ensure fair and high-quality decisions, combine face detection-based automation with human oversight.
- Don't use face detection for decisions that might have serious, adverse impacts. Decisions that are based on incorrect output can have serious, adverse impacts. It's advisable to include human review of decisions that have the potential for serious impacts on individuals.

## Face detection components

The following table describes how images in a media file are processed during the face detection procedure:

| Component | Definition |
|---|---|
| Source file | The user uploads the source file for indexing. |
| Detection and aggregation | The face detector identifies the faces in each frame. The faces are then aggregated and grouped. |
| Recognition | The celebrities model processes the aggregated groups to recognize celebrities. If you've created your own people model, it also processes groups to recognize other people. If people aren't recognized, they're labeled Unknown1, Unknown2, and so on. |
| Confidence value | Where applicable for well-known faces or for faces that are identified in the customizable list, the estimated confidence level of each label is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82 percent certainty is represented as an 0.82 score. |
