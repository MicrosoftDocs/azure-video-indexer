---
title: Add or remove cameras for use with the Azure AI Video Indexer live extension - Preview
description: Learn how to create, update, or delete cameras for use with the Azure AI Video Indexer live extension.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 11/05/2025
ms.service: azure-video-indexer
ms.topic: how-to
#customer intent: As a user of Azure AI Video Indexer, I want to add or remove cameras for use with the live extension so that I can enable live video analysis capabilities.
---

# Add or remove cameras for use with the Azure AI Video Indexer live extension - Preview

The Azure AI Video Indexer live extension allows you to connect cameras for live video analysis. This guide provides instructions about how to connect and remove cameras to the Azure AI Video Indexer live extension.

> [!IMPORTANT]
> Before you begin, you must already have the Azure AI Video Indexer live extension deployed in your Azure environment. If you didn't deploy it, see the [Manage live analysis extensions](live-extension.md) article for instructions on creating and managing the extension.

Video Indexer live analysis can operate with or without the **Azure IoT Operations** (AIO) extension. For more information about AIO, see [Deploy Azure IoT Operations to an Arc-enabled Kubernetes cluster](/azure/iot-operations/deploy-iot-ops/howto-deploy-iot-operations).

## Download the vi_cli.sh script file

```bash
# Download the script
curl -fsSL -o vi_cli.sh https://raw.githubusercontent.com/Azure-Samples/azure-video-indexer-samples/refs/heads/live-private-preview/VideoIndexerEnabledByArc/live/vi_cli.sh

# Make it executable
chmod +x ./vi_cli.sh

# View help
./vi_cli.sh -h

# For the first time using the script, please run this command:
./vi_cli.sh check dependencies
```

## Work with the live CLI

The `vi_cli.sh` script provides a comprehensive set of commands to manage Video Indexer and AIO resources. You can interact with the script in three different ways:

- Interactive mode (-it)
  - Guides you through parameter input
  - Prompts for required values
  - Best for beginners
- Command-line arguments
  - Specify all parameters in the command
  - Suitable for automation
  - Requires knowing parameter names
- Environment variables
  - Set common parameters once
  - Reduces command length

### Available environment variables

```bash
export VI_CLUSTER_NAME=""
export VI_CLUSTER_RESOURCE_GROUP=""
export VI_ACCOUNT_NAME=""
export VI_ACCOUNT_RESOURCE_GROUP=""
```

You can combine the approaches. For example:

```bash
export VI_CLUSTER_NAME="<cluster-name>"
./vi_cli.sh create camera --cameraName "<camera-name>" -it
```

### Available commands

| Command             | Description                                             | Example Usage |
| ------------------- | ------------------------------------------------------- | ------------- |
| `check dependencies`| Validates and installs required tools                   | `./vi_cli.sh check dependencies` |
| `create camera`     | Creates a new camera with optional analysis preset      | `./vi_cli.sh create camera -it` |
| `create aep`        | Creates a camera connection profile (AIO only)          | `./vi_cli.sh create aep -y` (AIO only) |
| `create asset`      | Creates stream handling settings (AIO only)             | `./vi_cli.sh create asset -y` (AIO only) |
| `create preset`     | Creates an analysis preset for video processing         | `./vi_cli.sh create preset --presetName "<name>"` |
| `delete camera`     | Removes a camera and its associated resources           | `./vi_cli.sh delete camera -y --cameraId "<id>"` |
| `delete preset`     | Removes an analysis preset configuration                | `./vi_cli.sh delete preset -y --presetId "<id>"` |
| `upgrade extension` | Updates the extension configuration                     | `./vi_cli.sh upgrade extension -it` |
| `show cameras`      | Lists all registered cameras                           | `./vi_cli.sh show cameras -y` |
| `show presets`      | Lists all available analysis presets                   | `./vi_cli.sh show presets -y` |
| `show token`        | Retrieves current access token                         | `./vi_cli.sh show token -y` |
| `show extension`    | Displays current extension settings                    | `./vi_cli.sh show extension -it` |
| `show account`      | Shows Video Indexer account details                    | `./vi_cli.sh show account -it` |

### Command options

