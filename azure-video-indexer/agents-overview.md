---
title: "AI Agents for Real-Time Video Analysis in Azure AI Video Indexer"
description: Discover how agentic intelligence uses specialized AI agents to analyze live video streams, offering insights for retail, customer service, security, and more.
#customer intent: As a developer, I want to integrate the API for activating agents so that I can automate live video analysis tasks in my application.
author: cwatson-cat
ms.author: cwatson
ms.reviewer: cwatson
ms.date: 12/21/2025
ms.topic: concept-article
ms.service: azure-video-indexer
ms.collection: ce-skilling-ai-copilot
appliesto: 
- Azure AI Video Indexer enabled by Azure Arc
ai-usage: ai-assisted
---

# AI agents for real-time video analysis in Azure AI Video Indexer

Azure AI Video Indexer (VI) uses specialized AI agents to deliver targeted, real-time insights from live video streams. These agents are modular, task-focused components that automatically analyze video for specific events, conditions, or behaviors such as safety hazards, customer experience problems, or operational anomalies. This article explains the available agents, activating and managing them by using the API, and best practices for integrating agentic intelligence into your video analysis workflows.  

## Agent types and their roles

Real-time analysis in VI uses a modular, agent-based architecture. Each agent performs a specific task. The agents act like AI analysts that look over the video stream and search for specific events in the video. The available agents are:

- **RetailOps agent** monitors the physical condition of retail spaces. It identifies messy shelves, missing stock, and safety hazards like spilled liquids. It helps ensure stores remain safe, clean, and well-stocked throughout the day.
- **Customer service agent** enhances customer experience by detecting forgotten personal items, such as wallets and phones. It measures wait times and flags accessibility problems, such as products placed too high. It supports staff in maintaining a responsive and inclusive environment.
- **Sales recommendations agent** analyzes customer engagement with products and correlates it with real-time sales data. It identifies items that attract attention but don't convert into purchases. It offers actionable insights on placement, pricing, and visual appeal to boost performance.
- **Security agent** safeguards individuals by proactively detecting potential hazards and unsafe conditions. This detection includes identifying signs of smoke or fire, detecting falls, and recognizing risky activities, such as employees in construction areas not following safety protocols.

## Agent requirements

To use agents, make sure your VI extension and environment meet the following requirements:

