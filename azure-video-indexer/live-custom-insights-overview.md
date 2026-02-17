---
title: Custom insights in the live AI Insights catalog using Azure AI Video Indexer
description: Learn about custom insights in the live AI Insights catalog using Azure AI Video Indexer.
author: cwatson-cat
ms.author: cwatson
ms.collection: ce-skilling-ai-copilot
ms.date: 02/17/2026
ai-usage: ai-assisted
ms.service: azure-video-indexer
ms.topic: concept-article
appliesto: 
- Azure AI Video Indexer enabled by Azure Arc
# CustomerIntent: As a security or operations manager, I want to understand what custom insights are and when to use them so that I can plan my real-time monitoring strategy.  
---

# Custom insights in the live AI Insights catalog - Preview

Custom insights are detections you define for specific objects or situations in your operations. They supplement the built-in people and vehicle detection that ships enabled out of the box. All insights, built-in and custom, appear in the AI insights catalog, where you apply them to cameras via presets. Create a custom insight when you need detection beyond people and vehicles.

## Types of custom insights

You can create two types of custom insights: object detection and situation detection. Choose 
based on whether you want to monitor a specific item or a broader condition.

### Object detection

Object detection identifies and tracks a specific item moving through your camera view. The system 
assigns each detected item a unique ID and follows it as it moves across the frame. Use object 
detection when you need to spot individual things or count occurrences.

For example, use object detection to track specific items in your operations to enforce safety standards, monitor inventory, or verify compliance. Here are some common examples:

- Safety equipment like hard hats, safety vests, goggles
- Equipment or vehicles like forklifts, pallet jacks, delivery vans
- Tools or materials like ladders, toolboxes, packages
- Apparel or accessories like uniforms, badges, reflective gear

### Situation detection

Situation detection recognizes a condition or scene across the full camera frame. Instead of tracking 
a single object, you describe what the overall frame should look like. Use situation detection when 
the context matters as much as individual items.

While object detection monitors individual items, situation detection watches for conditions 
and patterns. Use it to catch problems like crowding, blockages, or unsafe states. For example:

- Safety conditions like blocked walkway, spill on floor, or fire extinguisher missing
- Workflow states like crowding near a machine, long queue at checkout, or empty shelf
- Environmental conditions like lights off in a room, door left open, or water leak
- Compliance scenarios like area occupied after hours, restricted zone entry, or equipment in wrong location

## Best practices for object detection

Follow these tips to define object detection insights that help the model accurately identify and track specific items in your video streams:

### Describing your object

Write a clear, specific description of the object you want to detect.

- Use detailed, but concise descriptions like `a red classic car`, `person holding a yellow hard hat`, or `person wearing helmet`.
- Add a viewpoint like `a red car visible from behind`.
- Use synonyms like `motorbike`, `bike`, or `motorcycle`.
- The AI Insight Name isn't automatically added to the training data. For example, if you called the insight `computer`, you should also add that word to the training data section – **Text**.
- Create separate insights for different objects. For example, don't create a single "Animal detection" insight and then attempt to include 10 different animals that you want to detect. Instead, create a different insight for each animal. For example: Cow detection - `cow`, Cat detection - `cat`, Elephant detection - `elephant`, and Giraffe detection - `giraffe`.

### What to avoid in your descriptions

Avoid these common mistakes in your descriptions.

- Don't use adjectives or descriptive words like `big` or `empty`.
- Avoid using words that can refer to two different objects like `bat` or `nail`.
- Avoid using logical words like `and`, `or`, and `not`. Enter each word separately, unless the object itself includes two words. For example, `shopping cart`.

### Training words

You can include up to 10 words for a single custom insight. They're added in the training data section – **Text**.

- Use these words to represent various terms for the same object to ensure comprehensive detection. For example, to detect computers, use terms such as `computer`, `laptop`, and `PC`. All the terms create one class of detection and tracking. They're called by the value specified in **AI Insight Name**.
- If using as training data a high-level category word such as "vehicle", it is useful to add to the training data more specific words, such as "car", "automobile", etc.

### Training images

You can include up to 10 images for a single custom insight in addition or instead of the text section. They're added to the training data section – **Images**.

- Use images to represent various visual features of the same object to ensure comprehensive detection.
- Use images that include only the object you would like to detect.
- Use good quality images (i.e., avoid using low quality, pixelated, or blurry images).

### Negative examples (optional)

Use negative examples (text and/or images) to improve the detection results or get finer results. 

- For example, if you'd like to detect all vehicles that are not SUVs, use the positive example "vehicle" and the negative example "SUV".
- Use negative examples instead of negation words like `not` or `without`.

## Best practices for situation detection

Use these guidelines to define situation detection insights that help the model recognize specific scenarios or conditions in your video streams:

- Use this type of insight to describe the situation of the frame. For example, “A messy store”, “a fire in the apartment”. 

- Use concise descriptions. 

- Avoid using logical words like and, or, and not. 

- Consider starting the text description with “a photo of a...”, if you don’t get the desired results. 

- Use environmental details to enrich your description. For example, use “a photo of a shop with customers reaching for a product from a high shelf” instead of just “a customer reaching for a product from a shelf”. 

- Optionally, use negative text examples to improve or get finer results. For example, if you’d like to detect a non-empty shop, use the positive example “a photo of a shop with customers”, and the negative example “a photo of an empty shop”. 

## Limitations

In addition to the limitations that apply to all real-time AI insights, described in [Real-time AI Insights catalog](live-ai-insights-catalog.md), be aware of these limitations when you create custom insights:

- If you create a custom insights from an image, the detection doesn't identify objects by their color. For example, an image of a yellow vest results in detection for all vests, without specifying the yellow vest.
- To define a situation insight, you cannot use images. 
## Related content

- [Live AI Insights catalog](live-ai-insights-catalog.md)
- [Create custom insights in the live AI Insights catalog](live-ai-insights-catalog.md)
- [Manage real-time analysis cameras](live-manage-camera.md)