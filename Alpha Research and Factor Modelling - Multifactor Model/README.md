# Alpha Research and Factor Modelling - Multifactor Model
In this project, a statistical risk model is built using PCA. This model is used to build a portfolio along with 5 alpha factors. These factors are created and then evaluated using factor-weighted returns, quantile analysis, sharpe ratio, and turnover analysis. At the end of the project, the portfolio is optimized using the risk model and factors using multiple optimization formulations. For the dataset, the end of day is taken from Quotemedia and sector data from Sharadar.

### Project Files

The project uses these files and folders:

- [alpha_research_factor_modelling.ipynb](https://github.com/udaygoel/AI-For-Trading-Udacity/blob/master/Alpha%20Research%20and%20Factor%20Modelling%20-%20Multifactor%20Model/alpha_research_factor_modelling.ipynb): This Jupyter Notebook covers the project. 
- project_helper.py: helper functions to process the data. This is provided by Udacity.
- project_tests.py: Unit tests to test the functions created in the notebook. This is provided by Udacity.
- tests.py: helper functions used by project_tests.py
- requirements.txt: requirements file for python libraries to use with this project

This repository does not include the Data Bundle created by Udacity for this project.

### Contents

There are 5 main sections of the Project.

1.  Get Returns Data for the risk model

   This project uses Zipline to handle the stock price data. The Data Bundle contains the end of day prices for US stocks. Zipline's pipeline package is used to access the data. Zipline's DataPortal package from zipline.data.data_portal is used to access the returns data and the returns data for past 5 years is created.

2. Statistical Risk Model

   - Fit PCA: The PCA model is fit to the returns data using the number of PCA components as 20
   - Factor Betas: Retrieve the factor betas from the PCA model
   - Factor Returns: Calculate the factor returns from the PCA model using the returns data
   - Factor Covariance Matrix: Calculate the factor covariance matrix using the factor returns
   - Idiosyncratic Variance Matrix / Vector: Calculate the idiosyncratic returns and use these to calculate the idiosyncratic variance matrix and idiosyncratic variance vector.
   - Predict Using the Risk Model: implement a function to predict the portfolio risk using the above values

3. Create Alpha Factors

   The following factors are created:

   - Momentum 1 Year Factor
   - Mean Reversion 5 Day Sector Neutral Factor
   - Mean Reversion 5 Day Sector Neutral Smoothed Factor
   - Overnight Sentiment Factor
   - Overnight Sentiment Smoothed Factor

4. Evaluate Alpha Factors

   Alphalens package is used for this section. Following evaluations are conducted:

   - Quantile Analysis: This is done for Factor Returns and Basis Points per Day per Quantile.
   - Turnover Analysis. The stability of the alpha ranks is measured using factor rank autocorrelation.
   - Sharpe Ratio of the Alphas
   - Combining the Alpha Vectors: The alpha vectors are combined using a simple averaging of the scores from each alpha. This provides the combined alpha for each stock. In practice, this is an area where machine learning can be very helpful.

5. Optimal Portfolio Constrained by Risk Model

   This section involves the creation of Objective and Constraints and running an optimization to get the optimized portfolio weights using the CVXPY problem solver. Multiple defintions of Objective function are tested:

   - Maximizes the alpha return only. This puts most of the weight in a few stocks
   - Above plus optimize with a Regularization Parameter. This parameter is used on the [Euclidean Norm (2-Norm)](https://en.wikipedia.org/wiki/Norm_(mathematics)) on portfolio weights. This gives a well diversified portfolio
   - Maximize the alpha return and apply target weighting. The idea to take a predefined target weighting and solve to get as close to that portfolio while respecting portfolio level constraints. This also gives a diversified portfolio, in line with the target weights.


The project illustrates how to create a multi-factor optimized model. This can be further enhanced by applying transaction costs and transferring some constraints to the objective function, where possible, for better optimization results.