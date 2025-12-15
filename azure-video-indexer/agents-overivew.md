---
title: "Real-time Video Analysis Agents in Azure AI Video Indexer"
description: Discover how agentic intelligence uses specialized AI agents to analyze live video streams, offering insights for retail, customer service, security, and more.
#customer intent: As a developer, I want to integrate the API for activating agents so that I can automate live video analysis tasks in my application.
author: cwatson-cat
ms.author: cwatson
ms.reviewer: cwatson
ms.date: 12/15/2025
ms.topic: concept-article
ms.collection: ce-skilling-ai-copilot
appliesto: 
- Azure AI Video Indexer enabled by Azure Arc
ai-usage: ai-assisted
---

# Agents for real-time video event detection in Azure AI Video Indexer

Azure AI Video Indexer (VI) uses specialized AI agents to deliver targeted, real-time insights from live video streams. These agents are modular, task-focused components that automatically analyze video for specific events, conditions, or behaviors such as safety hazards, customer experience problems, or operational anomalies. This article explains the available agents, activating and managing them by using the API, and best practices for integrating agentic intelligence into your video analysis workflows.  

## Agent types and their roles

Live Video Analysis uses a modular, agent-based architecture. Each agent performs a specific task. The agents act like AI analysts that look over the video stream and search for specific events in the video. The available agents are:

- **RetailOps Agent** monitors the physical condition of retail spaces. It identifies messy shelves, missing stock, and safety hazards like spilled liquids. It helps ensure stores remain safe, clean, and well-stocked throughout the day.
- **Customer Service Agent** enhances customer experience by detecting forgotten personal items, such as wallets and phones. It measures wait times and flags accessibility problems, such as products placed too high. It supports staff in maintaining a responsive and inclusive environment.
- **Sales Recommendations Agent** analyzes customer engagement with products and correlates it with real-time sales data. It identifies items that attract attention but don't convert into purchases. It offers actionable insights on placement, pricing, and visual appeal to boost performance.
- **Security Agent** safeguards individuals by proactively detecting potential hazards and unsafe conditions. This detection includes identifying signs of smoke or fire, detecting falls, and recognizing risky activities, such as employees in construction areas not following safety protocols.
- **Event Investigation Agent** supports incident analysis by mapping interactions between people and objects over time. It helps reconstruct event sequences and understand causality. For example, operators can ask: *“Show me what happened before this machine stopped working.”* 

The following example image shows... 
:::image type="content" source="media/agentic-intelligence-agents-targeted-insights/hazard-detection.png" alt-text="Screenshot of the Agentic Intelligence agents targeted insights dashboard." lightbox="media/agentic-intelligence-agents-targeted-insights/hazard-detection.png"  :::

## Agent requirements

To use agents, make sure your VI extension and environment meet the following requirements:


## Managing the agents by using the API

You can only activate agents by using the API. This section explains how to update, view, and delete agent jobs by using the Azure AI Video Indexer API. It provides the endpoints and methods you need to manage your agents effectively.

### API parameter placeholders

The API endpoints use the following placeholders:

| Placeholder      | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| `{location}`     | The Azure region where your Video Indexer account is located (e.g., `westeurope`, `westus`). |
| `{accountId}`    | The unique ID of your Azure AI Video Indexer account.                       |
| `{agentId}`      | The unique ID of the agent you want to activate.                            |
| `{agentJobId}`   | The unique ID of the agent job created for your request.                    |
| `{chatId}`       | The unique chat session ID for polling agent responses.                     |
| `{cameraId}`     | The unique ID of the camera source, if applicable.                          |
| `{videoId}`      | The unique ID of the video, if applicable to the endpoint.                 |

Replace these placeholders with your actual values when you make API requests.

### Activating agents

To activate an agent, use the Azure AI Video Indexer API to find the agent ID, create an agent job, and receive insights through callback or polling.


Find the agent ID by making the following request:

```http
GET https://api.videoindexer.ai/{location}/Accounts/{accountId}/agents
```

Save the ID of the agent you want to use.

To create an agent job, make the following request:

