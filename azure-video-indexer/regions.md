---
title: Find and set your Azure region for API use with Azure AI Video Indexer
description: Learn how to find supported Azure regions for Azure AI Video Indexer and set the correct location for your API calls. Learn more now.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/06/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
ms.custom: references_regions
appliesto:
  - Cloud-based Azure AI Video Indexer
#customer intent: As a developer, I want to know which Azure regions support Azure AI Video Indexer so that I can route my API calls correctly.
---

# Find and set your Azure region for API use

Azure AI Video Indexer APIs contain a **location** parameter that you should set to the Azure region to which the call should be routed. It must be an [Azure region in which Azure AI Video Indexer is available](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all).

## Locations

The `location` parameter must be given the Azure region code name as its value. If you're using Azure AI Video Indexer in preview mode, you should put `"trial"` as the value. `trial` is the default value for the `location` parameter. To find the Azure region code for your account and route your calls correctly, use the Azure portal or run an [Azure CLI](/cli/azure) command.

### Azure portal

1. Sign in on the [Azure AI Video Indexer](https://www.videoindexer.ai/) website.
1. Select **User accounts** from the top-right corner of the page.
1. Find the location of your account in the top-right corner.  
    :::image type="content" source="./media/location/location1.png" border="true" alt-text="Screenshot showing the location of your Azure AI Video Indexer account." lightbox="./media/location/location1.png" :::

###  CLI command

```azurecli-interactive
az account list-locations
```

Once you run the line shown previously, you get a list of all Azure regions. Navigate to the Azure region that has the *displayName* you're looking for, and use its *name* value for the **location** parameter.

For example, for the Azure region West US 2 (the following example), you use `westus2` for the **location** parameter.

```json
   {
      "displayName": "West US 2",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/locations/westus2",
      "latitude": "47.233",
      "longitude": "-119.852",
      "name": "westus2",
      "subscriptionId": null
    }
```

## Related content

- [Azure AI Video Indexer documentation](index.yml)