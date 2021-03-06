# Multi Class Text Classification on Seinfeld Transcripts
*Seinfeld* is a sitcom created by Jerry Seinfeld and Larry David where the 4 main characters of Elaine, George, Jerry,
and Kramer navigate their lives through various fictious problems. At the time, the show pioneered a notion of being
about "nothing" and purely focused on the trivial happenings of daily life with a comedic outlook.

The show has been studied in many [qualitative applications](https://www.youtube.com/watch?v=sp79Q8Scyi8), however this project explores using quantitative
methods to analyze and understand if there are patterns in Jerry and Larry's transcripts of the show. This project
focuses on predicting which main character (elaine, george, jerry, kramer) would say a certain line by using natural 
language processing algorithms such a Naive Bayes and distilBERT.

Overall, Naive Bayes was able to predict 10% than baseline accuracy and distilBERT was able to predict 97% better than
baseline accuracy

--------
### Project Files

The project was coded in python with jupyter notebooks.

The data for this project was obtained by scraping [Seinfeld Scripts](https://www.seinfeldscripts.com/seinfeld-scripts.html)
using the notebook [Data Scraper.ipynb](https://github.com/Victor-Denisov/Seinfield-Transcripts-NLP/blob/main/Data%20Scraper.ipynb)

Data cleaning, data analysis, model building, and model analysis was compeleted using the notebook [Text Classification NLP](https://github.com/Victor-Denisov/Seinfield-Transcripts-NLP/blob/main/Data%20Scraper.ipynb)

--------
### Project Summary

Before jumping into model analysis, its useful to understand the distribution of character lines in the Seinfeld transcripts
Jerry has the most lines followed by George, Elaine, and Kramer.

![characterdistribution](https://github.com/Victor-Denisov/Seinfield-Transcripts-NLP/blob/main/images/character_lines_distribution.PNG "Character Distribution")

#### Naive Bayes Model

Naive bayes is a supervised learning algorithm that uses probabilistic classification (via Bayes' theorem) to predict an outcome

The model was able to predict with 42% accuracy, which is 4% higher than the baseline accuracy of 38% (always predicting Jerry).
Its also interesting to note the recall for jerry is fairly high at 0.91 with low prevision 0.41, meaning that it believes many lines belong to Jerry
(unsurprisingly as he is a writer on the show).

![detailNB](https://github.com/Victor-Denisov/Seinfield-Transcripts-NLP/blob/main/images/detail_nb.PNG "NB Details")

The confusion matrix below describes the performance of Naive Bayes by comparing the predicted values to the true value. 
The diagonal that aligns with characters on each axis represents a correct prediction ([elaine,elaine] = 140) and the rest being incorrect
([elaine,george]).

We can identify that the model primarily predicts jerry for all characters as its a safe bet - jerry has the most lines out of all characters.

![cf nb](https://github.com/Victor-Denisov/Seinfield-Transcripts-NLP/blob/main/images/cf_nb.PNG "Confusion Matrix - NB")

A receiver operating characteristic (ROC) curve describes performance of a classification model by graphing true positive rate vs false positive rate.

It is interesting to note that Kramer is above all other characters in the ROC, which could mean that Naive Bayes can identify
Kramer's lines the best out of all characters (based on TPR vs. FPR)

![roc nb](https://github.com/Victor-Denisov/Seinfield-Transcripts-NLP/blob/main/images/roc_nb.PNG "ROC - NB")

#### DistilBERT Model

Bidirectional Encoder Representations from Transformers (BERT) is a transformer-based machine learning technique for natural language processing (NLP) developed by Google.
[DistilBERT](https://huggingface.co/transformers/model_doc/distilbert.html) is a "distilled" version of a BERT model that retains 97% of its language understanding capabilities, 
while being 60% faster but with 40% less parameters.

DistilBERT (dBERT) was able to predict with 74% accuracy, which is 36% higher than the baseline accuracy of 37% (always predicting Jerry). This was also achieved via 5 epochs.
Compared to Naive Bayes, dBERT is able to predict with significantly better precision as when we analyze Jerry, recall remains high but precision is much higher than for Naive Bayes.

![dbert details](https://github.com/Victor-Denisov/Seinfield-Transcripts-NLP/blob/main/images/detail_dbert.PNG "dbert Details")

The confusion matrix for dBERT proves the model's good performance as the predictions align closely to the true value

![cf dbert](https://github.com/Victor-Denisov/Seinfield-Transcripts-NLP/blob/main/images/cf_dbert.PNG "Confusion Matrix - distilBERT")

The ROC for dBERT is 0.9 which indicates strong performance as well. If we compare again to Naive Bayes, its interesting to see the same pattern
of Kramer's TPR vs. FPR line (in red) being above other characters. Kramer has the highest precision but lowest recall of the characters, which could mean that the
model is able to identify kramer's lines the best from other characters. Kramer also had the least number of lines, which could also be an attributing factor.

![roc dbert](https://github.com/Victor-Denisov/Seinfield-Transcripts-NLP/blob/main/images/roc_dbert.PNG "ROC - distilBERT")

--------
### Conclusions and After-thought

This project proves that state of the art NLP algorithms such as distilBERT are capable of somewhat reliably predicing transcript lines for chracters in the sitcom Seinfeld.
There are certain biases to be aware of, in particular that the Jerry was a writer in the show so naturally his cadence of thought will follow his character.
A more robust analysis would be to run NLP on other shows where the writers aren't casted in the show. However given Seinfelds popularity, its not a surprise that an algorithm
can decisively predict characters as there is a clear structure, role, and purpose for each character. Seinfeld borrows concepts from [Dan Harmon's writing circle](https://blog.reedsy.com/guide/story-structure/dan-harmon-story-circle/),
which is attractive for a 22-24 minute show characters seemingly change over the course of time even though the plot is seemingly about nothing.

An interesting exercise would be to run the same analysis on a show such as "Curb Your Enthusiasm" because Curb's transcripts are only written based on the plot for the episode.
Afterwards, the entire show is improvisation and it could be insightful to understand whether a modern NLP would still be able to predict certain characters like Larry, Leon, etc.

