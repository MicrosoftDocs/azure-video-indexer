---
title: Azure AI Video Indexer enabled by Azure Arc release notes
description: Stay updated on the latest features, bug fixes, and known issues for Azure AI Video Indexer enabled by Azure Arc.
author: cwatson-cat
ms.author: cwatson
ms.collection: ce-skilling-ai-copilot
ms.date: 05/01/2026
ms.service: azure-video-indexer
ai-usage: ai-assisted
ms.topic: release-notes
appliesto:
  - Azure AI Video Indexer enabled by Azure Arc
#customer intent: As a video content manager using Azure AI Video Indexer enabled by Azure Arc, I want to track the latest features and updates so that I can use new capabilities and plan my workflows.
---

# Azure AI Video Indexer enabled by Azure Arc release notes

This article lists release notes for Azure AI Video Indexer enabled by Azure Arc. For cloud-based Azure AI Video Indexer release notes, see [Azure AI Video Indexer release notes](../release-notes.md).

## March 2026

### Custom AI insights for objects with attributes

Create object insights that match your specific operational needs. Describe objects with attributes in natural language-specify colors, types, conditions, or combinations like "a red classic car" or "person wearing a hard hat." Add example images and negative examples to refine detections and improve accuracy.

For more information, see [Custom insights](live-custom-insights-overview.md).

## January 2026

### Situation custom insight

The situation custom insight enables users to define scenario‑based detections in natural language in addition to the objects that were supported. This capability empowers teams to recognize complex conditions like hazards, anomalies, or operational states in real time. Situation custom insights deliver highly tailored, actionable insights without requiring coding or ML expertise.

For more information, see [Custom insights](live-ai-insights-catalog.md#custom-insights).

## November 2025

### Real-time analysis (preview)

Azure AI Video Indexer enabled by Azure Arc introduces real-time analysis, enabling real-time video intelligence at the edge. Extract actionable insights from live video streams with ultra-low latency and complete data privacy, keeping all video data on-premises. Azure Arc provides centralized management and scalability.

For more information, see [Live video analysis overview](live-analysis.md).

New capabilities in real-time analysis:

- **Agentic intelligence:** Modular, agent-based architecture with specialized AI agents trained to detect specific events. Prebuilt agents support detections such as safety hazards, customer experience issues, or operational anomalies. Use the API to trigger an agent and provide instructions for the events you want to detect. You don't need to know which agent is best for the task. Azure AI Video Indexer routes the queries to the appropriate agent.

- **Custom AI insights with natural language:** Define custom detection logic using natural language to monitor specific objects. No technical expertise required. Describe what you want to detect and upload supporting images or negative examples to fine-tune detection. Available through both API and portal.

- **Event summarization:** Generate end-of-shift summaries with your own focus, to get a textual summary from your video footage. Help teams quickly review key events and operational outcomes.

- **Area of interest:** Define specific regions within the video frame where you want to focus on the analysis.

For more information, see the following articles:

- [Real-time video analysis overview](live-analysis.md)
- [Manage real-time analysis extensions](live-extension.md)
- [Create custom insights](live-ai-insights-catalog.md)
- [Create an event summary for camera footage](live-event-summary.md)
- [Mark an area of interest](live-area-interest.md)

## March 2025

### General availability of Azure AI Video Indexer enabled by Arc

Azure AI Video Indexer enabled by Arc is now generally available. Now, you can run Video Indexer in your edge environment to generate audio and video insights and textual summaries on videos in more than 30 source languages. For more information, see [Azure AI Video Indexer enabled by Arc overview](azure-video-indexer-enabled-by-arc-overview.md).
