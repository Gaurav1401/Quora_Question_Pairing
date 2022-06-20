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

### Word Embeddings
Used [Sentence tranformer](https://huggingface.co/sentence-transformers/paraphrase-MiniLM-L3-v2) and Word2Vec technique to generated embeddingss out of the two questions.

