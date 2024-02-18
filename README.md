Full blog link is https://minimatech.org/fine-tuning-bert-for-sentiment-analysis/

## Introduction

Using a pre-trained Language Model like BERT (Bidirectional Encoder Representations from Transformers), we can leverage contextual embeddings to enhance the ability to understand and analyze natural language text. This blog will look into the process of fine-tuning BERT for sentiment analysis classification, building a classifier on top of the transformer to adapt it to a certain use case.

BERT is a transformer-based model that is pretrained on a large corpus of text using techniques like: attention, masked language modeling and next sentence prediction. This pre-training enabled BERT to capture a deep understanding of language nuances, context, and grammar.

## The Dataset

We will be using [IMDB Movie Review dataset](https://www.kaggle.com/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews). The data consists of a review (free text) and the sentiment, whether it is positive or negative.

We will not go in depth on how to deal with text data and preprocess it for modeling. The article focuses on the fine-tuning part. Of course, with more text preprocessing we will achieve better results and it is the best practice.

## Fine-Tuning BERT

BERT excels in understanding the text and producing contextual embeddings that capture very well the essence of a text. These embeddings can be very helpful in so many cases like our use case but we'd like to somehow adapt it (fine-tune) to our data so that it aligns with the task's requirements i.e. mapping the text to a sentiment. The process will involve adding a task-specific layer on top of BERT's output and training the model on the dataset. So technically speaking, we will add a linear layer on top of the contextualized embeddings layer of BERT `pooler_output`.

`pooler_output` represents the embedding of the CLS (classification) token passed through some more layers. In BERT it is used to predict whether or not Sentence2 is a sentence that directly follows Sentence1 in "next sentence prediction" task. So CLS is a token that represents the entire sequence i.e. sentence-level understanding. And as pooler_output is basically the embedding at CLS transformed with a linear layer, we will use pooler_output as a representation of the contextualized information about the input sequence on top of which we will add a task-specific linear layer to fine-tune the model to our task i.e. binary classifying the input to positive or negative.
