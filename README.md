# Build a multlingual virtual assistant with Watson Assistant and Language Translator

### Introduction

Use the code and instructions from this repository to integrate the **Language Translator** service with **Watson Assistant** to build a multilingual chatbot. Wastson Assistant is trained in one language only and uses the Language Translator service to provide realtime, machine translation for other languages. 

Integration with the Language Translator service is achieved using Watson Assistant [web chat events](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events) and IBM Cloud functions. We use the web chat `pre:send` and `pre:receive` events to call IBM Cloud Functions actions. The IBM Cloud Functions actions make calls to Language Translator REST API. 

Watch the video linked below that includes detailed steps to build this solution. 

[![Launch on YouTube](https://github.com/rodalton/multlingual-watson-assistant/blob/main/launch_video.png)](https://youtu.be/bQcKz1w6N50)


### Solution Outline

The sequence diagram below outlines the set of calls made between services. Note the split between `pre:send` and `pre:receive` events. `chat lang` refers to the language the end user i.e. the language of the end user when asking questions of Watson Assistant and the language the end user expects to receive replies. `watson lang` is the language used to define intents, entities and ultimately the dialog in Watson Assistant i.e. the language used to train your virtual assistant. 

![](https://github.com/rodalton/multlingual-watson-assistant/blob/main/multilingual_sequence.jpg)


### Steps to Build

#### Cloud Functions

1. Use the `translate.js` file from this repository to create two IBM Cloud Functions actions. Use one action to translate text from the end user being sent to Watson Assistant and another to translate the text returned from Watson Assistant before it's returned to the end user in the web chat UI. 

2. Update each action with your Language Translator API Key and service URL. Also update with the language translator model ID, that'll source and target languages for machine translation. You'll find details of the languages supported by the Language Translator service [here](https://cloud.ibm.com/docs/language-translator?topic=language-translator-translation-models#list-languages-supported). 

3. Finally, allow your Cloud Functions actions to handle HTTP events and expose as a web action. Make a note of the endpoint URL as you'll require this when customising the web chat UI. 

#### Web Chat UI

1. Use the `translate.html` file from this repository to launch a web chat UI that includes custom `pre:send` and `pre:receive` events. 

2. Include details of your assistant and Cloud Functions actions (from the step above) in the file before launching. 

#### Launch
Here's the easy bit, once you launch the web chat UI, your assistant should be fully functional, but in a new language thanks to the Watson Language Translator service! 
