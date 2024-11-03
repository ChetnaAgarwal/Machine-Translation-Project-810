# PROJECT DETAILS:

As a part of my masters curriculum, I did this Machine Learning Translation Project. 
In this, I prepared data and fine-tuned a machine translation model to convert Hinglish (a sentence consisting of a combination of 2 languages, English and Hindi) into pure English. This was a low resources problem.
This project was focused at coming up with novel solutions for the code mixed Machine Translation subtask 2 of WMT Competition (https://statmt.org/wmt22/code-mixed-translation-task.html). 
The data provided for this task was the PHINC dataset which consisted of 13.7k parallel sentences in the Hinglish and the English languages. Both the source and target languages were written in roman script.
1. My work involved first making baseline models from previous works. 
2. I found certain datasets online to increase the accuracy of the baseline model. There weren't much datasets that gave Hinglish to English translations, but I managed to get the number of data points from 13.7k (from PHINC dataset) to about 20k (using data from last years WMT competition, Kaggle Hg-Eng dataset, and custom data that I created using backtranslation and transliteration).
3. To increase the accuracy, I created a dataset using English sentences from the datasets ‘jigsaw-toxic-severity-rating’ dataset (from Kaggle) and ‘hate speech and offensive language’ dataset. These datasets contain simple English sentences.
4. I used mBART50 pretrained model to convert the English sentences into Devanagari Hindi sentences. I further converted these Devanagari to Roman Hindi using a transliteration script.
5. Using all the above data, trained many Seq2Seq models (BERT, M2M-100, Mbart50, T5) iteratively and evaluated these using BLEU score. The additional data I created allowed me to considerably increase the performance of the resulting model.
6. The best performing model achieved a BLEU Score that was 4 points higher than state-of-the-art benchmarks.

# DATASET CREATION 

The data creation process effectively creates a Romanized Hindi dataset from English text using translation and transliteration techniques, which can be used for language processing tasks such as hate speech analysis in Hinglish or other low-resource NLP tasks. The steps automate the collection, translation, transliteration, and saving of transformed text. The code produces a dataset where English sentences are translated to Hindi, then transliterated to Roman script, and saved for future Hinglish analysis.

### STEP BY STEP GUIDE:
(Code for this step can be found in the file: 810_custom_dataset_generation_script_contains_backtranslation_and_transliteration (1).ipynb)

1. Import Libraries and Load Data: Load numpy and pandas libraries for data handling. Load an English language dataset from a CSV file and extract a subset of tweets. Here, around 6300 new data points are created in batches on 100 samples.

2. Install and Import Necessary Packages: Install sentencepiece and transformers for working with language models. Load the mBART model and tokenizer to translate between languages, specifically English to Hindi.

3. Define Hindi-to-Roman Transliteration Mappings: Create dictionaries to map Hindi vowels and consonants to Romanized characters. Save Transliteration Mappings, ie, the vowel and consonant mappings to CSV files for later use.

4. Define a Transliteration Function: Create a function to convert Hindi text into Romanized text using the vowel and consonant mappings.

6. Define an English-to-Hindi Translation Function: Define a function to translate English sentences into Hindi using mBART, then transliterate the Hindi output to Romanized text.

7. Translate English Text to Romanized Hindi: Apply the translation function to each sentence in the selected dataset, storing the Romanized Hindi results in a list.
Save the English text and Romanized Hindi translations to a CSV file.

8. Repeat Process on Another Dataset

9. Combine all the data obtained from separate runs into a master CSV file.

# MODEL TRAINING

This part performs the translation task with fine-tuning of the mBART model on Hinglish-to-English data, and then evaluates the model’s performance based on BLEU scores.

### STEP BY STEP GUIDE:

1. Setup: Imports necessary libraries like numpy, pandas, and Hugging Face's transformers. It mounts Google Drive to save data and installs required packages (transformers, datasets, etc.).

2. Data Preparation: Loads training and validation datasets, which contain Hinglish sentences and their English translations. It processes the datasets to create dictionaries of sentences, then converts them into a datasets.Dataset format.

3. Tokenization: Loads the mBART tokenizer and prepares the data for training by tokenizing sentences, setting maximum input lengths for consistency.

4. Model Initialization: Loads the mBART model, which is pretrained to handle multilingual tasks, for conditional generation tasks.

5. Training Preparation: Sets up a training configuration, defining parameters like batch size, learning rate, and number of epochs.

6. Trainer Setup: Uses Hugging Face’s Seq2SeqTrainer to handle the training loop, evaluation, and metrics computation (BLEU score for translation accuracy). Training begins with trainer.train().

7. Test Set Processing: Loads test data, applies the same preprocessing and tokenization steps, and evaluates it against the model to generate predictions.

8. BLEU Score Calculation: Compares model predictions against true translations using the BLEU score to measure accuracy.

9. Model Saving: Saves the trained model to Google Drive. Finally, it saves and loads the model state to allow for further testing or use outside the training environment.

# CODE SCREENSHOTS


![Image1](810%20screenshots%20of%20code%20and%20results/pic1.png)

![Image2](810%20screenshots%20of%20code%20and%20results/pic2.png)

![Image3](810%20screenshots%20of%20code%20and%20results/pic3.png)

# RESULT

![Image4](810%20screenshots%20of%20code%20and%20results/pic4.png)

# EXAMPLE 
- X_test[0]: Original English sentence in kaggle dataset
- stripped_preds[0]: The result obtained after transliteration, backtranslation, and inference from the model trained.

![Image5](810%20screenshots%20of%20code%20and%20results/pic5.png)




