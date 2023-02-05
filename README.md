# Personal-Expense-Labeling
In this project I show the process of how I have created and tested a model to categorize my personal expenses for my budget. The model is 92% accurate in categorizing my expenses. I've accomplished this by using TF-IDF to quantify the descriptions from my credit card and bank account exports and categorize new expenses by using cosine similarity to label new expenses each month. 

## Introduction
:)

## Fixed Charges - Charges with a consistent or nearly consistent description
* Car Repairs & Maintenance
* Car Insurance
* Cell Phone Bill
* Electric Bill
* Gym Membership & Expenses
* Income
* Rent
* Renter's Insurance
* TV Streaming Services (Sling)
* Student Loan Payments
* YouTube Subscription
## Unfixed Charges - Charges from a variety of sources with inconsistent descriptions
* Bars
* Eating Out
* Gas
* Groceries
* Juul (Nicotine Vape)
* Uber
* Miscellaneous

## How It Works/How process was trained
1) Import the raw intakes, csv exports from my bank account and credit card, into R and format the data from both sources so that it is in the same format and can be unioned
2) **add photo, data snippet, something**
3) separate fixed charges,those that have consistent descriptions, with a few simple rules  
4) separate unfixed charges into training and testing datasets
5) create dataset of descriptions & labeled categories from training data
6) clean descriptions (convert to lower case remove punctuation, remvoe stop words, remove numbers, etc.)
7) tokenize cleaned & labeled training descriptions
8) create TF-IDF matrix of labeled data
9) perform cosine similarity of each description (text) and find highest matching (i.e. most similar) text
10) create indexes of labeled descriptions for each unfixed category in training data
11) create dataset of descriptions & labeled categories from training & testing data
12) repeat steps 6 through 8 so that the new TF-IDF matrix has been created with all tokenized words in both the training and testing data
13) perform cosine similarity of each description (text) and find highest matching (i.e. most similar) text
14) for each description in the testing data assign it to the category it has the highest average cosine similarity
15) 
