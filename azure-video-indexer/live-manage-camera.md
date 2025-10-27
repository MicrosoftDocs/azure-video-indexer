---
title: Manage live analysis cameras in Azure AI Video Indexer
description: Learn how to manage cameras for use with the Azure AI Video Indexer live extension.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 09/29/2025
ms.service: azure-video-indexer
ms.topic: how-to
#customer intent: As a user of Azure AI Video Indexer, I want to manage live analysis cameras so that I can enable live video analysis capabilities.
---

# Manage live analysis cameras - Preview

The Camera management page shows all cameras linked to your extension. For each camera, you can view and edit the following information:

- **Streaming** - Shows streaming status. If the camera is streaming, you can view the stream in the VI Live player. It might take a few minutes for the stream to appear in the live player.
- **Recording** - Shows recording status. When it’s recording, the camera stream is stored and playable in the VI video on demand (VOD) player.
- **Retention policy** – Choose how long you want to keep the camera’s recording files. The default setting is 100 days. You can change it to any value between 1 to 999 days. To retain indefinitely, select **never delete my files**.
  - If only streaming is selected, the video won't be retained and won't be playable after an hour. You can select Live and VOD streaming for a camera. In this scenario, you can play the camera in Live and VOD players.
- **Applied preset** - If you apply an AI preset to the camera, it displays the preset name. Otherwise, the **Add preset** option with a dropdown list of available presets is shown, where you can select one.
  - In the portal, you can’t apply an AI preset when both VOD and Live streaming are set to **off**. Configure it using the Live Video Analysis API.
- **Pin camera** – Indicates whether the camera appears on the gallery page. You can only select **Yes** for cameras with live streaming.
- **Status** – The camera displays **Updating** when camera management tasks such as preset changes, streaming modifications, and recording adjustments are in progress.

## Create a preset

To use Azure AI Video Indexer Live, create a preset and then apply it to your camera. A preset is a set of AI insights, either VI 1P insights or custom insights. For more information, see [Live AI insights catalog](live-ai-insights-catalog.md).

To create a preset in the VI portal:

1. Go to your live extension > **Manage AI insights**.
1. Select the **Presets** tab.
1. Select **+ Create preset**.
1. Enter the preset name.
1. Select the AI Insights you want to add to the preset from the available list. To create a new custom insight, see [Create a custom insight](live-ai-insights-catalog.md#custom-insights). Selecting AI Insights from the same model saves GPU efforts.
1. Review and select **Create preset**.

Here’s an example screenshot in the VI portal:

:::image type="content" source="./media/live-manage-camera/create-preset.png" border="true" alt-text="Screenshot showing the Create preset page." lightbox="./media/live-manage-camera/create-preset.png" :::

Selecting more than one AI insight with the same model name doesn't increase run time or GPU processing resources when you apply the preset to a camera.

View all created presets in your Arc extension by selecting **Manage AI insights** in the upper right corner and select the **Presets** tab. To edit a preset, select the ellipsis (**…**) in the preset row, then select **Edit preset**. Changing the insights in a preset updates the insights for all cameras using that preset. To duplicate a preset, select **Duplicate preset**. This action creates a new preset identical to the one you selected. This action doesn't affect the preset applied to any camera. Apply the new preset to cameras manually.

## Apply a preset to a camera

After you create a preset, apply it to the camera to get live insights. A camera can have only one preset applied at a time, which you can change instantly. Applying a preset can take a few minutes.

The preset insights run on the camera even when it's not streaming or recording. To access insights, see the Get Live Insights by DateTime API.

### Apply from the pinned cameras tab

1. Go to the live extension > **Pinned cameras** tab.
1. Select the ellipsis (**…**) located in the bottom right corner of the camera view > **+ Apply preset**.
1. The **Apply preset on camera** window opens. Select a preset from the list and then select **Apply preset**.

### Apply from the camera live player

1. Navigate to the live player of one of the cameras.
2. In the right side of the screen select **Apply preset.**
3. The **Apply preset on camera** window opens. Select a preset from the list and then select **Apply preset**.

### Apply from the camera management tab

1. Go to the live extension > **Camera management** tab.
2. Refer to the **Applied preset** column > select **+ Apply preset**.  
  If no preset is applied to the camera, you see the **+ Apply preset** button. Otherwise, you see the name of the applied preset.
3. The **Apply preset on camera** window opens. Select a preset from the list and then select **Apply preset**.  
    :::image type="content" source="./media/live-manage-camera/apply-preset.png" border="true" alt-text="Screenshot showing where to apply a preset." lightbox="./media/live-manage-camera/apply-preset.png" :::

## Change the camera preset

If a preset was applied to the camera, you can update it as needed. Changing the applied preset on the camera might take some time. During this process, the camera status changes to **Updating**.

### Change from the pinned cameras tab

1. Go to your live extension > **Pinned cameras** tab.
2. Select **change preset** in the bottom of the camera view.
3. The **Change preset** window opens. Select a preset from the list and then select **Apply preset**.

### Change from the camera live player

1. Navigate to the live player of one of the cameras.
2. In the right side of the screen upper to the insight timeline > see the **Applied preset** > select the preset name.
3. The **Change preset** window opens. Select a preset from the list and then select **Apply preset**.

### Change from the camera management tab

1. Go to the live extension > **Camera management** tab.
2. Refer to the **Applied preset** column > select **view preset**.
3. The **Change preset** window opens. Select a preset from the list and then select **Apply preset**.

## Add a Camera description

Use the camera description to provide details about the camera view. It helps the system capture the main events in your footage more effectively while generating a summary. Here are some practices to write the camera description:

Keep the description short and include the **location type**. For example:

- "Grocery Shop"
- "Store"
- "Parking Lot"
- "Garage"
- "Street"
- "Bus Station"
- "Factory Production Floor -2"

1. Go to a camera page.
2. Select **Camera properties** in the right upper corner of the screen.
3. Enter a description and apply the change.

## Related content

- [Create custom insights](live-ai-insights-catalog.md)