---
title: Create custom insights in the live AI Insights catalog using Azure AI Video Indexer
description: Learn how to create custom insights in the live AI Insights catalog using Azure AI Video Indexer.
author: cwatson-cat
ms.author: cwatson
ms.collection: ce-skilling-ai-copilot
ms.date: 12/08/2025
ai-usage: ai-assisted
ms.service: azure-video-indexer
ms.topic: how-to
appliesto: 
- Azure AI Video Indexer enabled by Azure Arc
# customer intent: As an Azure user, I want to create custom insights in the live AI Insights catalog using Azure AI Video Indexer.
---

# Create custom insights in the live AI Insights catalog - Preview

Azure AI Video Indexer enables real-time streaming with first party AI models that can detect vehicles and people as they appear. You can also create your own custom insights using natural language to detect any object that interests you in real time. To benefit from real-time detection, create a preset with the AI models you need and then apply it on the camera. For more information, see [Create a preset](live-manage-camera.md#create-a-preset) and [Apply a preset to a camera](live-manage-camera.md#apply-a-preset-to-a-camera) sections.

In the [Azure AI Video Indexer](https://www.videoindexer.ai/) website, you can view the AI insights catalog page to see all available insights.

:::image type="content" source="./media/live-ai-insights-catalog/ai-insights-catalog.png" border="true" alt-text="Screenshot of the AI insights catalog page." lightbox="./media/live-ai-insights-catalog/ai-insights-catalog.png" :::

## People and vehicle detection

Azure AI Video Indexer can detect people and vehicles in real-time video streams. It displays a bounding box around the detections and shows a real-time count of people and vehicles in the frame. Also, Azure AI Video Indexer can track objects within the camera and maintain a unique ID for each track. The ID is tracked through visual embeddings and location rather than with any personal biometric information. So, when an object leaves the frame and enters it again, it gets a new ID.

Here's an example of a real-time stream with people and vehicle detection:

:::image type="content" source="./media/live-ai-insights-catalog/people-vehicle-detection.png" border="true" alt-text="Screenshot of a live stream with people and vehicle detection." lightbox="./media/live-ai-insights-catalog/people-vehicle-detection.png" :::

## Custom insights


Customize AI insight detection to meet your requirements without coding skills or large datasets. Use open vocabulary (OV) technology to define custom insights for object or situation detection, then apply them to different cameras using presets.

### Create a custom AI insight

You can create a custom AI real-time insight in the VI portal to detect either objects or situations. The steps are mostly the same for both types, with a few differences noted below.

To create a new custom AI real-time insight:

1. Go to your live extension → **Manage AI insight**.
1. Move to the **AI insights** tab.
1. Select **Create custom insight**.
1. Choose the type of AI insight you want to create: **Object** or **Situation**.
1. Enter a name for the insight in the **AI insight name** field. The name isn't part of the training data.
1. Choose the **Training data** for the model:
     - **For Object detection**:
         - **Text**: Add words that describe the object. Use only nouns like `dog` or `shopping cart`. Don’t use adjectives or descriptive words like `big` or `empty`. For more examples, see [Best Practices](#best-practices-to-create-a-custom-insight).
         - **Image**: Upload one image of the object.

        :::image type="content" source="./media/live-ai-insights-catalog/create-custom-ai-insight.png" border="true" alt-text="Screenshot of the Create a custom AI insight page." lightbox="./media/live-ai-insights-catalog/create-custom-ai-insight.png" :::

     - **For Situation detection**:
         - **Text**: Describe the situation you want to detect, such as `A long queue in a store`.
         - Optionally, add negative examples in the fine-tune tab. Describe situations you don’t want to detect. Separate examples with commas.
1. Review and select **Create insight**.

## Best practices to create a custom insight

- Use only nouns like `dog` or `shopping cart`.
- Don't use adjectives or descriptive words like `big` or `empty`.
- You can include up to 10 words for a single custom insight. They're added in the **Training data**" section – **Text**. Use these words to represent various terms for the same object to ensure comprehensive detection. For example, to detect computers, use terms such as `computer`, `laptop`, and `PC`. All the terms create one class of detection and tracking. They're called by the value specified in **AI Insight Name**.
- The AI Insight Name isn't automatically added to the training data. For example, if you called the insight `computer`, you should also add that word to the training data section – **Text**.
- Create separate insights for different objects. For example, don't create a single "Animal detection" insight and then attempt to include 10 different animals that you want to detect. Instead, create a different insight for each animal. For example: Cow detection - `cow`, Cat detection - `cat`, Elephant detection - `elephant`, and Giraffe detection - `giraffe`.
- Avoid using words that can refer to two different objects like `bat` or `nail`.
- Avoid using logical words like `and`, `or`, and `not`. Enter each word separately, unless the object itself includes two words. For example, `shopping cart`.
- Use an image that includes only the object you would like to detect.
- Use a good quality image.

### Custom insight limitations

- Creating custom insights from an image doesn't identify objects by their color. For example, an image of a yellow vest results in detection for all vests, without specifying the yellow vest.
- You can't add an image and text as training data for the same insight.

## Limitations

The following limitations apply to all real-time AI insights (people, vehicle, and custom):

- The object tracker is limited to 150 concurrent tracks per stream.
- The confidence of the track as shown in the UI reflects the first occurrence of the track.
- Small objects might not get detected (smaller than 35 x 35 pixels).
- The detector might miss objects in darker areas and severe weather conditions.
- To best detect and track objects, they should be fully visible (no occlusions), with good lighting.
- Large crowds can get underestimated by the model and might not detect all persons.
- The tracker assigns a different ID to the same object after it exits and reenters the camera's view.
- Occlusions might reduce results quality and cause fragmentation in object tracking.
- The detector might misclassify objects observed from steep angles.

## Related content

- [Create a custom insight to detect objects](live-ai-insights-catalog.md)