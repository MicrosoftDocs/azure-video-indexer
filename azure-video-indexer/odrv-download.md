---
title: Index videos stored on OneDrive - Azure AI Video Indexer
description: Learn how to index videos stored on OneDrive by using Azure AI Video Indexer.
ms.topic: article
ms.date: 03/22/2024
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Index your videos stored on OneDrive

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

This article shows how to index videos stored on OneDrive by using the Azure AI Video Indexer website.

## Supported file formats

For a list of file formats that you can use with Azure AI Video Indexer, see [Standard Encoder formats and codecs](/azure/media-services/latest/encode-media-encoder-standard-formats-reference).

## Index a video by using the website

1. Sign into the [Azure AI Video Indexer](https://www.videoindexer.ai/) website, and then select **Upload**.

   > [!div class="mx-imgBorder"]
   > :::image type="content" source="./media/video-indexer-get-started/video-indexer-upload.png" alt-text="Screenshot that shows the Upload button.":::

1. Click on **enter a file URL** button
   > [!div class="mx-imgBorder"]
   > :::image type="content" source="./media/video-indexer-get-started/avam-enter-file-url.png" alt-text="Screenshot that shows the enter file URL button.":::

1. Next, go to your video/audio file located on your OneDrive using a web browser. Select the file you want to index, at the top select **embed**
   > [!div class="mx-imgBorder"]
   > :::image type="content" source="./media/video-indexer-get-started/avam-odrv-embed.png" alt-text="Screenshot that shows the embed code button.":::

1. On the right click on **Generate** to generate an embed url.
   > [!div class="mx-imgBorder"]
   > :::image type="content" source="./media/video-indexer-get-started/avam-odrv-embed-generate.png" alt-text="Screenshot that shows the embed code generate button.":::

1. Copy the embed code and extract only the URL part including the key. For example:

   `https://onedrive.live.com/embed?cid=5BC591B7C713B04F&resid=5DC518B6B713C40F%2110126&authkey=HnsodidN_50oA3lLfk`

   Replace **embed** with **download**. You will now have a url that looks like this:

   `https://onedrive.live.com/download?cid=5BC591B7C713B04F&resid=5DC518B6B713C40F%2110126&authkey=HnsodidN_50oA3lLfk`

1. Now enter this URL in the Azure AI Video Indexer website in the URL field.

   > [!div class="mx-imgBorder"]
   > :::image type="content" source="./media/video-indexer-get-started/avam-odrv-url.png" alt-text="Screenshot that shows the onedrive url field.":::

After your video is downloaded from OneDrive, Azure AI Video Indexer starts indexing and analyzing the video.

> [!div class="mx-imgBorder"]
> :::image type="content" source="./media/video-indexer-get-started/progress.png" alt-text="Screenshot that shows the progress of an upload.":::

Once Azure AI Video Indexer is done analyzing, you will receive an email with a link to your indexed video. The email also includes a short description of what was found in your video (for example: people, topics, optical character recognition).

## Upload and index a video by using the API

You can use the [Upload Video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video) API to upload and index your videos based on a URL. The code sample that follows includes the commented-out code that shows how to upload the byte array.

### Configurations and parameters

This section describes some of the optional parameters and when to set them. For the most up-to-date info about parameters, see the [Azure AI Video Indexer API developer portal](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video).

#### externalID

Use this parameter to specify an ID that will be associated with the video. The ID can be applied to integration into an external video content management (VCM) system. The videos that are in the Azure AI Video Indexer website can be searched via the specified external ID.

#### callbackUrl

Use this parameter to specify a callback URL.

[!INCLUDE [callback url](./includes/callback-url.md)]

Azure AI Video Indexer returns any existing parameters provided in the original URL. The URL must be encoded.

#### indexingPreset

Use this parameter to define an AI bundle that you want to apply on your audio or video file. This parameter is used to configure the indexing process. You can specify the following values:

- `AudioOnly`: Index and extract insights by using audio only (ignoring video).
- `VideoOnly`: Index and extract insights by using video only (ignoring audio).
- `Default`: Index and extract insights by using both audio and video.
- `DefaultWithNoiseReduction`: Index and extract insights from both audio and video, while applying noise reduction algorithms on the audio stream.

    The `DefaultWithNoiseReduction` value is now mapped to a default preset (deprecated).
- `BasicAudio`: Index and extract insights by using audio only (ignoring video). Include only basic audio features (transcription, translation, formatting of output captions and subtitles).
- `AdvancedAudio`: Index and extract insights by using audio only (ignoring video). Include advanced audio features (such as audio event detection) in addition to the standard audio analysis.
- `AdvancedVideo`: Index and extract insights by using video only (ignoring audio). Include advanced video features (such as observed people tracing) in addition to the standard video analysis.
- `AdvancedVideoAndAudio`: Index and extract insights by using both advanced audio and advanced video analysis.

Azure AI Video Indexer covers up to two tracks of audio. If the file has more audio tracks, they're treated as one track. If you want to index the tracks separately, you need to extract the relevant audio file and index it as `AudioOnly`.

Price depends on the selected indexing option. For more information, see [Media Services pricing](https://azure.microsoft.com/pricing/details/media-services/).

#### priority

Azure AI Video Indexer indexes videos according to their priority. Use the `priority` parameter to specify the index priority. The following values are valid: `Low`, `Normal` (default), and `High`.

This parameter is supported only for paid accounts.

#### streamingPreset

After your video is uploaded, Azure AI Video Indexer optionally encodes the video. It then proceeds to indexing and analyzing the video. When Azure AI Video Indexer is done analyzing, you get a notification with the video ID.

When you're using the [Upload Video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Upload-Video) or [Re-Index Video](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Re-Index-Video) API, one of the optional parameters is `streamingPreset`. If you set `streamingPreset` to `Default`, `SingleBitrate`, or `AdaptiveBitrate`, the encoding process is triggered.

After the indexing and encoding jobs are done, the video is published so you can also stream your video. The streaming endpoint from which you want to stream the video must be in the **Running** state.

For `SingleBitrate`, the standard encoder cost will apply for the output. If the video height is greater than or equal to 720, Azure AI Video Indexer encodes it as 1280 x 720. Otherwise, it's encoded as 640 x 468.
The default setting is [content-aware encoding](/azure/media-services/latest/encode-content-aware-concept).

If you only want to index your video and not encode it, set `streamingPreset` to `NoStreaming`.

#### videoUrl

This parameter specifies the URL of the video or audio file to be indexed. If the `videoUrl` parameter is not specified, Azure AI Video Indexer expects you to pass the file as multipart/form body content.

### Code sample

See the [sample repo](https://github.com/Azure-Samples/media-services-video-indexer/blob/master/API-Samples/C%23/ArmBased/Program.cs) for a code sample.

### Common errors

The upload operation might return the following status codes:

|Status code|ErrorType (in response body)|Description|
|---|---|---|
|409|VIDEO_INDEXING_IN_PROGRESS|The same video is already being processed in this account.|
|400|VIDEO_ALREADY_FAILED|The same video failed to process in this account less than 2 hours ago. API clients should wait at least 2 hours before reuploading a video.|
|429||Trial accounts are allowed 5 uploads per minute. Paid accounts are allowed 50 uploads per minute.|

## Uploading considerations and limitations

- The name of a video must be no more than 80 characters.
- When you're uploading a video based on the URL (preferred), the endpoint must be secured with TLS 1.2 or later.
- The upload size with the URL option is limited to 30 GB.
- The length of the request URL is limited to 6,144 characters. The length of the query string URL is limited to 4,096 characters.
- The upload size with the byte array option is limited to 2 GB.
- The byte array option times out after 30 minutes.
- The URL provided in the `videoURL` parameter must be encoded.
- Indexing Media Services assets has the same limitation as indexing from a URL.
- Azure AI Video Indexer has a duration limit of 4 hours for a single file.
- The URL must be accessible (for example, a public URL).

  If it's a private URL, the access token must be provided in the request.
- The URL must point to a valid media file and not to a webpage, such as a link to the `www.youtube.com` page.
- In a paid account, you can upload up to 50 movies per minute. In a trial account, you can upload up to 5 movies per minute.

> [!Tip]
> We recommend that you use .NET Framework version 4.6.2. or later, because older .NET Framework versions don't default to TLS 1.2.
>
> If you must use an older .NET Framework version, add one line to your code before making the REST API call:
>
> `System.Net.ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls | SecurityProtocolType.Tls11 | SecurityProtocolType.Tls12;`

<!--
## Firewall

For information about a storage account that's behind a firewall, see the [FAQ](faq.yml#can-a-storage-account-connected-to-the-media-services-account-be-behind-a-firewall).
-->
