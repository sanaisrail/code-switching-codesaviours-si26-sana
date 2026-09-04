# Code-Switching Language Detection

## Project Overview

This project focuses on detecting language at the word level in code-switched sentences. The dataset contains Urdu, English, and mixed-language words, and an XLM-RoBERTa model is trained to classify each word into one of three categories: URD, ENG, or MIX.

This project was developed as part of the Code Saviours ML/AI Internship, Batch SI-26.

## Week 6 – Dataset Creation

In Week 6, a manually labeled code-switching dataset was created for token classification.

The dataset contains:

* 2166 word-level entries
* 200 unique sentences
* 3 language labels:

  * URD – Urdu
  * ENG – English
  * MIX – Mixed Urdu-English word

The dataset was stored in CSV format with the following columns:

* `sentence`
* `word`
* `label`

The final label distribution was:

* URD: 1084
* ENG: 1042
* MIX: 40

The dataset was checked to make sure that the sentences contain code-switched language examples.

## Week 7 – Model Training

In Week 7, the prepared dataset was used to train an XLM-RoBERTa model for token classification.

### Data Preparation

The dataset was grouped sentence-wise so that each sentence contained a list of words and their corresponding labels.

The data was then divided into:

* 80% Training Data – 160 sentences
* 20% Testing Data – 40 sentences

The labels were converted into numerical IDs:

* URD → 0
* ENG → 1
* MIX → 2

### Tokenization

The XLM-RoBERTa tokenizer was used to convert words into tokens.

The original word-level labels were aligned with the generated tokens. Special tokens and additional sub-tokens were ignored during training using `-100`.

### Model

The model used in this project is:

`xlm-roberta-base`

It was configured for token classification with three labels:

* URD
* ENG
* MIX

### Training

The model was trained using the Hugging Face Transformers Trainer API.

Training configuration:

* Epochs: 5
* Training batch size: 16
* Evaluation batch size: 16
* Evaluation: After each epoch
* Model saving: After each epoch
* GPU: Tesla T4
* Mixed precision: Enabled when GPU was available

The training loss decreased from 1.0843 in the first epoch to 0.1934 in the fifth epoch.

The validation loss decreased from 0.5533 to 0.2267.

## Model Evaluation

The trained model was evaluated on the test dataset using accuracy, precision, recall, and F1-score.

### Overall Accuracy

**92.09%**

### Classification Report

| Label | Precision | Recall | F1-Score |
| ----- | --------- | ------ | -------- |
| URD   | 0.94      | 0.89   | 0.92     |
| ENG   | 0.90      | 0.94   | 0.92     |
| MIX   | 1.00      | 1.00   | 1.00     |

The model successfully classified Urdu, English, and mixed-language words. The MIX category achieved a perfect F1-score of 1.00 on the test set.

## Testing on New Sentences

The trained model was also tested on new code-switching sentences containing words such as:

* `msging`
* `downlod`
* `meetng`
* `passwrd`
* `presentatn`

The model was able to identify several mixed-language words as `MIX` and distinguish them from Urdu and English words.

## Model Saving

After training and evaluation, the trained model and tokenizer were saved locally using the Hugging Face Transformers library.

The saved model can be reused for future testing and deployment without retraining from scratch.

## Hugging Face Model

The trained token classification model was published on Hugging Face Hub.

Model repository:

https://huggingface.co/sanaisrail/code-switching-codesaviours-si26-sana

The model was successfully loaded again from Hugging Face using `AutoModelForTokenClassification`, confirming that the published model is available for use.

## Technologies Used

* Python
* Google Colab
* Pandas
* Scikit-learn
* PyTorch
* Hugging Face Transformers
* Hugging Face Datasets
* XLM-RoBERTa
* Hugging Face Hub

## Project Workflow

1. Create and label the code-switching dataset.
2. Save the dataset in CSV format.
3. Check dataset size and label distribution.
4. Group words and labels by sentence.
5. Split the dataset into training and testing sets.
6. Convert labels into numerical IDs.
7. Tokenize the dataset using XLM-RoBERTa.
8. Align word-level labels with tokens.
9. Train the XLM-RoBERTa token classification model.
10. Evaluate the model using accuracy and classification metrics.
11. Test the model on new sentences.
12. Save the trained model and tokenizer.
13. Publish the model on Hugging Face Hub.
14. Load the published model to verify successful deployment.

## Result

The final XLM-RoBERTa token classification model achieved an overall accuracy of **92.09%** on the test dataset.

The model successfully supports three categories:

**URD | ENG | MIX**

This demonstrates that the trained model can identify language at the word level in code-switched text.

