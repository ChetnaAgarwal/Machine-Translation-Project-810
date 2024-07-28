# Machine-Translation-Project-810

PROJECT DETAILS:

I prepared data and fine-tuned a machine translation model to convert Hinglish (a sentence consisting of a combination of 2 languages, English and Hindi) into pure English. 
This project was focused at coming up with novel solutions for the code mixed Machine Translation subtask 2 of WMT Competition (https://statmt.org/wmt22/code-mixed-translation-task.html). 
The data provided for this task was the PHINC dataset which consisted of 13.7k parallel sentences in the Hinglish and the English languages. Both the source and target languages were written in roman script.
1. My work involved first making baseline models from previous works. 
2. I found certain datasets online to increase the accuracy of the baseline model. There weren't much datasets that gave Hinglish to English translations, but I managed to get the number of data points from 13.7k (from PHINC dataset) to about 20k (using data from last years WMT competition, Kaggle Hg-Eng dataset, and custom data that I created using backtranslation and transliteration).
3. To increase the accuracy, I created a dataset using English sentences from the datasets ‘jigsaw-toxic-severity-rating’ dataset (from Kaggle) and ‘hate speech and offensive language’ dataset. These datasets contain simple English sentences.
4. I used mBART50 pretrained model to convert the English sentences into Devanagari Hindi sentences. I further converted these Devanagari to Roman Hindi using a transliteration script.
5. Using all the above data, trained many Seq2Seq models iteratively and evaluated these using BLEU score. The additional data I created allowed me to considerably increase the performance of the resulting model.
