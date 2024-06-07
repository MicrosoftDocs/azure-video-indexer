---
title: Azure AI Video Indexer media transcription, translation, and language identification overview  
description: An introduction to Azure AI Video Indexer media transcription, translation, and language identification components responsibly.
ms.date: 06/06/2024
ms.topic: article
ms.author: inhenkel
author: IngridAtMicrosoft
ms.service: azure-video-indexer
---

# Media transcription, translation, and language identification

[!INCLUDE [AMS VI retirement announcement](./includes/important-ams-retirement-avi-announcement.md)]

Azure AI Video Indexer transcription, translation, and language identification automatically detects, transcribes, and translates the speech in media files into over 50 languages. 

- Azure AI Video Indexer processes the speech in the audio file to extract the transcription that is then translated into many languages. When selecting to translate into a specific language, both the transcription and the insights like keywords, topics, labels or OCR are translated into the specified language. Transcription can be used as is or be combined with speaker insights that map and assign the transcripts into speakers. Multiple speakers can be detected in an audio file. An ID is assigned to each speaker and is displayed under their transcribed speech. 
-	Azure AI Video Indexer language identification (LID) automatically recognizes the supported dominant spoken language in the video file. For more information, see [Applying LID](/azure/azure-video-indexer/language-identification-model). 
-	Azure AI Video Indexer multi-language identification (MLID) automatically recognizes the spoken languages in different segments in the audio file and sends each segment to be transcribed in the identified languages. At the end of this process, all transcriptions are combined into the same file. For more information, see [Applying MLID](/azure/azure-video-indexer/multi-language-identification-transcription).
The resulting insights are generated in a categorized list in a JSON file that includes the ID, language, transcribed text, duration, and confidence score.
- When indexing media files with multiple speakers, Azure AI Video Indexer performs speaker diarization that identifies each speaker in a video and attributes each transcribed line to a speaker. The speakers are given a unique identity such as Speaker #1 and Speaker #2. This allows for the identification of speakers during conversations and can be useful in various scenarios such as doctor-patient conversations, agent-customer interactions, and court proceedings.

## Prerequisites  

Review [transparency note overview](/legal/azure-video-indexer/transparency-note?context=/azure/azure-video-indexer/context/context)

## View the insight

To view the insights on the website:

1. Go to Insight and scroll to Transcription and Translation.

To view language insights in `insights.json`:

1. Select Download -> Insights (JSON). 
1. Copy the desired element, under `insights`, and paste it into your online JSON viewer. 
    
    ```json
    "insights": {
      "version": "1.0.0.0",
      "duration": "0:01:50.486",
      "sourceLanguage": "en-US",
      "sourceLanguages": [
        "en-US"
      ],
      "language": "en-US",
      "languages": [
        "en-US"
      ],
      "transcript": [
        {
          "id": 1,
          "text": "Hi, I'm Doug from office. We're talking about new features that office insiders will see first and I have a program manager,",
          "confidence": 0.8879,
          "speakerId": 1,
          "language": "en-US",
          "instances": [
            {
              "adjustedStart": "0:00:00",
              "adjustedEnd": "0:00:05.75",
              "start": "0:00:00",
              "end": "0:00:05.75"
            }
          ]
        },
        {
          "id": 2,
          "text": "Emily Tran, with office graphics.",
          "confidence": 0.8879,
          "speakerId": 1,
          "language": "en-US",
          "instances": [
            {
              "adjustedStart": "0:00:05.75",
              "adjustedEnd": "0:00:07.01",
              "start": "0:00:05.75",
              "end": "0:00:07.01"
            }
          ]
        },
    ```
    
To download the JSON file via the API, use the [Azure AI Video Indexer developer portal](https://api-portal.videoindexer.ai/). 

## Transcription, translation, and language identification components  

During the transcription, translation and language identification procedure, speech in a media file is processed, as follows: 

|Component|Definition|
|---|---|
|Source language |	The user uploads the source file for indexing, and either:<br/>- Specifies the video source language.<br/>- Selects auto detect single language (LID) to identify the language of the file. The output is saved separately.<br/>- Selects auto detect multi language (MLID) to identify multiple languages in the file. The output of each language is saved separately.|
|Transcription API|	The audio file is sent to Azure AI services to get the transcribed and translated output. If a language is specified, it's processed accordingly. If no language is specified, a LID or MLID process is run to identify the language after which the file is processed. |
|Output unification	|The transcribed and translated files are unified into the same file. The outputted data includes the speaker ID of each extracted sentence together with its confidence level.|
|Confidence value	|The estimated confidence level of each sentence is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|

## Example use cases 

-	Promoting accessibility by making content available for people with hearing disabilities using Azure AI Video Indexer to generate speech to text transcription and translation into multiple languages.
- Improving content distribution to a diverse audience in different regions and languages by delivering content in multiple languages using Azure AI Video Indexer’s transcription and translation capabilities. 
- Enhancing and improving manual closed captioning and subtitles generation by using Azure AI Video Indexer’s transcription and translation capabilities and by using the closed captions generated by Azure AI Video Indexer in one of the supported formats.
- Using language identification (LID) or multi language identification (MLID) to transcribe videos in unknown languages to allow Azure AI Video Indexer to automatically identify the languages appearing in the video and generate the transcription accordingly. 

## Considerations and limitations when choosing a use case 

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
