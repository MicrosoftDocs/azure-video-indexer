---
title: Mark an area of interest in live camera footage using Azure AI Video Indexer
description: Learn how to mark an area of interest in live camera footage using Azure AI Video Indexer.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 11/05/2025
ms.service: azure-video-indexer
ms.topic: how-to
# customer intent: As an Azure Video Indexer user, I want to mark an area of interest in live camera footage to focus on specific regions for analysis.
---

# Mark an area of interest - Preview

Marking an Area of Interest (AOI) allows you to define specific regions within the video frame where you want to focus on the analysis. It's useful when only certain zones are relevant for detection or alerting.

It helps you gain insights into the areas that matter most to you and answer questions such as:

- How many people are waiting in line in front of the counters?
- Has someone entered a restricted area?
- Is a car parked in an accessible parking space?

After creating AOIs, you see **AI insight counters** displayed on top of the live video player, segmented by each AOI. It enables real-time visibility into activity within each defined zone.

Here's an example of marking an AOI:

:::image type="content" source="./media/live-area-interest/mark-area-interest.png" alt-text="Screenshot of a live stream showing a polygon marking an area of interest.":::

## Use cases

- **Queue monitoring** - Counts the number of people waiting in line in front of service counters or entry points.
- **Parking lot analysis** - Detect and count how many cars are currently parked in a designated parking area.
- **Restricted zone** - Create real-time alerts when individuals enter restricted or unauthorized zones.
- **Cross-camera AOI correlation** - Track and correlate activity across AOIs that appear in multiple camera views to understand movement patterns or confirm events.
- **AOI-based video search** - Search within AOIs to find specific moments in the video where a particular object (for example, a person or vehicle) was detected in that monitored zone.
- **Store entry/exit counting** - Count the number of people entering and exiting a store to analyze foot traffic and peak hours.

## Draw a line

1. Go to the camera live player page.
2. Select the **Line** tool from the annotation toolbar.
3. Position your cursor at the starting point for the line.
4. Select to mark the first point and then move the mouse to the ending point of the line and select again to complete the line annotation.
5.  Fill the line properties in the form opened in the **Spatial analysis** tab:
    - Give a **Line name -** names aren't required to be unique (each line is stored with unique ID).
    - Optionally, enter a **Description** for the area.
    - Optionally, choose from the list **Monitored zone** – use the field to indicate that lines in different cameras are meant to represent the same physical space.
    - Mark the **Reverse line direction** to change the line direction. The direction of the line affects the crossing direction.
6.  Review and select **Apply**.

You can use the line to count number of objects that cross the line, you can create two lines parallel to count for both sides crossing.

### When an object crosses a line

The system defines *line crossed* when the bottom middle edge of a detected object passed over any part of the marked line.

## Draw a polygon

1. Go to the camera live player page.
2. Select the **Polygon** tool from the annotation toolbar.
3. Position your cursor at the starting point for the polygon.
4. Select to mark the first point, then move the mouse to the next point of the polygon. Continue doing so until the shape is closed. Then, double-click the last point to complete the annotation.
5. Fill the line properties in the form opened in the **Spatial analysis** tab:
    - Give a **Polygon name -** names aren't required to be unique (each polygon is stored with unique ID)
    - Optionally, enter a **Description** for the area.
    - Optionally, choose from the list **Monitored zone** – use the field to indicate that lines in different cameras are meant to represent the same physical space.
6. Review and select **Apply**.

### When an object is inside a polygon

The system defines *inside polygon* when the middle point of the bottom edge of a detected object is within the polygon area.

## Notes

- It might take a while for the shape to become visible in the player.
- The line/polygon annotation persists and remains visible from now on during video playback and recording as well.

## Limitations

- You can add up to 10 shapes (lines or polygons) in one camera. Once you reach 10 shapes, the tool selector in the header becomes gray and disabled.
- The shapes displayed on the spatial analysis tab in the live stream page are the ones that were applied on the camera when the page was loaded. When changes are made by another user after the page gets loaded, there could be a mismatch between the shapes shown on the player and the shapes visible in the tab. When this situation occurs, you see the change in the player. To view it in the tab, you need to refresh the page.
- It might take a while for the shape to become visible on the player after its creation.

## Related content

- [Set up live cameras in Azure AI Video Indexer](live-manage-camera.md)