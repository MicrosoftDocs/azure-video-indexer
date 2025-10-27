---
title: Troubleshoot Azure AI Video Indexer enabled by Arc
description: Troubleshoot common issues with Azure AI Video Indexer enabled by Arc, including connectivity, streaming, and encoding problems.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 10/06/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: troubleshooting-general
# customer intent: As a user of Azure AI Video Indexer enabled by Arc, I want to troubleshoot common issues related to connectivity, streaming, and encoding so that I can resolve them quickly.
---

# Troubleshoot Azure AI Video Indexer enabled by Arc (preview)

Use the following information to troubleshoot issues with Azure AI Video Indexer enabled by Arc.

## Troubleshoot general errors

If you encounter an error while using Azure AI Video Indexer enabled by Arc, check the following issues:

### Video Indexer portal fails to access the extension

*The extension was installed successfully, but Video Indexer portal fails to access the extension.*

There are many reasons that might cause interactions between the Video Indexer portal and the Video Indexer extension, most are network related. For example, connectivity issues and certificate validation issues. Continue reading to determine which issue might be related to accessing the extension.

### Playback has buffering delays

*The playback has buffering delays when streaming from Video Indexer extension.*

This behavior is expected. Media is streamed from the virtual machine (VM) using network streaming. You can either:

- Encode your video to MP4/H264 and AAC audio before indexing, to make network streaming supported across most of the devices/browsers/OS.
- Implement your own streaming server endpoint that does the encoding beforehand or use just-in-time (JIT) encoding.

