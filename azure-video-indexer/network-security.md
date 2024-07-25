---
title: How to enable network security
description: This article gives an overview of the Azure AI Video Indexer  network security options.
ms.topic: article
ms.custom: devx-track-azurecli
ms.date: 03/22/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# NSG service tags for Azure AI Video Indexer

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-abbreviated.md)]

Azure AI Video Indexer is a service hosted on Azure. In some cases, the service must interact with other services to index video files (for example, a Storage account) or when you orchestrate indexing jobs against Azure AI Video Indexer API endpoint using your own service hosted on Azure (for example, AKS, Web Apps, Logic Apps, Functions).

> [!NOTE]
> If you are already using "AzureVideoAnalyzerForMedia" Network Service Tag you may experience issues with your networking security group starting 9 January 2023. This is because we are moving to a new Security Tag label "VideoIndexer". The mitigatation is to remove the old "AzureVideoAnalyzerForMedia" tag from your configuration and deployment scripts and start using the "VideoIndexer" tag going forward.

Use [Network Security Groups with Service Tags](/azure/virtual-network/service-tags-overview) to limit access to your resources on a network level. A service tag represents a group of IP address prefixes from a given Azure service, in this case Azure AI Video Indexer. Microsoft manages the address prefixes grouped by the service tag and automatically updates the service tag as addresses change. This management minimizes the complexity of frequent updates to network security rules by the customer.

> [!NOTE]
> The NSG service tags feature is not available for trial accounts. To update to an ARM account, see the [Update your Azure AI Video Indexer account](update-your-azure-video-indexer-account-and-migrate-assets.md) or [Import content from a trial account](import-content-from-trial.md).

## Get started with service tags

Currently we support the global service tag option for using service tags in your network security groups:

**Use a single global VideoIndexer service tag**: This option opens your virtual network to all IP addresses that the Azure AI Video Indexer service uses across all regions we offer our service. This method allows for all IP addresses owned and used by Azure AI Video Indexer to reach your network resources behind the NSG.

> [!NOTE]
> Currently we do not support IPs allocated to our services in the Switzerland North Region. These will be added soon. If your account is located in this region you cannot use Service Tags in your NSG today since these IPs are not in the Service Tag list and will be rejected by the NSG rule.

## Use a single global Azure AI Video Indexer service tag

The easiest way to begin using service tags with your Azure AI Video Indexer account is to add the global tag `VideoIndexer` to an NSG rule.

1. From the [Azure portal](https://portal.azure.com/), select your network security group.
1. Under **Settings**, select **Inbound security rules**, and then select **+ Add**.
1. From the **Source** drop-down list, select **Service Tag**.
1. From the **Source service tag** drop-down list, select **VideoIndexer**.

:::image type="content" source="./media/network-security/nsg-service-tag-videoindexer.png" alt-text="Add a service tag from the Azure portal":::

This tag contains the IP addresses of Azure AI Video Indexer services for all regions where available. The tag ensures that your resource can communicate with the Azure AI Video Indexer services.

## Using Azure CLI

You can also use Azure CLI to create a new or update an existing NSG rule and add the **VideoIndexer** service tag using the `--source-address-prefixes`. For a full list of CLI commands and parameters, see [az network nsg](/cli/azure/network/nsg/rule?view=azure-cli-latest&preserve-view=true)

Example of a security rule using service tags. For more details, visit https://aka.ms/servicetags

`az network nsg rule create -g MyResourceGroup --nsg-name MyNsg -n MyNsgRuleWithTags --priority 400 --source-address-prefixes VideoIndexer --destination-address-prefixes '*' --destination-port-ranges '*' --direction Inbound --access Allow --protocol Tcp --description "Allow traffic from Video Indexer"`
