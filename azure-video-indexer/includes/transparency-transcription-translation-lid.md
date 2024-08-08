---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 08/08/2024
ms.author: inhenkel
title: transparency transcription and language identification
---

## Transcription, translation and language identification

When used responsibly and carefully, Azure AI Video Indexer is a valuable tool for many industries. To respect the privacy and safety of others, and to comply with local and global regulations, we recommend:   

- Carefully consider the accuracy of the results, to promote more accurate data, check the quality of the audio, low quality audio might impact the detected insights.  
- Video Indexer doesn't perform speaker recognition so speakers aren't assigned an identifier across multiple files. You're unable to search for an individual speaker in multiple files or transcripts. 
- Speaker identifiers are assigned randomly and can only be used to distinguish different speakers in a single file. 
- Cross-talk and overlapping speech: When multiple speakers talk simultaneously or interrupt each other, it becomes challenging for the model to accurately distinguish and assign the correct text to the corresponding speakers.
- Speaker overlaps: Sometimes, speakers might have similar speech patterns, accents, or use similar vocabulary, making it difficult for the model to differentiate between them.
- Noisy audio: Poor audio quality, background noise, or low-quality recordings can hinder the model's ability to correctly identify and transcribe speakers.
- Emotional Speech: Emotional variations in speech, such as shouting, crying, or extreme excitement, can affect the model's ability to accurately diarize speakers.
- Speaker disguise or impersonation: If a speaker intentionally tries to imitate or disguise their voice, the model might misidentify the speaker.
- Ambiguous speaker identification: Some segments of speech might not have enough unique characteristics for the model to confidently attribute to a specific speaker.

For more information, see: guidelines and limitations in [language detection and transcription](/azure/azure-video-indexer/multi-language-identification-transcription).

## Transcription, translation and language identification components  

During the transcription, translation and language identification procedure, speech in a media file is processed, as follows: 

|Component|Definition|
|---|---|
|Source language |	The user uploads the source file for indexing, and either:<br/>- Specifies the video source language.<br/>- Selects auto detect single language (LID) to identify the language of the file. The output is saved separately.<br/>- Selects auto detect multi language (MLID) to identify multiple languages in the file. The output of each language is saved separately.|
|Transcription API|	The audio file is sent to Azure AI services to get the transcribed and translated output. If a language is specified, it's processed accordingly. If no language is specified, a LID or MLID process is run to identify the language after which the file is processed. |
|Output unification	|The transcribed and translated files are unified into the same file. The outputted data includes the speaker ID of each extracted sentence together with its confidence level.|
|Confidence value	|The estimated confidence level of each sentence is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.| 
