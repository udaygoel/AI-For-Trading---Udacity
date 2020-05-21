# Enhanced Alpha using Random Forest
In this project, Random Forest is used to combine multiple trading signals to create enhanced alpha. It solves the problem of overlapping samples to avoid overfitting. For the dataset, the end of day is taken from Quotemedia and sector data from Sharadar.

### Project Files

The project uses these files and folders:

- [Enhanced_Alpha_Random_Forest.ipynb](https://github.com/udaygoel/AI-For-Trading-Udacity/blob/master/Enhanced%20Alpha%20using%20Random%20Forest/Enhanced_Alpha_Random_Forest.ipynb): This Jupyter Notebook covers the project. 
- project_helper.py: helper functions to process the data. This is provided by Udacity.
- project_tests.py: Unit tests to test the functions created in the notebook. This is provided by Udacity.
- tests.py: helper functions used by project_tests.py
- requirements.txt: requirements file for python libraries to use with this project

This repository does not include the Data Bundle created by Udacity for this project.

### Contents

There are 8 main sections of the Project.

1.  Data Pipeline

   This section uses Zipline to handle the data and retrieve the returns data for stocks in the universe. 

2. Alpha Factors

   The following factors are created:
   
   - Momentum 1 Year Factor
   - Mean Reversion 5 Day Sector Neutral Smoothed Factor
   - Overnight Sentiment Smoothed Factor
   
3. Features and Labels

   This section creates features that will help the model make predictions:

   - "Universal" Quant Features:
     - Stock Volatility 20d, 120d
     - Stock Dollar Volume 20d, 120d
     - Sector
   - Regime Features:
     - High and Low Market Volatility 20d, 120d
     - High and Low Dispersion 20d, 120d
   - Date Features: these features will capture trader / investor behaviour due to calendar anomalies
     - is_January, is_December
     - weekday
     - quarter, quarter_year
     - month end, month start
     - quarter end, quarter start
   - One Hot Encode Sectors: this allows the model to better understand the sector data.

   The project will predict the go forward 1-week return. The factor created for this is the trailing 5 day return and this is quantized. These are shifted by 5 days for training the model.

4. IID Check of Target

   This section checks if the target values for successive days are independent and identically distributed using Rolling Autocorrelation of the labels shifted 1, 2, 3 and 4 days. The results show that there is an overlap between the labels which will have to be handled while developing the model

5.  Train/Valid/Test Splits

    The data is split by dates into a train, validation and test dataset in a 0.7 : 0.2 : 0.1 ratio. The data is also split into features and the label for each dataset.

6.  Random Forests

    With the data now ready, this section proceeds to create a Random Forest.  

    - First, a single Decision Tree is trained to see how it will use the data. The section displays the tree to get a good visual understanding and displays the features importance as calculated by scikit-learn methodology.

    - The section then proceeds to train Random Forests with different tree sizes and plots the accuracy scores for training and validation sets and the OOB Score. The plot indicates that the model is overfitting. The feature importance scores show that some features have low or no importance, which can be removed later when training the final model.
    - Model Results: Some additional metrics such as Sharpe Ratios, Factor Returns and Factor Rank Autocorrelations are created to see how well a model performs. The results are illustrated through plots for training and validation set using the last model trained with the highest tree size.

7.  Overlapping Samples:

    This section fixes the problem of overlapping samples. Three approaches have been used and the steps above for Random Forests are repeated:

    - Drop Overlapping Samples: 

      This is the simplest method of just dropping any overlapping samples from the dataset. The results look better but this approach results in throwing away a lot of information.

    - Use BaggingClassifier's max_samples: 

      The idea behind this approach is to pick a smaller number of samples for each bag in order to reduce the influence of redundant information. This feature is not available in scikit-learn's random forest implementation and so another classifier BaggingClassifier is used as it allows the bag size to be adjusted with a parameter called max_samples. 

      We can set the max_samples to be of the order of the average uniqueness of the labels. The results here also look much better.

    - Build an ensemble of non-overlapping trees:

      This method involves creating an ensemble of overlapping trees by writing a custom scikit-learn estimator. We inherit from VotingClassifier and override the "fit" method so we fit on non-overlapping periods.

      The result looks promising as we avoid overfitting and are able to use all the data.

8.  Final Model:

    The model for building an ensemble of non-overlapping trees is used to build the Final Model. The model is re-trained using training and validation dataset. The results are tested using the testing dataset. The results show that AI Alpha - the combined alpha factor using the final model - is able to consistently deliver positive performance.

    


The project illustrates how to use Random Forests to combine multiple alpha factors to create a single enhanced alpha. The project runs through the different features that can be created to capture market conditions and investor behaviour that cannot be easily predicted through stock price time series. We also see how the features can be filtered using feature importance scores. And finally, how to avoid overfitting due to overlapping labels.
