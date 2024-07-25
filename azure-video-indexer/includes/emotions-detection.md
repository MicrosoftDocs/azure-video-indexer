---
title: Text-based emotion detection
ms.service: azure-video-indexer
ms.topic: include
ms.date: 07/25/2024
ms.author: inhenkel
---

## Text-based emotion detection

[!INCLUDE [Emotions detection description](emotions-detection-description.md)]

> [!IMPORTANT]
> The model works on text only (labeling emotions in video transcripts.) This model doesn't infer the emotional state of people, may not perform where input is ambiguous or unclear, like sarcastic remarks. **Thus, the model shouldn't be used for things like assessing employee performance or the emotional state of a person**. 

### Text-based emotion detection use cases

- **Content Creators and Video Editors** - Content creators and video editors can use the system to analyze the emotions expressed in the text transcripts of their videos. The analysis helps them gain insights into the emotional tone of their content, allowing them to fine-tune the narrative, adjust pacing, or ensure the intended emotional impact on the audience.
- **Media Analysts and Researchers** - Media analysts and researchers can employ the system to analyze the emotional content of a large volume of video transcripts quickly. They can use the emotional timeline generated by the system to identify trends, patterns, or emotional responses in specific topics or areas of interest.
- **Marketing and Advertising Professionals** - Marketing and advertising professionals can utilize the system to assess the emotional reception of their campaigns or video advertisements. Understanding the emotions evoked by their content, helps them tailor messages more effectively and gauge the success of their campaigns.
- **Video Consumers and Viewers** - End-users, such as viewers or consumers of video content, can benefit from the system by understanding the emotional context of videos without having to watch them entirely. It's useful for users who want to decide if a video is worth watching or for people with limited time to spare.
- **Entertainment Industry Professionals** - Professionals in the entertainment industry, such as movie producers or directors, can utilize the system to gauge the emotional effect of their film scripts or storylines, aiding in script refinement and audience engagement.

> [!NOTE]
> Text-based emotion detection is language independent, however if the transcript is not in English, it is first being translated to English and only then the model is applied. This may cause a reduced accuracy in emotions detection for non English languages.

[!INCLUDE [get insights with the web portal](get-insights-web-portal.md)]

[!INCLUDE [get insights with the API](get-insights-api.md)]

### [Example response](#tab/emotionresponse) 

```json
"emotions": [ 
  { 
    "id": 1, 
    "type": "Sad", 
    "instances": [ 
      { 
        "confidence": 0.5518, 
        "adjustedStart": "0:00:00", 
        "adjustedEnd": "0:00:05.75", 
        "start": "0:00:00", 
        "end": "0:00:05.75" 
      }

```  

### [Components](#tab/emotioncomponents) 

During the emotions detection procedure, the transcript of the video is processed, as follows: 

|Component |Definition |
|---|---|
|Source language |The user uploads the source file for indexing. |
|Transcription API |The audio file is sent to Azure AI services and the translated transcribed output is returned. A language is processed if it's specified. |
|Emotions detection  |Each sentence is sent to the emotions detection model. The model produces the confidence level of each emotion. If the confidence level exceeds a specific threshold, and there's no ambiguity between positive and negative emotions, the emotion is detected. In any other case, the sentence is labeled as neutral.|
|Confidence level |The estimated confidence level of the detected emotions is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score. |

### [Transparency notes](#tab/emotiontransnote)

[!INCLUDE [General transparency note](read-general-transparency-note.md)]

- This model is designed to help detect emotions in the transcript of a video. However, it isn't suitable for making assessments about an individual's emotional state, their ability, or their overall performance.  
- This emotion detection model is intended to help determine the sentiment behind sentences in the video’s transcript. However, it only works on the text itself, and may not perform well for sarcastic input or in cases where input may be ambiguous or unclear. 
- To increase the accuracy of this model, it is recommended that input data be in a clear and unambiguous format. Users should also note that this model does not have context about input data, which can impact its accuracy.  
- This model can produce both false positives and false negatives. To reduce the likelihood of either, users are advised to follow best practices for input data and preprocessing, and to interpret outputs in the context of other relevant information. It's important to note that the system does not have any context of the input data. 
- The outputs of this model should not be used to make assessments about an individual's emotional state or other human characteristics. This model is supported in English and may not function properly with non-English inputs. Not English inputs are being translated to English before entering the model, therefore may produce less accurate results. 
- The model should not be used to evaluate employee performance and monitoring individuals.
- The model should not be used for making assessments about a person, their emotional state, or their ability.
- The results of the model can be inaccurate, as this is an AI system, and should be treated with caution.
- The confidence of the model in its prediction should also be taken into account.
- Non-english videos will produce less accurate results.

### [Sample code](#tab/emotionsamplecode)

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

---