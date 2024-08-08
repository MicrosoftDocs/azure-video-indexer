---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 08/08/2024
ms.author: inhenkel
title: Transparency clapper board detection
---

## Clapper board detection notes

- The detection algorithm might not correctly identify the values.
- The titles of the fields appearing on the clapper board are optimized to identify the most popular fields appearing on top of clapper boards.  
- The fields detection algorithm might not correctly identify handwritten text or digital digits.
- The algorithm is optimized to identify fields' categories that appear horizontally.  
- The clapper board might not be detected if the frame is blurred or the text written on it can't be read by the human eye.  
- Empty fields’ values might lead to wrong fields categories.

## Clapper board detection components

No components are defined.