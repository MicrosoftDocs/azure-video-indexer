---
title: "Agentic Intelligence: Live Video Analysis Agents Overview"
description: Discover how Agentic Intelligence uses specialized AI agents to analyze live video streams, offering insights for retail, customer service, security, and more.
#customer intent: As a developer, I want to integrate the API for activating agents so that I can automate live video analysis tasks in my application.
author: cwatson-cat
ms.author: cwatson
ms.reviewer: cwatson
ms.date: 12/12/2025
ms.topic: concept-article
ms.collection: ce-skilling-ai-copilot
ms.service: azure-video-indexer
appliesto: 
- Azure AI Video Indexer enabled by Azure Arc
- ai-usage: ai-assisted
---

# Agentic intelligence: Specialized agents for targeted insights - preview

Live Video Analysis uses a modular, agent-based architecture. Each agent performs a specific task. The agents act like AI analysts that look over the video stream and search for specific events in the video. The available agents are:

- **RetailOps Agent** monitors the physical condition of retail spaces. It identifies messy shelves, missing stock, and safety hazards like spilled liquids. It helps ensure stores remain safe, clean, and well-stocked throughout the day.
- **Customer Service Agent** enhances customer experience by detecting forgotten personal items, such as wallets and phones. It measures wait times and flags accessibility issues, such as products placed too high. It supports staff in maintaining a responsive and inclusive environment.
- **Sales Recommendations Agent** analyzes customer engagement with products and correlates it with real-time sales data. It identifies items that attract attention but don't convert into purchases. It offers actionable insights on placement, pricing, and visual appeal to boost performance.
- **Security Agent** safeguards individuals by proactively detecting potential hazards and unsafe conditions. This detection includes identifying signs of smoke or fire, detecting falls, and recognizing risky activities, such as employees in construction areas not following safety protocols.
- **Event Investigation Agent** supports incident analysis by mapping interactions between people and objects over time. It helps reconstruct event sequences and understand causality. For example, operators can ask: *“Show me what happened before this machine stopped working.”* 

The following example image shows... 
:::image type="content" source="media/agentic-intelligence-agents-targeted-insights/hazard-detection.png" alt-text="Screenshot of the Agentic Intelligence agents targeted insights dashboard." lightbox="media/agentic-intelligence-agents-targeted-insights/hazard-detection.png"  :::

## Prerequisites for using Agents in Video indexer live video analysis

To start using the agent, make sure your extension and environment follow these requirements: ...

## Activating the agent

Activate by using the API.

1. Find the agent ID by running the following command:

   `Get <extension base url>/<account_id>/agents`

   Save the ID of the agent you want to use.

1. Create -  Post `<extension base url>/accounts/<account_id>/agentJobs`

   Body:

   ```json
   {
       "agentId": "<agent ID>",
       "name": "demo",
       "description": "Periodic Agent Job",
       "eventName": "itemonfloor2",
       "intervalInSeconds": 5,
       "enabled": true,
       "prompt": "Is there a personal item directly on the FLOOR, in the current video segment? If so, describe the exact place and item and provide recommendations. Answer shortly in a json format: {\\isDetected\\: True if there is a personal item directly on the floor, False if not, \\description\\: item description and its place, \\recommendations\\: recommendations what should be done, \\answer\\: the full answer including recommendations}",
       "callbackUrl": "<https://webhook-test.com/%22>",
       "cameraId":  "<camera ID>"
   }
   ```

   From the response of the create agent job, you will get the chat ID of this agent job. Keep it to see the agent response

   From the response of the create agent job, you get the chat ID of this agent job. Keep it to see the agent response.

   Use the `callbackUrl` to get the agent response automatically in your own environment or application. The service calls this URL and posts HTTP calls.

## Receiving the agent response

There are two ways to get the agent insights:

- Automate the receiving of the agent insights by using the callback. The body the callback received is:

   ```json
   {
     "eventName": "Messy Store",
     "cameraId": "camera-456",
     "cameraName": "Store Front",
     "agentId": "<agent id>",
     "agentJobId": "123e4567-e89b-12d3-a456-426614174000",
     "agentJobName": "Store Monitoring",
     "chatId": "chat-789",
     "startTime": "2025-10-15T21:02:42Z",
     "endTime": "2025-10-15T21:07:42Z",
     "status": "completed",
     "errorMessage": null,
     "agentResponse":
       {
         "answer": "Yes, the store appears messy with items scattered on the floor and shelves disorganized. I recommend to send someone tp organize the store."
       }
   }
   ```

- Poll the chat Id by running the following API call:

   To see the agent output using the chat ID- `GET <extension base url>/<account_id>/chats/<chat id>/messages`

## Editing and deleting an Agent

Use these API calls to update, view, and delete an agent:

| Method  | Endpoint   | Description    |
|---------|-------------|--------------|
| PUT     | `<extension base url>/accounts/<account_id>/agentJobs/<agent job ID>`   | Update an agent job |
| DELETE  | `<extension base url>/accounts/<account_id>/agentJobs/<agent job ID>`   | Delete an agent job |
| GET     | `<extension base url>/accounts/<account_id>/agentJobs/<agent job ID>`   | View an agent job   |
| GET     | `<extension base url>/accounts/<account_id>/agentJobs`                  | List agent jobs     |

## Best practices

The event investigation agent can operate in two modes for each user input:

- **Current Frame Analysis:** This mode provides fast, single-frame analysis.
- **Video Analysis:** This mode provides slower, more comprehensive temporal analysis.

By default, the agent decides which mode to use based on the user’s query. However, the user can guide the agent to use a specific mode by including certain keywords in their prompt:

- To focus on the current frame, add phrases like "in the current frame" or "in the current image."
- To analyze a video segment, use phrases such as "in the video" or "in the clip."

Generally, video analysis over recorded footage is faster than video analysis over live-streamed footage.


## Limitations

While agentic intelligence provides powerful real-time insights, there are important constraints to consider when using these features. Understanding these limitations can help you set the right expectations and design your workflows for the best results.

- The current frame analysis tool examines only the image currently displayed in the player when you send the user input. Because frame extraction can fluctuate in time, this method isn't reliable for rapidly changing scenes and is best suited for static footage.
- The video analysis tool reviews the last 10 minutes of footage (if available) up to the player’s current timestamp, processing at 2 frames per second. It can't answer questions about events that occurred more than 10 minutes before the current time marker, nor can it reliably detect rapid changes that require a higher frame rate.
- To analyze a different time interval, you must manually adjust the player’s timeline and then submit your query.

## Related content

- [Real-time video analysis in Azure AI Video Indexer](live-analysis.md)
- [Manage Azure AI Video Indexer extensions for real-time analysis](live-extension.md)


