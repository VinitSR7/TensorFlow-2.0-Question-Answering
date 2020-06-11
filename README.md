# TensorFlow-2.0-Question-Answering

## Introduction
<ol>
  <li>This is a question an <a href = "https://en.wikipedia.org/wiki/Question_answering">open-domain question answering</a> (QA) system should be able to respond to Question Answer systems.</li>
  <li>In this case study, the goal is to predict short and long answer responses to real questions about Wikipedia articles. The dataset is provided by <a href = "https://ai.google.com/research/NaturalQuestions/dataset">Google's Natural Questions </a>, but contains its own unique private test set. </li>
  <li>A <a href="https://ai.google.com/research/NaturalQuestions/visualization">visualization of examples </a>shows long and—where available—short answers.</li>
</ol>
    
## Data Overview
<ol>
  <li> 
    <h3> Data Format </h3> 
        <ol>
          	<li> 
          		Each sample contains a Wikipedia article, a related question, and the candidate long form answers. 
      		</li>
          	<li> 
          	    The training examples also provide the correct long and short form answer or answers for the sample, if any exist.
          	</li>
        </ol>
  </li>
  <li>	
    <h3> What we have to Predict </h3>
        <ol>
          <li> 
            For each article + question pair, we must predict / select 
              <ol>
                <li> long and </li>
                <li> short </li>
              </ol>
            form answers to the question drawn directly from the article 
          </li>
          <li>  
             A long answer would be a longer section of text that answers the question - several sentences or a paragraph.  
       	  </li>
          <li> 
             A short answer might be a sentence or phrase, or even in some cases a YES/NO. The short answers are always contained within / a subset of one of the plausible long answers. 
          </li>
          <li> 
          	A given article can (and very often will) allow for both long and short answers, depending on the question
          </li>
          <li> 
          	There is more detail about the data and what you're predicting on the <a href="https://github.com/google-research-datasets/natural-questions/blob/master/README.md">Github </a> page for the Natural Questions dataset.
          </li></ol> 
      
  </li>
  <li>
    <h3> File Description </h3> 
      <ol>
          <li>	simplified-nq-train.jsonl - the training data, in newline-delimited JSON format. </li>
          <li> simplified-nq-kaggle-test.jsonl - the test data, in newline-delimited JSON format. </li>
          <li> sample_submission.csv - a sample submission file in the correct format</li>
      </ol> 
  </li>  
  <li>
  	<h3>Data Attributes</h3>
  	<ol>
  	<li>document_text - the text of the article in question (with some HTML tags to provide document structure). The text can be tokenized by splitting on whitespace.</li>
  	<li>question_text - the question to be answered</li>
  	<li>long_answer_candidates - a JSON array containing all of the plausible long answers.</li>
	<li>annotations - a JSON array containing all of the correct long + short answers. Only provided for train.</li>
	<li>document_url - the URL for the full article. Provided for informational purposes only. This is NOT the simplified version of the article so indices from this cannot be used directly. The content may also no longer match the html used to generate document_text. Only provided for train.</li>
	<li>example_id - unique ID for the sample.</li></ol>
</ol>

