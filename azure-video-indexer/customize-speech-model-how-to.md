---
title: Customize a speech model in Azure AI Video Indexer  
description: This article shows you how to customize a speech model with Azure AI Video Indexer. 
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/04/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
---

# Customize a speech model
 
> [!NOTE]
> Speech model customization, including pronunciation training, is available in Video Indexer Azure trial accounts and Resource Manager accounts. Classic accounts don't support this feature. To learn how to use the custom language experience, see [Customize a language model](customize-language-model-overview.md).

Azure AI Video Indexer lets you create custom speech models to customize speech recognition by uploading datasets that are used to create a speech model. This article goes through the steps to do so through the Video Indexer website. You can also use the API, as described in [Customize speech model using API](customize-speech-model-with-api.md). 

For a detailed overview and best practices for custom speech models, see [Customize a speech model with Azure AI Video Indexer](customize-speech-model-overview.md).

## Prerequisites
- Read the [Speech model training best practices guide](speech-model-training-best-practices.md).
- An Azure account
- An Azure AI Video Indexer account

## [Web portal](#tab/customizewebportal) 

## Create a dataset 

As all custom models must contain a dataset, start with the process of how to create and manage datasets. 
 
1. Select the **Model customization** button. 
1. Select the **Speech (new)** tab.
1. Select **Upload dataset**. 
1. Select either *Plain text* or *Pronunciation* from the **Dataset type** dropdown menu. Every speech model must have a plain text dataset and can optionally have a pronunciation dataset.
1. Select **Browse** and select the dataset file. You can choose only one. 
1. Select a **Language** for the model. Choose the language that is spoken in the media files you plan on indexing with this model. The Dataset name is prepopulated with the name of the file but you can modify the name. 
1. You can optionally add a description of the dataset. It could be helpful to distinguish each dataset if you expect to have multiple datasets.
1. Select **Upload**. When the dataset creation is complete, you can use it for training and creation of new models.

## Review and update a dataset 

You can view a dataset and its properties by:

- Clicking on the dataset name
- Hovering over the dataset
- Selecting the ellipsis

Then, select **View Dataset**.  

You can then view the name, description, language, and status of the dataset plus the following properties: 

**Number of lines**: indicates the number of lines successfully loaded out of the total number of lines in the file. If the entire file is loaded successfully the numbers match (for example, 10 of 10 normalized). If the numbers don't match (for example, 7 of 10 normalized), it means that only some of the lines successfully loaded and the rest had errors. Common causes of errors are formatting issues with a line, such as not spacing a tab between each word in a pronunciation file. Reviewing the plain text and pronunciation data for training articles should be helpful in finding the issue. To troubleshoot the cause, review the error details, which are contained in the report. Select **View report** to view the error details regarding the lines that didn't load successfully (errorKind). You can also view it selecting the **Report** tab.

**Dataset ID**: Each dataset has a unique GUID, which is needed when using the API for operations that reference the dataset. 

**Plain text (normalized)**: It contains the normalized text of the loaded dataset file. Normalized text is the recognized text in plain form without formatting. 

**Edit Details**: To edit a dataset's name or description, when hovering over the dataset, select on the ellipsis and then select Edit details. You're then able to edit the dataset name and description. 

> [!Note]
> The data in a dataset can't be edited or updated once the dataset has been uploaded. If you need to edit or update the data in a dataset, download the dataset, perform the edits, save the file, and upload the new dataset file. 

**Download**: To download a dataset file, when hovering over the dataset, select on the ellipsis and then select Download. Alternatively, when viewing the dataset, you can select Download and then have the option of downloading the dataset file or the upload report in JSON form. 

**Delete**: To delete a dataset, when hovering over the dataset, select on the ellipsis and then select Delete.  

## Create a custom speech model 

Datasets are used in the creation and training of models. After you create a plain text dataset, you can create and start using a custom speech model.  

Keep the following points in mind when you create and use custom speech models: 

* A new model must include at least one plain text dataset and can have multiple plain text datasets.  
* It's optional to include a pronunciation dataset and no more than one can be included.
* Once a model is created, you can't add more datasets to it or perform any modifications to its datasets. If you need to add or modify datasets, create a new model. 
* If you index a video using a custom speech model and then delete the model, the transcript isn't impacted unless you perform a reindex.  
* If you deleted a dataset used to train a custom model, it continues to use it until the speech model is deleted. The reason is because the speech model got trained by the dataset.
* If you delete a custom model, it doesn't affect video transcription for videos that were already indexed using the model.

## Train a model

