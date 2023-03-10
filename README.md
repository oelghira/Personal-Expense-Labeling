
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
* ![tf-idf matrix](https://user-images.githubusercontent.com/46107551/217439054-81514bd8-58c3-4eb7-a603-98b53c50f3d2.png)
9) perform cosine similarity of each description (text) and find highest matching (i.e. most similar) text
10) create indexes of labeled descriptions for each unfixed category in training data
11) create dataset of descriptions & labeled categories from training & testing data
12) repeat steps 6 through 8 so that the new TF-IDF matrix has been created with all tokenized words in both the training and testing data
13) perform cosine similarity of each description (text) and find highest matching (i.e. most similar) text
14) for each description in the testing data assign it to the category it has the highest average cosine similarity
* In more words, the indexes allowed me to group all unfixed charges from my labeled data to find the average cosine similarity of a new charge in my test data to each description in each labeled group. Then the new charge would be assigned to the category of the unfixed charges that gave the highest average cosine similarity. The code to accomplish this is below. 
```
i = 1
while(i<= nrow(total_description)){
  
  total_description$bar.similarity[i] = mean(total.similarities[i,bar.indexes])
  total_description$grocery.similarity[i] = mean(total.similarities[i,grocery.indexes])
  total_description$uber.similarity[i] = mean(total.similarities[i,uber.indexes])
  total_description$misc.similarity[i] = mean(total.similarities[i,misc.indexes])
  total_description$juul.similarity[i] = mean(total.similarities[i,juul.indexes])
  total_description$eating_out.similarity[i] = mean(total.similarities[i,eating_out.indexes])
  total_description$gas.similarity[i] = mean(total.similarities[i,gas.indexes])
  
  i = i+1
}

```

## Cross Validation  
In a 20 fold cross validation, my method has an average accuracy of 92% in correctly classifying test data. 
![CV results](https://user-images.githubusercontent.com/46107551/217437996-cb07cfee-316c-4035-be8b-9e3fbf5d7549.png)

Below are tables showing the accuracy of the 2 best and 2 worst performing categorizations of unfixed charges. Consistently eating_out and misc are the hardest unfixed charges to correctly classify. These low performing categories are a result of sparse and inconsistent data. When it comes to eating out at a resturant, I am a health nut and only go out to eat on rare occasions. When these rare occasions occur they take place at usually some place I have not been before. What this means is that there are not a lot of similar descriptions in my data at this time to improve accuracy using cosine similarity. The miscellaneous category has the problem of being applicable to too wide a range of unfixed charge descriptions everything from airline tickets to amazon purchases to a paypal or venmo purchase with a description that just says "VENMO" is included. As this category is meant to capture those one off purchases there will always be some percentage of charges that resemble another unfixed charge category. 
![CV results - accuracy](https://user-images.githubusercontent.com/46107551/218004959-b3b8a0ef-f784-4085-80e2-929eb3f04442.png)


## Visualizing The Final Personal Expesne Labeling
After my method has been validated & the code has been cleaned and runs from importing a new month to classifying all of the unfixed charges, I track how my money is spent using the table created below from the new R package mmtable2!
![result table 2 5 2023(2)](https://user-images.githubusercontent.com/46107551/217440758-139ac2f2-c0c4-4dd2-ba34-3ceee56e2762.png)


