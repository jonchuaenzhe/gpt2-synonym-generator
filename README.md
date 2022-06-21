# GPT2 Synonym Generator (June 2020)

Most people often have a very small vocabulary that limits the quality of their writing. This project aims to develop a model that can produce synonyms of a given word to expand the user's range of vocabulary in writing.

Refer to the README for a quick summary of the project and results, or view the notebooks for an in-depth description.

## GPT2 Background

The GPT2 is a language model developed using the Transformer architecture. It is trained to predict the next word in a given text sequence. After training on large corpuses with millions of pages, the GPT2 is able to achieve near-human level text generation, such as writing a short story on its own after being given an initial prompt. As it is trained on a large amount of data, the GPT2 has a good "understanding" of human language and is able to perform well on other language tasks after fine-tuning, such as question answering, summarization, and translation.

## Model Overview

This simple project develops a model that can generate synonyms of a user-given word by fine-tuning a GPT2 on different pairs of synonyms. The GPT2's pre-trained "understanding" of the given word will then enable it to pick out similar words from its "memory".

## Data



This project fine-tunes the GPT2 model to generate synonyms to input words. The training and test data is obtained from https://www.wordsapi.com/

In depth project descriptions are in the notebooks

HELLO!

i am a achicken

NO!
