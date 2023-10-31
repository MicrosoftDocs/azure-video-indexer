---
title: Customize a Language model in Azure AI Video Indexer - Azure  
description: This article gives an overview of what is a Language model in Azure AI Video Indexer and how to customize it.
ms.topic: conceptual
ms.date: 11/23/2022
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Customize a Language model with Azure AI Video Indexer

[!INCLUDE [AMS AVI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

Azure AI Video Indexer supports automatic speech recognition through integration with the Microsoft [Custom Speech Service](https://azure.microsoft.com/services/cognitive-services/custom-speech-service/). You can customize the Language model by uploading adaptation text, namely text from the domain whose vocabulary you'd like the engine to adapt to. Once you train your model, new words appearing in the adaptation text will be recognized, assuming default pronunciation, and the Language model will learn new probable sequences of words. See the list of supported by Azure AI Video Indexer languages in [supported langues](language-support.md). 

Let's take a word that is highly specific, like *"Kubernetes"* (in the context of Azure Kubernetes service), as an example. Since the word is new to Azure AI Video Indexer, it's recognized as *"communities"*. You need to train the model to recognize it as *"Kubernetes"*. In other cases, the words exist, but the Language model isn't expecting them to appear in a certain context. For example, *"container service"* isn't a 2-word sequence that a nonspecialized Language model would recognize as a specific set of words.

There are two ways to customize a language model:

- **Option 1**: Edit the transcript that was generated by Azure AI Video Indexer. By editing and correcting the transcript, you're training a language model to provide improved results in the future.
- **Option 2**: Upload text file(s) to train the language model. The upload file can either contain a list of words as you would like them to appear in the Video Indexer transcript or the relevant words included naturally in sentences and paragraphs. As better results are achieved with the latter approach, it's recommended for the upload file to contain full sentences or paragraphs related to your content.
 
> [!Important]
> Do not include in the upload file the words or sentences as currently incorrectly transcribed (for example, *"communities"*) as this will negate the intended impact. 
> Only include the words as you would like them to appear (for example, *"Kubernetes"*).

You can use the Azure AI Video Indexer APIs or the website to create and edit custom Language models, as described in articles in the [Next steps](#next-steps) section of this article.

## Best practices for custom Language models

Azure AI Video Indexer learns based on probabilities of word combinations, so to learn best:

* Give enough real examples of sentences as they would be spoken.
* Put only one sentence per line, not more. Otherwise the system will learn probabilities across sentences.
* It's okay to put one word as a sentence to boost the word against others, but the system learns best from full sentences.
* When introducing new words or acronyms, if possible, give as many examples of usage in a full sentence to give as much context as possible to the system.
* Try to put several adaptation options, and see how they work for you.
* Avoid repetition of the exact same sentence multiple times. It may create bias against the rest of the input.
* Avoid including uncommon symbols (~, # @ % &) as they'll get discarded. The sentences in which they appear will also get discarded.
* Avoid putting too large inputs, such as hundreds of thousands of sentences, because doing so will dilute the effect of boosting.

## Next steps

[Customize Language model using APIs](customize-language-model-with-api.md)

[Customize Language model using the website](customize-language-model-with-website.md)