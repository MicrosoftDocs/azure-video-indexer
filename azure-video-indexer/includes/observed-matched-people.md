---
title: Observed people tracking and matched faces
ms.service: azure-video-indexer
ms.topic: include
ms.date: 07/25/2024
ms.author: inhenkel
---

## Observed people tracking and matched faces

> [!IMPORTANT]
> Face identification, customization and celebrity recognition features access is limited based on eligibility and usage criteria in order to support our Responsible AI principles. Face identification, customization and celebrity recognition features are only available to Microsoft managed customers and partners. Use the [Face Recognition intake form](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR7en2Ais5pxKtso_Pz4b1_xUQjA5SkYzNDM4TkcwQzNEOE1NVEdKUUlRRCQlQCN0PWcu) to apply for access.

Observed people tracking and matched faces automatically detect and match people in media files. Observed people tracking and matched faces can be set to display insights on people, their clothing, and the exact timeframe of their appearance.

In the web portal, the resulting insights are displayed in a categorized list in the Insights tab, the tab includes a thumbnail of each person and their ID. Clicking the thumbnail of a person displays the matched person (the corresponding face in the People insight). Insights are also generated in a categorized list in a JSON file that includes the thumbnail ID of the person, the percentage of time appearing in the file, Wiki link (if they're a celebrity) and confidence level.

## Observed people tracking and matched faces use cases

- Tracking a person’s movement, for example,  in law enforcement for more efficiency when analyzing an accident or crime.
- Improving efficiency by deep searching for matched people in organizational archives for insight on specific celebrities, for example when creating promos and trailers.
- Improved efficiency when creating feature stories, for example, searching for people wearing a red shirt in the archives of a football game at a News or Sports agency.

[!INCLUDE [get insights with the web portal](get-insights-web-portal.md)]
[!INCLUDE [get insights with the API](get-insights-api.md)]

## Example response

```json
    "observedPeople": [
      {
        "id": 1,
        "thumbnailId": "4addcebf-6c51-42cd-b8e0-aedefc9d8f6b",
        "clothing": [
          {
            "id": 1,
            "type": "sleeve",
            "properties": {
              "length": "long"
            }
          },
          {
            "id": 2,
            "type": "pants",
            "properties": {
              "length": "long"
            }
          }
        ],
        "instances": [
          {
            "adjustedStart": "0:00:00.0667333",
            "adjustedEnd": "0:00:12.012",
            "start": "0:00:00.0667333",
            "end": "0:00:12.012"
          }
        ]
      },
      {
        "id": 2,
        "thumbnailId": "858903a7-254a-438e-92fd-69f8bdb2ac88",
        "clothing": [
          {
              "id": 1,
              "type": "sleeve",
              "properties": {
                  "length": "short"
              }
          }
        ],
        "instances": [
          {
              "adjustedStart": "0:00:23.2565666",
              "adjustedEnd": "0:00:25.4921333",
              "start": "0:00:23.2565666",
              "end": "0:00:25.4921333"
          },
          {
              "adjustedStart": "0:00:25.8925333",
              "adjustedEnd": "0:00:25.9926333",
              "start": "0:00:25.8925333",
              "end": "0:00:25.9926333"
          },
          {
              "adjustedStart": "0:00:26.3930333",
              "adjustedEnd": "0:00:28.5618666",
              "start": "0:00:26.3930333",
              "end": "0:00:28.5618666"
          }
        ]
      },
      {
        "id": 3,
        "thumbnailId": "1406252d-e7f5-43dc-852d-853f652b39b6",
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
                "length": "long"
            }
          },
          {
            "id": 3,
            "type": "skirtAndDress"
          }
        ],
        "instances": [
          {
            "adjustedStart": "0:00:31.9652666",
            "adjustedEnd": "0:00:34.4010333",
            "start": "0:00:31.9652666",
            "end": "0:00:34.4010333"
          }
        ]
      },
      {
        "id": 4,
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
[!INCLUDE [transparency-observed-people-tracking-matched-faces](transparency-observed-people-tracking-matched-faces.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)
