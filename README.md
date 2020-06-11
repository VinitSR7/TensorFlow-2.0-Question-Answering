# TensorFlow-2.0-Question-Answering

# Introduction
<ol>
  <li>This is a question an <a href = "https://en.wikipedia.org/wiki/Question_answering">open-domain question answering</a> (QA) system should be able to respond to Question Answer systems.</li>
  <li>In this case study, the goal is to predict short and long answer responses to real questions about Wikipedia articles. The dataset is provided by <a href"https://ai.google.com/research/NaturalQuestions/dataset">Google's Natural Questions </a>, but contains its own unique private test set. </li>
  <li>A <a href="https://ai.google.com/research/NaturalQuestions/visualization">visualization of examples </a>shows long and—where available—short answers.</li>
</ol>
    
# Data Overview
<ol>
  <li> 
    <h2> Data Format </h2> 
        <ol>
          <li> Each sample contains a Wikipedia article, a related question, and the candidate long form answers. </li>
          <li> The training examples also provide the correct long and short form answer or answers for the sample, if any exist.</li>
        </ol>
  </li>
  
  <li>
    <h2> File Description </h2> 
      <ol>
          <li>	simplified-nq-train.jsonl - the training data, in newline-delimited JSON format. </li>
          <li> simplified-nq-kaggle-test.jsonl - the test data, in newline-delimited JSON format. </li>
          <li> sample_submission.csv - a sample submission file in the correct format</li>
      </ol> 
  </li>

  <li>
  	<h2>Data Attributes</h2>
  		<li> document_text - the text of the article in question (with some HTML tags to provide document structure). The text can be tokenized by splitting on whitespace.</li>
  		<li> question_text - the question to be answered</li>
  		<li> long_answer_candidates - a JSON array containing all of the plausible long answers.</li>
		<li>iv.	annotations - a JSON array containing all of the correct long + short answers. Only provided for train.</li>
		<li> document_url - the URL for the full article. Provided for informational purposes only. This is NOT the simplified version of the article so indices from this cannot be used directly. The content may also no longer match the html used to generate document_text. Only provided for train.</li>
		<li> example_id - unique ID for the sample.</li>

  </li>

</ol>

# Evaluation
<ol>
	<li> Submissions are evaluated using micro F1 between the predicted and expected answers. Predicted long and short answers must match exactly the token indices of one of the ground truth labels ((or match YES/NO if the question has a yes/no short answer). There may be up to five labels for long answers, and more for short. If no answer applies, leave the prediction blank/null.</li>
	<li> Refer <a href = "https://www.kaggle.com/c/tensorflow2-question-answering/overview/evaluation">here</a> for more details </li>

</ol>
