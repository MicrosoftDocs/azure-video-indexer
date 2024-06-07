---
title: Azure AI Video Indexer optical character recognition (OCR) overview 
titleSuffix: Azure AI Video Indexer 
description: An introduction to Azure AI Video Indexer optical character recognition (OCR) component responsibly.
ms.date: 03/22/2024
ms.topic: article
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Optical character recognition (OCR)

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

Optical character recognition (OCR) is an Azure AI Video Indexer AI feature that extracts text from images like pictures, street signs and products in media files to create insights.  

OCR currently extracts insights from printed and handwritten text in over 50 languages, including from an image with text in multiple languages. For more information, see [OCR supported languages](/azure/ai-services/computer-vision/language-support#optical-character-recognition-ocr).    

## Prerequisites  

Review [transparency note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context) 

## View the insight

When working on the website the insights are displayed in the **Timeline** tab. They can also be generated in a categorized list in a JSON file that includes the ID, transcribed text, duration and confidence score.  

To see the instances on the website, do the following: 

1. Go to View and check OCR.  
1. Select Timeline to display the extracted text. 

Insights can also be generated in a categorized list in a JSON file that includes the ID, language, text together with each instance’s confidence score.  

To see  the insights in a JSON file, do the following: 

1. Select Download -> Insight (JSON).  
1. Copy the `ocr` element, under `insights`, and paste it into your online JSON viewer. 
    
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
        },
    ```
    
To download the JSON file via the API, use the [Azure AI Video Indexer developer portal](https://api-portal.videoindexer.ai/). 

## OCR components 

During the OCR procedure, text images in a media file are processed, as follows:  

|Component|Definition|
|---|---|
|Source file|	The user uploads the source file for indexing.|
|Read model	|Images are detected in the media file and text is then extracted and analyzed by Azure AI services. |
|Get read results model	|The output of the extracted text is displayed in a JSON file.|
|Confidence value|	The estimated confidence level of each word is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty will be represented as an 0.82 score.|

For more information, see [OCR technology](/azure/ai-services/computer-vision/overview-ocr). 

## Example use cases 

- Deep searching media footage for images with signposts, street names or car license plates, for example, in law enforcement. 
- Extracting text from images in media files and then translating it into multiple languages in labels for accessibility, for example in media or entertainment. 
- Detecting brand names in images and tagging them for translation purposes, for example in advertising and branding. 
- Extracting text in images that is then automatically tagged and categorized for accessibility and future usage, for example to generate content at a news agency. 
- Extracting text in warnings in online instructions and then translating the text to comply with local standards, for example, e-learning instructions for using equipment.     

## Considerations and limitations when choosing a use case 

- Video Indexer has an OCR limit of 50,000 words per indexed video. Once the limit has been reached, no additional OCR results are generated.
- Carefully consider the accuracy of the results, to promote more accurate detections, check the quality of the image, low quality images might impact the detected insights.  
- Carefully consider when using for law enforcement that OCR can potentially misread or not detect parts of the text. To ensure fair and high-quality decisions, combine OCR-based automation with human oversight. 
- When extracting handwritten text, avoid using the OCR results of signatures that are hard to read for both humans and machines. A better way to use OCR is to use it for detecting the presence of a signature for further analysis. 
- Don't use OCR for decisions that may have serious adverse impacts. Machine learning models that extract text can result in undetected or incorrect text output. Decisions based on incorrect output could have serious adverse impacts. Additionally, it's advisable to include human review of decisions that have the potential for serious impacts on individuals. 

## Learn more about OCR

- [Azure AI services documentation](/azure/ai-services/computer-vision/overview-ocr)
- [Transparency note](/legal/cognitive-services/computer-vision/ocr-transparency-note)  
- [Use cases](/legal/cognitive-services/computer-vision/ocr-transparency-note#example-use-cases) 
- [Capabilities and limitations](/legal/cognitive-services/computer-vision/ocr-characteristics-and-limitations) 
- [Guidance for integration and responsible use with OCR technology](/legal/cognitive-services/computer-vision/ocr-guidance-integration-responsible-use)
- [Data, privacy and security](/legal/cognitive-services/computer-vision/ocr-data-privacy-security)
- [Meter: WER](/legal/cognitive-services/computer-vision/ocr-characteristics-and-limitations#word-level-accuracy-measure)  
