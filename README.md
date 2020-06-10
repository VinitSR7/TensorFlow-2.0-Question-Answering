# TensorFlow-2.0-Question-Answering-
https://www.kaggle.com/c/tensorflow2-question-answering/notebooks
Overview
Introduction
This is a question an open-domain question answering (QA) system should be able to respond to Question Answer systems.
In this case study, the goal is to predict short and long answer responses to real questions about Wikipedia articles. The dataset is provided by Google's Natural Questions, but contains its own unique private test set. 
A visualization of examples shows long and—where available—short answers.
Data Overview
Data Format
Each sample contains a Wikipedia article, a related question, and the candidate long form answers. 
The training examples also provide the correct long and short form answer or answers for the sample, if any exist.
What we have to Predict
For each article + question pair, we must predict / select 
long and 
short 
form answers to the question drawn directly from the article. - 
A long answer would be a longer section of text that answers the question - several sentences or a paragraph. - 
A short answer might be a sentence or phrase, or even in some cases a YES/NO. The short answers are always contained within / a subset of one of the plausible long answers. - 
A given article can (and very often will) allow for both long and short answers, depending on the question.
There is more detail about the data and what you're predicting on the Github page for the Natural Questions dataset.
File Description 
simplified-nq-train.jsonl - the training data, in newline-delimited JSON format.
simplified-nq-kaggle-test.jsonl - the test data, in newline-delimited JSON format.
sample_submission.csv - a sample submission file in the correct format
Data Attributes
document_text - the text of the article in question (with some HTML tags to provide document structure). The text can be tokenized by splitting on whitespace.
question_text - the question to be answered
long_answer_candidates - a JSON array containing all of the plausible long answers.
annotations - a JSON array containing all of the correct long + short answers. Only provided for train.
document_url - the URL for the full article. Provided for informational purposes only. This is NOT the simplified version of the article so indices from this cannot be used directly. The content may also no longer match the html used to generate document_text. Only provided for train.
example_id - unique ID for the sample.
Evaluation
Submissions are evaluated using micro F1 between the predicted and expected answers. Predicted long and short answers must match exactly the token indices of one of the ground truth labels ((or match YES/NO if the question has a yes/no short answer). There may be up to five labels for long answers, and more for short. If no answer applies, leave the prediction blank/null.
Refer here for more details 

Research-Papers/Solutions/Architectures/Kernels
BERT :- 
[1810.04805] BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding
A Visual Guide to Using BERT for the First Time
BERT is a bi-directional transformer.
BERT works in two steps, First, it uses a large amount of unlabeled data to learn a language representation in an unsupervised fashion called pre-training.
Then, the pre-trained model can be fine-tuned in a supervised fashion using a small amount of labeled trained data to perform various supervised tasks.
Bert pre-training is done by 2 tasks called Masked Language Model(MLM) and Next Sentence Prediction (NSP). 
MLM makes it possible to perform bidirectional learning from the text.  The MLM pre-training task converts the text into tokens and uses the token representation as an input and output for the training. A random subset of the tokens (15%) are masked, i.e. hidden during the training, and the objective function is to predict the correct identities of the tokens.	
The NSP task allows BERT to learn relationships between sentences by predicting if the next sentence in a pair is the true next or not.
BERT was trained using 3.3 Billion words total with 2.5B from Wikipedia and 0.8B from BooksCorpus.
ALBERT
[1909.11942] ALBERT: A Lite BERT for Self-supervised Learning of Language Representations
ALBERT is advancement over BERT, where researchers introduced three concepts
Factorized embedding parameterization:
The model isolates the size of the hidden layers from the size of vocabulary embeddings by projecting one-hot vectors into a lower dimensional embeddings space and then to the hidden space.
Cross-layer parameter sharing:
It shares all parameters across layers to prevent the parameters from growing along with the depth of the network.
It results in 18 times less parameters compared to BERT-large.
Inter-sentence coherence loss:
In case of pre-training, instead of using next sentence prediction technique (NSP), it uses sentence-order prediction(SOP) loss, which enable more robust multi-sentence encoding tasks
For pretraining baseline models, researchers used the BOOKCORPUS and English Wikipedia, which together contain around 16GB of uncompressed text.
XLNet:
[1906.08237] XLNet: Generalized Autoregressive Pretraining for Language Understanding
XLNet was trained with over 130 GB of textual data and 512 TPU chips.
XLNet is a large bidirectional transformer that is an advancement in training methodology from BERT, trained with larger data to achieve better performance than BERT on 20 language tasks.
XLNet introduces the concept of permutation language modeling, i.e where all tokens are predicted but in random order.  This helps the model to learn bidirectional relationships and therefore better handles dependencies and relations between words\
Base architecture for XLNet is Transformer XL, which showed good performance even in the absence of permutation based training. 
RoBERTa:
RoBERTa uses 160 GB of text for pre-training, including 16GB of Books Corpus and English Wikipedia used in BERT. 
Robustly optimized BERT approach RoBERTa, is a retraining of BERT with improved training methodology, 1000% more data and compute power. 
RoBERTa removes the Next Sentence Prediction (NSP) task from BERT’s pre-training and introduces dynamic masking so that the masked token changes during the training epochs.
As a result, RoBERTa outperforms both BERT and XLNet on GLUE benchmark results.
Comparison Between all the above models.
Seems like ALBERT and RoBERTa are the most dominant model.
Hugging Face Transformers for Question Answering 
Applied Course
Usage — transformers 2.11.0 documentation
Text Extraction From a Corpus Using BERT (AKA Question Answering)
HuggingFace question / BertForQuestionAnswering
Kernels:-
RoBERTa [fastai, HuggingFace 🤗Transformers]
Exploratory data analysis and baseline
Applied Course
