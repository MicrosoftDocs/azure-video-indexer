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

1. Go to your VI extension → **Manage AI insight**.
1. Move to the **AI insights** tab.
1. Select **Create custom insight**.
1. Choose the type of AI insight you want to create: **Object** or **Situation**.

   :::image type="content" source="media/live-ai-insights-catalog/choose-custom-ai-insight-type.png" alt-text="Screenshot of create a custom AI insight page with option to select object or situation detection.":::
1. Enter a name for the insight in the **AI insight name** field. The name isn't part of the training data.
1. For object detection:
   - **Detected object**: Describe the object to detect. Use only nouns like `dog` or `shopping cart`. Don’t use adjectives or descriptive words like `big` or `empty`. For more examples, see [Best Practices](#best-practices-to-create-a-custom-insight).
   - **Image**: Upload up to 10 images of the object.
   :::image type="content" source="./media/live-ai-insights-catalog/create-custom-ai-insight.png" border="true" alt-text="Screenshot of the create custom AI insight page for object detection where you add a name, describe the object, and upload images."  :::
   - Select the **Fine-tune (optional)** tab to add negative examples.
      - Add words to name objects you don't want to detect. Separate the words by commas.
      - Upload up to 10 images that represent objects you do not want to detect.
1. For situation detection:
   - **Detected situation**: Describe the situation you want to detect, such as `A long queue in a store`.
      :::image type="content" source="media/live-ai-insights-catalog/create-custom-ai-insight-situation.png" alt-text="Screenshot of the basic settings tab for situation type custom insight where you describe what you want to detect.":::
   - Select the **Fine-tune (optional)** tab to add negative examples. Describe situations you don’t want to detect. Separate examples with commas.
1. Review and select **Create insight**.

## Best practices to create a custom insight

Use the following best practices to help you define custom AI insights that deliver accurate, reliable detection results. The tips below cover how to choose effective training data, avoid common mistakes, and get the most from object and situation detection.

### Object detection

Follow these tips to define object detection insights that help the model accurately identify and track specific items in your video streams:

- Use only nouns like `dog` or `shopping cart`.
- Don't use adjectives or descriptive words like `big` or `empty`.
- You can include up to 10 words for a single custom insight. They're added in the **Training data**" section – **Text**. Use these words to represent various terms for the same object to ensure comprehensive detection. For example, to detect computers, use terms such as `computer`, `laptop`, and `PC`. All the terms create one class of detection and tracking. They're called by the value specified in **AI Insight Name**.
- If using as a training data a high-level category word such as “vehicle”, it is useful to add to the training data more specific words, such as “car”, “automobile”, etc. 

- You can include up to 10 images for a single custom insight in addition or instead of the text section. They’re added to the Training data section – Images. Use these images to represent various visual features of the same object to ensure comprehensive detection. 

- Optionally, use negative examples (text and/or images) to improve the detection results or get finer results. For example, if you’d like to detect all vehicles that are not SUVs, use the positive example “vehicle” and the negative example “SUV”. 

- The AI Insight Name isn't automatically added to the training data. For example, if you called the insight `computer`, you should also add that word to the training data section – **Text**.
- Create separate insights for different objects. For example, don't create a single "Animal detection" insight and then attempt to include 10 different animals that you want to detect. Instead, create a different insight for each animal. For example: Cow detection - `cow`, Cat detection - `cat`, Elephant detection - `elephant`, and Giraffe detection - `giraffe`.
- Avoid using words that can refer to two different objects like `bat` or `nail`.
- Avoid using logical words like `and`, `or`, and `not`. Enter each word separately, unless the object itself includes two words. For example, `shopping cart`.
- Use images that include only the object you would like to detect.

- Use good quality images (i.e., avoid using low quality, pixelated, or blurry images).

### Situation detection

Use these guidelines to define situation detection insights that help the model recognize specific scenarios or conditions in your video streams:

- Use this type of insight to describe the situation of the frame. For example, “A messy store”, “a fire in the apartment”. 

- Use concise descriptions. 

- Avoid using logical words like and, or, and not. 

- Consider starting the text description with “a photo of a...”, if you don’t get the desired results. 

- Use environmental details to enrich your description. For example, use “a photo of a shop with customers reaching for a product from a high shelf” instead of just “a customer reaching for a product from a shelf”. 

- Optionally, use negative text examples to improve or get finer results. For example, if you’d like to detect a non-empty shop, use the positive example “a photo of a shop with customers”, and the negative example “a photo of an empty shop”. 

### Custom insight limitations

Be aware of these limitations when you create custom insights to set the right expectations for detection results:

- If you create a custom insights from an image, the detection doesn't identify objects by their color. For example, an image of a yellow vest results in detection for all vests, without specifying the yellow vest.
- To define a situation insight, you cannot use images. 

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