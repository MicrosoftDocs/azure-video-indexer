<!-- This include was created so that tranparency notes could be kept in one repo. Changes to this include update the page on the DocLegal repo. The date is the date that any of the includes were edited. -->

An AI system includes not only the technology, but also the people who use it, the people affected by it, and the environment in which it's deployed. Creating a system that is fit for its intended purpose requires an understanding of how the technology works, its capabilities and limitations, and how to achieve the best performance.

## What is transparency?

Microsoft’s Transparency Notes are intended to help you understand:

- How our AI technology works
- The choices system owners can make that influence system performance and behavior
- The importance of thinking about the whole system, including the technology, the people, and the environment

You can use Transparency Notes when developing or deploying your own system or share them with the people who use or get affected by your system.  

Microsoft’s Transparency Notes are part of a broader effort at Microsoft to put our AI principles into practice.

To find out more, see [Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai?rtc=1&activetab=pivot1%3aprimaryr6).

## Introduction to Azure AI Video Indexer

Azure AI Video Indexer (VI) is a cloud-based tool that processes and analyzes uploaded video and audio files to generate different types of insights. These insights include detected objects, people, faces, key frames, and translations or transcriptions in at least 60 languages. The insights and their time frames are displayed in a categorized list on the Azure AI Video Indexer website where each insight can be seen by pressing its Play button.

While processing the files, the Azure AI Video Indexer employs a portfolio of Microsoft AI algorithms to analyze, categorize, and index the video footage. The resulting insights are then archived and can be comprehensively accessed, shared, and reused. For example, a news media outlet might implement a deep search for insights related to the Empire State Building and then reuse their findings in different movies, trailers, or promos.  

## The basics of Azure AI Video Indexer

Azure AI Video Indexer is a cloud-based Azure AI services product that is integrated with Azure AI services. It allows you to:

- Upload video and audio files
- Process the video (including running AI models on them)
- Save the processed files and resulting data to a cloud-based Azure Media Services account

To process the media files, Azure AI Video Indexer employs AI technologies. They include Optical Character Recognition (OCR), Natural Language Processing (NLP), and hierarchical ontology models with voice tonality analysis to extract insights like brands, keywords, topics, and text-based emotion detection.

Azure AI Video Indexer’s capabilities include searching for insights in archives, promoting content accessibility, content moderation, and content editing.

Insights categories include:

| Insight category | Description |
|--|--|
| Audio media | For example, transcriptions, translations, audio event detection like clapping and crowd laughter, gun shots, and explosions |
| Video media | For example, faces, clothing detection |
| Video with audio media | For example, named entities in transcripts, and Optical Character Recognition (OCR), for example, names of locations, people, or brands |

For more information, see [Introduction to Azure AI Video Indexer](/azure/azure-video-indexer/video-indexer-overview).

## Key terms and features

