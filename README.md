June 2020
# GPT2 Synonym Generator

Most people have a small vocabulary that limits their writing quality. This project develops a model that generates synonyms of a given word to expand the user's vocab range. Refer to this README for a quick summary of the project and results, or view the notebooks for an in-depth description.

Below are some examples of synonyms generated from an unseen test set:
```
brilliance <|startgen|> brilliancy luster lustre radiance exultation
tribute <|startgen|> homage respect due thankfulness thank
```

## GPT2 Background

The GPT2 is a language model with a Transformer architecture that is trained to predict the next word of a sentence. After training on millions of pages, it can achieve near-human level text generation, such as writing a short story on its own after being given a prompt. The GPT2 has a good "understanding" of human language and is able to perform well on other language tasks after fine-tuning, such as question answering, summarization, and translation. Fine-tuning involves training it on a much smaller set of application specific data.

## Model Overview

This model generates multiple synonyms of a user-input word by fine-tuning a GPT2 on different pairs of synonyms. The GPT2's pre-trained "understanding" of the given word enables it to pick out similar words from its "memory".

## Data & Preprocessing

8740 common words and its synonyms (1-5 synonyms) were obtained from https://www.wordsapi.com/. About 10% of the data was kept as testing data, while the other 8000 words (and synonyms) were used to train the model. As the GPT2 is a language model, the input data has to be a single piece of text. Thus, each group of words (given word and its synonyms) were arranged as such:

```
"given_word <|startgen|> synonym_1 synonym_2 synonym_3 synonym_4 synonym_5 <|endgen|>"
```

All the 8000 groups were then concatenated into a single string and saved in data/train_string.txt.

## GPT2 Finetuning

A pre-trained GPT2 model was installed from https://pypi.org/project/gpt-2-simple/ and after setting up the environment and loading the model, the finetune function was called:

```
sess = gpt2.start_tf_sess()
gpt2.finetune(sess,
              dataset="data/train_string.txt",
              model_name='345M',
              steps=2500,
              learning_rate = 2e-5,
              restore_from='fresh'
              )
```

Early stopping was employed to prevent the model from overfitting to the small fine-tuning set.

## Synonym Generation

Synonyms were generated from the trained model by using the prefix "given_word <|startgen|>", and running the generate function. The generation was truncated when the "<|endgen|>" token was encountered.

```
gpt2.generate(sess,
              length=250,
              temperature=0.7,
              prefix=f"{word} <|startgen|>",
              truncate='<|endgen|>'
              )
```

## Results

Some good results were generated from the test set:

```
brilliance <|startgen|> brilliancy luster lustre radiance exultation
tribute <|startgen|> homage respect due thankfulness thank
nurture <|startgen|> educate groom raise model
disposition <|startgen|> attitude outlook
```

However, there were also some poor results:

```
auxiliary <|startgen|> auxiliary annunciate prophetic
follow <|startgen|> ah! ahh! ahhh! ahh!
```

A fine-tuning set larger than the existing 8000 words (which is relatively small for NLP purposes) would likely lead to much better results.