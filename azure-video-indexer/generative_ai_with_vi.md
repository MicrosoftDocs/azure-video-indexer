---
title: Generative AI with Azure AI Video Indexer
description: This article discusses the use of generative AI with Azure AI Video Indexer.
ms.topic: how-to
ms.date: 06/18/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Generative AI with Azure AI Video Indexer

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

This article discusses the use of generative AI with Azure AI Video Indexer.

## Other AI models with VI

Azure Video Indexer is capable of connecting to other AI models offered by Azure OpenAI. If using VI on an Edge device, you can also [bring your own model](azure-video-indexer-enabled-by-arc-bring-your-own-model-overview.md). 

You can use VI insights to create prompts for LLMs, or you can create a question and answer interface to find the exact video content you are looking for.

## Supported models

Azure AI Video Indexer supports the following models.

### Cloud
- Llama 2
- Phi 2
- GPT3-5 Turbo
- GPT4

### Edge
- Phi 3

## Related content

- [Text summarization with Azure OpenAI](text-summarization-overview.md)
- [Use Azure OpenAI text summarization](text-summarization-task.md)
- [Prompt content](prompt-overview.md)
- [Use Azure AI Video Indexer to create prompt content](prompt-task.md)
- [Bring Your Own Model](azure-video-indexer-bring-your-own-model-overview.md)
- [Bring Your Own Model sample](https://github.com/Azure-Samples/azure-video-indexer-samples/tree/master/BringYourOwn-Samples)
