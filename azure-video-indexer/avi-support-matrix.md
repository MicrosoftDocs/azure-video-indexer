---
title: Azure AI Video Indexer support matrix and service limits
description: Learn about supported formats, file size and duration limits, languages, optical character recognition, projects, person models, and codecs in Azure AI Video Indexer.
author: bandersmsft
ms.author: banders
ms.collection: ce-skilling-ai-copilot
ms.date: 06/09/2025
ms.update-cycle: 180-days
ms.service: azure-video-indexer
ms.topic: concept-article
# customer intent: As a user of Azure AI Video Indexer, I want to understand the supported formats and limitations of the service, so that I can effectively use it for my video indexing needs.
---

# Azure AI Video Indexer support matrix and service limits

This article describes the supported formats and limitations of Azure AI Video Indexer.

## Upload file size and video duration

When you upload a video to Azure AI Video Indexer, there are limits on the file size and video duration based on the preset you choose. The following sections explain the limits:

### File size limits

If uploading a file from your device, the file size limit is 2 GB.

If the video is uploaded from a URL, the file size limit is 30 GB. The URL must lead to an online media file with a media file extension (for example `myvideo.MP4`) and not a webpage such as `https://www.youtube.com`.

### File duration limit

The file duration limit is 6 hours for all presets with the exclusion of the Basic Audio preset which has a file duration limit of 12 hours. 

> [!NOTE]
> Recordings that are less than 2 seconds in duration could fail to index.

## Index request limit

When you upload and index through the VI website, you can index up to 10 videos in a single request. When you submit requests through the API, there's an API request limit of 10 requests per second and up to 120 requests per minute.

## Languages

See our [Language support article](language-support.md) for the list of languages supported.

When you use single or multi language detection, there's a limit of 10 languages allowed for identification during the indexing of a media file. You can select the 10 languages.

## Optical character recognition (OCR)

Video Indexer has an OCR limit of 50,000 words per indexed video. Once the limit is reached, no more OCR results are generated.

## Projects

The number of source files in a Project is limited to 10 when using the website and 100 when using the API.

## Custom person models

Each Person model supports up to 1 million people and each VI account can have up to 50 Person models.

## Logo detection

A logo group can contain up to 50 logos.

## Supported file formats

Azure AI Video Indexer supports the following file formats:

| File formats (file extensions)                        |
| :---------------------------------------------------- |
| FLV (with H.264 and AAC codecs) (.flv)                |
| MXF (.mxf)                                            |
| GXF (.gxf)                                            |
| MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg) |
| Windows Media Video (WMV)/ASF (.wmv, .asf)            |
| AVI (Uncompressed 8bit/10bit) (.avi)                  |
| MP4 (.mp4, .m4a, .m4v)/ISMV (.isma, .ismv)            |
| Microsoft Digital Video Recording (DVR-MS) (.dvr-ms)  |
| Matroska (.mkv)                                       |
| WAVE/WAV (.wav)                                       |
| QuickTime (.mov)                                      |

## Supported input video codecs

| Input video codecs                                                       |
|--------------------------------------------------------------------------|
| AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra, 8 bit 4:2:0 and 4:2:2 |
| Sony XAVC / XAVC S (in MXF container)                                    |
| Avid DNxHD (in MXF container)                                            |
| DVCPro/DVCProHD (in MXF container)                                       |
| Digital video (DV) (in AVI files)                                        |
| JPEG 2000                                                                |
| MPEG-2 (up to 422 Profile and High Level; including variants such as Sony XDCAM, Sony XDCAM HD, Sony XDCAM IMX, CableLabs®, and D10), up to 420 profiles                                   |
| MPEG-1                                                                   |
| VC-1/WMV9                                                                |
| MPEG-4 Part 2                                                            |
| Theora                                                                   |
| YUV420 uncompressed, or mezzanine                                        |
| HEVC/H.265 Main Profile                                                  |

## Supported input audio codecs

| Input Audio Codecs                            |
|-----------------------------------------------|
| AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1) |
| MPEG Layer 2                                  |
| MP3 (MPEG-1 Audio Layer 3)                    |
| Windows Media Audio                           |
| WAV/PCM                                       |
| FLAC                                          |
| Opus                                          |
| Vorbis                                        |
| AMR (adaptive multi-rate)                     |

## Output format

Videos are transcoded to a single format and resolution (720p), mp4 H254 for video and AAC for audio.

## Related content

- [Azure AI Video Indexer documentation](index.yml).