- On top of the [recommended hardware requirements for VI](live-analysis.md#hardware-requirements), add two GPU NVIDIA A100 or H100 nodes.

- During the extension installation, enable agentic capabilities. For more information, see [Manage Azure AI Video Indexer extensions for real-time analysis](live-extension.md).

  If you already installed the extension, update the extension to support agents by using the following command. Replace the placeholder values with information for your Kubernetes cluster and VI extension:

  ```azurecli
  az k8s-extension update \
    --cluster-type connectedClusters \
    --cluster-name <ARC_CLUSTER_NAME> \
    --resource-group <RESOURCE_GROUP> \
    --name <EXTENSION_NAME> \
    --config "videoIndexer.agents.enabled=true"
  ```

## Managing the agents

You can activate agents only through the API. This section explains how to update, view, and delete agent jobs by using the Azure AI Video Indexer API. It provides the endpoints and methods you need to manage your agents effectively.

### API parameter placeholders

The API endpoints use the following placeholders:

| Placeholder      | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
|`{extension base url}` |The cluster endpoint, either an IP address or DNS name, to use as the API endpoint.|
| `{accountId}`    | The unique ID of your Azure AI Video Indexer account.                       |
| `{agentId}`      | The unique ID of the agent you want to activate.                            |
| `{agentJobId}`   | The unique ID of the agent job created for your request.                    |
| `{chatId}`       | The unique chat session ID for polling agent responses.                     |
| `{cameraId}`     | The unique ID of the camera source, if applicable.                          |
|`{intervallsinSeconds}`|Defines how often (in seconds) the agent runs and checks for the event you described in the prompt. The min value is 10 sec and max is 60 sec|
|`{callbackUrl}`|**Optional parameter** - a web address where the agent sends its output.|
| `{videoId}`      | The unique ID of the video, if applicable to the endpoint.                 |

Replace these placeholders with your actual values when you make API requests.

### Activating agents

To activate an agent, use the Azure AI Video Indexer API to find the agent ID, create an agent job, and receive insights through callback or polling.


Find the agent ID by making the following request:

```http
GET {extension base url}/{accountId}/agents
```

Save the ID of the agent you want to use.

To create an agent job, make the following request:

```http
POST {extension base url}/accounts/{accountId}/agentJobs
```
  Request body example:

  ```json
  {
    "agentId": "{agentId}",
    "name": "demo",
    "description": "Periodic Agent Job",
    "eventName": "itemonfloor2",
    "intervalInSeconds": "{intervalInSeconds}",
    "enabled": true,
    "prompt": "Is there a personal item directly on the FLOOR, in the current video segment? If so, describe the exact place and item and provide recommendations. Answer shortly in a json format: {\\isDetected\\: True if there is a personal item directly on the floor, False if not, \\description\\: item description and its place, \\recommendations\\: recommendations what should be done, \\answer\\: the full answer including recommendations}",
    "callbackUrl": "{callbackUrl}",
    "cameraId":  "{cameraId}"
  }
  ```
  
From the response of the create agent job, you get the `chatId` of this agent job. Keep it to see the agent response.

Use the `callbackUrl` to get the agent response automatically in your own environment or application. The service calls this URL and posts HTTP requests.

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
  GET {extension base url}/{accountId}/chats/{chatId}/messages
  ```

### Editing and deleting an agent

Use these API calls to update, view, and delete an agent:


| Method  | Endpoint                                                                 | Description          |
|---------|--------------------------------------------------------------------------|----------------------|
| PUT     | `{extension base url}/accounts/{accountId}/agentJobs/{agentJobId}`   | Update an agent job |
| DELETE  | `{extension base url}/accounts/{accountId}/agentJobs/{agentJobId}`   | Delete an agent job |
| GET     | `{extension base url}/accounts/{accountId}/agentJobs/{agentJobId}`   | View an agent job   |
| GET     | `{extension base url}/accounts/{accountId}/agentJobs`                | List agent jobs     |

## Best practices

Use these best practices to help agents interpret your intent consistently and produce dependable insights. Write precise prompts, iterate on wording, and state what to include or ignore.

- Be specific and detailed when describing the event you want the agent to detect. For example, instead of “when there's a mess,” use “when there are clothes on the floor or any item lying on the ground.”   

    Some events and requests include a certain level of interpretation. Words like “near,” “far,” and “messy” can be up for interpretation. It helps the agent to have extra emphasis about the appropriate level or resolution of the request. Phrases like “directly on the floor,” “completely empty,” and “ignore minor disarrays and alert only for significant mess or disorder” work well. Using direct framing typically works better than letting the agent determine the degree of interpretation.  

  Treat agent‑job creation as an iterative process. Try different terms, phrases, and wording to refine results and level of detail. 

- If you're unsure which agent type to choose, select the general agent. It automatically determines which specific agent to use for your prompt.

- Use emphasis or exclusions through wording such as “ignore,” “minor,” or “large” to guide how the event should be interpreted.  

## Limitations

While agentic intelligence provides powerful real-time insights, consider these important constraints when using these features. Understanding these limitations can help you set the right expectations and design your workflows for the best results.

- Agents interpret descriptions literally. Providing several levels of detail can improve results. For example, say “a mess is scattered items on the floor” rather than simply “mess.” 

    Vague or relative terms such as “near” or “messy” typically produce inconsistent detection. Specify them more clearly to avoid misinterpretation.  

- Descriptions that rely on object location, missing items, or relative positioning can lead to unreliable detection. 

- Agents might miss quick events.  

## Related content

- [Real-time video analysis in Azure AI Video Indexer](live-analysis.md)
- [Manage Azure AI Video Indexer extensions for real-time analysis](live-extension.md)
- [Azure AI Video Indexer API developer portal](https://api-portal.videoindexer.ai/)