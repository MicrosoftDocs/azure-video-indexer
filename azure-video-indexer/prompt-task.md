---
title: Use Azure AI Video Indexer to create prompt content 
description: This article shows you how to use Azure AI Video Indexer to create prompt content. 
ms.topic: how-to
ms.date: 06/19/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Use Azure AI Video Indexer to create prompt content

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

This article shows you how to Use Azure AI Video Indexer to create prompt content.

## Prerequisites

- An [Azure AI Video Indexer account](/azure/azure-video-indexer/create-account?tabs=portal).

## Open web pages in your browser

It's easier to follow these instructions if you already have the needed web pages open. Copy and paste the following parameters to your favorite text editor. Here's a list to get you started:

- VI account ID:
- video file ID:
- access token:

1. Open the [Azure portal](https://portal.azure.com) in one tab or window, and sign in.
    1. Navigate to the Azure AI Video Indexer account page for the account ID.
    1. Navigate to the Azure OpenAI account page
        1. From the menu, select Model deployments, then select Manage deployments. The Azure OpenAI Studio opens. Copy the Deployment Name you want to use. 
1. Open the [Azure AI Video Indexer web portal](https://www.videoindexer.ai) in another tab or window and sign in.
    1. Navigate to the library page, choose a video, then right-click on it for the video file ID.
1. Open the [Azure AI Video Indexer API](https://api-portal.videoindexer.ai/) in another tab or window and sign in.

## Generate an access token

Generate an access token in the Azure portal:

1. Navigate to your Azure AI Video Indexer account.
1. From the menu, select **Management** then **Management API**.
1. From the **Permission** type dropdown, select **Contributor**.
1. From the **Scope** dropdown, select **Account**.
1. Select **Generate**. The access token is generated.
1. Copy the access token to your clipboard.

## Create prompt content

You should have all of the parameters needed to create a video summary ready to go in your text editor.

1. Got to the [Create Promot Content](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Prompt-Content) page in the API, or on the Azure AI Video Indexer API page, search for *prompt*.
1. Select the **Try it** button next to *Create Prompt Content*. The API parameters pane opens.
1. Select the location from the **location** dropdown list.
1. Copy and paste the VI account ID in the **accountId** field.
1. Copy the video file ID and paste it into the **videoId** field.
1. Choose the language model you want to use, *LLama2*, *Phi2*, *GPT3_5Turbo*, or *GPT4* from the **modelName** dropdown list.
1. Choose the prompt style, *Full* or *Summarized*, from the **style** dropdown list.
1. Paste the access token on your clipboard into the **accessToken** field.
1. Select **Send**.

If there aren't any issues with the request, the response shows *HTTP/1.1 202 Accepted*.

> [!NOTE]
> For summary related prompts, we recommend selecting the Summarized style. For search tasks,including answering specific questions about the video, we recommend using the Search style. 

### Check job status

It takes a few minutes for the prompt job to complete. If you would like to check on the job status, you can use the **Job Status** request by using all of the same parameters for the Create Prompt Content request. Find the Job Status request by using the search field as you did before.

## Get prompt content

1. Select **Get Prompt Content**.
1. Enter the account ID, the video ID, the summary ID, and the access token into the appropriate fields.
1. Select **Send**.

The prompt content will be in the response.

### Sample response

```json

HTTP/1.1 200 OK

cache-control: max-age=18000, private
content-type: application/json; charset=utf-8
expires: Tue, 07 May 2024 04:57:23 GMT

{
    "partition": null,
    "name": "satya_nadella_build_keynote_2018",
    "sections": [{
        "id": 0,
        "start": "0:00:00.050033",
        "end": "0:02:06.700033",
        "content": "[Video title] satya_nadella_build_keynote_2018\n[Known people] Satya Nadella\n[Visual labels] indoor, 
        audience, clothing, person, presentation, human face, man, wall, footwear, glasses, auditorium, microphone\n[OCR] Satya, 
        Nadella, 0:01 / 4:59, Nadel, 8-8, Microsoft, oft, Satya Nadella, Chief Executive Officer, Micr, Microsoft Build, 
        Opportunity & Responsibility, Mi, Micros, croso\n[Transcript] Please welcome Satya Nadella.\nGood morning and welcome to 
        Bill 2018.\nWelcome to Seattle.\nIt's fantastic to see you all back here.\nYou know, this morning I got up and I was 
        reading the news and I hear Bill Gates is talking about stock and he's talking about the Apple stock.\nAnd I said, wow, in 
        the 30 years that at least I've known Bill, I've never seen him talk about stock.\nBut today must be a new day for sure 
        when you hear Bill talk about Apple stock.\nSo that's the new Microsoft for you.\nYou know last year we talked about 
        opportunity and responsibility and both those topics have been so far amplified.\nIt's unimaginable.\nIn fact, for the 
        first time here, last year is when I started talking about the Intelligent Edge, and 12 months after it's everywhere.\nIn 
        fact, at this conference it's going to be something that we will unpack in great detail.\nThe platform advances are pretty 
        amazing, but most importantly, it's the developers who are pushing these platform advances.\nSo to see the Intelligent 
        edge go from some sort of a conceptual frame to this real thing that's shaping the cloud is stunning."
    }, {
        "id": 1,
        "start": "0:02:06.700033",
        "end": "0:04:38.916667",
        "content": "[Video title] satya_nadella_build_keynote_2018\n[Known people] Satya Nadella\n[Detected objects] car\n[Visual 
        labels] indoor, audience, clothing, person, presentation, human face, man, footwear, glasses, outdoor\n[OCR] Microsoft, 
        Opportunity & Responsibility, ponsibility, ros, SPEA., 4:03 / 4:59\n[Transcript] Last year, we also talked about this 
        notion of responsibility and that none of us wanted to see a future that Huxley imagined or Orville imagined, and that's 
        now become a mainstream topic of discussion.\nAnd so I was thinking about the historical parallels, where there was this 
        much change, this kind of opportunity, this kind of tumultuous discussion.\nAnd I was reminded of a book that I read maybe 
        three years ago by Robert Gordon, The Rise and Fall of American Productivity or American Growth.\nAnd in there he in fact 
        talks about the industrial revolution and even contrasts it with the digital revolution.\nHe gives Peace C credit for the 
        last time digital technology showed up in our productivity stats, which is nice.\nBut in general he sort of talks about 
        what an amazing revolution the industrial revolution was in terms of its broad sectoral impact and productivity and growth.
        \nThis is a picture of New York City probably 1905, I'm told.\nFlat iron building and what you see is horse carriages.    
        \nAnd if you go to the next picture, this is 20 years after and you see all the artefacts of the industrial revolution and 
        it's diffusion.\nYou see the automobiles.\nThese buildings now are beginning to have sewage systems, drainage, air 
        conditioning is coming, Radios, telephones, high rises.\nIt's pretty amazing."
    }]
}

```

## Use keyframes for video with very little audio

Prompt content API supports visual language models. When selecting the GPT-4V model, you can include keyframes as part of the prompt provided to the model. This feature is recommended for videos with limited insights available is or when there is no transcript in the video.

1. Create and send a Prompt Content request.
1. As described above, textual content for the prompt is in the JSON response.
1. Each string in the "frames" part of the JSON response is the ID of the keyframe. 
1. Use the ID to download the keyframe artifact using the [Get Video Artifact Download Url](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Artifact-Download-Url) request. (You can also download artifacts from the VI web portal.)
1. Once you have both the textual content and the keyframe artifacts, you can combine them as prompts for an AI model of your choice. 
