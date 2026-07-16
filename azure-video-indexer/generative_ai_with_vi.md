---
title: Generative AI with Azure AI Video Indexer (VI)
description: This article discusses the use of generative AI with Azure AI Video Indexer.
author: cwatson-cat
ms.author: cwatson
ms.date: 07/14/2026
ms.service: azure-video-indexer
ms.topic: concept-article
appliesto:
  - Azure AI Video Indexer enabled by Azure Arc
  - Cloud-based Azure AI Video Indexer
ai-usage: ai-assisted
#customer intent: As a developer, I want to understand how to integrate generative AI models with Azure AI Video Indexer so that I can summarize videos, generate insights, and ask questions about video content.
---

# Generative AI with Azure AI Video Indexer

Azure AI Video Indexer can connect to various generative AI models and services to enable advanced capabilities like video summarization, question answering, and custom insights. In this article, you learn about supported models and explore the main ways to add AI capabilities to your Azure AI Video Indexer workflows.

## Connect Video Indexer to generative AI models

Azure AI Video Indexer can connect to other AI models offered by Azure OpenAI. You can also [bring your own model](azure-video-indexer-enabled-by-arc-bring-your-own-model-overview.md). 

You can use Azure AI Video Indexer insights to create prompts for large language models (LLMs), or you can create a question and answer interface to find the exact video content you're looking for.

To learn more about Azure AI Video Indexer and generative AI, see the following articles:

- [Textual summarization with Azure OpenAI](text-summarization-overview.md)
- [Use Azure OpenAI textual summarization](text-summarization-task.md)
- [Prompt content](prompt-overview.md)
- [Bring Your Own (BYO) model](bring-your-own-model-overview.md)
- [Bring Your Own model samples](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/BringYourOwn-Samples)

## Supported models

Azure AI Video Indexer supports the following models.

### Cloud

- Llama 2
- Phi 2
- GPT3-5 Turbo
- GPT4

### VI enabled by Arc

- Phi 3
