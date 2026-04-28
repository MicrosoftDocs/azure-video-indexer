---
title: Create an event summary for camera footage using Azure AI Video Indexer
description: Learn how to create an event summary for camera footage using Azure AI Video Indexer.
author: cwatson-cat
ms.author: cwatson
ms.collection: ce-skilling-ai-copilot
ms.date: 11/05/2025
ms.service: azure-video-indexer
ms.topic: how-to
appliesto:
  - Azure AI Video Indexer enabled by Azure Arc
# customer intent: As an Azure Video Indexer user, I want to create an event summary for live camera footage to quickly identify key events.
---

# Create an event summary for camera footage - Preview

Azure AI Video Indexer offers concise summaries for up to six hour segments of recorded video footage from live cameras. The summary consists of two parts. The first part is a high-level overview that provides a general description of the activities within the video. The second part is a collection of highlights that specifically identify anomalous events and events requested in the "Focus on" field, including their timestamps and ranges.

The summary can help you catch up on the most notable events in the video without having to watch the entire video. It helps you save you time by digesting long videos and giving you the gist of a video in a short format.

To identify relevant unusual events in a video, add a "Focus on" prompt describing the type of events you're interested in, such as "violent behavior." The **Camera description** field provides more contextual information that can make the summary more accurate. For example, specifying the location of the camera or what it's looking at (for example, "East parking lot") contributes to the summary’s quality. It's part of the input to the summary and can help the large language model (LLM) get more context of the footage.

If no "Focus on" prompt is selected, there's a third part for the summary called "Detailed log." It includes a list of all the object tracks found by the detectors that were part of the camera preset. The LLM verified the objects and each object includes a description, time, movement, and confidence (by the LLM).

## Use cases

The AI-based video summarization system is designed to help you quickly and efficiently comprehend the content. It captures unusual events in long recorded videos from live cameras, without needing to view the entire footage.

Here are some specific intended uses:

- **Airport** - Use the summary for long videos to find interesting and unusual things like a person injured and criminal activities like violence.
- **Security agencies** – Use the summary to recap camera footage and identify notable events near the border.
- **Manufacturing** – The system can provide summaries of recorded videos from live cameras focused on employee safety. It can capture unusual events such as safety vest violations, fall detection, oil or water leaks, fire, and anomalies in the production line.
- **Retail –** Use the summary to identify the peak hour of customer traffic during the day.

Output formats - You can set summaries to use different styles of language: neutral, casual, or formal. You can also set the length of a summary to short, medium, or long.

## Set the focus on prompt

To generate a summary, add a customized "Focus on" prompt. It ensures the summary is accurate and tailored to your needs by identifying the events that interest you. It helps the summary concentrate on the events relevant to you. See the following examples.

### Examples

- **Airport** – Focus on unusual events like: person falling, people entering restricted areas, and fall detection.
- **Shopping mall -** Focus on unusual events such as violence or physical altercation.
- **Employee safety** - Focus on unusual events such as employee safety, including employees wearing safety vests and helmets, fall detection, and oil or water leaks.
- **Manufacturing -** Focus on people entering the production line.

### Best Practices for setting the focus on prompt

- Use generalized, less explicit phrasing when you describe extreme events. For example, use "physical altercation" instead of "fight."
- We recommend that you use an LLM to describe the focus on. For example:
  - Focus on retail store conditions and customer behaviors, including:
    - Shelf status: Empty shelf, partially empty shelf.
    - Sanitation: Overflowing trash bin, dirty aisle.
    - Crowd and flow: Checkout congestion, crowd density threshold breach, and unattended cart.
    - Environment: Temperature alert in refrigerated sections.
    - Objects and people: Person with shopping cart, child alone, employee uniform, person with mobility aid, customer with pet, person with backpack open, suspicious package, and damaged or open product.
    - Customer actions: Leaving without purchase, returning item to shelf. Hazards: wet floor, liquid spilled.
  - Detect and classify construction site events that present risk to workers or other people nearby:
    - Unsafe or hazardous behavior (for example, improper use of tools, unsafe climbing, and lack of fall protection).
    - Potential accidents or near misses.
    - Violations of construction safety protocols (for example, missing personal protective equipment (PPE) like helmets or harnesses, unsafe proximity to heavy machinery).
    - Unsafe site conditions (for example, cluttered walkways, and unstable structures).
    - Not wearing safety equipment such as safety vest and helmet.

## Limitations

- Results from the summarization feature get created by an AI language model. They're intended to provide a general overview. Although we aim for accuracy and reliability, the content might not fully encapsulate the essence of the original material. We recommend that you review and edit the summary before use. It shouldn't be viewed as professional or personalized advice.
- The summary's results are consistent within each summary style. However, editing the timeframe or rerunning the summary might lead to different results.
- When utilizing summary styles, the Neutral style can occasionally resemble the Formal style, and the Casual style might sometimes include content-related hashtags. Also, in some instances, a "Medium" length summary might be shorter than a "Short" summary.
- Supported video segment lengths for generating a summary range from 1 minute to 6 hours. Short videos or timeframes that have little content might produce potential summarization inaccuracies that can ensue when dealing with a short input.
- The length of the video might influence the level of detail extracted from the video summary. Long videos can result in a high-level (nondetailed) summary.
- The generated summary might contain inaccuracies, such as incorrect identification of gender, age, and other personal characteristics.
- The summary might occasionally include or reference internal instructions provided to it (referred to as "meta-prompt"). It could encompass directives to exclude harmful content.
- The summary might miss or misinterpret short events. The algorithm samples at one frame per second (FPS), it might overlook or inaccurately interpret brief occurrences or ones that fall between sampled frames.
- If the original video contains inappropriate content, the video summarization output extract can be affected in the following ways:
  - It might be incomplete
  - It might contain disclaimers regarding the inappropriate content. In certain instances, it might include the actual inappropriate quotes, which might be presented with or without a disclaimer.
- The summary can show inaccurate timeframes if a camera disconnects and you request a summary for a recorded file that includes the disconnection period. This issue occurs because the timestamps in the video don't align correctly due to the disconnection.

## Generate a summary

1. Select a specific video on demand (VOD) recorded file.
2. Select **Configure and generate** under the player.
3. Write a **Focus on prompt** to specify interesting or unusual events happening in the video to highlight in the summary.
4. Choose the **time range** to summarize from the video. Longer ranges can take several hours to process.
5. Review and then select **Generate summary** to start generating the summary.
6. To regenerate the summary for a different time range, select **Customize summary** and choose a new time range. Do the same actions to edit the focus on prompt and output format.

Here's a screenshot of the Generate summary window in the VI portal:

:::image type="content" source="./media/live-event-summary/generate-summary.png" border="true" alt-text="Screenshot showing the Generate summary window." lightbox="./media/live-event-summary/generate-summary.png" :::

## Related content

- [Watch live video recordings](live-watch-recordings.md)