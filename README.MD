# Med Vise  - OpenSource  Medical Assistant for any medical realted question 




# Background and problem statement:

In the healthcare field, non-critical injuries such as minor bruises, cuts or sprains often lack immediate and reliable first-aid advice. Typically, these injuries, while not life-threatening, can cause discomfort or concern for individuals. The problem is compounded by the fact that such minor ailments aren't usually a priority in traditional medical settings, leading to delays in seeking professional advice. In addition, the vast and unstructured information available online can be overwhelming, often leading to confusion rather than clarity.

# Our Solution

*MedVise* is a healthcare chat assistant app that provides a comprehensive solution to the need for immediate and reliable first aid advice for non-critical injuries. The app addresses the common gap in professional advice for minor health concerns such as bruises, cuts or sprains, which are often not prioritized in traditional healthcare settings.

A key feature of *MedVise* is its multimodal and multilingual interface. Not only does the app allow users to upload images of their injuries for more nuanced analysis, it also supports audio input, allowing users to verbally describe their symptoms. This feature is particularly beneficial for those who prefer to express their health concerns verbally or find typing inconvenient.

In addition, MedVise's multilingual capabilities make it accessible to a diverse user base, breaking down language barriers that often impede access to quality healthcare information. By supporting multiple languages, ShifaChat ensures that users can receive medical advice in their preferred language, further personalizing the experience.

Combining these features with a knowledge base vetted by medical professionals ensures that the advice provided is specific, reliable and medically sound. By incorporating these advanced features, *MedVise* aims to not only streamline the management of minor health issues, but also reduce the reliance on unnecessary doctor visits. It provides an efficient, user-friendly and inclusive platform for health concerns, ultimately promoting improved self-care practices and increased health awareness among diverse communities.

# Workflow

![Workflow](/Workflow.png)


---
When building the project, we had a goal of relying only on open-source and openly available models, which we achieved. The project consists of the following parts:

## 1. Automatic Speech Recognition:

This feature provides the ability to record and input your audio instead of text.

For this we used the *[SeamlessM4T V2 large](https://huggingface.co/facebook/seamless-m4t-v2-large)* model.

## 2. Text translation:

Since our knowledge base only contains English data, we decided to use translation to make the use of different languages possible.

Similar to ASR, the *[SeamlessM4T V2 large](https://huggingface.co/facebook/seamless-m4t-v2-large)* model was used.

## 3. Retrieval Augmented Generation:

To base the answers and suggestions to the user questions, we use retrieval augmented generation to base the answers of the LLM on the (doctor-vetted) knowledge base to be able to make factual suggestions and prevent the model from hallucinating.

For the purpose of this hackathon, we use the *[First Aid Recommendation](https://huggingface.co/datasets/badri55/First_aid__dataset)* dataset.

To encode the questions available in the dataset, we use the *[Bge v1.5 Large](https://huggingface.co/BAAI/bge-large-en-v1.5)* model.

The vectors were then indexed using the *[FAISS](https://github.com/facebookresearch/faiss)* library to enable semantic search and find similar questions to the user query and retrieve the related suggestions.

## 4. Vision Language Model:

Since the user has the ability to upload an image, we needed a vision language model to generate a description of the provided image. For this purpose, we use the *GPT-Vision Language model*.

## 5. Large Language Model:

To reason and generate suggestions based on the different inputs (User query/question, retrieved suggestions and the image description), we use a finetuned of the GPT-4. A system prompt was also included to instruct the model to come up with the correct answer.


