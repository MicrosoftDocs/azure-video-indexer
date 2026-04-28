---
title: Create custom insights in the live AI Insights catalog using Azure AI Video Indexer
description: Learn how to create custom insights in the live AI Insights catalog using Azure AI Video Indexer.
author: cwatson-cat
ms.author: cwatson
ms.collection: ce-skilling-ai-copilot
ms.date: 03/31/2026
ai-usage: ai-assisted
ms.service: azure-video-indexer
ms.topic: how-to
appliesto: 
- Azure AI Video Indexer enabled by Azure Arc
# customer intent: As an Azure user, I want to create custom insights in the live AI Insights catalog using Azure AI Video Indexer.
---

# Create custom insights in the live AI Insights catalog - Preview

Create custom insights to detect objects or situations tailored to your operations without coding. Use natural language descriptions, images, and examples to build detections for anything from safety equipment to workflow conditions. Then apply them instantly to live camera streams.

## Prerequisites

Before you begin:

- Review the [Custom Insights overview](live-ai-insights-catalog.md) to understand the best practices and limitations.
- Review [limitations for all live AI insight detections](live-ai-insights-catalog.md#limitations).

## Create a custom AI insight

You can create a custom AI real-time insight in the VI portal to detect either objects or situations. The steps are mostly the same for both types, with a few differences noted below.

To create a new custom AI real-time insight:

1. Go to your VI extension → **Manage AI insight**.
1. Move to the **AI insights** tab.
1. Select **Create custom insight**.
1. Choose the type of AI insight you want to create: **Object** or **Situation**.

   :::image type="content" source="media/live-ai-insights-catalog/choose-custom-ai-insight-type.png" alt-text="Screenshot of create a custom AI insight page with option to select object or situation detection.":::
1. Enter a name for the insight in the **AI insight name** field. The name isn't part of the training data.
1. For object detection:
   - **Detected object**: Describe the object to detect.
   - **Object example images**: Upload up to 10 images of the object.
   :::image type="content" source="./media/live-ai-insights-catalog/create-custom-ai-insight.png" border="true" alt-text="Screenshot of the create custom AI insight page for object detection where you add a name, describe the object, and upload images."  :::
   - Select the **Fine-tune (optional)** tab to add negative examples.
      - Add words to name objects you don't want to detect. Separate the words by commas.
      - Upload up to 10 images that represent objects you do not want to detect.
1. For situation detection:
   - **Detected situation**: Describe the situation you want to detect, such as `A long queue in a store`.
      :::image type="content" source="media/live-ai-insights-catalog/create-custom-ai-insight-situation.png" alt-text="Screenshot of the basic settings tab for situation type custom insight where you describe what you want to detect.":::
   - Select the **Fine-tune (optional)** tab to add negative examples. Describe situations you don’t want to detect. Separate examples with commas.

1. Review and select **Create insight**.

## Related content

After you create a custom insight:

- [Create a preset](live-manage-camera.md#create-a-preset) 
- [Apply a preset to a camera](live-manage-camera.md#apply-a-preset-to-a-camera)