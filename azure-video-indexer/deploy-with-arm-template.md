---
title: Deploy Azure AI Video Indexer by using an ARM template
description: Learn how to create an Azure AI Video Indexer account by using an Azure Resource Manager (ARM) template.
ms.topic: quickstart
ms.custom: devx-track-arm-template
ms.date: 03/27/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Quickstart: Deploy Azure AI Video Indexer by using an ARM template

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

[!INCLUDE [Gate notice](./includes/face-limited-access.md)]

Using this quickstart, you can create an Azure AI Video Indexer account by using an Azure Resource Manager template.

A [Azure Resource Manager template](/azure/azure-resource-manager/templates/overview) is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration using declarative syntax. You describe your intended deployment without writing the sequence of programming commands to create the deployment.

Once the account is created, you can use the Video Indexer API to interact with the account, upload videos, and get AI Insights. To get started, see [Use Azure AI Video Indexer REST API](/azure/azure-video-indexer/video-indexer-use-apis).


## Deploy the sample

You have two deployment options:

### [Deploy button](#tab/deplybutton)

Select the button for deploying to Azure, and fill in the missing parameters.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fazure-video-indexer-samples%2Fmaster%2FDeploy-Samples%2FArm%2Fvideoindexer.template.json)


### [Deploy with CLI](#tab/deplycli)

Use the Bash environment in Azure Cloud Shell. For more information, see [Quickstart for Bash in Azure Cloud Shell](/azure/cloud-shell/overview).

If you prefer to run CLI reference commands locally, [install](/cli/azure/install-azure-cli) the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see [How to run the Azure CLI in a Docker container](/cli/azure/run-azure-cli-docker). 
 
If you're using a local installation, sign in to the Azure CLI by using the [az login](/cli/azure/reference-index#az-login) command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see [Sign in with the Azure CLI](/cli/azure/authenticate-azure-cli). 

Run [az version](/cli/azure/reference-index?#az-version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/cli/azure/reference-index?#az-upgrade). 

1. Open the [template file](https://github.com/Azure-Samples/azure-video-indexer-samples/blob/master/Deploy-Samples/Arm/videoindexer.template.json) and inspect its contents. 
1. Open the [parameter file](https://github.com/Azure-Samples/azure-video-indexer-samples/blob/master/Deploy-Samples/Arm/videoindexer.parameters.json) and fill in the required parameters (see parameters). 
1. Run the following command: 

    `az group create -n myResourceGroup -l eastus` 

1. Create a new resource group in the same location as your Azure AI Video Indexer account using the `az group` create command:
    
    `az deployment group create --resource-group myResourceGroup --template-file .\videoindexer.template.json --parameters=.\videoindexer.parameters.json`

---

## Parameters

### name

- Type: string
- Description: The name of the new Azure AI Video Indexer account.
- Required: true

### storageAccountName

- Type: string 
- Description: The Name of the storageAccount that will be used by Video Indexer Account. 
- Required: true 

### tags

- Type: object
- Description: The array of objects that represents custom user tags on the Azure AI Video Indexer account.
- Required: false

## Reference documentation

If you're new to Azure AI Video Indexer, see:

- [The Azure AI Video Indexer documentation](./index.yml)
- [The Azure AI Video Indexer API developer portal](https://api-portal.videoindexer.ai/)
- See other [Azure AI Video Indexer samples](https://github.com/Azure-Samples/media-services-video-indexer/blob/master/README.md).

If you're new to template deployment, see:

- [Azure Resource Manager documentation](/azure/azure-resource-manager/)
- [Deploy resources with ARM templates](/azure/azure-resource-manager/templates/deploy-powershell)
- [Deploy resources with Bicep and the Azure CLI](/azure/azure-resource-manager/bicep/deploy-cli)
