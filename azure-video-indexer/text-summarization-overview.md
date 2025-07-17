---
title: Textual Video Summary with Azure OpenAI
description: Learn how Azure AI Video Indexer generates concise, customizable summaries of video content to save time and boost productivity.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 05/28/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: concept-article
#customer intent: As a video content manager, I want to quickly summarize long videos so that I can efficiently review content without watching the entire video.
---

# Textual summarization with Azure AI Video Indexer

This article is an overview of textual summarization with Azure AI Video Indexer.

## What is textual video summarization?

Azure AI Video Indexer provides a brief summary of what a video is about without having to watch the entire video. It saves you time by digesting long videos and giving you the gist of a video in a short format. It’s like having a friend who watches all the episodes of a show and then catches you up on the plot in just a few minutes.

The system is intended to be a supportive tool that enhances productivity and learning by distilling lengthy videos into concise, digestible summaries.

It uses summarization algorithms to identify the most relevant insights for the video, and scores insights based on their importance and relevance to the overall theme. A user-friendly interface allows you to input videos and customize the type of summary you need.

The system provides options for feedback, enabling it to learn and improve over time based on user interactions.

> [!IMPORTANT]
> The system isn't intended to replace complete viewing, especially for content where details and nuances are **critical for making responsible decisions**. Also, it isn't designed to summarize highly sensitive or confidential videos where context and privacy are paramount.

## Textual summarization with keyframes

Textual video summarization with keyframes uses keyframes from the video to generate a more comprehensive summary. This feature is useful when there's limited audio content, such as transcription, or when a more holistic summary is desired.

## Use cases

The intended uses of the AI-based video summarization system are to provide users with a quick and efficient way to understand the content of longer videos without having to watch them in their entirety. Here are some specific intended uses:

- **Education** - Students and educators can use the system to summarize lectures, seminars, or educational content, making study materials more accessible and easier to review and to focus on key learning points or definitions.
- **Corporate** - Professionals can generate summaries of meetings, presentations, or training sessions that highlight decisions, action items, or key points from meetings. It provides quick recaps and ensures important information isn't missed.
- **Media** - Journalists and the general public can use the system to get the essence of news reports, documentaries, or interviews, saving time while staying informed. It condenses news or documentaries into bite-sized pieces without losing the narrative. 
- **Output formats** - You can set summaries to use different styles of language: neutral, casual, or formal. You can also set the length of a summary to short or long.

## Textual summarization on VI enabled by Arc

If you're using the VI enabled by Arc extension, you can generate a summary from the video page in the web portal and use the same functionality such as customizations. However, you can't change the model deployment. Instead, every new extension created includes a local [Phi-3-mini-4k-instruct](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct/tree/main) model developed by Microsoft. There's no charge for requests to the model.

## Transparency notes

For more information about specifications and limitations, see the [Textual summarization section of the transparency notes](/legal/azure-video-indexer/transparency-note#text-summarization).

## Try textual video summarization
[Try using textual video summarization](text-summarization-task.md).
