---
title: Use network security groups with service tags in Azure AI Video Indexer
description: Learn how to use network security groups with service tags to control access and simplify rule management. Get started now.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/09/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: how-to
#customer intent: As an Azure user, I want to add the VideoIndexer service tag to my NSG rules so that my resources can communicate with Azure AI Video Indexer.
---

# Use network security groups with service tags

Azure AI Video Indexer is a service hosted on Azure. In some cases, the service must interact with other services to index video files. For example, a Storage account. In other cases, the service interacts with services when you orchestrate indexing jobs against Azure AI Video Indexer API endpoint when using your own service hosted on Azure. For example, Azure Kubernetes Service (AKS), Web Apps, Logic Apps, and Functions.

> [!NOTE]
> If you're using the `AzureVideoAnalyzerForMedia` network service tag, you might experience issues with your networking security group. This situation occurs because Azure AI Video Indexer moved to a new security tag label: `VideoIndexer`. To mitigate the problem, remove the old `AzureVideoAnalyzerForMedia` tag from your configuration and deployment scripts. Then, use the `VideoIndexer` tag afterward.

To limit access to your resources on a network level, use [Network security groups with service tags](/azure/virtual-network/service-tags-overview). A service tag represents a group of IP address prefixes from a given Azure service, in this case Azure AI Video Indexer. Microsoft manages the address prefixes grouped by the service tag and automatically updates the service tag as addresses change. This management minimizes the complexity of frequent updates to network security rules by the customer.

> [!NOTE]
> The network security group (NSG) service tags feature isn't available for trial accounts.

## Get started with service tags

Currently, we support the global service tag option for using service tags in your network security groups:

**Use a single global VideoIndexer service tag**: This option opens your virtual network to all IP addresses that the Azure AI Video Indexer service uses across all regions we offer our service. This method allows for all IP addresses owned and used by Azure AI Video Indexer to reach your network resources behind the NSG.

> [!NOTE]
> Currently, Azure AI Video Indexer doesn't support IPs allocated to its services in the Switzerland North Region. If your account is located in this region, you can't use service tags in your NSG today since these IPs aren't in the service tag list. They get rejected by the NSG rule.

## Use a single global Azure AI Video Indexer service tag

The easiest way to begin using service tags with your Azure AI Video Indexer account is to add the global tag `VideoIndexer` to an NSG rule.

1. From the [Azure portal](https://portal.azure.com/), select your network security group.
1. Under **Settings**, select **Inbound security rules**, and then select **+ Add**.
1. From the **Source** drop-down list, select **Service Tag**.
1. From the **Source service tag** drop-down list, select **VideoIndexer**.

:::image type="content" source="./media/network-security/nsg-service-tag-videoindexer.png" alt-text="Screenshot showing how to add a service tag in the Azure portal.":::

This tag contains the IP addresses of Azure AI Video Indexer services for all regions where available. The tag ensures that your resource can communicate with the Azure AI Video Indexer services.

## Using Azure CLI

You can also use Azure CLI to create a new or update an existing NSG rule and add the **VideoIndexer** service tag using the `--source-address-prefixes`. For a full list of CLI commands and parameters, see [az network nsg](/cli/azure/network/nsg/rule?view=azure-cli-latest&preserve-view=true)

Here's an example of a security rule using service tags. For more information, see [Virtual network service tags](https://aka.ms/servicetags)

```azurecli
az network nsg rule create -g MyResourceGroup --nsg-name MyNsg -n MyNsgRuleWithTags --priority 400 --source-address-prefixes VideoIndexer --destination-address-prefixes '*' --destination-port-ranges '*' --direction Inbound --access Allow --protocol Tcp --description "Allow traffic from Video Indexer"
```

## Related content

- [Use private endpoints with Azure AI Video Indexer](private-endpoint-how-to.md)
- [Azure AI Video Indexer documentation](index.yml)