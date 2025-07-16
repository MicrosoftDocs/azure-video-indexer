## OCR notes

- Video Indexer has an OCR limit of 50,000 words per indexed video. Once the limit is reached, no additional OCR results are generated. In some languages, such as Japanese, the limit is applied based on characters instead of words.
- Carefully consider the accuracy of the results, to promote more accurate detections, check the quality of the image, low quality images might affect the detected insights.  
- Carefully consider when using for law enforcement. OCR might misread or not detect parts of the text. To ensure fair and high-quality VI determinations, combine OCR-based automation with human oversight. 
- When extracting handwritten text, avoid using the OCR results of signatures that are hard to read for both humans and machines. A better way to use OCR is to use it for detecting the presence of a signature for further analysis. 
- Don't use OCR for decisions that might have serious adverse impacts to individuals or groups. Machine learning models that extract text can result in undetected or incorrect text output. Decisions based on incorrect output could have serious adverse impacts that must be avoided. You should always to include human review of decisions that have the potential for serious impacts on individuals.

## OCR components 

During the OCR procedure, text images in a media file are processed, as follows:  

|Component|Definition|
|---|---|
|Source file|	The user uploads the source file for indexing.|
|Read model	|Images are detected in the media file and text, then extracted and analyzed by Azure AI services. |
|Get read results model	|The output of the extracted text is displayed in a JSON file.|
|Confidence value|	The estimated confidence level of each word is calculated as a range of 0 to 1. The confidence score represents the certainty in the accuracy of the result. For example, an 82% certainty is represented as an 0.82 score.|
