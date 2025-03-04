# Image Text Translator

In Progress: Moving code here from the private repo to this public repo to make sure no api keys get leaked

## About the Project

-> What problem does it solve?

Translates text in images and writes translated text back onto the image

![GoogleOCR32 drawio](https://github.com/user-attachments/assets/fb725583-93d8-4b9a-b402-c85a8b9de371)

<br/>

## Technology Built With

* Java (using Maven - pom.xml for deps)

* Options for Text Detection
  * *Google Cloud Vision* (faster and most accurate but will be charged for usage)
  * *EasyOCR* locally called through python wrapper (slower, less accurate, free)

* Options for translations:
  * *OpenAI* can specify any desired chat model (most accurate, accuracy can vary depending on model used, expensive, requests can run in parallel)
  * *Ollama Locally* can specify any ollama model which matches the request format used. (accuracy is model dependent, will be slower than OpenAI, but how much so will be system dependent)
  * *NLLB Translate Locally* (Least accurate, has a very hard time with short snippets from word bubbles)

<br/>

### Using Google Vision and OpenAI external calls, flow looks like this

![GoogleOCR3Diagram23244 drawio](https://github.com/user-attachments/assets/710e8db1-9b53-4d90-87ca-a13ae0b672b9)

<br/>

## How to run

1. Set OpenAI key (export OPENAI_KEY='123456')
2. Set Google Cloud api key and authorize Google Vision api usage through console
3. Place images as .jpg or .webp into the directory "inputs/{image_group_name}"
4. Run "mvn spring-boot:run"
5. Translated images are output to directory "translated/inputs/{image_group_name}"




## How to use local Ollama for translation

*Prompt*

"Act as a translator. Only respond with the translated text and nothing else. If you are unsure about the translation due to it having multiple possibilities, just pick one of the possibilities. If you don't have any idea what the possible translation could be, respond with nothing. If there is no text provided to be translated, provide an empty response. Following the previous instructions, translate the following text into english, translate it like it is dialogue spoken aloud by a character in a story: {text}"

### Model Request Parameters 

#### Dolphin-Mixtral

```json
{
	"model": "dolphin-mixtral:latest",
	"prompt": "{prompt goes here}"
}
```

#### Deepseek

```json
{
	"model": "deepseek",
	"prompt": "{prompt goes here}",
	"temperature": 0.7, 		// optional
	"top_k": 40, 			// optional
	"stream": false 		// optional
}
```
