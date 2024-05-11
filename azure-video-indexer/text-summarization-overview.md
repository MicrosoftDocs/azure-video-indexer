---
title: Azure OpenAI text summarization with Azure AI Video Indexer overview
description: This article is an overview of Azure OpenAI text summarization with Azure AI Video Indexer. 
ms.topic: overview
ms.date: 05/5/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Azure OpenAI text summarization with Azure AI Video Indexer overview

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

This article is an overview of Azure OpenAI text summarization with Azure AI Video Indexer.

## What is textual video summarization with Azure AI Video Indexer? 

Azure AI Video Indexer provides a brief summary of what a video is about without having to watch the entire video. It's designed to save you time by digesting long videos and giving you the gist in a much shorter format. It’s like having a friend who watches all the episodes of a show and then catches you up on the plot in just a few minutes. 

The system is intended to be a supportive tool that enhances productivity and learning by distilling lengthy videos into concise, digestible summaries.

It uses summarization algorithms to identify the most relevant insights for the video. It involves scoring insights based on their importance and relevance to the overall theme. A user-friendly interface allows you to input videos and customize the type of summary you need.

The system provides options for feedback, enabling it to learn and improve over time based on user interactions.

> [!IMPORTANT]
> The system isn't intended to replace complete viewing, especially for content where details and nuances are **critical for making responsible decisions**. Also, it isn't designed for summarizing highly sensitive or confidential videos where context and privacy are paramount.

## Use cases 

The intended uses of the AI-based video summarization system are to provide users with a quick and efficient way to understand the content of longer videos without having to watch them in their entirety. Here are some specific intended uses:

### Educational 

Students and educators can use the system to summarize lectures, seminars, or educational content, making study materials more accessible and easier to review and to focus on key learning points or definitions.

### Corporate 

Professionals can generate summaries of meetings, presentations, or training sessions that highlight decisions, action items, or key points from meetings. It provides quick recaps and ensures important information isn't missed.

### Media
 
Journalists and the general public can use the system to get the essence of news reports, documentaries, or interviews, saving time while staying informed. It condenses news or documentaries into bite-sized pieces without losing the narrative. 

## Output formats

You can set summaries to use different styles of language: neutral, casual, or formal. You can also set the length of a summary to short or long.

## Limitations

### Non-English languages
The text summarization is optimized for the English language. However, it's compatible with all languages supported by the specific GenAI model being used, that is, GPT3.5 Turbo or GPT4.0. So, when applied to non-English languages, the accuracy and quality of the summaries might vary. To mitigate this limitation, be extra careful and verify the generated summaries for accuracy and completeness.  

### Videos with multiple languages 
If a video contains speech in multiple languages, the text summarization might struggle to accurately recognize all the languages featured in the video. Be aware of this potential limitation when utilizing the Textual Video Summarization feature for multilingual videos. 

### Highly specialized or technical videos 
Video summary AI models are typically trained on a wide variety of videos, including news, movies, and other general content. If the video is highly specialized or technical, the model might not be able to accurately extract the summary of the video.  

### Videos with poor audio quality or Optical Character Recognition (OCR)
Text summarization AI models also rely on audio (among other insights) to extract the summary from the video or on OCR to extract the text appearing on screen. If the audio quality is poor and there's no OCR identified, the model might not be able to accurately extract the summary from the video.  

### Videos with low lighting or fast motion
Videos that are shot in low lighting or have fast motion might be difficult for the model to process, resulting in poor performance.

### Videos with uncommon accents or dialects
AI models are typically trained on a wide variety of speech, including different accents and dialects. However, if the video contains speech with an accent or dialect that isn't well represented in the training data, the model might struggle to accurately extract the transcript from the video.

### Videos containing harmful content
Videos containing harmful or sensitive content may result in a partial summary as the parts containing sensitive or harmful content (including adjustment scenes) might be excluded.

## Additional information

For more information about the way text summarization is used, see the [Transparency notes](/legal/azure-video-indexer/transparency-note#text-summarization) for text summarization.

## Limitations

Fine tuned models are not supported.

## Try textual video summarization
[Try using textual video summarization](text-summarization-task.md).