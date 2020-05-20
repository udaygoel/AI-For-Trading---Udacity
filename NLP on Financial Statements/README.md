# NLP on Financial Statements
In this project, a NLP analysis is performed on 10-K financial statements to generate an alpha factor. For the dataset, the end of day prices are taken from Quotemedia and sentiment words for [Loughran-McDonald sentiment word lists](https://sraf.nd.edu/textual-analysis/resources/#LM Sentiment Word Lists).

### Project Files

The project uses these files and folders:

- [NLP_Financial_Statements.ipynb](): This Jupyter Notebook covers the project. 
- project_helper.py: helper functions to process the data. This is provided by Udacity.
- project_tests.py: Unit tests to test the functions created in the notebook. This is provided by Udacity.
- tests.py: helper functions used by project_tests.py
- requirements.txt: requirements file for python libraries to use with this project

This repository does not include the Data Bundle created by Udacity for this project and the sentiment word lists.

### Contents

There are 5 main sections of the Project.

1.  Download10-Ks

   The 10-Ks for 7 stocks are downloaded from SEC EDGAR service

2. Preprocess the Data

   The 10-Ks are text documents. First, all non 10-k documents from these text documents are filtered out. The resulting documents are cleaned up to remove the html tags, lowercase all text, lemmatize verbs and remove stopwords.
   
3. Analysis on 10-Ks

   This section performs sentiment analysis on the 10-Ks. The [Loughran-McDonald sentiment word lists]([https://sraf.nd.edu/textual-analysis/resources/#LM%20Sentiment%20Word%20Lists](https://sraf.nd.edu/textual-analysis/resources/#LM Sentiment Word Lists)) are used to cover the following sentiments:

   - Negative
   - Positive
   - Uncertainty
   - Litigious
   - Constraining
   - Superfluous
   - Modal

   Using the sentiment word lists, the following analysis is performed:

   - **Sentiment Bag of Words** are created from the 10-k documents. These bag of words count the number of sentiment words in each document and ignore the words that are not in the sentiment word lists. 
   - **Jaccard Similarity** is calculated on these bag of words and plotted over time. The Jaccard Similarity is calculated between each tick in time for each stock and sentiment.
   - **Sentiment TFIDF** is calculated from the 10-K documents using the sentiment word lists.
   - **Cosine Similarity** is computed using the TFIDF values and plotted over time. The Cosine Similarity is calculated between each tick in time for each stock and sentiment, similar to Jaccard Similarity.

4. Evaluate Alpha Factors

   Alphalens package is used for this section. The cosine similarities are used as the factor. Following evaluations are conducted:

   - Factor Returns: Computing period wise returns for portfolio weighted by factor values 
   - Basis Points per Day per Quantile
   - Turnover Analysis. The stability of the alpha ranks is measured using factor rank autocorrelation.
   - Sharpe Ratio of the Alphas


The project illustrates how to process the 10-Ks and create a factor using sentiment analysis. This can be further enhanced by applying different techniques to interpret the sentiment from the documents. One such example is [Analyzing Stock Sentiment from Twits]() where Deep Learning is used to analyse the sentiment. 