| Term | Definition |
|--|--|
| Text-based emotion detection | Emotions such as joy, sadness, anger, and fear that were detected via transcript analysis. |
| Insight | The information and knowledge derived from the processing and analysis of video and audio files that generate different types of insights and can include detected objects, people, faces, key frames and translations or transcriptions. To view and download insights via the API, use the [Azure AI Video Indexer portal](https://api-portal.videoindexer.ai/). |
| Object detection | The ability to identify and find objects in an image or video. For example, a table, chair, or window. |
| Facial detection | Finds human faces in an image and returns bounding boxes indicating their locations. Face detection models alone don't find individually identifying features, only a bounding box marking the entire face. Facial detection doesn't involve distinguishing one fact from another face, predicting or classifying facial attributes, or creating a Face template. |
| Facial identification | "One-to-many" matching of a face in an unmanipulated image to a set of faces in a secure repository. An example is a touchless access control system in a building that replaces or augments physical cards and badges. In this example, a smart camera captures the face of one person entering a secured door and attempts to find a match from a set of images of faces of individuals who are approved to access the building. This process gets implemented by Azure AI Face service and involves the creation of Face templates. |
| Face template | Unique set of numbers generated from an image or video that represents the distinctive features of a face. |
| Observed people detection and matched faces | Features that automatically detect and match people in media files. Observed people detection and matched faces can be set to display insights on people, their clothing, and the exact time frame of their appearance. |
| Keyword extraction | The process of automatically detecting insights on the different keywords discussed in media files. Keywords extraction can extract insights in both single language and multi-language media files. |
| Deep search | The ability to retrieve only relevant video and audio files from a video library by searching for specific terms within the extracted insights. |
| Labels | The identification of visual objects and actions appearing in a frame. For example, identifying an object such as a dog, or an action such as running. |
| Named entities | Feature that uses Natural Language Processing (NLP) to extract insights on the locations, people, and brands appearing in audio and images in media files. |
| Natural Language Processing (NLP) | The processing of human language as it is spoken and written. |
| Optical Character Recognition (OCR) | Extracts text from images like pictures, street signs, and products in media files to create insights. For more information, see [OCR technology](/azure/ai-services/computer-vision/overview-ocr). |
| Hierarchical Ontology Model | A set of concepts or categories in a subject area or domain that possess shared properties and relationships. |
| Audio effects detection | Feature that detects insights on various of acoustic events and classifies them into acoustic categories. Audio effect detection can detect and classify different categories such as laughter, crowd reactions, alarms and/or sirens. |
| Transcription, translation and language identification | Feature that automatically detects, transcribes, and translates the speech in media files into over 50 languages. |
| Topics inference | Feature that automatically creates inferred insights derived from the transcribed audio, OCR content in visual text, and celebrities recognized in the video. |
| Speaker diarization | Feature that identifies each speaker in a video and attributes each transcribed line to a speaker. It allows for the identification of speakers during conversations and can be useful in various scenarios. |
| Bring Your Own Model | Feature that allows you to send insights and artifacts generated by Azure AI Video Indexer to external AI models. |
| Textual Video Summarization | Feature that summarizes the uses artificial intelligence to summarize the content of a video. |

## Components of Azure AI Video Indexer

During the Azure AI Video Indexer procedure, a media file is processed using Azure APIs to extract different types of insights, as follows:

| Component | Definition |
|--|--|
| Video uploader | The user uploads a media file to get processed by Azure AI Video Indexer. |
| Insights generation | *Azure services APIs such as Azure AI services OCR and Transcription, extract insights.* <br/> Internal AI models are run to generate insights like Detected Audio Events, Observed People, Detected Clothing, and Topics. |
| Insights processing | More logic such as confidence level threshold filtering is applied to the output of Insights generation. It creates the final insights that are then displayed in the Azure AI Video Indexer portal and in the JSON file that can be downloaded from the portal. |
| Storage | Output from the processed media file is saved in: <br/><br/> • Azure Storage <br/> • Azure Search, where users can search for videos using specific insights like an actor’s name, a location, or a brand. <br/><br/> |
| Notification | The user receives notification that the indexing process is complete. |

## Limited Access features of Azure AI Video Indexer

Facial recognition features of Azure AI Video Indexer (including facial detection, facial identification, facial templates, observed people detection, and matched faces) are Limited Access and are only available to Microsoft managed customers and partners, and only for certain use cases selected at the time of registration. Access to the facial identification and celebrity recognition capabilities requires registration. Facial detection doesn't require registration. To learn more, visit [Microsoft’s Limited Access policy](https://aka.ms/limitedaccesscogservices).

### Approved commercial use cases for Limited Access features

**Facial Identification to search for a face in a media or entertainment video archive**: to find a face within a video and generate metadata for media or entertainment use cases only.

**Celebrity Recognition**: to detect and identify celebrities within images or videos in digital asset management systems, for accessibility and/or media and entertainment use cases only.

### Approved public sector use cases for Limited Access features

**Facial identification** for preservation and enrichment of public media archives: to identify individuals in public media or entertainment video archives for the purposes of preserving and enriching public media only. Examples of public media enrichment include identifying historical figures in video archives and generating descriptive metadata.

**Facial identification** to:

- assist law enforcement or court officials in prosecution or defense of a criminal suspect who has already been apprehended, to the extent specifically authorized by a duly empowered government authority in a jurisdiction that maintains a fair and independent judiciary OR
- assist officials of duly empowered international organizations in the prosecution of abuses of international criminal law, international human rights law, or international humanitarian law.

**Facial identification** for purposes of providing humanitarian aid, or identifying missing persons, deceased persons, or victims of crimes.

## Respect privacy

When used responsibly and carefully Azure AI Video Indexer is a valuable tool for many industries. To respect the privacy and safety of others, we recommend the following points:  

- Always respect an individual’s right to privacy, and only ingest videos for lawful and justifiable purposes.  
- Do not purposely disclose inappropriate media showing young children or family members of celebrities or other content that may be detrimental or pose a threat to an individual’s personal freedom.  
- Commit to respecting and promoting human rights in the design and deployment of your analyzed media.  
- When using third party materials, be aware of any existing copyrights or required permissions before distributing content derived from them.
- Always seek legal advice when using media from unknown sources.
- Always obtain appropriate legal and professional advice to ensure that your uploaded videos are secured and have adequate controls to preserve the integrity of your content and to prevent unauthorized access.
- Provide a feedback channel that allows users and individuals to report issues with the service.  
- Be aware of any applicable laws or regulations that exist in your area regarding processing, analyzing, and sharing media containing people.
- Keep a human in the loop. Do not use any solution as a replacement for human oversight and decision-making.  
- Fully examine and review the potential of any AI model you are using to understand its capabilities and limitations.

For more information, see [Microsoft Global Human Rights Statement](https://www.microsoft.com/corporate-responsibility/human-rights-statement?activetab=pivot_1:primaryr5).

## Example use cases for Azure AI Video Indexer

Azure AI Video Indexer can be used in multiple scenarios in various industries, such as:  

- **Creating feature stories** at news or media agencies by implementing deep searches for specific people and/or words to find what was said, by whom, where and when. Facial identification capabilities are Limited Access. For more information, visit [Microsoft’s Limited Access policy](https://aka.ms/limitedaccesscogservices).  
- **Creating promos and trailers** using important moments previously extracted from videos. Azure AI Video Indexer can assist by adding keyframes, scene markers, timestamps, and labeling so that content editors invest less time reviewing numerous files.
- **Promoting accessibility** by translating and transcribing audio into multiple languages and adding captions, or by creating a verbal description of footage via OCR processing to enhance accessibility for the visually impaired.
- **Improving content distribution to a diverse audience in different regions and languages** by delivering content in multiple languages using Azure AI Video Indexer’s transcription and translation capabilities.
- **Enhancing targeted advertising**, industries like news media or social media can use Azure AI Video Indexer to extract insights to enhance the relevance of targeted advertising.
- **Enhancing user engagement** using metadata, tags, keywords, and embedded customer insights to filter and tailor media to customer preferences.  
- **Moderating inappropriate content** such as banned words using textual and visual content control to tag media as child approved or for adults only.
- **Accurately and quickly detecting violence incidents** by classifying gunshots, explosions, and glass shattering in a smart-city system or in other public environments that include cameras and microphones.
- **Enhancing compliance with local standards** by extracting text in warnings in online instructions and then translating the text. For example, e-learning instructions for using equipment.
- **Enhancing and improving manual closed captioning and subtitles generation** by applying Azure AI Video Indexer’s transcription and translation capabilities and by using the closed captions generated by Azure AI Video Indexer in one of the supported formats.
- **Transcribing videos in unknown languages** by using language identification (LID) or multi language identification (MLID) to allow Azure AI Video Indexer to automatically identify the languages appearing in the video and generate the transcription accordingly.

## Use case considerations

- Avoid using Video Indexer for decisions that may have serious adverse impacts. Decisions based on incorrect output could have serious adverse impacts. Additionally, it's advisable to include human review of decisions that have the potential for serious impacts on individuals.
- The Video Indexer text-based emotion detection wasn't designed to assess employee performance or the emotional state of an individual.
- Bring Your Own Model
    - Azure AI Video Indexer isn't responsible for the way you use an external AI model. It is your responsibility to ensure that your external AI models are compliant with Responsible Artificial Intelligence standards.
    - Azure AI Video Indexer isn't responsible for the custom insights you create while using the Bring Your Own Model feature as they aren't generated by Azure Video Indexer models.

## Characteristics and limitations of Video Indexer

The intended use of Azure AI Video Indexer is to generate insights from recorded media and entertainment content. Extracted insights are created in a JSON file that lists the insights in categories. Each insight holds a list of unique elements, and each element has its own metadata and a list of its instances. For example, a face might have an ID, a name, a thumbnail, other metadata, and a list of its temporal instances. The output of some insights might also display a confidence score to indicate its accuracy level.

A JSON file can be accessed in three ways:

- Azure AI Video Indexer portal, an easy-to-use solution that lets you evaluate the product, manage the account, and customize models.  
- API integration, via a REST API, which lets you integrate the solution into your apps and infrastructure.  
- Embeddable widget, which lets you embed the Azure AI Video Indexer insights, player, and editor experiences into your app to customize the insights displayed in a web interface. For example, the list can be customized to display insights only about people appearing in a video. To find videos that include a specific celebrity, a content editor can implement a deep search using the name appearing in the Face or People insights categories.

### Video

- Azure AI Video Indexer has a storage limit of 30 GB and 4 hours for uploaded, previously recorded videos.
- Always upload high-quality video and audio content. The recommended maximum frame size is HD and frame rate is 30 frames per second (FPS). A frame should contain no more than 10 people. When outputting frames from videos to AI models, only send around two or three frames per second. Processing 10 or more frames might delay the AI result. At least 1 minute of spontaneous conversational speech is required to perform analysis. Audio effects are detected in nonspeech segments only. The minimal duration of a nonspeech section is 2 seconds. Voice commands and singing aren't supported.
- Lower accuracy of the generated insights might occur when people and faces recorded by cameras that are high-mounted, down-angled or with a wide field of view (FOV) might have fewer pixels.
- Typically, small people or objects under 200 pixels and people who are seated might not be detected. People wearing similar clothes or uniforms might be detected as being the same person and are given the same ID number. People or objects that are obstructed might not be detected. Tracks of people with front and back poses might be split into different instances.
- An observed person must first be detected and appear in the People category before they're matched. Tracks are optimized to handle observed people who frequently appear in the foreground. Obstructions like overlapping people or faces might cause mismatches between matched people and observed people. Mismatching might occur when different people appear in the same relative spatial position in the frame within a short period.
- Dresses and skirts are categorized as Dresses or Skirts. Clothing the same color as a person’s skin isn't detected. A full view of the person is required. To optimize detection, both the upper and lower body should be included in the frame.
- Avoid using the OCR results of signatures that are hard to read for both humans and machines. A better way to use OCR is to use it for detecting the presence of a signature for further analysis.
- Named entities only detect insights in audio and images. Logos in a brand name might not be detected.
- Detectors might misclassify objects in videos that are in a "birds-eye" view as there were trained with a frontal view of objects.

### Audio

- Avoid use of audio with loud background music or music with repetitive and/or linearly scanned frequency. Audio effects detection is designed for nonspeech audio only and therefore can't classify events in loud music. Music with repetitive and/or linearly scanned frequency many be incorrectly classified as an alarm or siren.

### Textual summarization notes

> [!IMPORTANT]
> When using textual summarization, it's important to note that the system isn't intended to replace the full viewing experience. Especially for content where details and nuances are crucial. It's also not designed for summarizing highly sensitive or confidential videos where context and privacy are paramount.

- **Non-English languages**: The Textual Video Summary was primarily tested and optimized for the English language. However, it's compatible with all languages supported by the specific GenAI model being used, that is, GPT3.5 Turbo or GPT4.0. So, when applied to non-English languages, the accuracy and quality of the summaries might vary. To mitigate this limitation, users employing the feature for non-English languages should be extra careful and verify the generated summaries for accuracy and completeness.  
- **Videos with multiple languages**: If a video incorporates speech in multiple languages, the Textual Video Summary might struggle to accurately recognize all the languages featured in the video content. Users should be aware of this potential limitation when utilizing the Textual Video Summarization feature for multilingual videos. 
- **Highly specialized or technical videos**: Video Summary AI models are typically trained on a wide variety of videos, including news, movies, and other general content. If the video is highly specialized or technical, the model might not be able to accurately extract the summary of the video.
- **Videos with poor audio quality nor OCR**: Textual Video Summary AI models also rely on audio and other insights to extract the summary from the video, or on OCR to extract the text appearing on screen. If the audio quality is poor and there's no OCR identified, the model might not be able to accurately extract the summary from the video.   
- **Videos with low lighting or fast motion**: Videos that are shot in low lighting or have fast motion might be difficult for the model to process the insights, resulting in poor performance.   
- **Videos with uncommon accents or dialects**: AI models are typically trained on a wide variety of speech, including different accents and dialects. However, if the video contains speech with an accent or dialect that isn't well represented in the training data, the model might struggle to accurately extract the transcript from the video.  
- **Videos containing harmful content**: Videos with harmful or sensitive content might be filtered out and excluded, leading to a partial summary.
- **User choices and customization**: The Textual Summarization feature has settings that allow users to tailor the summarization process to their needs. They include summary length, quality, output format, and formal, casual, short, or long text styles. However these settings also introduce variability in the system’s performance. It can enhance your experience, but it might also influence the system’s accuracy and efficiency. It’s a balance between personalization and the system’s operational capabilities. You're expected to use the system responsibly, with an understanding of its limitations and the effect of your choices on the final output.
- **Textual summarization with keyframes**: Summarization with keyframes is based on [keyframes selection with shots detection](/azure/azure-video-indexer/scene-shot-keyframe-detection-insight). Therefore, any limitation that applies to shots detection applies to textual summarization with keyframes. Keyframe selection is based on a proprietary AI model that might make mistakes. Keyframe detection might not capture all the visual aspects of the video so they might be missed in the summary. In addition, there's a varying limit to the number of frames that can be used for summarizing a section of a video. Frames in sections filtered by harmful content detection or other filters might be discarded. So, the summarization results might be incomplete or incorrect for some parts or sections of the video.

## Textual summarization using VI enabled by Arc notes

Textual summarization enabled by Arc (also known as using VI on an edge device) utilizes the [Phi-3.5-mini-instruct](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct/tree/main) model. The Phi-3.5 model has a context size of 128k and modest hardware requirements. There’s no charge for requests to change the model.

### Specifications

- Hardware requirements: GPU V100 or Intel CPU 32 cores. CPU is slow and not recommended.
- Tested [on Standard_NC24ads_A100_v4](/azure/virtual-machines/sizes/gpu-accelerated/nca100v4-series?tabs=sizebasic). For more support hardware support information, refer to the [official release](https://huggingface.co/microsoft/Phi-3.5-vision-instruct).
- Average runtime on A100 was ~14.5% of the video duration. For short videos, the runtime can be as low as ~11.9%.

## Known limitations and known issues

- An AI language model creates the summarization feature and serves to provide a general overview. The content might not fully encapsulate the essence of the original material. We recommend that a human review and edit the summary before use. It shouldn’t be viewed as professional or personalized advice.
- The summary’s results are consistent within each flavor. However, editing the transcript or reindexing the video might lead to different results output.
- When utilizing Flavors, the Neutral style might occasionally resemble the Formal style. The Casual style might include content-related hashtags. Additionally, a Medium length summary might be shorter than a Short summary.
- Videos that have little content (such as short videos) are typically not summarized to mitigate the potential model inaccuracies that can happen when the input is short.
- The summary might occasionally include, or reference internal instructions provided to it (referred to as "meta-prompt"). It could contain directives to exclude harmful content.
- Longer videos might result in high-level summary, and less detailed.
- The generated summary might contain inaccuracies, such as incorrect identification of gender, age, and other personal characteristics.
- If the original video contains inappropriate content:
  - The video summarization output extract might be incomplete
  - Contain disclaimers regarding the inappropriate content
  - Include the actual inappropriate quotes, which might be presented with or without a disclaimer

## Textual summarization with keyframes using VI enabled by Arc notes

Textual summarization with keyframes is based on [keyframes selection with shots detection](/azure/azure-video-indexer/scene-shot-keyframe-detection-insight). Therefore, any limitation that applies to shots detection applies to textual summarization with keyframes.

### Specifications

- Hardware requirements: GPU A100 for vision, and CPU 24 cores for mini-instruct (can be either AMD or Intel).
- Language models: [Phi-3.5-Vision-Instruct](https://huggingface.co/microsoft/Phi-3.5-vision-instruct) and [Phi-3.5-mini-instruct](https://huggingface.co/microsoft/Phi-3.5-mini-instruct).
- Tested [on Standard_NC24ads_A100_v4](/azure/virtual-machines/sizes/gpu-accelerated/nca100v4-series?tabs=sizebasic). For more support hardware support information, refer to the [official release](https://huggingface.co/microsoft/Phi-3.5-vision-instruct).

### Known limitations and known issues 

- Keyframe selection is based on a proprietary AI model that might make mistakes.
- Average runtime on A100 was ~24% of the video duration. For short videos, the runtime can be a low as ~20%.
- Keyframe detection might not capture all the visual aspects of the video so they might be missed in the summary.
- There's a varying limit to the number of frames that can be used for summarizing a section of a video. Frames in sections filtered by harmful content detection or other filters might be discarded. So, the summarization results might be incomplete or incorrect for some parts or sections of the video

## Audio effects detection

[Audio effects detection](/azure/azure-video-indexer/audio-effects-detection-overview)

[!INCLUDE [transparency-audio-effects-detection](transparency-audio-effects-detection.md)]

## Clapper board detection

[Clapper board detection](/azure/azure-video-indexer/clapper-board-insight)

[!INCLUDE [transparency-clapper-board-detection](transparency-clapper-board-detection.md)]

## Content moderation

[See Cognitive Services Content Moderation.](/legal/cognitive-services/computer-vision/imageanalysis-transparency-note)

## Face detection and celebrity recognition

[Face detection](/azure/azure-video-indexer/face-detection) and [celebrity recognition](/azure/azure-video-indexer/face-detection-insight?branch=main#celebrities-recognition-model)

[!INCLUDE [transparency-named-entities](transparency-face-detection.md)]

## Keywords extraction

[Keywords extraction](/azure/azure-video-indexer/keywords#example-use-cases)

[!INCLUDE [transparency-keywords-extraction](transparency-keywords-extraction.md)]

## Labels identification

[Labels identification](/azure/azure-video-indexer/labels-identification#example-use-cases)

[!INCLUDE [transparency-labels-identification](transparency-labels-identification.md)]

## Named entities

[Named entities](/azure/azure-video-indexer/named-entities)

[!INCLUDE [transparency-named-entities](transparency-named-entities.md)]

## Observed people detection and matched faces

[Observed people detection and matched faces](/azure/azure-video-indexer/observed-matched-people)

[!INCLUDE [transparency-observed-people-detection-matched-faces](transparency-observed-people-detection-matched-faces.md)]

## Optical character recognition (OCR)

[OCR](/azure/azure-video-indexer/ocr)

[!INCLUDE [transparency-ocr](transparency-ocr.md)]

## Textual emotion detection

[Textual emotion detection](/azure/azure-video-indexer/text-based-emotions-detection-insight)

[!INCLUDE [transparency-text-based-emotion-detection](transparency-text-based-emotion-detection.md)]

## Topics inference

See [topics inference](/azure/azure-video-indexer/topics-inference)

[!INCLUDE [transparency-topics-inference](transparency-topics-inference.md)]

## Transcription, translation, and language identification

[Transcription and captions](/azure/azure-video-indexer/transcription-translation-lid)

[!INCLUDE [transparency-transcription-translation-lid](transparency-transcription-translation-lid.md)]
