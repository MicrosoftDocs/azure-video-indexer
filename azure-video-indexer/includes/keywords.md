---
title: Keywords extraction
ms.service: azure-video-indexer
ms.topic: include
ms.date: 10/09/2024
ms.author: inhenkel
---

## Keywords extraction

[!INCLUDE [keywords-descritpion](keywords-description.md)]

### Keywords extraction use cases

- Personalization of keywords to match customer interests, for example websites about England posting promotions about English movies or festivals. 
- Deep-searching archives for insights on specific keywords to create feature stories about companies, personas, or technologies, for example by a news agency.

[!INCLUDE [get insights with the web portal](get-insights-web-portal.md)]
[!INCLUDE [get insights with the API](get-insights-api.md)]

## Example response

```json
    "keywords": [
      {
        "id": 1,
        "text": "office insider",
        "confidence": 1,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:00:00",
            "adjustedEnd": "0:00:05.75",
            "start": "0:00:00",
            "end": "0:00:05.75"
          },
          {
            "adjustedStart": "0:01:21.82",
            "adjustedEnd": "0:01:24.7",
            "start": "0:01:21.82",
            "end": "0:01:24.7"
          },
          {
            "adjustedStart": "0:01:31.32",
            "adjustedEnd": "0:01:32.76",
            "start": "0:01:31.32",
            "end": "0:01:32.76"
          },
          {
            "adjustedStart": "0:01:35.8",
            "adjustedEnd": "0:01:37.84",
            "start": "0:01:35.8",
            "end": "0:01:37.84"
          }
        ]
      },
      {
        "id": 2,
        "text": "insider tip",
        "confidence": 0.9975,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:01:14.91",
            "adjustedEnd": "0:01:19.51",
            "start": "0:01:14.91",
            "end": "0:01:19.51"
          }
        ]
      }
```
[!INCLUDE [General transparency note](read-general-transparency-note.md)]
[!INCLUDE [transparency-keywords-extraction](transparency-keywords-extraction.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)
