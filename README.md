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
	    <h2> What we have to Predict </h2>
		<ol>
		  <li> 
		    For each article + question pair, we must predict / select 
		      <ol>
			<li> long and </li>
			<li> short </li>
		      </ol>
		    form answers to the question drawn directly from the article. - 
		  </li>
		  <li>  A long answer would be a longer section of text that answers the question - several sentences or a paragraph.  </li>
		  <li> A short answer might be a sentence or phrase, or even in some cases a YES/NO. The short answers are always contained within / a subset of one of the plausible long answers. -  </li>
		  <li> A given article can (and very often will) allow for both long and short answers, depending on the question
		  </li>
		  <li> There is more detail about the data and what you're predicting on the <a href="https://github.com/google-research-datasets/natural-questions/blob/master/README.md">Github</a> page for the Natural Questions dataset.</li>

		</ol> 

	  </li>	
	
</ol>

# Evaluation
<ol>
	<li> Submissions are evaluated using micro F1 between the predicted and expected answers. Predicted long and short answers must match exactly the token indices of one of the ground truth labels ((or match YES/NO if the question has a yes/no short answer). There may be up to five labels for long answers, and more for short. If no answer applies, leave the prediction blank/null.</li>
	<li> Refer <a href = "https://www.kaggle.com/c/tensorflow2-question-answering/overview/evaluation">here</a> for more details </li>

</ol>
