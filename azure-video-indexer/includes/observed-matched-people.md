---
title: Observed people detection and matched faces
ms.service: azure-video-indexer
ms.topic: include
ms.date: 08/22/2024
ms.author: inhenkel
---

## Observed people detection, matched faces, detected clothing

> [!IMPORTANT]
> Face identification, customization and celebrity recognition features access is limited based on eligibility and usage criteria in order to support our Responsible AI principles. Face identification, customization and celebrity recognition features are only available to Microsoft managed customers and partners. Use the [Face Recognition intake form](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR7en2Ais5pxKtso_Pz4b1_xUQjA5SkYzNDM4TkcwQzNEOE1NVEdKUUlRRCQlQCN0PWcu) to apply for access.

Observed people detection and matched faces automatically detect and match people in media files. Observed people detection and matched faces can be set to display insights on people, their clothing, and the exact timeframe of their appearance.

In the web portal, the resulting insights are displayed in a categorized list in the Insights tab, the tab includes a thumbnail of each person and their ID. Clicking the thumbnail of a person displays the matched person (the corresponding face in the People insight). Insights are also generated in a categorized list in a JSON file that includes the thumbnail ID of the person, the percentage of time appearing in the file, Wiki link (if they're a celebrity) and confidence level.

## Observed people detection, detected clothing and matched faces use cases

- Improving efficiency by deep searching for matched people in organizational archives for insight on specific celebrities, for example when creating promos and trailers.
- Improved efficiency when creating feature stories, for example, searching for people wearing a red shirt in the archives of a football game at a News or Sports agency.  
- Create a summary out of a long video, like court evidence of a specific person’s appearance in a video, using the same detected person’s ID.
- Learn and analyze trends over time, for example—how customers move across aisles in a shopping mall or how much time they spend in checkout lines.

The **matched faces** and **detected clothing** features are available when indexing your file by choosing the **Advanced** -> **Video + audio indexing** preset.


[!INCLUDE [get insights with the web portal](get-insights-web-portal.md)]
[!INCLUDE [get insights with the API](get-insights-api.md)]

## Example response

```json
"observedPeople": [
    {
        "id": 1,
        "thumbnailId": "d09ad62e-e0a4-42e5-8ca9-9a640c686596",
        "clothing": [
            {
                "id": 1,
                "type": "sleeve",
                "properties": {
                    "length": "short"
                }
            },
            {
                "id": 2,
                "type": "pants",
                "properties": {
                    "length": "short"
                }
            }
        ],
        "matchingFace": {
            "id": 1310,
            "confidence": 0.3819
        },
        "instances": [
            {
                "adjustedStart": "0:00:34.8681666",
                "adjustedEnd": "0:00:36.0026333",
                "start": "0:00:34.8681666",
                "end": "0:00:36.0026333"
            },
            {
                "adjustedStart": "0:00:36.6699666",
                "adjustedEnd": "0:00:36.7367",
                "start": "0:00:36.6699666",
                "end": "0:00:36.7367"
            },
            {
                "adjustedStart": "0:00:37.2038333",
                "adjustedEnd": "0:00:39.6729666",
                "start": "0:00:37.2038333",
                "end": "0:00:39.6729666"
            }
        ]
    }
]
```

[!INCLUDE [General transparency note](read-general-transparency-note.md)]
[!INCLUDE [transparency-observed-people-detection-matched-faces](transparency-observed-people-detection-matched-faces.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)
