## Optical character recognition (OCR)

[!INCLUDE [ocr description](ocr-description.md)]

OCR extracts insights from printed and handwritten text in over 50 languages, including from an image with text in multiple languages. For more information, see [OCR supported languages](/azure/ai-services/computer-vision/language-support#optical-character-recognition-ocr).

For more information about OCR, see [OCR technology](/azure/ai-services/computer-vision/overview-ocr).

## OCR use cases

- Deep searching media footage for images with signposts, street names, or car license plates, for example, in law enforcement. 
- Extracting text from images in media files and then translating it into multiple languages in labels for accessibility, for example in media or entertainment. 
- Detecting brand names in images and tagging them for translation purposes, for example in advertising and branding. 
- Extracting text in images that is then automatically tagged and categorized for accessibility and future usage, for example to generate content at a news agency. 
- Extracting text in warnings in online instructions and then translating the text to comply with local standards, for example, e-learning instructions for using equipment.

## View the insight JSON with the web portal

After you upload and index a video, download insights in JSON format from the web portal.

1. Select the **Library** tab.
1. Select the media you want.
1. Select **Download**, and then select **Insights (JSON)**. The JSON file opens in a new browser tab.
1. Find the key pair described in the example response.

## Use the API

1. Use a [Get Video Index](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Video-Index) request. Pass `&includeSummarizedInsights=false`.
2. Find the key pairs described in the example response.

## Example response

```json
    "ocr": [
        {
          "id": 1,
          "text": "2017 Ruler",
          "confidence": 0.4365,
          "left": 901,
          "top": 3,
          "width": 80,
          "height": 23,
          "angle": 0,
          "language": "en-US",
          "instances": [
            {
              "adjustedStart": "0:00:45.5",
              "adjustedEnd": "0:00:46",
              "start": "0:00:45.5",
              "end": "0:00:46"
            },
            {
              "adjustedStart": "0:00:55",
              "adjustedEnd": "0:00:55.5",
              "start": "0:00:55",
              "end": "0:00:55.5"
            }
          ]
        },
        {
          "id": 2,
          "text": "2017 Ruler postppu - PowerPoint",
          "confidence": 0.4712,
          "left": 899,
          "top": 4,
          "width": 262,
          "height": 48,
          "angle": 0,
          "language": "en-US",
          "instances": [
            {
              "adjustedStart": "0:00:44.5",
              "adjustedEnd": "0:00:45",
              "start": "0:00:44.5",
              "end": "0:00:45"
            }
          ]
        }
``` 

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

[!INCLUDE [transparency-ocr](transparency-ocr.md)]

## Sample code

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)
