---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 07/25/2024
ms.author: inhenkel
title: transparency imitations - textual summarization cloud
---

### Textual summarization

> [!IMPORTANT]
> When using textual summarization, it's important to note that the system is not intended to replace the full viewing experience, especially for content where details and nuances are crucial. It's also not desinged for summarizing highly sensitive or confidential videos where context and privacy are paramount.

- **Non-English languages**: The Textual Video Summary was primary tested and optimized for the English language. However, it is compatible with all languages supported by the specific GenAI model being used, i.e. GPT3.5 Turbo or GPT4.0. Consequently, when applied to non-English languages, the accuracy and quality of the summaries might vary. To mitigate this limitation, users employing the feature for non-English languages should be extra careful and verify the generated summaries for accuracy and completeness.  
- **Videos with multiple languages**: If a video incorporates speech in multiple languages, the Textual Video Summary may struggle to accurately recognize all the languages featured in the video content. Users should be aware of this potential limitation when utilizing the Textual Video Summarization feature for multilingual videos. 
- **Highly specialized or technical videos**: Video Summary AI models are typically trained on a wide variety of videos, including news, movies, and other general content. If the video is highly specialized or technical, the model may not be able to accurately extract the summary of the video.
- **Videos with poor audio quality nor OCR**: Textual Video Summary AI models also rely on audio (among other insights) to extract the summary from the video or on OCR to extract the text appearing on screen , if the audio quality is poor and there is no OCR identified, the model may not be able to accurately extract the summary from the video.   
- **Videos with low lighting or fast motion**: Videos that are shot in low lighting or have fast motion might be difficult for the model to process the insights, resulting in poor performance.   
- **Videos with uncommon accents or dialects**: AI models are typically trained on a wide variety of speech, including different accents and dialects. However, if the video contains speech with an accent or dialect that is not well represented in the training data, the model may struggle to accurately extract the transcript from the video.  
- **Videos containing harmful content**: Videos with harmful or sensitive content may be filtered out and excluded, leading to a partial summary.
- **User choices and customization**: The Textual Summarization feature has settings that allow users to tailor the summarization process to their needs. These include summary length, quality, output format, and formal, casual, short or long text styles. However these settings also introduce variability in the system’s performance. You should be aware that it can enhance your experience, it may also influence the system’s accuracy and efficiency. It’s a balance between personalization and the system’s operational capabilities. The system is expected to be used responsibly, with an understanding of its limitations and the impact of your choices on the final output.
- **Textual summarization with keyframes**: Summarization with keyframes is based on the keyframes selection done woith shots detectopm. Therefore, any limitation that applies to shots detection applies to textual summarization with keyframes. Keyframe selection is based on AI model that may have mistakes. Keyframe detection may not capture all the visual aspects of the video so they might be missed in the summary.  In addition, there is a limit to the number of frames that can be used for summarizing a section of a video, and there are frames in sections that can be discarded if the textual content in these sections is harmful. The video’s essence may not be captured well in some parts or sections of the video, which may be random or continuous, and may occur at the beginning, middle, or end of the video.
