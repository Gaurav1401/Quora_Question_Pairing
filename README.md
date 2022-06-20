# Quora_Question_Pairing
## Problem Statement
Multiple questions with the same intent can cause seekers to spend more time finding the best answer to their question, and make writers feel they need to answer multiple versions of the same question. The objective is to predict which of the provided pairs of questions contain two questions with the same meaning. The ground truth is the set of labels that have been supplied by human experts. 

## Attributes
 - **id** :- the id of a training set question pair.
 - **qid1**, **qid2** - unique ids of each question.
 - **question1**, **question2** - the full text of each question.
 - **is_duplicate** - the target variable, set to 1 if question1 and question2 have essentially the same meaning, and 0 otherwise.

## My Approach
### Basic Feature Engineering
 - Number of words in each of the question.
 - Number of characters in each of the quesitons.
 - Difference in number of words in each question.
 - Number of common words in both of the questions.
 - Shared words ratio :- Number of common words/total words in both the question.
 - first_word_eq:- 1 if first word is same else 0.
 - last_word_eq:- 1 if last word is same else 0.

### Advanced Feature Engineering
Used [FuzzyWuzzy](https://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/) library to calculate different similarities between both the questions.

### Text Preprocessing
Preprocessed the text in both the question column in the following ways:
 - Converted the string to lower.
 - Removed digits, special characters, unwanted spaces, stopwords.
 - expanded the contracted words.
 - Lemmatization. 

### Word Embeddings
Used [Sentence tranformer](https://huggingface.co/sentence-transformers/paraphrase-MiniLM-L3-v2) and Word2Vec technique to generated embeddings out of the two questions.
<br><br>
**There were two final datasets, one with base and derived features and Word2Vec embeddings having the final dimensionality of (404290, 618) and the other one was having the base and derived features and word embeddings generated from sentence transformer having the dimensionality of (404290, 786).**

### Performance Metric Used
**Log Loss**
 - Ranges from 0-∞.
 - **Lower** the score, better the model performance is.

### Final Results
Model | Embeddings | Score
--- | --- | ---
Logistic Regression | Word2Vec | **0.4785**
Logistic Regression | Sent2Vec | **0.4727**
SVM | Word2Vec | **0.4797**
SVM | Sent2Vec | **0.4735**
Xgboost | Word2Vec | **0.3686**
Xgboost | Sent2Vec | **0.3861**


Here we can see that **Xgboost** is giving the best results on **Word2Vec** embeddings data.

## Conclusions:-
 - Logistics regression performance improves as the dimensionality of data increases as we can see the results above.
 - As the dimesionality of data increases, the Xgboost slows down.
<br>
Both the above conclusions can be easily explained and understood by learning the intuition behind both the algorithms.

## Future Work:-
 - Use of better sentence transformer to generate the embeddings can definitely imporve the results(But we require better computational power for that).
 - Other Boosting algorithms like Catboost and LightGBM can also be used in this case.
