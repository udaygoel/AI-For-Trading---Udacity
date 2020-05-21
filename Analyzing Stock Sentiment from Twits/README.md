# Analyzing Stock Sentiment from Twits
In this project, a deep learning model using Embedding and LSTM is built in PyTorch to classify the sentiment of messages from [StockTwits](https://stocktwits.com/), a social network for investors and traders. The model is able to predict if any particular message is positive or negative. From this, we are able to generate a signal of the public sentiment for various ticker symbols.

### Project Files

The project uses these files and folders:

- [Analyzing_Stock_Sentiment_Twits.ipynb](https://github.com/udaygoel/AI-For-Trading-Udacity/blob/master/Analyzing%20Stock%20Sentiment%20from%20Twits/Analyzing_Stock_Sentiment_Twits.ipynb): This Jupyter Notebook covers the project. 
- test_twits.json: Testing data set for the twits

This repository does not include the training and validation set created by Udacity for this project due to size constraints.

### Contents

There are 4 main sections of the Project.

1.  Importing Twits and splitting data into message and score

2. Preprocessing the Data

   - Removing ticker symbols (denoted with a leader $ symbol), usernames (denoted with a leader @ symbol) and URLs
   - The messages are converted to lowercase, tokenized and lemmatized for verbs and nouns
   - Creating a vocabulary through a bag of words, while removing the most common words and the rare words.
   - Balancing the classes: Roughly 50% of the twits are labelled as neutral. This means the network will be 50% accurate just by guessing 'neutral'. To help the network learn appropriately, the classes are balanced by dropping some neutral sentiment twits randomly so that 20% of the remaining twits are now neutral.

3. Neural Network

   The network is developed using PyTorch. The architecture of the network is designed as:

   - Embedding Layer - converts the vocabulary to an Embedding Table. 
   - LSTM Layer
   - Dropout Layer
   - Fully Connected Layer with LogSoftmax activation 
   - Overnight Sentiment Smoothed Factor

   The twits are split into training (80%) and validation (20%) sets. The model is trained for 5 epochs. The gradients are clipped to avoid exploding gradients during backpropagation. 

   The network is able to achieve more than 70% validation accuracy.

4. Testing

   The trained network is tested using the twits in test_twits.json file. This dataset does not have the sentiment scores and so a testing accuracy cannot be calculated. By running the sentiment prediction on selected twits, we can see the scores given to each of the 5 classes.



The project illustrates how a deep learning network using LSTMs can be created for sentiment analysis on stocks. This work can be enhanced by optimizing the architecture and hyperparameters of the network and also checking the accuracy on a testing set.