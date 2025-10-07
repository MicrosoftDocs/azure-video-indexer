---
title: Customize a Language model in Azure AI Video Indexer
description: This article shows you how to customize a language model in Azure AI Video Indexer.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/06/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
---

# Customize a language model with Azure AI Video Indexer

Azure AI Video Indexer supports automatic speech recognition through integration with the Microsoft [Custom Speech Service](https://azure.microsoft.com/services/cognitive-services/custom-speech-service/). You can customize the language model by uploading adaptation text. This text comes from the domain whose vocabulary you'd like the engine to use to adapt. Once you train your model, the engine recognizes new words appearing in the adaptation text, assuming default pronunciation, and the language model learns new probable sequences of words. See the list of languages supported by Azure AI Video Indexer in [supported languages](language-support.md). 

For example, *Kubernetes* (in the context of Azure Kubernetes service), is a word that's highly specific. Since the word is new to Azure AI Video Indexer, it gets recognized as *communities*. Train the model to recognize it as *Kubernetes*. In other cases, the words exist, but the language model isn't expecting them to appear in a certain context. For example, *container service* isn't a two-word sequence that a nonspecialized language model would recognize as a specific set of words.

There are two ways to customize a language model:

- **Option 1**: Edit the transcript that Azure AI Video Indexer generated. By editing and correcting the transcript, you train a language model to provide improved results in the future.
- **Option 2**: Upload text files to train the language model. The file can contain a list of words as you want them to appear in the Azure AI Video Indexer transcript. Or, it can contain the relevant words included naturally in sentences and paragraphs. As better results are achieved with the latter approach, include full sentences or paragraphs related to your content in the upload file.
 
> [!IMPORTANT]
> Don't include the words or sentences as currently incorrectly transcribed (for example, *communities*) in the upload file as this inclusion negates the intended impact. 
> Only include the words as you want them to appear (for example, *Kubernetes*).

## Optimize your custom language model

Azure AI Video Indexer learns based on probabilities of word combinations, so to learn best:

* Give enough real examples of sentences as they would be spoken.
* Put only one sentence per line, not more. Otherwise the system  learns probabilities across sentences.
* It's okay to put one word as a sentence to boost the word against others, but the system learns best from full sentences.
* When introducing new words or acronyms, if possible, give as many examples of usage in a full sentence to give as much context as possible to the system.
* Try to put several adaptation options, and see how they work for you.
* Avoid repetition of the exact same sentence multiple times. It might create bias against the rest of the input.
* Avoid including uncommon symbols (~, # @ % &) because they get discarded. The sentences in which they appear also get discarded.
* Avoid putting too large inputs, such as hundreds of thousands of sentences, because doing so dilutes the effect of boosting.

## Prerequisites

- An Azure account
- An Azure AI Video Indexer account

## [Web portal](#tab/customizewebportal)

## Create a language model

1. Go to the [Azure AI Video Indexer](https://www.videoindexer.ai/) website and sign in.
1. To customize a model in your account, select the **Content model customization** button on the left of the page.
1. Select the **Language** tab. You see a list of supported languages.
1. Under the language that you want, select **Add model**.
1. Type in the name for the language model and press Enter. This step creates the model and gives the option to upload text files to the model.
1. To add a text file, select **Add file**. Your file explorer opens.
1. Navigate to and select the text file. You can add multiple text files to a language model. You can also add a text file by selecting the **...** button on the right side of the language model and selecting **Add file**.
1. When you're done uploading the text files, select the green **Train** option.

The training process can take a few minutes. When the training is done, **Trained** appears next to the model. You can preview, download, and delete the file from the model.

### Use a language model on a new video

To use your language model on a new video, complete one of the following actions:

1. Select **Upload** at the top of the page.
1. Drop your audio or video file or browse for your file.
1. Select a language model you created from the **Video source language** list.
1. Select the **Upload** option at the bottom of the page. Your new video gets indexed by using your language model.

### Using a language model to reindex

1. Sign in to the [Azure AI Video Indexer](https://www.videoindexer.ai/) home page.
1. Select the ellipsis (**...**) on the video and then select **Re-index**.
1. Select the **Video source language** list and select a language model that you created from the list.
1. Select **Re-index** and your video gets reindexed using your language model.

## Edit a language model

You can edit a language model by changing its name, adding files to it, and deleting files from it. If you add or delete files from the language model, you need to train the model again by selecting the green **Train** option.

### Rename the language model

You can change the name of the language model by selecting the ellipsis (**...**) on the right side of the language model and selecting **Rename**. Enter the new name.

### Add files

1. Select **Add file**. Your File Explorer opens.
1. Navigate to and select the text file. You can add multiple text files to a language model.

You can also add a text file by selecting the ellipsis (**...**) button on the right side of the language model and selecting **Add file**.

### Delete files

This action removes the file completely from the language model.

1. Select the ellipsis (**...**) button on the right side of the text file.
1. Select **Delete**. A new window pops up telling you that the deletion can't be undone. 
1. Select the **Delete** option in the new window.

## Delete a language model

This action removes the language model from your account. Any video that uses the deleted language model keeps the same index until you reindex the video. If you reindex the video, you can assign a new language model to the video. Otherwise, Azure AI Video Indexer uses its default model to reindex the video.

1. Select the ellipsis (**...**) button on the right side of the Language model.
1. Select **Delete**. A new window pops up telling you that the deletion can't be undone. 
1. Select the **Delete** option in the new window. 

## Customize language models by correcting transcripts

Azure AI Video Indexer customizes language models based on the actual corrections users make to the transcriptions of their videos. It captures all lines that you corrected in the transcription of your video and adds them to a text file called `From transcript edits`. These edits are used to retrain the language model that was used to index the video.

Edits that you make in the [widget's](video-indexer-embed-widgets.md) timeline are also included.

If you don't specify a language model when indexing this video, Azure AI Video Indexer stores all edits for this video in a default language model called `Account adaptations` within the detected language of the video.
    
If you make multiple edits to the same line, Azure AI Video Indexer uses only the last version of the corrected line for updating the language model.

> [!NOTE]
> Only textual corrections are used for the customization. Corrections that don't involve actual words (for example, punctuation marks or spaces) aren't included.

1. Select the video that you want to edit from your library. 
1. Select the **Timeline** tab.
1. Select the pencil icon to edit the transcript of your transcription.
1. You see transcript corrections appear in the **Language** tab of the Content model customization page. To look at the "From transcript edits" file for each of your Language models, select it to open it.

## [API](#tab/customizeapi)

## Create a language model

Make a [Create Language Model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Language-Model) API request to create a new custom language model for the specified account. You can upload files for the language model with this request. Alternatively, you can create the language model here and upload files for the model later by updating the language model.

You must upload files in the body by using FormData in addition to providing values for the required parameters. You can define the key pair for this task in two ways:

1. Key is the file name and value is the txt file.
1. Key is the file name and value is a URL to txt file.

> [!NOTE]
> You must still train the model with its enabled files for the model to learn the contents of its files.

### Example response

```json
{
    "id": "dfae5745-6f1d-4edd-b224-42e1ab57a891",
    "name": "TestModel",
    "language": "En-US",
    "state": "None",
    "languageModelId": "00000000-0000-0000-0000-000000000000",
    "files": [
    {
        "id": "25be7c0e-b6a6-4f48-b981-497e920a0bc9",
        "name": "hellofile",
        "enable": true,
        "creator": "John Doe",
        "creationTime": "2018-04-28T11:55:34.6733333"
    },
    {
        "id": "33025f5b-2354-485e-a50c-4e6b76345ca7",
        "name": "worldfile",
        "enable": true,
        "creator": "John Doe",
        "creationTime": "2018-04-28T11:55:34.86"
    }
    ]
}

```

## Train a language model

The [Train Language Model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Train-Language-Model) request trains a custom language model for the specified account with the contents of the uploaded and enabled files in the language model.

> [!NOTE]
> You must first create the language model and upload its files. You can upload files when creating the language model or by updating the language model.

### Example response

```json
{
    "id": "41464adf-e432-42b1-8e09-f52905d7e29d",
    "name": "TestModel",
    "language": "En-US",
    "state": "Waiting",
    "languageModelId": "531e5745-681d-4e1d-b124-12e5ab57a891",
    "files": [
    {
        "id": "84fcf1ac-1952-48f3-b372-18f768eedf83",
        "name": "RenamedFile",
        "enable": false,
        "creator": "John Doe",
        "creationTime": "2018-04-27T20:10:10.5233333"
    },
    {
        "id": "9ac35b4b-1381-49c4-9fe4-8234bfdd0f50",
        "name": "hellofile",
        "enable": true,
        "creator": "John Doe",
        "creationTime": "2018-04-27T20:10:10.68"
    }
    ]
}
```

The `id` is a unique ID used to distinguish between language models. However, `languageModelId` is used for [uploading a video to index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video) and [reindexing a video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Re-Index-Video) requests. Azure AI Video Indexer upload and reindex requests also refer to it as `linguisticModelId`.

## Delete a language model

Use the [Delete Language Model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Language-Model) API request to delete a custom language model from the specified account. Any video that uses the deleted language model keeps the same index until you reindex the video. If you reindex the video, you can assign a new language model to the video. Otherwise, Azure AI Video Indexer uses its default model to reindex the video.

### Example response

There's no returned content when the language model is deleted successfully.

## Update a language model

The [Update Language Model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Language-Model) request updates a custom language person model in the specified account.

> [!NOTE]
> Make sure you created the language model. Use this call to: enable or disable all files under the model, update the name of the language model, and upload files to add to the language model.

To upload files to add to the language model, you must upload files in the body using FormData. You must also provide values for the required parameters mentioned previously. To accomplish the task, there are two ways:

* Key is the file name and value is the txt file.
* Key is the file name and value is a URL to txt file.

### Example response

```json
{
    "id": "41464adf-e432-42b1-8e09-f52905d7e29d",
    "name": "TestModel",
    "language": "En-US",
    "state": "Waiting",
    "languageModelId": "531e5745-681d-4e1d-b124-12e5ab57a891",
    "files": [
    {
        "id": "84fcf1ac-1952-48f3-b372-18f768eedf83",
        "name": "RenamedFile",
        "enable": true,
        "creator": "John Doe",
        "creationTime": "2018-04-27T20:10:10.5233333"
    },
    {
        "id": "9ac35b4b-1381-49c4-9fe4-8234bfdd0f50",
        "name": "hellofile",
        "enable": true,
        "creator": "John Doe",
        "creationTime": "2018-04-27T20:10:10.68"
    }
    ]
}
```

To download the contents of the file, use the `id` of the files returned in the response.

## Update a file from a language model

The [Update Language Model File](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Language-Model-file) request updates the name and `enable` state of a file in a custom language model in the specified account.

### Example response

```json
{
  "id": "84fcf1ac-1952-48f3-b372-18f768eedf83",
  "name": "RenamedFile",
  "enable": false,
  "creator": "John Doe",
  "creationTime": "2018-04-27T20:10:10.5233333"
}
```

To download the contents of the file, use the `id` of the file returned in the response.

## Get a specific language model

Make a [Get Language Model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Language-Model) API request to return information on the specified language model in the specified account, such as language and the files that are in the language model.

### Example response

```json
{
    "id": "dfae5745-6f1d-4edd-b224-42e1ab57a891",
    "name": "TestModel",
    "language": "En-US",
    "state": "None",
    "languageModelId": "00000000-0000-0000-0000-000000000000",
    "files": [
    {
        "id": "25be7c0e-b6a6-4f48-b981-497e920a0bc9",
        "name": "hellofile",
        "enable": true,
        "creator": "John Doe",
        "creationTime": "2018-04-28T11:55:34.6733333"
    },
    {
        "id": "33025f5b-2354-485e-a50c-4e6b76345ca7",
        "name": "worldfile",
        "enable": true,
        "creator": "John Doe",
        "creationTime": "2018-04-28T11:55:34.86"
    }
    ]
}
```

To download the contents of the file, use the `id` of the file returned in the response.

## Get all the language models

Use a [Get Language Models](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Language-Models) API request to return all of the custom Azure AI Language models in the specified account in a list.

### Example response

```json
[
    {
        "id": "dfae5745-6f1d-4edd-b224-42e1ab57a891",
        "name": "TestModel",
        "language": "En-US",
        "state": "None",
        "languageModelId": "00000000-0000-0000-0000-000000000000",
        "files": [
        {
            "id": "25be7c0e-b6a6-4f48-b981-497e920a0bc9",
            "name": "hellofile",
            "enable": true,
            "creator": "John Doe",
            "creationTime": "2018-04-28T11:55:34.6733333"
        },
        {
            "id": "33025f5b-2354-485e-a50c-4e6b76345ca7",
            "name": "worldfile",
            "enable": true,
            "creator": "John Doe",
            "creationTime": "2018-04-28T11:55:34.86"
        }
        ]
    },
    {
        "id": "dfae5745-6f1d-4edd-b224-42e1ab57a892",
        "name": "AnotherTestModel",
        "language": "En-US",
        "state": "None",
        "languageModelId": "00000000-0000-0000-0000-000000000001",
        "files": []
    }
]
```

## Delete a file from a language model

The [Delete Language Model File](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Language-Model-File) request deletes the specified file from the specified Azure AI Language model in the specified account.

### Example response

There's no returned content when the file is deleted from the language model successfully.

## Get metadata on a file from a Azure AI Language model

The [Get Azure AI Language Model File Data](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Language-Model-File-Data) request returns the contents of and metadata on the specified file from the chosen Azure AI Language model in your account.

### Example response

```json
{
    "content": "hello\r\nworld",
    "id": "84fcf1ac-1952-48f3-b372-18f768eedf83",
    "name": "Hello",
    "enable": true,
    "creator": "John Doe",
    "creationTime": "2018-04-27T20:10:10.5233333"
}
```

> [!NOTE]
> The contents of this example file are the words "hello" and "world" in two separate lines.

## Download a file from a Azure AI Language model

The [Download Azure AI Language Model File Content](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Download-Language-Model-File-Content) request downloads a text file containing the contents of the specified file from the specified Azure AI Language model in the specified account. This text file matches the contents of the text file that you originally uploaded.

### Example response

The response is the download of a text file with the contents of the file in the JSON format.

---
