---
title:  Azure AI Video Indexer with LLM prompts  
description: Azure AI Video Indexer integrates with Large Language Models (LLMs). LLMs are natural language AI models that you can use to ask questions about video content and much more. Extract Azure AI Video Indexer’s insights into a prompt ready format that can be easily used with LLMs. There's no need to reindex videos to create the prompt-ready format of the videos.
ms.topic: conceptual
ms.date: 1/31/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Azure AI Video Indexer with LLM prompts

## Overview

Azure AI Video Indexer integrates with Large Language Models (LLMs). LLMs are natural language AI models that you can use to ask questions about video content and much more. Extract Azure AI Video Indexer’s insights into a prompt ready format that can be easily used with LLMs. There's no need to reindex videos to create the prompt-ready format of the videos.

## Use Cases

**Generate a Video Summarization:** You can ask the LLM model to generate summaries of whole videos or video segments. Those segments can be combined to create several types of summaries like an informative summary, a teaser or other summary depending on your needs.

**Searchability:** By converting video content into a text-based, prompt-ready format, you can perform detailed, natural language searches within your video content. This can significantly improve discoverability within large video libraries based on specific queries.

**Content Creation**: You can query your video library for specific moments in your videos associated with certain emotions or events. For example, you can retrieve ‘funny’ or ‘sad’ moments from a video series and use that to create a promo or highlight. Similarly, you can retrieve moments related to specific events of interest such as “past earthquakes during the last decade.”

**Educational Purposes**: Create summaries from lecture videos to make it easier for students to review and understand the material. Students can also ask specific questions related to the lecture material. You can refer to the exact part of the video where the article is discussed making the learning experience more efficient.

**Interactive Experiences**: You can create interactive experiences, such as video-based chatbots or virtual assistants, that can answer user queries based on the content of the video.

## How it works

For the output to be prompt-ready, the video is split into coherent sections that fit both the essence of the video and the prompt size. The sections are divided based on Azure AI Video Indexer Scene Segmentation and other insights. The results of the prompt content are consolidated and generated per segment separately. For example:

### Insights

The following table contains the insights used for prompt generation.

| **VI Insight**                        | **Tag and format** |
| :------------------------------------ | :------------------ |
|  Video title                          |  [Video title] \<video title\> |
|  Object detection                     |  [Detected objects] \<object 1\>, \<object 2\>, ... |
|  Labels                               |  [Visual labels] \<label 1\>, \<label 2\>, ... |
|  OCR                                  |  [OCR] \<ocr cluster1\> \<ocr cluster2\> ...   |
|  Transcript and speakers              | [Transcript] \<speaker name\>: \<transcript lines\>\\n\<speaker name\>: \<transcript lines\>\\n  ... |
|  Faces                                |  [Known people] \<face 1\>, \<face 2\>, ... |
|  Audio effects (AED)                  |  [Audio effects] \< effect 1\>, \<effect 2\>, ... |
|  Segment’s position within the video  |  [Tags] [Beginning, Middle, End, Rolling credits] |

## Create Prompt content for a video

Use the Prompt Content API on your indexed video in order to get Prompt-Ready format per each segment.

> [!Note]
> The prompt content insights are subjected to the specific preset being used to index the video.

- To generate the Prompt Content API, use the [POST Create Prompt Content](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Prompt-Content) request.
- To view the prompt content, use the [Get PromptContent](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-PromptContent) request.

### Example request

Use your AVI account ID and the video ID.

```
POST https://api.videoindexer.ai/trial/Accounts/{accountId}/Videos/{videoId}/PromptContent

```

### Example response

```REST
index
{
  "algoVersion": "2.0.0",
  "schemaVersion": "0.0.1",
  "partition": null,
  "name": "10_best_dressed_grammy",
  "sections": [
    {
      "id": 0,
      "start": "0:00:00",
      "end": "0:00:40.915875",
      "content": "[Video title] 10_best_dressed_grammy\n[Detected objects] necktie\n[Visual labels] human face, clothing, person, woman, suit, wedding dress, dress, indoor, wall, carpet, rug, fashion, lady, long hair, fashion accessory, fashion design\n[OCR] TROPHy, LIFE, SPECIAL, EDITION, news FEED, BY

 CLEVVER, CLEVVER, @NazPerez, BEST DRESSED CELEBS AT 2018 GRAMMYS\n[Transcript] Check out the 10 best dressed celebs from the 2018 Grammy Awards and don't forget to subscribe to our channel to get all the latest celebrity updates.\nFrom white roses to white hot looks, this year's Grammy Awards was a feast of fashion thanks to so many celebs bringing their A game to the show.\nSo let's kick off this list of the best dress from the red carpet, starting with Lady Gaga.\nGaga looked like a gothic Princess in her dramatic all black ball gown.\nThe Armani Preve dress featured A Lacy bodysuit and billowing black skirt with a huge train.\nAga's black heeled boots were also some of the highest we've ever seen, like ever, but we wouldn't expect anything less from Mama Monster.\nAnother look we love from the carpet was Anna Kendrick's sexy suit by Belmont."
    },
    {
      "id": 1,
      "start": "0:00:40.915875",
      "end": "0:01:17.202125",
      "content": "[Video title] 10_best_dressed_grammy\n[Detected objects] remote\n[Visual labels] human face, clothing, person, dress, carpet, rug, fashion, lady, furniture, female person, fashion model, model, haute couture, smile\n[OCR] TROPHy, LIFE, news FEED, BEST DRESSED CELEBS AT 2018 GRAMMYS, D CELEBS AT 2018 GRAMMYS, BEST DRESSED\n[Transcript] Anna gave the structured look a sexy feminine touch by wearing a Lacy strapless top underneath and some pale pink stilettos.\nHer suit may have said business, but her relaxed WAVY hairstyle said I came to get down.\nNext on our list is the literally red hot Camila Cabello.\nCamila was all glitzing glam in her strapless Vivian Westwood gown.\nThat humped her curves perfectly.\nCamila opted to wear her hair up and accessorized with some serious bling, but it's that plunging neckline that has this unable to look away.\nAnother look we loved came courtesy of Miley Cyrus, who absolutely slayed in this black velvet bodysuit.\nMiley looked beyond chic, from her classic Hollywood hairstyle to her glitter heels."
    },
}
```

## Limitations

The prompt feature is optimized for videos that contain as many insights as possible.
