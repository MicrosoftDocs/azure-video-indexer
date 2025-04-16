---
title: How to use global face grouping
description: With VI, scaling facial recognition of thousands of faces is easy if a labeled and tagged dataset already exists. However, what if the dataset doesn't exist yet or isn't available for detecting faces in your video collection? Global face grouping can help you find faces that are frequently detected in videos but aren’t yet labeled or tagged. By using global face grouping, you can enhance your account’s custom face identification database.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/09/2024
ms.service: azure-video-indexer
ms.topic: how-to
---

# How to use global face grouping

With VI, scaling the facial recognition of thousands of faces is easy if a labeled and tagged dataset already exists. However, what if the dataset doesn't exist yet or isn't available for detecting faces in your video collection? Global face grouping can help you find faces that are frequently detected in videos but aren’t yet labeled or tagged. By using global face grouping, you can enhance your account’s custom face identification database.

## Overview

You can use this feature by selecting the **group faces** button located in the **people customization** tab of the **model customization** screen in the Azure AI Video Indexer web interface. Then, you can review the grouped faces and tag them. You can group faces iteratively to find more face groupings.

## Limitations and requirements

-   **Minimum Requirements**: For effective processing, accounts must have a minimum of 50 high-quality, indexed, unknown face detections.
-   **Maximum Threshold**: Accounts are allowed 500,000 unknown faces. After the 500,000 unknown faces threshold is reached, the oldest videos' unidentified faces don't get used or presented for grouping.
-   **Quality Control**: Duplicate detections, and detections that are smaller than 50 pixels in width or height, or having significant occlusions or blurriness, are excluded from the process.

## Use global face grouping

1.  In the Azure AI Video Indexer web interface, select the **model customizations** icon from the menu.
2.  Select **People**.
3.  Select the **Unknown people** tab, then select the **Group Faces** button. If there are unknown people in your already indexed video archive, they appear grouped by facial similarity.
4.  Label the person.

> [!IMPORTANT]
> It's crucial to ensure accuracy in naming and to eliminate any erroneous face examples to prevent future duplication. You can delete irrelevant groups or false detections within groups before finalizing the naming process.

Once a person is labeled, the videos in which this person appears are sampled and assigned to the designated person catalog. There's no need to reindex the videos.

### Find all the videos where the person is detected

After a person is labeled, you can find all the videos where the identified person appears. You can use the people section of a video’s insights, select the People item from the Model customizations menu, or you can search for the person’s name.
