---
layout: post
title: Google Summer of Code Summary
author: Indraneil Paul

---


<div class="message" style="text-align: justify">
  This is a summary of my work done in the 2017 Google Summer of Code with Green Navigation. I was recommended this program by a friend who had done the same a year prior. The purpose of this project was to test out the viability and effectiveness of various machine learning algorithms, in predicting the fuel consumption of an electric vehicle given the terrain and telemetry data of the vehicle motion. This can, in turn, have a wide variety of applications such as suggesting the most fuel-efficient paths to a destination and alleviating user range-anxiety of electric vehicles thus expediting their general adoption.
</div>

# Overview

Using the data obtained from the scan tool of various models of electric vehicles from [ChargeCar](http://chargecar.org/data), we were able to get the terrain information of various routes and the time series of the fuel usages accompanying those routes depending on several other factors such as velocity and acceleration as well as vehicle weight. Our job was to train multiiple models on this data to best estimate the fuel consumption so as to be able to select the best route from several competing ones. What follows is a summary timeline of the implementation of the various approaches and how they compare to one another:

## Week 1 :
* Organize scan tool data sources
* Visualize data using dimensionality reduction by t-SNE

## Week 2 :
* Set a baseline using simple vanilla linear regression
* Implemented a best-subsets variant of linear regression by eliminating predictors by variance inflation factors

## Week 3-4 :
* Implemented L1 and L2 regularized variants of linear regression
* Tested different penalty coefficients for the aforementioned ridge and lasso regression

## Week 5-6 :
* Implemented random forest regressor
* Performed hyperparameter search for the aforementioned random forest regressor using random search and grid search.

## Week 7-8 :
* Implemented xgboost regressor
* Performed hyperparameter search for the aforementioned xgboost regressor using random search and grid search

## Week 9-11 :
* Implemented windowed random forest and windowed xgboost regressor feeding not only telemetry data but also first order and second order gradient information
* Performed hyperparameter search for the aforementioned windowed random forest and windowed xgboost regressor using random search and grid search

## Week 12-13 :
* Implemented an LSTM network with dropout that used not only telemetry data but also first order and second order gradient and historical observations
* Fixed some bugs in the data reader

<br><br>
The L1 regularized linear regression slightly ouperformed the L2 variant, ostensibly due to its better feature selection abilities. Both these methods significantly outperformed the vanilla linear regression and the best subsets linear regression. While all the other methods surpassed this baseline set by the linear regression approach, the two methods that stood out were xgboost with gradient inputs (Week 9-11) and the LSTM with gradient and historical inputs (Week 12-13). 

# Proposal link

[Prediction of Energy Consumption of Electric Vehicles](https://github.com/Greennav/greennav.github.io/files/1253905/Indraneil_Paul_Proposal_GSoC2017.pdf)

# Possible Extensions
* Since the recurrent neural network approach using LSTMs has been promising, a more sophisticated stacked LSTM architechture capable of learning more complicated fuctions may yield better results
* Ensemble methods that combine predictions from various different types of regressors, may also be very promising
* The Grid Search that was used for hyperparameter selection was only run on a very narrow sub-range of the complete space of values. A Gaussian Process based Bayesian Optimisation of the parameter values over their complete space was tried but found to be intractable on consumer hardware. This method could however, yield an improvement that may help infer better combinations of values.


