---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.date: 08/08/2024
ms.author: inhenkel
title: Transparency imitations - textual summarization cloud
---

### Textual summarization notes

> [!IMPORTANT]
> When using textual summarization, it's important to note that the system is not intended to replace the full viewing experience, especially for content where details and nuances are crucial. It's also not desinged for summarizing highly sensitive or confidential videos where context and privacy are paramount.

- **Non-English languages**: The Textual Video Summary was primarily tested and optimized for the English language. However, it's compatible with all languages supported by the specific GenAI model being used, that is, GPT3.5 Turbo or GPT4.0. So, when applied to non-English languages, the accuracy and quality of the summaries might vary. To mitigate this limitation, users employing the feature for non-English languages should be extra careful and verify the generated summaries for accuracy and completeness.  
- **Videos with multiple languages**: If a video incorporates speech in multiple languages, the Textual Video Summary might struggle to accurately recognize all the languages featured in the video content. Users should be aware of this potential limitation when utilizing the Textual Video Summarization feature for multilingual videos. 
- **Highly specialized or technical videos**: Video Summary AI models are typically trained on a wide variety of videos, including news, movies, and other general content. If the video is highly specialized or technical, the model might not be able to accurately extract the summary of the video.
- **Videos with poor audio quality nor OCR**: Textual Video Summary AI models also rely on audio and other insights to extract the summary from the video, or on OCR to extract the text appearing on screen. If the audio quality is poor and there's no OCR identified, the model might not be able to accurately extract the summary from the video.   
- **Videos with low lighting or fast motion**: Videos that are shot in low lighting or have fast motion might be difficult for the model to process the insights, resulting in poor performance.   
- **Videos with uncommon accents or dialects**: AI models are typically trained on a wide variety of speech, including different accents and dialects. However, if the video contains speech with an accent or dialect that isn't well represented in the training data, the model might struggle to accurately extract the transcript from the video.  
- **Videos containing harmful content**: Videos with harmful or sensitive content might be filtered out and excluded, leading to a partial summary.
- **User choices and customization**: The Textual Summarization feature has settings that allow users to tailor the summarization process to their needs. These include summary length, quality, output format, and formal, casual, short, or long text styles. However these settings also introduce variability in the system’s performance. It can enhance your experience, but it might also influence the system’s accuracy and efficiency. It’s a balance between personalization and the system’s operational capabilities. You're expected to use the system responsibly, with an understanding of its limitations and the effect of your choices on the final output.

<!-- removed text summarization keyframes -->
