## Named entities extraction

[!INCLUDE [Named entities description](named-entities-description.md)]

## Named entities use cases

- Contextual advertising, for example, placing an ad for a pizza chain following footage on Italy.
- Deep searching media archives for insights on people or locations to create feature stories for the news.
- Creating a verbal description of footage using optical character recognition (OCR) processing to enhance accessibility for the visually impaired, for example a background storyteller in movies.
- Extracting insights on brand names.

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
    namedPeople: [
    {
    referenceId: "Satya_Nadella",
    referenceUrl: "https://en.wikipedia.org/wiki/Satya_Nadella",
    confidence: 1,
    description: "CEO of Microsoft Corporation",
    seenDuration: 33.2,
    id: 2,
    name: "Satya Nadella",
    appearances: [
    {
    startTime: "0:01:11.04",
    endTime: "0:01:17.36",
    startSeconds: 71,
    endSeconds: 77.4
    },
    {
    startTime: "0:01:31.83",
    endTime: "0:01:37.1303666",
    startSeconds: 91.8,
    endSeconds: 97.1
    },
```

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

[!INCLUDE [transparency-named-entities](transparency-named-entities.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)