## Evaluation
<ol>
	<li> Submissions are evaluated using micro F1 between the predicted and expected answers. Predicted long and short answers must match exactly the token indices of one of the ground truth labels ((or match YES/NO if the question has a yes/no short answer). There may be up to five labels for long answers, and more for short. If no answer applies, leave the prediction blank/null.</li>
	<li> Refer <a href = "https://www.kaggle.com/c/tensorflow2-question-answering/overview/evaluation">here</a> for more details </li>

</ol>



## Modelling 
Comming Soon




## References and concepts learnt
<ol>
	<li>
		<h3>BERT:-</h3>
			<ol>
				<li><a href="https://arxiv.org/abs/1810.04805">[1810.04805] BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding</a></li>
				<li><a href="http://jalammar.github.io/a-visual-guide-to-using-bert-for-the-first-time/">	A Visual Guide to Using BERT for the First Time</a></li>
				<li>BERT is a bi-directional transformer.</li>
				<li> BERT works in two steps, First, it uses a large amount of unlabeled data to learn a language representation in an unsupervised fashion called pre-training.</li>
				<li> Then, the pre-trained model can be fine-tuned in a supervised fashion using a small amount of labeled trained data to perform various supervised tasks.</li>
				<li> Bert pre-training is done by 2 tasks called Masked Language Model(MLM) and Next Sentence Prediction (NSP). </li>
				<li> MLM makes it possible to perform bidirectional learning from the text.  The MLM pre-training task converts the text into tokens and uses the token representation as an input and output for the training. A random subset of the tokens (15%) are masked, i.e. hidden during the training, and the objective function is to predict the correct identities of the tokens.	</li>
				<li> The NSP task allows BERT to learn relationships between sentences by predicting if the next sentence in a pair is the true next or not.</li>
				<li> BERT was trained using 3.3 Billion words total with 2.5B from Wikipedia and 0.8B from BooksCorpus.</li>
			</ol>
	</li>
	<li>
		<h3> ALBERT:-</h3>
			<ol>
				<li><a href="https://arxiv.org/abs/1909.11942"> [1909.11942] ALBERT: A Lite BERT for Self-supervised Learning of Language Representations</a></li>
				<li> ALBERT is advancement over BERT, where researchers introduced three new concepts
					<ol>
						<li>
							<b> Factorized embedding parameterization: </b>
							<ol>
								<li> The model isolates the size of the hidden layers from the size of vocabulary embeddings by projecting one-hot vectors into a lower dimensional embeddings space and then to the hidden space.</li>
							</ol>
						</li>
						<li>
							<b>	Cross-layer parameter sharing: </b>
							<ol>
								<li> It shares all parameters across layers to prevent the parameters from growing along with the depth of the network.</li>
								<li> It results in 18 times less parameters compared to BERT-large.</li>
							</ol>
						</li>
						<li>
							<b>  Inter-sentence coherence loss: </b>
							<ol>
								<li> In case of pre-training, instead of using next sentence prediction technique (NSP), it uses sentence-order prediction(SOP) loss, which enable more robust multi-sentence encoding tasks</li>
							</ol>
						</li>
						<li>
							 For pretraining baseline models, researchers used the BOOKCORPUS and English Wikipedia, which together contain around 16GB of uncompressed text.
						</li>
					</ol>
				</li></ol>
	</li>
	<li>
		 <h3>XLNet:-</h3>
			<ol>
				<li><a href="https://arxiv.org/abs/1906.08237"> [1906.08237] XLNet: Generalized Autoregressive Pretraining for Language Understanding</a></li>
				<li>  XLNet was trained with over 130 GB of textual data and 512 TPU chips.</li>
				<li> XLNet is a large bidirectional transformer that is an advancement in training methodology from BERT, trained with larger data to achieve better performance than BERT on 20 language tasks.</li>
				<li> XLNet introduces the concept of permutation language modeling, i.e where all tokens are predicted but in random order.  This helps the model to learn bidirectional relationships and therefore better handles dependencies and relations between words</li>
				<li> Base architecture for XLNet is Transformer XL, which showed good performance even in the absence of permutation based training. </li>
			</ol>
	</li>
	<li>
		<h3>RoBERTa:-</h3>
			<ol>
				<li> RoBERTa uses 160 GB of text for pre-training, including 16GB of Books Corpus and English Wikipedia used in BERT.</li>
				<li> Robustly optimized BERT approach RoBERTa, is a retraining of BERT with improved training methodology, 1000% more data and compute power. </li>
				<li> RoBERTa removes the Next Sentence Prediction (NSP) task from BERT’s pre-training and introduces dynamic masking so that the masked token changes during the training epochs.</li>
				<li> As a result, RoBERTa outperforms both BERT and XLNet on GLUE benchmark results.</li>
			</ol>
	</li> 
	<li>
		Comparison Between all the above models<br><img src="https://github.com/VinitSR7/TensorFlow-2.0-Question-Answering-/blob/master/PDF/Picture1.jpg?raw=true"></li>
	<li>
		Hugging Face Transformers for Question Answering
		<ol>
			<li>
				<a href="https://www.appliedaicourse.com/lecture/11/applied-machine-learning-online-course/4216/code-walkthrough-bert-questionanswering-system/8/module-8-neural-networks-computer-vision-and-deep-learning">Bert Fine Tuining Code Walk Through</a>
			</li>
			<li>
				<a href="https://huggingface.co/transformers/usage.html">Hugging face Transformer Usage</a>
			</li>
			<li><a href="https://www.youtube.com/watch?v=XaQ0CBlQ4cY"> Text Extraction From a Corpus Using BERT (AKA Question Answering)</a></li>
		</ol> 
	</li>
</ol>
 