For example, you could use [ffmpeg](https://ffmpeg.org/) and [Shaka Packager](https://github.com/shaka-project/shaka-packager) to do the encoding preprocessing and the packaging of the encoded file that allows streaming of HLS/DASH protocols. When you use this method, the streamable files can be placed in the storage and the streaming endpoint just serve the files.

## Troubleshoot live analysis issues

Use the following sections to troubleshoot issues with Azure AI Video Indexer enabled by Arc for Live video analysis.

### Error connecting to the extension

:::image type="content" source="./media/azure-video-indexer-enabled-by-arc-troubleshooting/error-reach-arc-extension.png" alt-text="Screenshot showing the Couldn't reach the Arc extension error.":::

If you get an error saying `Couldn't reach the Arc extension`:

- In your browser's URL bar, enter `https://{cluster endpoint URL}/info`
- Select **Advanced** and then select **Continue to {cluster endpoint URL} (unsafe)**.  
    :::image type="content" source="./media/azure-video-indexer-enabled-by-arc-troubleshooting/error-connection-not-private-general.png" alt-text="Screenshot showing the connection not private error (general).":::  

    :::image type="content" source="./media/azure-video-indexer-enabled-by-arc-troubleshooting/error-connection-not-private-details.png" alt-text="Screenshot showing the connection not private error (details).":::

### Error connecting to camera

When a camera fails to connect, it's important to identify the root cause quickly to restore functionality. Use the following steps to diagnose and resolve common camera connection errors in our system.

#### Detect camera failures

You can monitor camera health in two ways:

- Use the **Camera Management tab** – View the status of all connected cameras in the dashboard.  
    :::image type="content" source="./media/azure-video-indexer-enabled-by-arc-troubleshooting/camera-management-tab-details.png" alt-text="Screenshot showing details on the Camera management tab.":::
- Use the **List-Cameras API** – Retrieve detailed information about each camera programmatically, including status and error messages.  
    :::image type="content" source="./media/azure-video-indexer-enabled-by-arc-troubleshooting/camera-management-api-details.png" alt-text="Screenshot showing details from the List-Cameras API.":::
    In the example, there are five cameras configured. Four cameras are listed as `Online` and one camera is in a `Failed` state.

#### Key fields for troubleshooting

For each failed camera, the following fields provide essential diagnostic information:

- `status` – Indicates whether the camera is operational. A failed status means the camera is considered `offline`.
- `errorInfo` – Provides the *error type* and an *error message* explaining why the camera failed.

### Common camera failure situations

Use the following sections to troubleshoot common camera failure situations.

#### RTSP URI unreachable

- **Error message:** `RTSP uri is unreachable, camera not added`
- **Cause:** The RTSP URL provided when creating the camera can't be reached.
- **Resolution:**
  - Verify that the RTSP stream is live and accessible from your network.
  - Since RTSP URLs can't be updated for existing cameras, delete the camera and create a new one with a valid RTSP URL.

#### Heartbeat Not Received

- **Error message:** `PGIE/Recording/Live Streaming heartbeat not received`
- **Cause:** No video frames were processed for more than 2 minutes. It might happen due to:  
  - **Stream interruption** – The camera stopped sending frames, possibly due to network instability or camera crash.
  - **Insufficient space on File Share / Disk** – The disk might be full, preventing new files from being created and frames from being processed.  
  - **Internal DeepStream error** – Rare, but possible due to system issues.
- **Resolution:**
  1. Confirm that the RTSP stream is still active and frames are being transmitted.
  2. In the logs, look for the `gst-resource-error-quark; Could not open resource for writing.` message:  
  3. Next, check the properties field. If it contains `No space left on device`, the information indicates that the file share or disk is full, and you need to increase its volume. You can do so with the following command:  
      ```azurecli
      az k8s-extension update -n $EXTENSION_NAME -g $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --cluster-type $CLUSTER_TYPE --config storage.indexing.size=$STORAGE_SIZE --yes
      ```
  4. Apply a configuration change and then restore it. For example:
    1. Disable **Streaming** for the affected camera.
    2. Re-enable **Streaming**.
    3. The camera status should transition from **Offline > Updating > Online**.
  5. If the issue persists or reoccurs frequently, contact support for assistance.

#### Internal errors

- **Error message:** `An internal error occurred` or other unspecified errors.
- **Resolution:**
  - Apply a configuration toggle as described previously (disable and re-enable one of the features: **Streaming**, **Recording**, or **Preset**).
  - If the problem continues, contact support for assistance.

#### Too many cameras

Each GPU type supports a different number of cameras. If too many cameras are connected, the GPU might not be able to handle the extra streams. For more information about the limits of each GPU, see [Connect cameras to the live extension](../live-add-remove-camera.md#connect-cameras-to-the-live-extension).

### When all cameras are in a failed state

If **all configured cameras** show a failed status:

1. Disable **Streaming**, **Recording**, and **Presets** for all cameras. The actions reset them to an offline state with no active configuration.
2. Wait **at least 5 minutes**.
3. Reapply the required configuration (enable streaming, recording, or presets as needed).
4. If the issue reoccurs after recovery, contact support for assistance and have logs and error details ready.

**Additional Recommendations**

- Retry the previous steps.

### No detections after 5 minutes

If there are no detections reported after more than **5 minutes**, even though objects should be detected, the issue is often related to configuration or GPU compatibility. The following information outlines the most common causes and resolutions.

**Possible Causes and Resolutions**

#### Preset misconfiguration

**Cause:** The preset might be incorrectly configured or applied to the wrong camera. Common issues include:

- Incorrect spelling in **Custom Insights** keywords.
- Applying the preset to the wrong camera.

**Resolution:**

- Review the preset configuration in the UI.
- Confirm that the preset is attached to the correct camera.
- Verify that all custom insight keywords are spelled correctly and match the expected input.

#### GPU compatibility issue

**Cause:** An **incompatible GPU extension** is being used in the cluster. It typically happens in environments with multiple GPU types, where the wrong GPU might be selected if installation wasn't performed correctly.

**Resolution:**

1. Check which GPUs are available in your cluster.
2. Confirm which GPU is being used by the extension. You can do it by executing the following commands:
3. Set the right context with: `kubectl config use-context \$ctx`
4. Set the Video Indexer namespace with: `kubectl config set-context --current --namespace=video-indexer`
5. Get all the pods with: `kubectl get pods`
6. Copy the deepstream pod name and execute with: `kubectl exec -it \$pod -- /bin/bash`
7. Run the following command within the deepstream container: `nvidia-smi`. This command prints the GPU details including GPU type.
8. If there's a mismatch between the intended GPU and the running GPU, update the extension to use the correct GPU with the following **upgrade extension** command:  
    ```azurecli
    az k8s-extension update --cluster-name "${CLUSTER_NAME}" -g "${RG}" --cluster-type connectedClusters -n ${EXTENSION_NAME} --config "ViAi.deepstream.nodeSelector.workload=deepstream"
    ```

#### Other causes

If none of the preceding steps fix the issue, contact support and include details about:

- The affected cameras
- Preset configuration
- GPU information
- Logs covering the last 10 minutes before the issue occurred

#### Other recommendations

- Ensure that the camera stream is stable and actively producing frames.
- If using multiple GPUs, document the mapping of workloads to GPUs for easier troubleshooting.
- Periodically validate presets after upgrades or configuration changes.

Following these checks resolves most "no detection" cases. If detections don't resume, contact **support** with logs and configuration details.

## Related content

- [What is Azure AI Video Indexer enabled by Arc?](azure-video-indexer-enabled-by-arc-overview.md)