---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 07/25/2024
ms.author: inhenkel
title: transparency text-based emotion detection
---

## Text-based emotion detection transparency notes

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

## Text-based emotion detection components 

During the emotions detection procedure, the transcript of the video is processed, as follows: 

|Component |Definition |
|---|---|
|Source language |The user uploads the source file for indexing. |
|Transcription API |The audio file is sent to Azure AI services and the translated transcribed output is returned. A language is processed if it's specified. |
|Emotions detection  |Each sentence is sent to the emotions detection model. The model produces the confidence level of each emotion. If the confidence level exceeds a specific threshold, and there's no ambiguity between positive and negative emotions, the emotion is detected. In any other case, the sentence is labeled as neutral.|
|Confidence level |The estimated confidence level of the detected emotions is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score. |
