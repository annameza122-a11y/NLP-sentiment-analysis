# NLP-sentiment-analysis
Sentiment analysis project.

# Overview
This project implements a sentiment analysis system trained on Amazon product reviews.
The system classifies a given text input as either a positive or negative review.
The final deliverable is a website where a user can enter a review and receive a sentiment prediction.

## Team Members
- Ana Meza — Data Cleaning and GitHub Management
- Jonathan Edward — Model Training and Website Development

## Dataset
Amazon Multi-Domain Sentiment Dataset
Source: http://www.cs.jhu.edu/~mdredze/datasets/sentiment/index2.html

The dataset contains Amazon product reviews across 4 categories:
- Books
- DVD
- Electronics
- Kitchen and Housewares

Each category contains labelled positive and negative reviews.

## Project Structure




## My Contribution - Data Cleaning
The data cleaning notebook covers the following steps:
1. Load all raw reviews from all 4 categories
2. Parse the XML-like review files
3. Clean the text (remove HTML, URLs, punctuation, contractions)
4. Remove outliers (reviews that are too short or duplicates)
5. Balance the dataset to ensure equal positive and negative samples
6. Shuffle and export the cleaned data for model training

## Ethical Considerations
- The original dataset may contain unequal numbers of positive and negative reviews.
  This was addressed by undersampling the majority class to ensure a balanced dataset.
- Very short reviews (under 10 words) were removed as they do not provide enough
  context for accurate sentiment classification.
- Reviews across all 4 product categories were included to avoid category bias.
- The dataset only contains English reviews which limits the model to English input.

## How to Run the Data Cleaning Notebook
1. Open the notebook in Google Colab
2. Download from: http://www.cs.jhu.edu/~mdredze/datasets/sentiment/index2.html
3. Run all cells in order
4. The cleaned dataset will be downloaded as cleaned_reviews.json

