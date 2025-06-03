## Topics inference

[!INCLUDE [topics inference description](topics-inference-description.md)] 

In the web portal, the extracted Topics and categories (when available) are listed in the Insights tab. To jump to the topic in the media file, select a Topic -> Play Previous or Play Next.

## Topics inference use cases 

- Personalization using topics inference to match customer interests, for example websites about England posting promotions about English movies or festivals.
- Deep-searching archives for insights on specific topics to create feature stories about companies, personas, or technologies, for example by a news agency. 
- Monetization, increasing the worth of extracted insights. For example, industries like the news or social media that rely on ad revenue can deliver relevant ads by using the extracted insights as other signals to the ad server.

## View the insight JSON with the web portal

After you upload and index a video, download insights in JSON format from the web portal.

1. Select the **Library** tab.
1. Select the media you want.
1. Select **Download**, and then select **Insights (JSON)**. The JSON file opens in a new browser tab.
1. Find the key pair described in the example response.

## Use the API

1. Use a [Get Video Index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Index) request. Pass `&includeSummarizedInsights=false`.
2. Find the key pairs described in the example response.

## Example response
     
```json
    "topics": [
      {
        "id": 1,
        "name": "Pens",
        "referenceId": "Category:Pens",
        "referenceUrl": "https://en.wikipedia.org/wiki/Category:Pens",
        "referenceType": "Wikipedia",
        "confidence": 0.6833,
        "iabName": null,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:00:30",
            "adjustedEnd": "0:01:17.5",
            "start": "0:00:30",
            "end": "0:01:17.5"
          }
        ]
      },
      {
        "id": 2,
        "name": "Musical groups",
        "referenceId": "Category:Musical_groups",
        "referenceUrl": "https://en.wikipedia.org/wiki/Category:Musical_groups",
        "referenceType": "Wikipedia",
        "confidence": 0.6812,
        "iabName": null,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:01:10",
            "adjustedEnd": "0:01:17.5",
            "start": "0:01:10",
            "end": "0:01:17.5"
          }
        ]
      },
```
[!INCLUDE [General transparency note](read-general-transparency-note.md)]

[!INCLUDE [transparency-topics-inference](transparency-topics-inference.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)
