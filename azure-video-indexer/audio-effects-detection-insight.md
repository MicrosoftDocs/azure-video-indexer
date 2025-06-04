---
title: Get audio effects detection insights 
description: This article shows you how to get the Azure AI Video Indexer audio effects detection insights.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/04/2025
ms.service: azure-video-indexer
ms.topic: how-to
---

# Get audio effects detection insights

Audio effects detection detects acoustic events and classifies them into categories like laughter, crowd reactions, alarms, or sirens.

### Audio effects use cases

- Improve accessibility by offering more context for a hearing- impaired audience by transcription of nonspeech effects. 
- Improving efficiency when creating raw data for content creators. Important moments in promos and trailers such as laughter, crowd reactions, gunshots, or explosions can be identified, for example, in Media and Entertainment. 
- Detect and classify gunshots, explosions, and glass shattering in a smart-city system or in other public environments that include cameras and microphones.

## Supported audio categories  

Audio effects detection can detect and classify effects into standard and advanced categories. For more information, see [pricing](https://azure.microsoft.com/pricing/details/video-indexer/).

The following table shows which categories are supported depending on **Preset Name** (**Audio Only** / **Video + Audio** vs. **Advance Audio** / **Advance Video + Audio**). When you're using the **Advanced** indexing, categories appear in the **Insights** pane of the website.

|Class |Standard indexing| Advanced indexing|
|---|---|---|
| Crowd Reactions || :heavy_check_mark:|
| Silence| :heavy_check_mark:| :heavy_check_mark:|
| Gunshot or explosion || :heavy_check_mark: |
| Breaking glass || :heavy_check_mark: |
| Alarm or siren|| :heavy_check_mark: |
| Laughter|| :heavy_check_mark: |
| Dog || :heavy_check_mark:|
| Bell ringing|| :heavy_check_mark:|
| Bird|| :heavy_check_mark:|
| Car|| :heavy_check_mark:|
| Engine|| :heavy_check_mark:|
| Crying|| :heavy_check_mark:|
| Music playing|| :heavy_check_mark:|
| Screaming|| :heavy_check_mark:|
| Thunderstorm || :heavy_check_mark:|

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
    "audioEffects": [
      {
        "id": 1,
        "type": "Silence",
        "instances": [
          {
            "confidence": 0,
            "adjustedStart": "0:01:46.243",
            "adjustedEnd": "0:01:50.434",
            "start": "0:01:46.243",
            "end": "0:01:50.434"
          }
        ]
      },
      {
        "id": 2,
        "type": "Speech",
        "instances": [
          {
            "confidence": 0,
            "adjustedStart": "0:00:00",
            "adjustedEnd": "0:01:43.06",
            "start": "0:00:00",
            "end": "0:01:43.06"
          }
        ]
      }
    ]
```

> [!IMPORTANT]
> Read the [transparency note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context) for all VI features. Each insight also has its own transparency note.

[!INCLUDE [transparency-audio-effects-detection](./includes/transparency-audio-effects-detection.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

---

## Closed captions

Audio effects in closed caption files appear as square brackets:

|Type| Example|
|---|---|
|SRT |00:00:00,000  00:00:03,671<br/>[Gunshot or explosion]|
|VTT |00:00:00.000  00:00:03.671<br/>[Gunshot or explosion]|
|TTML|Confidence: 0.9047 <br/> `<p begin="00:00:00.000" end="00:00:03.671">[Gunshot or explosion]</p>`|
|TXT |[Gunshot or explosion]|
|CSV |0.9047,00:00:00.000,00:00:03.671, [Gunshot or explosion]|

> [!NOTE]
> - `Silence` event type isn't added to the closed captions.
> - Minimum timer duration to show an event is 700 milliseconds.

## Add audio effects to closed caption files

### API
You can add audio effects to closed captions files with the [Get video captions](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Captions) request and by choosing *true* for the `includeAudioEffects` parameter. 

> [!NOTE]
> When you use the [update transcript](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Video-Transcript) from closed caption files or [update custom language model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Language-Model) from closed caption files, audio effects included in those files are ignored.

### Web portal
You can also use the web portal by selecting **Download** -> **Closed Captions** -> **Include Audio Effects**.

