---
title: Audio effects detection
services: azure-video-indexer
ms.service: azure-video-indexer
ms.topic: include
ms.date: 07/25/2024
ms.author: inhenkel
---

## Audio effects detection

[!INCLUDE [Audio effects detection description](audio-effects-detection-description.md)]

### Audio effects use cases

- Improve accessibility by offering more context for a hearing- impaired audience by transcription of nonspeech effects. 
- Improving efficiency when creating raw data for content creators. Important moments in promos and trailers such as laughter, crowd reactions, gunshots, or explosions can be identified, for example,  in Media and Entertainment. 
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

[!INCLUDE [get insights with the web portal](get-insights-web-portal.md)]
[!INCLUDE [get insights with the API](get-insights-api.md)]

### [Example response](#tab/audioeffectsresponse)

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

### [Components](#tab/audioeffectscomponents)

During the audio effects detection procedure, audio in a media file is processed, as follows:

|Component|Definition|
|---|---|
|Source file |	The user uploads the source file for indexing. |
|Segmentation|  	The audio is analyzed, nonspeech audio is identified and then split into short overlapping internals. |
|Classification| 	An AI process analyzes each segment and classifies its contents into event categories such as crowd reaction or laughter. A probability list is then created for each event category according to department-specific rules. |
|Confidence level|	The estimated confidence level of each audio effect is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|

### [Transparency notes](#tab/audioeffectstransnote)

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

- Avoid use of short or low-quality audio, audio effects detection provides probabilistic and partial data on detected nonspeech audio events. For accuracy, audio effects detection requires at least 2 seconds of clear nonspeech audio. Voice commands or singing aren't supported.   
- Avoid use of audio with loud background music or music with repetitive and/or linearly scanned frequency, audio effects detection is designed for nonspeech audio only and therefore can't classify events in loud music. Music with repetitive and/or linearly scanned frequency many be incorrectly classified as an alarm or siren. 
- Carefully consider the methods of usage in law enforcement and similar institutions. To promote more accurate probabilistic data, ensure that: 

    - Audio effects can be detected in nonspeech segments only. 
    - The duration of a nonspeech section should be at least 2 seconds. 
    - Low quality audio might affect the detection results.  
    - Events in loud background music aren't classified.  
    - Music with repetitive and/or linearly scanned frequency might be incorrectly classified as an alarm or siren. 
    - Knocking on a door or slamming a door might be labeled as a gunshot or explosion. 
    - Prolonged shouting or sounds of physical human effort might be incorrectly classified. 
    - A group of people laughing might be classified as both laughter and crowd. 
    - Natural and nonsynthetic gunshot and explosions sounds are supported.

### [Sample code](#tab/audioeffectssamplecode)

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
> - `Silence` event type won't be added to the closed captions.
> - Minimum timer duration to show an event is 700 milliseconds.

## Add audio effects to closed caption files

### API
You can add audio effects to closed captions files with the [Get video captions](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Captions) request and by choosing *true* for the `includeAudioEffects` parameter. 

> [!NOTE]
> When using [update transcript](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Video-Transcript) from closed caption files or [update custom language model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Language-Model) from closed caption files, audio effects included in those files are ignored.

### Web portal
You can also use the web portal by selecting **Download** -> **Closed Captions** -> **Include Audio Effects**.
