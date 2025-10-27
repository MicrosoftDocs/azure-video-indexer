---
title: Search using Edge Retrieval Augmented Generation (RAG) in Azure Video Indexer
description: Learn how to use Edge RAG for efficient media file exploration in Azure Video Indexer.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 09/29/2025
ms.service: azure-video-indexer
ms.topic: how-to
# customer intent: As an Azure Video Indexer user, I want to search for specific video content using natural language queries and filters.
---

# Search using Edge Retrieval Augmented Generation (RAG) - Preview

You can efficiently explore the media files gallery using natural language queries (VLM based) combined with inline filters. It enables you to search for points of interest within video files, even when visuals aren't predefined, and apply filters to identify specific elements.

Search in Azure AI Video Indexer (VI) supports natural language queries, allowing you to type questions or requests in everyday language. For example, you can search for, *a red car parking in the street yesterday* or *a man with a yellow jacket waiting in the line*, and the search understands your intent and returns relevant video segments from your media files library in VI.

Here's an example showing where to search. The search text used is *Find all the people that appeared in the last day in camera "cctv"*.

:::image type="content" source="./media/live-search-edge-rag/search-example-text.png" alt-text="Screenshot showing the search interface with plain text." lightbox="./media/live-search-edge-rag/search-example-text.png":::

You can also use slash (`/`) to trigger inline filters (for example, `/source`, `/tag`, `/created/`, and `/insight`) to narrow down results. It enhances precision and speeds up query formulation. For example, you can search for `/suitcase` appeared yesterday in `/camera A`.

:::image type="content" source="./media/live-search-edge-rag/search-example-slash-filter.png" alt-text="Screenshot showing a search example with slash filters." lightbox="./media/live-search-edge-rag/search-example-slash-filter.png":::

> [!NOTE]
> To start using this capability, you need to create an **Edge RAG resource** and connect it to **Video Indexer (VI)**. For more information, see [Edge RAG documentation](/azure/azure-arc/edge-rag/overview).

## Use cases

The filters and search functionality empowers video analysts in post events analysis, to efficiently navigate and analyze extensive video libraries. By enabling targeted filtering of video attributes, such as dates, tags, or specific video source, and providing natural language search capabilities, analysts can identify critical moments, use the AI detections to uncover patterns, and craft compelling storytelling. This functionality bridges the gap between raw data and actionable narratives, making it easier for analysts to derive value from every video, ensuring accuracy, and driving impactful decision-making.

Here are some specific intended uses:

- **Modern safety** - Use the search to find camera footage were car park near prohibited area, people around the building yesterday night, person holding phone, and much more.
- **Manufacturing** - The system can provide summaries of recorded videos from live cameras focused on employee safety. It can help find employee with helmet but without a vest, people fall, oil or water leaks, fire, and anomalies in the production line.
- **Retail** - Use the search to identify people with empty basket, leaving the store without products, restricted areas.

## Connect RAG capabilities

For information about integrating Edge RAG into Video Indexer, see [Edge RAG documentation](/azure/azure-arc/edge-rag/overview).

## Best practices for natural language user queries

The following sections cover best practices, suggestions, and caveats that might exist when relying on a natural user query. Some of these query parameters can be explicitly defined using the filters mechanism (when using the `/` character in the search box). Alternatively, you can also define them using natural language.

### Time ranges

Use explicit time references to yield better results. *Soft* time references such as `yesterday`, `last week`, `at noon` might get interpreted broadly or inconsistently. For best results either use `/createdAfter` and `/createdBefore` in the search box, or specify explicit time frames such as:

- `from June 20th 2025` (include the entire day)
- `during April 11 2025 from 08:00 until 13:00`

We advise you to avoid ambiguous dates formats for the search query. They might get misinterpreted by the search. For example, avoid dd/mm mm/dd.

To get the best results, we advise you to detail the time range. For example, `from 2025-08-10 until 2025-08-13`.

### Sources (also known as cameras)

- Sources can get referred to by their UUID, Name, and Description. Best results are achieved by using either UUID or Name.
- If not specified, the default behavior searches all sources available. That said, it might sometimes lead to incomplete results, where only some of the sources are selected. In this case, it's useful to specify the UUIDs using the UI.

### Tags

Phrases such as `tagged as`, `tagged with` often work best to let the system know about specific tags you're interested in.

### Limitations

- The feature currently doesn't support activities. For example, `person running`, `person jumping`, `moving car`, and so on. Search doesn't guarantee quality results.
- Small background objects might get missed or get inconsistently reported when using the search. It's due to the reliance of the search on VectorDB and VLM, both of which might miss small background objects.
- Relative position words might get interpreted inconsistently (`near`, `far`, and so on) and lead to inconsistent results.
- Relative times and inexact times (`yesterday`, `morning`, `noon`, and so on) might get broadly and sometimes inconsistently interpreted.

## Related content

- [Azure AI Video Indexer live analysis overview](live-analysis.md)
- [Watch live video recordings](live-watch-recordings.md)