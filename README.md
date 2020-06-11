# TensorFlow-2.0-Question-Answering

# Introduction
<ol>
  <li>This is a question an <a href = "https://en.wikipedia.org/wiki/Question_answering">open-domain question answering</a> (QA) system should be able to respond to Question Answer systems.</li>
  <li>In this case study, the goal is to predict short and long answer responses to real questions about Wikipedia articles. The dataset is provided by <a href"https://ai.google.com/research/NaturalQuestions/dataset">Google's Natural Questions </a>, but contains its own unique private test set. </li>
  <li>A <a href="https://ai.google.com/research/NaturalQuestions/visualization">visualization of examples </a>shows long and—where available—short answers.</li>
</ol>
    
# Data OverView


# Evaluation
<ol>
	<li> Submissions are evaluated using micro F1 between the predicted and expected answers. Predicted long and short answers must match exactly the token indices of one of the ground truth labels ((or match YES/NO if the question has a yes/no short answer). There may be up to five labels for long answers, and more for short. If no answer applies, leave the prediction blank/null.</li>
	<li> Refer <a href = "https://www.kaggle.com/c/tensorflow2-question-answering/overview/evaluation">here</a> for more details </li>

</ol>
