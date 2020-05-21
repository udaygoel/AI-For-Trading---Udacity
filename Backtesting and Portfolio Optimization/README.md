# Backtesting and Portfolio Optimization
In this project, a backtesting notebook is created to perform portfolio optimization that includes transaction costs and is implemented with computational efficiency in mind to allow for a reasonably fast backtest. The notebook also uses performance attribution to identify the major drivers of the portfolio's profit-and-loss (PnL). The project uses Barra data.

### Project Files

The project uses these files and folders:

- [Backtesting_Portfolio_Optimization](): This Jupyter Notebook covers the project. 
- requirements.txt: requirements file for python libraries to use with this project

This repository does not include the Barra data created by Udacity for this project.

### Contents

There are 8 main sections of the Project.

1.  Loading and Processing Data

   This section loads the Barra data for Factor Exposures, Covariance and daily stock returns which is already processed by Udacity. Few additional processing steps are taken such as shifting daily returns data,  adding new date column, winsorizing daily returns. The winsorized distribution of returns for a single day are plotted using density plot.

2. Factor Exposures and Factor Returns

   Factor Returns are estimated using the Ordinary Least Squares (OLS) method and values of Factor Exposures and Daily Returns from Barra data.
   
3. Choosing Alpha Factors

   Select some factors in the Barra data as alpha factors.

4.  Merge Previous Portfolio Holdings
    In order to optimize the portfolio, the previous day's holdings are used to estimate the trade size and transaction costs. A column to hold the portfolio holdings of the previous day is added to keep track of such holdings

5.  Build Universe

    Building a universe by applying filter for market capitalization and previous day's holdings.

6.  Preparing Data for Optimization

    The following data items are created for use in optimizing the portfolio:

    - Matrix of Risk Factor Exposures
    - Specific Variance
    - Factor Covariance matrix
    - Transaction Costs
    - Matrix of Alpha Factors
    - Alpha Factors Combination: This project combines each alpha factor equally. There can be more sophisticated methods of alpha combination such as [Enhanced Alpha using Random Forest](https://github.com/udaygoel/AI-For-Trading-Udacity/tree/master/Enhanced%20Alpha%20using%20Random%20Forest).

7. Optimization

   This section is broken down into the following steps:

   - Objective Function: this is the function we wish to minimize to achieve optimization. This function includes terms for :
     - Factor Risk (using risk factors)
     - Idiosyncratic Risk
     - Expected Portfolio Return (using alpha factors)
     - Transaction costs
   - Gradient: This is essential to tell the optimizer in which direction, and how much, it should shift the portfolio holdings in order to improve the objective function (that is, minimize variance, minimize transaction cost and maximize expected portfolio return)
   - Optimize: This project uses Scipy's optimization function scipy.optimize.fmin_l_bfgs_b(func, initial_guess, func_gradient), where:
     - func is the Objective function
     - initial_guess is the initial guess. The previous portfolio holdings will be used as initial guess.
     - func_gradient is the Gradient function

8. Optimized Portfolio Analysis

   The optimization of the objective function returns the weights for the new optimal portfolio. This can be used to perform analysis on the new portfolio:

   - Risk and Alpha Exposures: Calculate the portfolio's risk and alpha exposures
   - Transaction Costs: calculate the total transaction costs
   - Trade List: this is the most recent optimal asset holdings minus the previous day's optimal holdings

9.  Run the Backtest

    The Steps 4 - 8 can be repeated for each day historically to calculate the optimal portfolio holdings and trade list. The optimization in these steps has been set up to be computationally efficient to reduce the time required for the backtest to run. 

10. Profit and Loss (PnL) Attribution

    Profit and Loss is the aggregate realized daily returns of the assets, weighted by the optimal portfolio holdings chosen, and summed up to get the portfolio's profit and loss. 

    The PnL attributed to the alpha factors equals the factor returns times factor exposures for the alpha factors. Likewise, for the risk factors. 

    Similarly the PnL attributed to the cost can be calculated

11. Build Portfolio Characteristics

    Calculate the sum of long positions, short positions, net positions, gross market value and the amount of dollars traded. These are plotted to see the profile over the backtested period.


The project illustrates how to run portfolio optimization in a computationally efficient way. The optimization uses risk factors, alpha factors, idiosyncratic risk and transaction costs. The alpha factors combination approach is very simple in this project and it can be made more sophisticated using methods such as [Enhanced Alpha using Random Forest](https://github.com/udaygoel/AI-For-Trading-Udacity/tree/master/Enhanced%20Alpha%20using%20Random%20Forest). Finally, this project shows how to use performance attribution to identify the major drivers of the portfolio's PnL. 