> [!NOTE]
> Once a model is created, datasets can't be added.
> A model can only contain datasets of the same language.

There are two ways to train a model – through the dataset tab and through the model tab.

## Train a model through the Datasets tab 

1. View the list of datasets.
1. Select a plain text dataset. Then select the **Train new model** symbol.
1. Select **Train new model**.
1. Enter a name for the model, a language, and optionally add a description.
1. Select the **Datasets** tab
1. Select the datasets you want to be included in the model. 
1. Select **Create and train**. 

## Train a model through the Models tab 

1. Select the **Models** tab.
1. Select **Train new model** icon. 
1. Select the datasets that you want to be part of the model. 
1. Enter a name for the model, a language, and optionally add a description. 
1. Select the **Datasets** tab.
1. Select the datasets you want to be included in the model. 
1. Select **Create and train**. 

## Review and update a model 

**View Model**: You can view a model and its properties by either selecting the model’s name or when you hover over the model. Then select the ellipsis (**...**) and then select **View Model**.
    
Then you see in the Details tab the name, description, language, and status of the model plus the following properties: 

**Model ID**: Each model has a unique GUID, which is needed when using the API for operations that reference the model. 

**Created on**: The date the model was created. 

**Edit Details**: To edit a model’s name or description, when hovering over the model, select on the ellipsis and then select Edit details. You're then able to edit the model’s name and description.

> [!Note] 
> Only the model’s name and description can be edited. If you want to make any changes to its datasets or add datasets, a new model must be created. 

**Delete**: To delete a model, when hovering over the dataset, select on the ellipsis and then select Delete.  

**Included datasets**: Select on the Included datasets tab to view the model’s datasets.

## Use a custom language model when indexing a video 

A custom language model isn't used by default for indexing jobs, so must be selected during the index upload process.  

1. During the upload process, select your custom language model source from the **language** drop-down menu. 
1. Select **Upload**. 

The same steps apply when you want to reindex a video with a custom model.

## [API](#tab/customizeapi)

The following table provides descriptions for some of the parameters used with the speech model requests: 

|Name   | Type |  Description |  
|---|---|---|
|`displayName`      |string |The desired name of the dataset/model.|
|`locale`           |string |The language code of the dataset/model. For full list, see [Language support](language-support.md).|
|`kind`             |integer|0 for a plain text dataset, 1 for a pronunciation dataset.| 
|`description`      |string |Optional description of the dataset/model.|
|`contentUrl`       |uri    |URL of source file used in creation of dataset.| 
|`customProperties` |object |Optional properties of dataset/model.| 

## Create a speech dataset 

You can make a [Create Speech Dataset](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Speech-Dataset) API request to create a dataset to train a speech model. Upload a file that is used to create a dataset with this request. The content of a dataset can't be modified after you create it.

Define the parameters in the request body, including a URL to the text file to be uploaded. The description and custom properties fields are  optional. Here's an example of a request body:

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

### Example response 

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

You can make a [Create Speech Model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Speech-Model) API request to create and train a custom speech model. Use it to improve the transcription accuracy of your videos. It must contain at least one plain text dataset. It can optionally have pronunciation datasets. Create it with all of the relevant dataset files as a model’s datasets can't be added or updated after its creation.

Define the parameters in the request body, including a list of strings that the dataset or datasets for the model to include. The description and custom properties fields are optional. Here's a sample request body:

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

### Example response 

```json
{ 
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

You can use a [Get Speech Dataset](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Speech-Dataset) API call to return information for the specified dataset.

### Example response

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

The [Get Speech Dataset Files](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Speech-Dataset-Files) request returns the files and metadata of the specified dataset. 

### Example response

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

You can use a [Get Speech Datasets](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Speech-Datasets) API request to return information for all of the specified accounts datasets.

### Example response 

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

You can use a [Get Speech Model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Speech-Model) API request to return information for the specified model.

### Example response 

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

You can use a [Get Speech Models](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Speech-Models) API request to return information for all of the models in the specified account.

### Example response 

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

You can use a [Delete Speech Dataset](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Speech-Dataset) API request to delete the specified dataset. Any model that was trained with the deleted dataset continues to be available until the model is deleted. You can't delete a dataset while it is in use for indexing or training.

### Example response 

There's no returned content when the dataset is deleted successfully. 

## Delete a speech model 

You can use a [Delete Speech Model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Speech-Model) API request to delete the specified speech model. You can't delete a model while it is in use for indexing or training. 

### Response 

There's no returned content when the speech model is deleted successfully. 
