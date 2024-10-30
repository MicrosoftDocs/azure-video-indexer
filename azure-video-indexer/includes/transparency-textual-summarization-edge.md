## Textual summarization on an edge device notes

Textual summarization on an edge device utilizes the [Phi-3.5-mini-instruct](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct/tree/main) model. The Phi-3.5 model has a context size of 128k and modest hardware requirements. There’s no charge for requests to change the model.

### Specifications

- Supports CPU and GPU, though CPU is very slow and not recommended.
- Tested [on Standard_NC24ads_A100_v4](/azure/virtual-machines/sizes/gpu-accelerated/nca100v4-series?tabs=sizebasic). For more support hardware support information, refer to the [official release](https://huggingface.co/microsoft/Phi-3.5-vision-instruct).
- Average runtime on A100 was ~14.5% of the video duration. For short videos, the runtime can be as low as ~11.9%.

## Known limitations and known issues

- An AI language model creates the summarization feature and serves to provide a general overview. The content might not fully encapsulate the essence of the original material. It's recommended that a human review and edit the summary before use. It shouldn’t be viewed as professional or personalized advice.
- The summary’s results are generally consistent within each flavor. However, editing the transcript or reindexing the video might lead to different results output.
- When utilizing Flavors, the Neutral style might occasionally resemble the Formal style. The Casual style might include content-related hashtags. Additionally, a Medium length summary might be shorter than a Short summary.
- Videos that have little content (such as very short videos) are typically not summarized to mitigate the potential model inaccuracies that can happen when the input is short.
- The summary might occasionally include, or reference internal instructions provided to it (referred to as “meta-prompt”). It could contain directives to exclude harmful content.
- Longer videos might result in high-level summary, and less detailed.
- The generated summary might contain inaccuracies, such as incorrect identification of gender, age, and other personal characteristics.
- If the original video contains inappropriate content, the video summarization output extract might be incomplete, contain disclaimers regarding the inappropriate content, and include the actual inappropriate quotes, which might be presented with or without a disclaimer.

## Textual summarization with keyframes on an edge device

Textual summarization with keyframes is based on [keyframes selection with shots detection](/azure/azure-video-indexer/scene-shot-keyframe-detection-insight). Therefore, any limitation that applies to shots detection applies to textual summarization with keyframes.

### Specifications

- Language Model: [Phi-3.5-Vision-Instruct](https://huggingface.co/microsoft/Phi-3.5-vision-instruct) and [Phi-3.5-mini-instruct](https://huggingface.co/microsoft/Phi-3.5-mini-instruct).
- Tested [on Standard_NC24ads_A100_v4](/azure/virtual-machines/sizes/gpu-accelerated/nca100v4-series?tabs=sizebasic). For more support hardware support information, refer to the [official release](https://huggingface.co/microsoft/Phi-3.5-vision-instruct).
- Average runtime on A100 was ~24% of the video duration. For short videos, the runtime can be a low as ~20%.

### Known limitations and known issues 
Keyframe selection is based on a proprietary AI model that might make mistakes.

- Keyframe detection might not capture all the visual aspects of the video so they might be missed in the summary.
- There's a varying limit to the number of frames that can be used for summarizing a section of a video, so frames in sections filtered by harmful content detection or other filters might be discarded. So, the summarization results might be incomplete or incorrect for some parts or sections of the video
