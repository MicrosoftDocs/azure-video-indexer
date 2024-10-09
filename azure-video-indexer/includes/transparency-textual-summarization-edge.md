---
author: inhenkel
ms.topic: include 
ms.service: azure-video-indexer
ms.collection: ce-skilling-ai-copilot,rai-skilling-ai-copilot
ms.date: 10/09/2024
ms.author: inhenkel
title: Transparency imitations - textual summarization edge
---

### Textual summarization on an Edge device notes

If you're using the Edge extension, you can generate a summary from the video page in the web portal and use the same functionality such as customizations but there's no option to change the model deployment. Instead, every new extension created includes a local [Phi-3-mini-4k-instruct](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct/tree/main) model that is developed by Microsoft. There's no charge for requests to the model.

#### Specifications

- Supported hardware: currently supports only Intel CPU and Nvidia GPU. 
    - CPU tested on: [Standard_F64s_v2](/azure/virtual-machines/fsv2-series) (utilization: ~30-32 cores) 
    - GPU tested on: [Standard_NC6s_v3](/azure/virtual-machines/ncv3-series)
- Average runtime ranges between 46-57% of video length on CPU, or 15-17% on GPU.

#### Known Limitations and Known Issues

- CPU: Currently, running VI on AMD CPUs might lead to significantly longer runtimes and isn't supported at this time.
- The summarization feature is created by an AI language model and serves to provide a general overview. Although we aim for accuracy and reliability, the content might not fully encapsulate the essence of the original material. We recommend that a human review and edit the summary before using it. It should **not** be viewed as professional or personalized advice.
- The summary results are generally consistent within each summarization setting. However, editing the transcript or reindexing the video might lead to different output results.
- Disclaimer for product documentation: When utilizing summarization settings, the Neutral style might occasionally resemble the Formal style. The Casual style might include content-related hashtags. Additionally, in some instances, a Medium length summary might be shorter than a Short summary. 
- Videos that have little content (such as very short videos) are typically not summarized to mitigate the potential model inaccuracies that can happen when dealing with short input.
- The summary might occasionally include or reference internal instructions provided to it (referred to as “meta-prompt”), including directives to exclude harmful content.
- The length of the summary might influence the level of detail extracted from the video summary. Longer summaries might result in less specific details being included.
- The generated summary might contain inaccuracies, such as incorrect identification of gender, age, and other personal characteristics.
- If the original video contains inappropriate content, the video summarization output might be affected in the following ways: it might be incomplete, contain disclaimers regarding the inappropriate content, and in certain instances, it might include the actual inappropriate quotes, which might be presented with or without a disclaimer.

See also the transparency notes for textual summarization. 