| Option                         | Description                                     | Required |
| ----------------------------- | ----------------------------------------------- | -------- |
| `-y`, `--yes`                | Skip confirmation prompts                       | No |
| `-h`, `--help`               | Show command help and examples                  | No |
| `-it`, `--interactive`       | Enable interactive parameter input              | No |
| `-aio`, `--aio-enabled`      | Enable Azure IoT Operations integration         | No |
| `-live`, `--live-enabled`    | Enable live stream capability                   | No |
| `-media`, `--media-enabled`  | Enable media files capability                   | No |
| `--clusterName`              | Name of the cluster                             | Yes ¹ |
| `--clusterResourceGroup`     | Resource group of the cluster                   | Yes ¹ |
| `--accountName`              | Name of the Video Indexer account               | Yes ¹ |
| `--accountResourceGroup`     | Resource group of the Video Indexer account     | Yes ¹ |
| `--cameraName`               | Name of the camera                              | Yes ¹ |
| `--cameraAddress`            | RTSP address of the camera                      | Yes ¹ |
| `--presetName`               | Name of the preset                              | No |
| `--presetId`                 | ID of the preset                                | Yes ¹ |
| `--cameraId`                 | ID of the camera                                | Yes ¹ |
| `--cameraDescription`        | Description of the camera                       | No |
| `--cameraStreamingEnabled`   | Enable streaming for the camera                 | No |
| `--cameraRecordingEnabled`   | Enable recording for the camera                 | No |
| `--cameraUsername`           | Username for camera authentication (AIO only)   | No |
| `--cameraPassword`           | Password for camera authentication (AIO only)   | No |

¹ Required for most commands unless using interactive mode (`-it`)  

>[!NOTE]
> To enter interactive mode, use the `-it` flag with any command, which prompts you for required parameters.

### Prerequisites validation

The script automatically validates:
- Required dependencies (az, jq, curl)
- Azure CLI version (>= 2.64.0)
- Required Azure CLI extensions (azure-iot-ops, connectedk8s, k8s-extension, customlocation)
- Valid Azure sign-in and tokens
- Azure resource provider registration

### Manage the Video Indexer extension

Show current extension settings:

```bash
./vi_cli.sh show extension -it
```

Upgrade current extension settings:

```bash
./vi_cli.sh upgrade extension -it
```

This interactive mode command asks you to:

- Enable Live Stream? (true/false)
- Enable Media Files? (true/false)

Update extension settings (enable both Media Files and Live modes):

```bash
./vi_cli.sh upgrade extension \
--clusterName "<your-cluster-name>" \
--clusterResourceGroup "<your-cluster-resource-group>" \
--accountName "<your-account-name>" \
--accountResourceGroup "<your-account-resource-group>" \
--live-enabled \
--media-enabled
```

## Connect cameras to the live extension

To connect a camera to the Azure AI Video Indexer (VI) live extension, you need to download the vi_cli.sh script file, and then run it with the required parameters. The script allows you to connect cameras to the VI live extension, enabling live video analysis capabilities.

Then choose one of the options to connect the cameras, select the method you prefer:

- Connect your cameras to VI and to Azure IoT Operations (AIO) in the same time.
- Connect your cameras to VI only.

> [!NOTE]
> When connecting cameras to the extension, ensure you don't exceed the specified limit of cameras. The number of supported cameras in one extension depends on the GPU used and the capabilities running on the camera.

| **Scenario \\ GPU**                  | **Cameras per A10 GPU**| **Cameras per V100 GPU** | **Cameras per A100 GPU** | **Cameras per H100 GPU** |
|--------------------------------------|------------------------|--------------------------|--------------------------|--------------------------|
| **Streaming + Recording + Insights** | 6                      | 2                        | 8                        | 11       |
| **Streaming + Insights**             | 7                      | 2                        | 11                       | 12       |
| **Insights Only**                    | 7                      | 2                        | 16                       | 16       |
| **Hard Limit**                       | 8                      | 4                        | 16                       | 16       |

## Connect a camera with AIO

Connecting cameras to VI with AIO requires first to configure the relevant cameras to work with AIO and then create the required AIO assets and asset endpoint profiles. Use the following command to create a camera with full AIO integration.

