---
title: Textual Summarization with Azure AI Video Indexer
description: Learn how Azure AI Video Indexer generates concise, customizable summaries of video content to save time and boost productivity.
author: cwatson-cat
ms.author: cwatson
ms.date: 07/14/2026
ms.service: azure-video-indexer
ms.topic: concept-article
appliesto:
  - Azure AI Video Indexer enabled by Azure Arc
  - Cloud-based Azure AI Video Indexer
ai-usage: ai-assisted
#customer intent: As a video content manager, I want to quickly summarize long videos so that I can efficiently review content without watching the entire video.
---

# Textual summarization with Azure AI Video Indexer

Textual summarization is a feature that automatically generates concise, customizable summaries of video content. You can quickly understand key information without watching the entire video. By turning long videos into digestible insights, it saves you time and enhances your ability to review content efficiently. Whether you're an educator, corporate professional, or content creator, this feature helps you.

In this article, you learn how textual summarization works, explore practical applications across different industries, and discover how to customize summaries to match your specific needs.

## What is textual video summarization?

Think of textual summarization like having a friend watch all the episodes of a show and then catch you up on the plot in just a few minutes. Behind the scenes, Azure AI Video Indexer uses summarization algorithms to identify the most relevant insights for the video and scores them based on their importance and relevance to the overall theme.

A user-friendly interface lets you input videos and customize the type of summary you need. The system also provides options for feedback, enabling it to learn and improve over time based on user interactions.

> [!IMPORTANT]
> The system isn't intended to replace complete viewing, especially for content where details and nuances are **critical for making responsible decisions**. Also, it isn't designed to summarize highly sensitive or confidential videos where context and privacy are paramount.

## Textual summarization with keyframes

Textual summarization can work with two inputs: audio/transcription or visual keyframes (key moments captured from the video). When summarizing videos with limited audio content or transcription, keyframes provide visual context that ensures the summary captures essential visual information. This approach generates a more holistic summary by combining both visual and textual signals. Use keyframes-based summarization when the visual narrative is as important as the audio narrative.

## Use cases

Here are some specific ways you can use Azure AI Video Indexer textual summarization:

- **Education** - Summarize lectures, seminars, and educational content to make study materials more accessible and easier to review. Students can focus on key learning points and definitions, or ask specific questions about the material.
- **Corporate** - Generate summaries of meetings, presentations, and training sessions that highlight decisions, action items, and key points. Get quick recaps and ensure important information isn't missed.
- **Media** - Get the essence of news reports, documentaries, and interviews quickly. Condense content into bite-sized pieces while preserving the narrative for journalists and general audiences.
- **Output formats** - Customize summaries with different language styles (neutral, casual, or formal) and lengths (short or long).

## Textual summarization on VI enabled by Arc

If you're using the Azure AI Video Indexer enabled by Arc extension, you can generate a summary from the video page in the web portal and use the same functionality such as customizations. However, you can't change the model deployment. Instead, every new extension created includes a local [Phi-3-mini-4k-instruct](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct/tree/main) model developed by Microsoft. There's no charge for requests to the model.

## Transparency notes

For more information about specifications and limitations, see the [Textual summarization section of the transparency notes](/legal/azure-video-indexer/transparency-note#text-summarization).

## Related content

- [Try using text summarization task](text-summarization-task.md)
- [Upload and index media](upload-index-media.md)
- [Azure AI Video Indexer overview](video-indexer-overview.md)