```http
POST https://api.videoindexer.ai/{location}/Accounts/{accountId}/agentJobs
```
  Request body example:

  ```json
  {
    "agentId": "{agentId}",
    "name": "demo",
    "description": "Periodic Agent Job",
    "eventName": "itemonfloor2",
    "intervalInSeconds": 5,
    "enabled": true,
    "prompt": "Is there a personal item directly on the FLOOR, in the current video segment? If so, describe the exact place and item and provide recommendations. Answer shortly in a json format: {\\isDetected\\: True if there is a personal item directly on the floor, False if not, \\description\\: item description and its place, \\recommendations\\: recommendations what should be done, \\answer\\: the full answer including recommendations}",
    "callbackUrl": "https://webhook-test.com/",
    "cameraId":  "{cameraId}"
  }
  ```

From the response of the create agent job, you get the `{chatId}` of this agent job. Keep it to see the agent response.

Use the `callbackUrl` to get the agent response automatically in your own environment or application. The service calls this URL and posts HTTP calls.

### Receiving the agent response

You can get the agent insights in two ways:

- Automate the receiving of the agent insights by using the callback. The body the callback receives is similar to the following example.


   Example callback response:

   ```json
   {
     "eventName": "Messy Store",
     "cameraId": "{cameraId}",
     "cameraName": "Store Front",
     "agentId": "{agentId}",
     "agentJobId": "{agentJobId}",
     "agentJobName": "Store Monitoring",
     "chatId": "{chatId}",
     "startTime": "2025-10-15T21:02:42Z",
     "endTime": "2025-10-15T21:07:42Z",
     "status": "completed",
     "errorMessage": null,
     "agentResponse": {
       "answer": "Yes, the store appears messy with items scattered on the floor and shelves disorganized. I recommend to send someone to organize the store."
     }
   }
   ```

- Poll the chat ID by running the following API call, replacing the placeholders with your values:

  ```http
  GET https://api.videoindexer.ai/{location}/Accounts/{accountId}/chats/{chatId}/messages
  ```

### Editing and deleting an agent

Use these API calls to update, view, and delete an agent:


| Method  | Endpoint                                                                 | Description          |
|---------|--------------------------------------------------------------------------|----------------------|
| PUT     | `https://api.videoindexer.ai/{location}/Accounts/{accountId}/agentJobs/{agentJobId}`   | Update an agent job |
| DELETE  | `https://api.videoindexer.ai/{location}/Accounts/{accountId}/agentJobs/{agentJobId}`   | Delete an agent job |
| GET     | `https://api.videoindexer.ai/{location}/Accounts/{accountId}/agentJobs/{agentJobId}`   | View an agent job   |
| GET     | `https://api.videoindexer.ai/{location}/Accounts/{accountId}/agentJobs`                | List agent jobs     |

## Best practices

The event investigation agent can operate in two modes for each user input:

- **Current Frame Analysis:** This mode provides fast, single-frame analysis.
- **Video Analysis:** This mode provides slower, more comprehensive temporal analysis.

By default, the agent decides which mode to use based on the user’s query. However, you can guide the agent to use a specific mode by including certain keywords in your prompt:

- To focus on the current frame, add phrases like "in the current frame" or "in the current image."
- To analyze a video segment, use phrases such as "in the video" or "in the clip."

Generally, video analysis over recorded footage is faster than video analysis over live-streamed footage.

## Limitations

While agentic intelligence provides powerful real-time insights, consider these important constraints when using these features. Understanding these limitations can help you set the right expectations and design your workflows for the best results.

- The current frame analysis tool examines only the image currently displayed in the player when you send the user input. Because frame extraction can fluctuate in time, this method isn't reliable for rapidly changing scenes and is best suited for static footage.
- The video analysis tool reviews the last 10 minutes of footage (if available) up to the player’s current timestamp, processing at two frames per second. It can't answer questions about events that occurred more than 10 minutes before the current time marker, nor can it reliably detect rapid changes that require a higher frame rate.
- To analyze a different time interval, you must manually adjust the player’s timeline, and then submit your query.

## Related content

- [Real-time video analysis in Azure AI Video Indexer](live-analysis.md)
- [Manage Azure AI Video Indexer extensions for real-time analysis](live-extension.md)
- [Azure AI Video Indexer API developer portal](https://api-portal.videoindexer.ai/)