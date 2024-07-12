---
title: Customize a speech model in Azure AI Video Indexer  
description: This article gives an overview of what is a speech model in Azure AI Video Indexer. 
ms.topic: conceptual
ms.date: 07/11/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Customize a speech model

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

[!INCLUDE [speech model](./includes/speech-model-note.md)]

Through Azure AI Video Indexer integration with [Azure AI Speech services](/azure/ai-services/speech-service/captioning-concepts), a Universal Language Model is utilized as a base model that is trained with Microsoft-owned data and reflects commonly used spoken language. The base model is pretrained with dialects and phonetics representing various common domains. The base model works well in most speech recognition scenarios. 

However, sometimes the base model’s transcription doesn't accurately handle some content. In these situations, a customized speech model can be used to improve recognition of domain-specific vocabulary or pronunciation that is specific to your content by providing text data to train the model. Through the process of creating and adapting speech customization models, your content can be properly transcribed. There's no additional charge for using Video Indexers speech customization. 

## When to use a customized speech model?  

If your content contains industry specific terminology or when reviewing Video Indexer transcription results you notice inaccuracies, you can create and train a custom speech model to recognize the terms and improve the transcription quality. It may only be worthwhile to create a custom model if the relevant words and names are expected to appear repeatedly in the content you plan to index. Training a model is sometimes an iterative process and you might find that after the initial training, results could still use improvement and would benefit from additional training, see [How to Improve your custom model](#how-to-improve-your-custom-models) section for guidance.  

However, if you notice a few words or names transcribed incorrectly in the transcript, a custom speech model might not be needed, especially if the words or names aren’t expected to be commonly used in content you plan on indexing in the future. You can just edit and correct the transcript in the Video Indexer website (see [View and update transcriptions in Azure AI Video Indexer website](edit-transcript-lines-portal.md)) and don’t have to address it through a custom speech model.  

For a list of languages that support custom models and pronunciation, see the Customization and Pronunciation columns of the language support table in [Language support in Azure AI Video Indexer](language-support.md).

## Train datasets 

When indexing a video, you can use a customized speech model to improve the transcription. Models are trained by loading them with [datasets](/azure/ai-services/speech-service/how-to-custom-speech-test-and-train) that can include plain text data and pronunciation data.   

Text used to test and train a custom model should include samples from a diverse set of content and scenarios that you want your model to recognize. Consider the following factors when creating and training your datasets: 

- Include text that covers the kinds of verbal statements that your users make when they're interacting with your model. For example, if your content is primarily related to a sport, train the model with content containing terminology and subject matter related to the sport. 
- Include all speech variances that you want your model to recognize. Many factors can vary speech, including accents, dialects, and language-mixing. 
- Only include data that is relevant to content you're planning to transcribe. Including other data can harm recognition quality overall. 

### Dataset types 

There are two dataset types that you can use for customization. To help determine which dataset to use to address your problems, refer to the following table: 

|Use case|Data type|
|---|---|
|Improve recognition accuracy on industry-specific vocabulary and grammar, such as medical terminology or IT jargon. |Plain text|  
|Define the phonetic and displayed form of a word or term that has nonstandard pronunciation, such as product names or acronyms. |Pronunciation data  |

### Plain-text data for training 

A dataset including plain text sentences of related text can be used to improve the recognition of domain-specific words and phrases. Related text sentences can reduce substitution errors related to misrecognition of common words and domain-specific words by showing them in context. Domain-specific words can be uncommon or made-up words, but their pronunciation must be straightforward to be recognized. 

### Best practices for plain text datasets 

- Provide domain-related sentences in a single text file. Instead of using full sentences, you can upload a list of words. However, while this adds them to the vocabulary, it doesn't teach the system how the words are ordinarily used. By providing full or partial utterances (sentences or phrases of things that users are likely to say), the language model can learn the new words and how they're used. The custom language model is good not only for adding new words to the system, but also for adjusting the likelihood of known words for your application. Providing full utterances helps the system learn better. 
- Use text data that’s close to the expected spoken utterances. Utterances don't need to be complete or grammatically correct, but they must accurately reflect the spoken input that you expect the model to recognize.  
- Try to have each sentence or keyword on a separate line.  
- To increase the weight of a term such as product names, add several sentences that include the term.  
- For common phrases that are used in your content, providing many examples is useful because it tells the system to listen for these terms.  
- Avoid including uncommon symbols (~, # @ % &) as get discarded. The sentences in which they appear also get discarded.   
- Avoid putting too large inputs, such as hundreds of thousands of sentences, because doing so dilutes the effect of boosting. 

Use this table to ensure that your plain text dataset file is formatted correctly: 

|Property|Value|
|---|---| 
|Text encoding |UTF-8 BOM| 
|Number of utterances per line |1 |
|Maximum file size |200 MB |

Try to follow these guidelines in your plain text files: 

- Avoid repeating characters, words, or groups of words more than three times, such as "yeah yeah yeah yeah" as the service might drop lines with too many repetitions. 
- Don't use special characters or UTF-8 characters above U+00A1. 
- URIs is rejected. 
- For some languages such as Japanese or Korean, importing large amounts of text data can take a long time or can time out. Consider dividing the dataset into multiple text files with up to 20,000 lines in each. 

## Pronunciation data for training 

You can add to your custom speech model a custom pronunciation dataset to improve recognition of mispronounced words, phrases, or names.  

Pronunciation datasets need to include the spoken form of a word or phrase as well as the recognized displayed form. The spoken form is the phonetic sequence spelled out, such as “Triple A”. It can be composed of letters, words, syllables, or a combination of all three.  The recognized displayed form is how you would like the word or phrase to appear in the transcription. This table includes some examples: 

|Recognized displayed form |Spoken form |
|---|---|
|3CPO |three c p o |
|CNTK |c n t k |
|AAA |Triple A |

You provide pronunciation datasets in a single text file. Include the spoken utterance and a custom pronunciation for each. Each row in the file should begin with the recognized form, then a tab character, and then the space-delimited phonetic sequence. 

```
3CPO    three c p o 
CNTK    c n t k 
IEEE    i triple e 
```

Consider the following when creating and training pronunciation datasets: 

It’s not recommended to use custom pronunciation files to alter the pronunciation of common words.  

If there are a few variations of how a word or name is incorrectly transcribed, consider using some or all of them when training the pronunciation dataset. For example, if Robert is mentioned five times in the video and transcribed as Robort, Ropert, and robbers. You can try including all variations in the file as in the following example but be cautious when training with actual words like robbers as if robbers is mentioned in the video, it is transcribed as Robert. 

`Robert    Roport`   
`Robert    Ropert`   
`Robert    Robbers` 

Pronunciation model isn't meant to address acronyms. For example, if you want Doctor to be transcribed as Dr., this can't be achieved through a pronunciation model. 

Refer to the following table to ensure that your pronunciation dataset files are valid and correctly formatted. 

|Property |Value |
|---|---|
|Text encoding |UTF-8 BOM (ANSI is also supported for English) |
|Number of pronunciations per line |1 |
|Maximum file size |1 MB (1 KB for free tier) |

## How to improve your custom models  

Training a pronunciation model can be an iterative process, as you might gain more knowledge on the pronunciation of the subject after initial training and evaluation of your model’s results. Since existing models can't be edited or modified, training a model iteratively requires the creation and uploading of datasets with additional information as well as training new custom models based on the new datasets. You would then reindex the media files with the new custom speech model. 

Example: 

Let's say you plan on indexing sports content and anticipate transcript accuracy issues with specific sports terminology as well as in the names of players and coaches. Before indexing, you've created a speech model with a plain text dataset with content containing relevant sports terminology and a pronunciation dataset with some of the player and coaches’ names. You index a few videos using the custom speech model and when reviewing the generated transcript, find that while the terminology is transcribed correctly, many names aren't. You can take the following steps to improve performance in the future: 

1. Review the transcript and note all the incorrectly transcribed names. They could fall into two groups:  

    - Names not in the pronunciation file.  
    - Names in the pronunciation file but they're still incorrectly transcribed. 
2. Create a new dataset file. Either download the pronunciation dataset file or modify your locally saved original. For group A, add the new names to the file with how they were incorrectly transcribed (Michael Mikel). For group B, add additional lines with each line having the correct name and a unique example of how it was incorrectly transcribed. For example: 

    `Stephen Steven`   
    `Stephen Steafan`   
    `Stephen Steevan` 
3. Upload this file as a new dataset file. 
4. Create a new speech model and add the original plain text dataset and the new pronunciation dataset file. 
5. Reindex the video with the new speech model. 
6. If needed, repeat steps 1-5 until the results are satisfactory. 

## [Web portal](#tab/customizeapi)

[!INCLUDE [speech model](./includes/speech-model-note.md)]
 
Azure AI Video Indexer lets you create custom speech models to customize speech recognition by uploading datasets that are used to create a speech model. This article goes through the steps to do so through the Video Indexer website. You can also use the API, as described in [Customize speech model using API](customize-speech-model-with-api.md). 

For a detailed overview and best practices for custom speech models, see [Customize a speech model with Azure AI Video Indexer](customize-speech-model-overview.md). 

## Create a dataset 

As all custom models must contain a dataset, we'll start with the process of how to create and manage datasets. 

1. Go to the [Azure AI Video Indexer website](https://www.videoindexer.ai/) and sign in. 
1. Select the Model customization button on the left of the page. 
1. Select the Speech (new) tab. Here you'll begin the process of uploading datasets that are used to train the speech models.  

    > [!div class="mx-imgBorder"]
    > :::image type="content" source="./media/customize-speech-model/speech-model.png" alt-text="Screenshot of uploading datasets which are used to train the speech models.":::
1. Select Upload dataset. 
1. Select either Plain text or Pronunciation from the Dataset type dropdown menu. Every speech model must have a plain text dataset and can optionally have a pronunciation dataset. To learn more about each type, see Customize a speech model with Azure AI Video Indexer. 
1. Select Browse which will open the File Explorer. You can only use one file in each dataset. Choose the relevant text file. 
1. Select a Language for the model. Choose the language that is spoken in the media files you plan on indexing with this model. 
1. The Dataset name is prepopulated with the name of the file but you can modify the name. 
1. You can optionally add a description of the dataset. This could be helpful to distinguish each dataset if you expect to have multiple datasets. 

    > [!div class="mx-imgBorder"]
    > :::image type="content" source="./media/customize-speech-model/dataset-type.png" alt-text="Screenshot of multiple datasets.":::
1. Once you're ready, select Upload. You'll then see a list of all of your datasets and their properties, including the type, language, status, number of lines, and creation date. Once the status is complete, it can be used in the training and creation or new models. 

    > [!div class="mx-imgBorder"]
    > :::image type="content" source="./media/customize-speech-model/datasets.png" alt-text="Screenshot of a new model.":::

## Review and update a dataset

Once a Dataset has been uploaded, you might need to review it or perform any number of updates to it. This section covers how to view, download, troubleshoot, and delete a dataset. 

**View dataset**: You can view a dataset and its properties by either clicking on the dataset name or when hovering over the dataset or clicking on the ellipsis and selecting **View Dataset**.  

> [!div class="mx-imgBorder"]
> :::image type="content" source="./media/customize-speech-model/view-dataset.png" alt-text="Screenshot of how to view dataset.":::

You'll then view the name, description, language and status of the dataset plus the following properties: 

**Number of lines**: indicates the number of lines successfully loaded out of the total number of lines in the file. If the entire file is loaded successfully the numbers will match (for example, 10 of 10 normalized). If the numbers don't match (for example, 7 of 10 normalized), this means that only some of the lines successfully loaded and the rest had errors. Common causes of errors are formatting issues with a line, such as not spacing a tab between each word in a pronunciation file. Reviewing the plain text and pronunciation data for training articles should be helpful in finding the issue. To troubleshoot the cause, review the error details, which are contained in the report. Select **View report** to view the error details regarding the lines that didn't load successfully (errorKind). This can also be viewed by selecting the **Report** tab.   

> [!div class="mx-imgBorder"]
> :::image type="content" source="./media/customize-speech-model/report-tab.png" alt-text="Screenshot of how to view by selecting report tab.":::

**Dataset ID**: Each dataset has a unique GUID, which is needed when using the API for operations that reference the dataset. 

**Plain text (normalized)**: This contains the normalized text of the loaded dataset file. Normalized text is the recognized text in plain form without formatting. 

**Edit Details**: To edit a dataset's name or description, when hovering over the dataset, click on the ellipsis and then select Edit details. You're then able to edit the dataset name and description. 

> [!Note]
> The data in a dataset can't be edited or updated once the dataset has been uploaded. If you need to edit or update the data in a dataset, download the dataset, perform the edits, save the file, and upload the new dataset file. 

**Download**: To download a dataset file, when hovering over the dataset, click on the ellipsis and then select Download. Alternatively, when viewing the dataset, you can select Download and then have the option of downloading the dataset file or the upload report in JSON form. 

**Delete**: To delete a dataset, when hovering over the dataset, click on the ellipsis and then select Delete.  

## Create a custom speech model 

Datasets are used in the creation and training of models. Once you have created a plain text dataset, you are now able to create and start using a custom speech model.  

Keep in mind the following when creating and using custom speech models: 

* A new model must include at least one plain text dataset and can have multiple plain text datasets.  
* It's optional to include a pronunciation dataset and no more than one can be included.   
* Once a model is created, you can't add additional datasets to it or perform any modifications to its datasets. If you need to add or modify datasets, create a new model. 
* If you have indexed a video using a custom speech model and then delete the model, the transcript is not impacted unless you perform a re-index.  
* If you deleted a dataset that was used to train a custom model, as the speech model was already trained by the dataset, it continues to use it until the speech model is deleted. 
* If you delete a custom model, it has no impact of the transcription of videos that were already indexed using the model. 


**The following are instructions to create and manage custom speech models.  There are two ways to train a model – through the dataset tab and through the model tab.**

## Train a model through the Datasets tab 

1. When viewing the list of datasets, if you select a plain text dataset by clicking on the circle to the left of a plain text dataset’s name, the Train new model icon above the datasets will now turn from greyed out to blue and can be selected. Select Train new model. 

    > [!div class="mx-imgBorder"]
    > :::image type="content" source="./media/customize-speech-model/train-model.png" alt-text="Screenshot of how to train new model.":::
1. In the Train a new model popup, enter a name for the model, a language, and optionally add a description. A model can only contain datasets of the same language. 
1. Select the Datasets tab and then select from the list of your datasets the datasets you would like to be included in the model. Once a model is created, datasets can't be added. 
1. Select Create ad train. 

## Train a model through the Models tab 

1. Select the Models tab and then the Train new model icon. If no plain text datasets have been uploaded, the icon is greyed out. Select all the datasets that you want to be part of the model by clicking on the circle to the left of a plain text dataset’s name. 
1. In the Train a new model pop-up, enter a name for the model, a language, and optionally add a description. A model can only contain datasets of the same language. 
1. Select the Datasets tab and then select from the list of your datasets the datasets you would like to be included in the model. Once a model is created, datasets can't be added. 
1. Select Create and train. 

## Model review and update 

Once a Model has been created, you might need to review its datasets, edits its name, or delete it.  

**View Model**: You can view a model and its properties by either clicking on the model’s name or when hovering over the model, clicking on the ellipsis and then selecting View Model.  

> [!div class="mx-imgBorder"]
> :::image type="content" source="./media/customize-speech-model/view-model.png" alt-text="Screenshot of how to review and update a model.":::
    
You'll then see in the Details tab the name, description, language and status of the model plus the following properties: 

**Model ID**: Each model has a unique GUID, which is needed when using the API for operations that reference the model. 

**Created on**: The date the model was created. 

**Edit Details**: To edit a model’s name or description, when hovering over the model, click on the ellipsis and then select Edit details. You're then able to edit the model’s name and description. 

> [!div class="mx-imgBorder"]
> :::image type="content" source="./media/customize-speech-model/create-model.png" alt-text="Screenshot of how to hover over the model.":::

> [!Note] 
> Only the model’s name and description can be edited. If you want to make any changes to its datasets or add datasets, a new model must be created. 

**Delete**: To delete a model, when hovering over the dataset, click on the ellipsis and then select Delete.  

**Included datasets**: Click on the Included datasets tab to view the model’s datasets. 

> [!div class="mx-imgBorder"]
> :::image type="content" source="./media/customize-speech-model/included-datasets.png" alt-text="Screenshot of how to delete the model.":::

## How to use a custom language model when indexing a video 

A custom language model isn't used by default for indexing jobs and must be selected during the index upload process.  To learn how to index a video, see Upload and index videos with Azure AI Video Indexer - Azure AI Video Indexer | Microsoft Learn.  

During the upload process, you can select the source language of the video. In the Video source language drop-down menu, you'll see your custom model among the language list. The naming of the model is the language of your Language model and the name that you gave it in parentheses. For example: 

> [!div class="mx-imgBorder"]
> :::image type="content" source="./media/customize-speech-model/contoso-model.png" alt-text="Screenshot of indexing a video.":::

Select the Upload option in the bottom of the page, and your new video will be indexed using your Language model. The same steps apply when you want to re-index a video with a custom model. 


## [Web portal](#tab/customizeapi)

[!INCLUDE [speech model](./includes/speech-model-note.md)]

Azure AI Video Indexer lets you create custom language models to customize speech recognition by uploading adaptation text, namely text from the domain whose vocabulary you'd like the engine to adapt to or aligning word or name pronunciation with how it should be written. 

For a detailed overview and best practices for custom speech models, see [Customize a speech model with Azure AI Video Indexer](customize-speech-model-overview.md). 

You can use the Azure AI Video Indexer APIs to create and edit custom language models in your account. You can also use the website, as described in [Customize speech model using the Azure AI Video Indexer website](customize-speech-model-with-website.md). 

The following are descriptions of some of the parameters: 

|Name   | Type |  Description |  
|---|---|---|
|`displayName`      |string |The desired name of the dataset/model.|
|`locale`           |string |The language code of the dataset/model. For full list, see [Language support](language-support.md).|
|`kind`             |integer|0 for a plain text dataset, 1 for a pronunciation dataset.| 
|`description`      |string |Optional description of the dataset/model.|
|`contentUrl`       |uri    |URL of source file used in creation of dataset.| 
|`customProperties` |object |Optional properties of dataset/model.| 

## Create a speech dataset 

The [create speech dataset](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Speech-Dataset) API creates a dataset for training a speech model. You upload a file that is used to create a dataset with this call. The content of a dataset can't be modified after it's created. 
To upload a file to a dataset, you must update parameters in the Body, including a URL to the text file to be uploaded. The description and custom properties fields are  optional. The following is a sample of the body:

```json
{
    "displayName": "Pronunciation Dataset",
    "locale": "en-US",
    "kind": "Pronunciation",
    "description": "This is a pronunciation dataset.",
    "contentUrl": https://contoso.com/location,
    "customProperties": {
        "tag": "Pronunciation Dataset Example"
    }
}
```

### Response 

The response provides metadata on the newly created dataset following the format of this example JSON output: 

```json
{ 
    "id": "000000-0000-0000-0000-f58ac7002ae9", 
    "properties": { 
        "acceptedLineCount": 0, 
        "rejectedLineCount": 0, 
        "duration": null, 
        "error": null 
    }, 
    "displayName": "Contoso plain text", 
    "description": "VI dataset", 
    "locale": "en-US", 
    "kind": "Language", 
    "status": "Waiting", 
    "lastActionDateTime": "2023-02-28T13:24:27Z", 
    "createdDateTime": "2023-02-28T13:24:27Z", 
    "customProperties": null 
} 
```

## Create a speech model 

The [create a speech model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Speech-Model) API creates and trains a custom speech model that could then be used to improve the transcription accuracy of your videos. It must contain at least one plain text dataset and can optionally have pronunciation datasets. Create it with all of the relevant dataset files as a model’s datasets can't be added or updated after its creation. 

When creating a speech model, you must update parameters in the Body, including a list of strings where the strings are the dataset/s the model will include. The description and custom properties fiels are optional. The following is a sample of the body:

```json
{
    "displayName": "Contoso Speech Model",
    "locale": "en-US",
    "datasets": ["ff3d2bc4-ab5a-4522-b599-b3d5ba768c75", "87c8962d-1d3c-44e5-a2b2-c696fddb9bae"],
    "description": "Contoso ads example model",
    "customProperties": {
        "tag": "Example Model"
    }
}
```

### Response 

The response provides metadata on the newly created model following the format of this example JSON output: 

```json{ 
    "id": "00000000-0000-0000-0000-85be4454cf", 
    "properties": { 
        "deprecationDates": { 
            "adaptationDateTime": null, 
            "transcriptionDateTime": "2025-04-15T00:00:00Z" 
        }, 
        "error": null 
    }, 
    "displayName": "Contoso speech model", 
    "description": "Contoso speech model for video indexer", 
    "locale": "en-US", 
    "datasets": ["00000000-0000-0000-0000-f58ac7002ae9"], 
    "status": "Processing", 
    "lastActionDateTime": "2023-02-28T13:36:28Z", 
    "createdDateTime": "2023-02-28T13:36:28Z", 
    "customProperties": null 
} 
```

## Get speech dataset 

The [get speech dataset](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Speech-Dataset) API returns information on the specified dataset.  

### Response 

The response provides metadata on the specified dataset following the format of this example JSON output: 

```json
{ 
    "id": "00000000-0000-0000-0000-f58002ae9", 
    "properties": { 
        "acceptedLineCount": 41, 
        "rejectedLineCount": 0, 
        "duration": null, 
        "error": null 
    }, 
    "displayName": "Contoso plain text", 
    "description": "VI dataset", 
    "locale": "en-US", 
    "kind": "Language", 
    "status": "Complete", 
    "lastActionDateTime": "2023-02-28T13:24:43Z", 
    "createdDateTime": "2023-02-28T13:24:27Z", 
    "customProperties": null 
} 
```

## Get speech datasets files 

The [get speech dataset files](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Speech-Dataset-Files) API returns the files and metadata of the specified dataset. 

### Response 

The response provides a URL with the dataset files and metadata following the format of this example JSON output: 

```json
[{ 
    "datasetId": "00000000-0000-0000-0000-f58ac72a", 
    "fileId": "00000000-0000-0000-0000-cb190769c", 
    "name": "languagedata", 
    "contentUrl": "", 
    "kind": "LanguageData", 
    "createdDateTime": "2023-02-28T13:24:43Z", 
    "properties": { 
        "size": 1517 
    } 
}, { 
    "datasetId": "00000000-0000-0000-0000-f58ac72” 
    "fileId": "00000000-0000-0000-0000-2369192e", 
    "name": "normalized.txt", 
    "contentUrl": "", 
    "kind": "LanguageData", 
    "createdDateTime": "2023-02-28T13:24:43Z", 
    "properties": { 
        "size": 1517 
    } 
}, { 
    "datasetId": "00000000-0000-0000-0000-f58ac7", 
    "fileId": "00000000-0000-0000-0000-05f1e306", 
    "name": "report.json", 
    "contentUrl": "", 
    "kind": "DatasetReport", 
    "createdDateTime": "2023-02-28T13:24:43Z", 
    "properties": { 
        "size": 78 
    } 
}] 
```

## Get the specified account datasets

The [get speech datasets](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Speech-Datasets) API returns information on all of the specified accounts datasets.  

### Response 

The response provides metadata on the datasets in the specified account following the format of this example JSON output: 

```json
[{ 
    "id": "00000000-0000-0000-abf5-4dad0f", 
    "properties": { 
        "acceptedLineCount": 41, 
        "rejectedLineCount": 0, 
        "duration": null, 
        "error": null 
    }, 
    "displayName": "test", 
    "description": "string", 
    "locale": "en-US", 
    "kind": "Language", 
    "status": "Complete", 
    "lastActionDateTime": "2023-02-27T08:42:02Z", 
    "createdDateTime": "2023-02-27T08:41:39Z", 
    "customProperties": null 
}] 
```

## Get the specified speech model 

The [get speech model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Speech-Model) API returns information on the specified model.  

### Response 

The response provides metadata on the specified model following the format of this example JSON output: 

```json
{ 
    "id": "00000000-0000-0000-0000-5685be445", 
    "properties": { 
        "deprecationDates": { 
            "adaptationDateTime": null, 
            "transcriptionDateTime": "2025-04-15T00:00:00Z" 
        }, 
        "error": null 
    }, 
    "displayName": "Contoso speech model", 
    "description": "Contoso speech model for video indexer", 
    "locale": "en-US", 
    "datasets": ["00000000-0000-0000-0000-f58ac7002"], 
    "status": "Complete", 
    "lastActionDateTime": "2023-02-28T13:36:38Z", 
    "createdDateTime": "2023-02-28T13:36:28Z", 
    "customProperties": null 
} 
```

## Get the specified account speech models 

The [get speech models](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Speech-Models) API returns information on all of the models in the specified account.  

### Response 

The response provides metadata on all of the speech models in the specified account following the format of this example JSON output: 

```json
[{ 
    "id": "00000000-0000-0000-0000-5685be445", 
    "properties": { 
        "deprecationDates": { 
            "adaptationDateTime": null, 
            "transcriptionDateTime": "2025-04-15T00:00:00Z" 
        }, 
        "error": null 
    }, 
    "displayName": "Contoso speech model", 
    "description": "Contoso speech model for video indexer", 
    "locale": "en-US", 
    "datasets": ["00000000-0000-0000-0000-f58ac7002a"], 
    "status": "Complete", 
    "lastActionDateTime": "2023-02-28T13:36:38Z", 
    "createdDateTime": "2023-02-28T13:36:28Z", 
    "customProperties": null 
}] 
```

## Delete speech dataset 

The [delete speech dataset](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Speech-Dataset) API deletes the specified dataset. Any model that was trained with the deleted dataset continues to be available until the model is deleted. You cannot delete a dataset while it is in use for indexing or training.

### Response 

There's no returned content when the dataset is deleted successfully. 

## Delete a speech model 

The [delete speech model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Speech-Model) API deletes the specified speech model. You cannot delete a model while it is in use for indexing or training. 

### Response 

There's no returned content when the speech model is deleted successfully. 

