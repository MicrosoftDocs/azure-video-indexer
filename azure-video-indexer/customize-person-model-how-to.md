---
title: Customize a Person model in Azure AI Video Indexer  
description: This article shows you how to customize a Person model in Azure AI Video Indexer. 
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/03/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
---

# Customize a person model in Azure AI Video Indexer

> [!NOTE]
> Face identification, customization, and celebrity recognition features access is limited based on eligibility and usage criteria in order to support our Responsible AI principles. Face identification, customization, and celebrity recognition features are only available to Microsoft managed customers and partners. Use the [Face Recognition intake form](https://aka.ms/facerecognition) to apply for access.

Faces that Azure AI Video Indexer doesn't recognize are still detected, but are left unnamed. You can build custom person models and enable Azure AI Video Indexer to recognize faces that don't get recognized by default. You can build them by pairing a person's name with image files of the person's face.

You can create multiple person models per account. For example, if the content in your account is meant to be sorted into different channels, you might want to create a separate person model for each channel. 

> [!NOTE]
> Each person model supports up to 1 million people and each account has a limit of 50 person models. 

You can use a person model when uploading/indexing or reindexing a video by providing the person model ID. Training a new face for a video updates the associated custom model.

If you don't need the multiple person model support, don't assign a person model ID to your video when uploading/indexing or reindexing. Azure AI Video Indexer uses the default person model in your account.

## Prerequisites

- An Azure account
- An Azure AI Video Indexer account

## [Web portal](#tab/customizewebportal)

## Create a new Person model

1. Select the **+ Add model** button.
1. Enter the name of the model and select the **check** button.
1. Select the list menu button and choose **+ Add person**.

## Add a new person to a Person model

1. Select the list menu button next to the person model that you want to add the face to.
1. Select **+ Add person** from the menu.
1. Enter the name of the person and select the **check** button.
1. Choose from your file explorer or drag and drop the face images of the face.

Azure AI Video Indexer allows you to add multiple people with the same name in a person model. However, we recommend that you give unique names to each person in your model for usability and clarity.

Azure AI Video Indexer can detect occurrences of the person in the future videos that you index and the current videos that you already indexed, using the person model to which you added the new face. Recognition of the person in your current videos might take some time to take effect because it's a batch process.

## Rename a Person model

You can rename any person model in your account including the default person model. Even if you rename your default person model, it still serves as the default person model in your account.

1. Select the **menu** button next to the person model you want to rename.
1. Select **Rename** from the menu.
1. Select the current name of the model.
1. Enter the new name and select the **check** button.

## Delete a Person model

You can delete any person model except the default person model.

1. Select **Delete** from the menu. You're warned about the permanence of the action.
1. If you're sure, select **Delete** again.

> [!NOTE]
> You can edit the names of faces in the associated videos only after you reindex them using another person model. If you reindex without specifying a person model, the default model gets used.

## Central management of Person models in your account

1. Select the **content model customization** button on the left of the page.
1. Select the **People** tab. 

The Default Person model holds any faces you previously edited or changed in the insights of your videos for which you didn't specify a custom person model during indexing. If you created other person models, they're also listed on this page.

### Rename a person

1. Select the list menu button and choose **Rename** from the list menu.
1. Select the current name of the person and type in the new name.
1. Select the **check** button.

### Delete a person

1. Select the list menu button and choose **Delete** from the list menu. A pop-up tells you that this action deletes the person and that this action can't be undone.
1. If you're sure, select **Delete** again.

### Check if a person already exists 

You can use the search to check if a person already exists in the model.

### Manage a person

If you select **Manage**, you see the **Person's details** window with all the faces that this person model is being trained from. These faces come from occurrences of that person in videos that use this person model or from images that you manually uploaded.

#### Add a face

You can add more faces to the person by selecting **Add images**.

#### Delete a face

Select the image you wish to delete and select **Delete**.

#### Rename and delete a person 

Rename the person and to delete the person from the person model in **Manage** area.

## Use a person model to index a video

You can use a person model to index your new video by assigning the person model during the upload of the video.

To use your person model on a new video, do the following steps:

1. Select the **Upload** button.
1. Drag and drop your video file or browse for your file.
1. Select the **Advanced options** arrow.
1. Select the drop-down and select the person model that you created.
1. Select the **Upload** option in the bottom of the page.

If you don't specify a Person model during the upload, Azure AI Video Indexer indexes the video using the Default Person model in your account.

## Use a person model to reindex a video

To use a person model to reindex a video in your collection, go to your library on the Azure AI Video Indexer home page, and hover over the name of the video that you want to reindex.

You see options to edit, delete, and reindex your video.

1. Select the reindex your video option.
1. Select the person model drop-down and select the person model that you want to use.
2. Select **Reindex**.

Any new edits that you make to the faces detected and recognized in the video are saved in the Person model that you used to reindex the video.

## Managing people in your videos

You manage any faces detected and recognized people by editing and deleting them in your indexed videos.

Deleting a face removes a specific face from the insights of the video.

Editing a face renames the detected face and possibly recognized in your video. When you edit a face in your video, that name is saved as a person entry in the person model that was assigned to the video during upload and indexing.

If you don't assign a person model to the video during upload, your edit is saved in your account's Default person model.

### Edit a face

> [!NOTE]
> If a Person model has two or more different people with the same name, you can't tag that name within the videos that use that person model. You can only make changes to people that share that name in the People tab of the content model customization page in Azure AI Video Indexer. For this reason, we recommend that you give unique names to each person in your Person model.

1. Select the video you want to work with from your library.
1. Select the **Insights** tab and select the **pencil** icon.
1. Select any of the detected faces and change their names from **Unknown #X** (or the name that was previously assigned to the face).
1. Enter the new name and select the **check** symbol. The action saves the new name. It recognizes and names all occurrences of the face in your other current videos and in the future videos that you upload.

Recognition of the face in your other current videos might take some time to take effect because it's a batch process.

If you assign a name to a face that matches an existing person in the video's person model, the detected face images from the video are combined with the existing images in the model. If you name a face with a new name, a new person entry is created in the person model that the video is using.

### Delete a face
1. Select the video you want to work with from your library.
1. Select the **Insights** pane and select the pencil symbol.
1. Select the **Delete** option underneath the name of the face. This action removes the detected face from the video. The person's face is still detected in the other videos in which it appears. You can also delete the face from those videos after they're indexed.

 If the person was named, they continue to exist in the person model that was used to index the video from which you deleted the face unless you specifically delete the person from the person model.

## Get an indication of the quality of your people model

You can get an indication on the quality of your customized people model (poor, fair, good). The quality gets determined by the number of images used for labeling with the more images you use to label a person, the higher the probability to identify the person correctly. For example, the probability of identifying a person with 24 labeled images is higher than the probability of identifying a person with two labeled images. You can see the number of images used for labeling each person in your customized people model page.

## Choose the custom people model as default

You can choose a customized people model as default on the VI account user level, so you don't have to keep selecting the model name for every video upload. It saves you time and effort when you upload videos that need to get analyzed by your customized people model.

## Group unknown people in the video

You can see the unknown people in your videos grouped by their appearance similarity. It helps you label the unknown people easily and quickly, and improves the accuracy of your customized people model. For example, it could help you to label a local celebrity or a local politician. You can see the grouping of unknown people in your customization page. Choose **people** and then navigate to the **unknown people** tab.

## Search results with max confidence score for identified person name

You can search for the name of an identified person and get the timestamp for when the person appears in the video along with the maximum confidence score. It helps you decide which videos are the most relevant to explore. For example, you can search for `John Smith` and get the videos where John Smith gets recognized by your customized people model and the confidence score for each video.

## [API](#tab/customizeapi)

## Create a new person model

Make a [Create Person Model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Create-Person-Model) API request.

### Example response

```json
{
    "id": "227654b4-912c-4b92-ba4f-641d488e3720",
    "name": "Example Person Model"
}
```

You then use the **id** value for the **personModelId** parameter when [uploading a video to index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video) or [reindexing a video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Re-Index-Video).

## Delete a person model

To delete a custom person model from the specified account, use a [Delete Person Model](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Delete-Person-Model) API request.

Once the person model is deleted successfully, the index of your current videos that were using the deleted model remains unchanged until you reindex them. When reindexed, Azure AI Video Indexer doesn't recognize the named faces from the deleted model in your current videos when they were indexed using the model. However, the faces are still detected. Indexed videos using the deleted model use your account's default person model. Named faces from the deleted model in your account's default model continue to be recognized in the videos.

### Example response

There's no response when the person model is deleted successfully.

## Get all person models

To get all Person models in the specified account, use the [Get-Person-Models](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Person-Models) request.

The response provides a list of all of the Person models in your account and each of their names and IDs.

```json
[
    {
        "id": "59f9c326-b141-4515-abe7-7d822518571f",
        "name": "Default"
    }, 
    {
        "id": "9ef2632d-310a-4510-92e1-cc70ae0230d4",
        "name": "Test"
    }
]
```

You can choose which model you want to use for a video by using the `id` value of the Person model for the `personModelId` parameter when [uploading a video to index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video) or [reindexing a video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Re-Index-Video).

## Update a face

Use the [Update Video Face](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Update-Video-Face) request.

This request allows you to update a face in your video with a name using the ID of the video and ID of the face. The action then updates the person model that the video was associated with upon uploading/indexing or reindexing. If no person model was assigned, it updates the account's default person model.

The system then recognizes the occurrences of the same face in your other current videos that share the same person model. Recognition of the face in your other current videos might take some time to take effect because it's a batch process.

## Update celebrity names

You can update a face that Azure AI Video Indexer recognized as a celebrity with a new name. The new name that you give takes precedence over the built-in celebrity recognition.

---

## Managing multiple person models

Azure AI Video Indexer supports multiple person models per account through the Azure AI Video Indexer API.

If your account provides different use cases, you might want to create multiple person models per account. For example, if your content is related to sports, you can create a separate person model for each sport (football, basketball, soccer, and so on).

Each account has a limit of 50 person models. If you don't need the multiple person model support, don't assign a person model ID to your video when uploading/indexing or reindexing. In this case, Azure AI Video Indexer uses the default custom person model in your account.

## Optimize the ability to recognize a person

To optimize your model ability to recognize the person, upload as many different images as possible and from different angles. To get optimal results, use high resolution images.