```bash
./vi_cli.sh create camera -aio -y \
--cameraName "<camera-name>" \
--cameraAddress "<rtsp-camera-address>" \
--presetName "<preset-name>" \
--cameraUsername "<optional-username>" \
--cameraPassword "<optional-password>" \
--clusterName "<cluster-name>" \
--clusterResourceGroup "<cluster-resource-group>" \
--accountName "<account-name>" \
--accountResourceGroup "<account-resource-group>"
```

The preceding command performs the following steps automatically:

1. Creates an asset endpoint profile in AIO
2. Creates an asset in AIO for stream management
3. Creates a video preset in Video Indexer
4. Creates a camera in Video Indexer
5. Links all components together for seamless operation

## Create a camera

There are two recommended ways to create a camera:

- Use interactive mode

   ```bash
   ./vi_cli.sh create camera -it
   ```
   Interactive mode is the simplest option. The script guides you through entering all required parameters.

- Use prefilled parameters

   ```bash
   ./vi_cli.sh create camera --cameraName "<camera-name>" --clusterName "<cluster-name>"
   ```

## Create a camera with a preset

To enable automatic video analysis on your camera, include the `--presetName` parameter when creating the camera. The script  automatically creates a preset that detects:

  - People in the video stream
- Vehicles in the video stream

```bash
./vi_cli.sh create camera -y \
--cameraName "<camera-name>" \
--cameraAddress "<rtsp-camera-address>" \
--presetName "<preset-name>" \
--clusterName "<cluster-name>" \
--clusterResourceGroup "<cluster-resource-group>" \
--accountName "<account-name>" \
--accountResourceGroup "<account-resource-group>"
```

## Disconnect a camera without AIO

To delete a camera, use the following steps:

1. Get the camera ID

   ```bash
   ./vi_cli.sh show cameras -y \
   --clusterName "<cluster-name>" \
   --clusterResourceGroup "<cluster-resource-group>" \
   --accountName "<account-name>" \
   --accountResourceGroup "<account-resource-group>"
   ```

2. Delete using the camera ID

   ```bash
   ./vi_cli.sh delete camera -y \
   --cameraId "<camera-id>" \
   --clusterName "<cluster-name>" \
   --clusterResourceGroup "<cluster-resource-group>" \
   --accountName "<account-name>" \
   --accountResourceGroup "<account-resource-group>"
   ```

## Remove a camera with AIO integration

To remove a camera and all its associated components:

```bash
./vi_cli.sh delete camera -aio -y \
--cameraId "<camera-id>" \
--clusterName "<cluster-name>" \
--clusterResourceGroup "<cluster-resource-group>" \
--accountName "<account-name>" \
--accountResourceGroup "<account-resource-group>"
```

The command removes:

- The asset Endpoint Profile from AIO
- The asset configuration from AIO
- The camera from Video Indexer

All components are deleted in the correct order to ensure clean removal.

## Other commands

Here are some other commands you can use with the vi_cli.sh script:

### List all cameras

```bash
./vi_cli.sh show cameras -y \
--clusterName "<cluster-name>" \
--clusterResourceGroup "<cluster-resource-group>" \
--accountName "<account-name>" \
--accountResourceGroup "<account-resource-group>"
```

### List presets

```bash
./vi_cli.sh show presets -y \
--clusterName "<cluster-name>" \
--clusterResourceGroup "<cluster-resource-group>" \
--accountName "<account-name>" \
--accountResourceGroup "<account-resource-group>"
```

### Show access token

```bash
./vi_cli.sh show token -y \
--clusterName "<cluster-name>" \
--clusterResourceGroup "<cluster-resource-group>" \
--accountName "<account-name>" \
--accountResourceGroup "<account-resource-group>"
```

### Show account details

```bash
./vi_cli.sh show account -y \
--accountName "<account-name>" \
--accountResourceGroup "<account-resource-group>"
```

## Related content

- [Live video analysis in Azure AI Video Indexer](live-analysis.md)
- [Manage live analysis extensions](live-extension.md)
- [Manage live analysis cameras](live-manage-camera.md)