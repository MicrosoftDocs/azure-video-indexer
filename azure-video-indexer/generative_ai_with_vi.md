---
title: Generative AI with Azure AI Video Indexer (VI)
description: This article discusses the use of generative AI with Azure AI Video Indexer.
author: IngridAtMicrosoft
ms.author: inhenkel
ms.collection: ce-skilling-ai-copilot
ms.date: 10/09/2024
ms.service: azure-video-indexer
ms.topic: how-to
---

# Generative AI with Azure AI Video Indexer (VI)

This article discusses the use of generative AI with Azure AI Video Indexer.

## Other AI models with VI

Azure Video Indexer is capable of connecting to other AI models offered by Azure OpenAI. You can also [bring your own model](azure-video-indexer-enabled-by-arc-bring-your-own-model-overview.md). 

You can use VI insights to create prompts for LLMs, or you can create a question and answer interface to find the exact video content you are looking for.

See the following articles to learn more about VI and generative AI.

- [Textual summarization with Azure OpenAI](text-summarization-overview.md)
- [Use Azure OpenAI textual summarization](text-summarization-task.md)
- [Prompt content](prompt-overview.md)
- [Use Azure AI Video Indexer to create prompt content](prompt-task.md)
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
