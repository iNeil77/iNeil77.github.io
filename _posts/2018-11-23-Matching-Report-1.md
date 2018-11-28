---
layout: post
title: Matching Algorithms Paper Review I
author: Indraneil Paul

---

<div class="message" style="text-align: justify">
This is the start of a series on summarizing a few seminal and interesting papers in the field of optimal graph matchings.
</div>

## [Online Auctions for Dynamic Assignment: Theory and Empirical Evaluation](https://infoscience.epfl.ch/record/223122/files/ECAI2016GujarFaltings.pdf)

This paper looks into the dynamic resource assignment problem wherein agents have varying arrival and departure times and have preference orders on a set of resources. The agent reporting it's preference truthfully is not a given and four algorithms are evaluated to this end:

* **Arrival Priority Serial Dictatorship (APSD):** In this method each agent on arrival selects the resource for which he has the highest valuation and no payments are made to the platform. This method has been proven to be the only one in which a true value elicitation over resources is a dominant strategy given that payments are not allowed and that an agent does not misreport his arrival and departure times to be earlier than and later than actual respectively.
* **Split Dynamic VCG (SDV):** It finds an assignment that maximizes the sum of agents valuations for their alloted resources and their payments are determined by the extent to which they have affected other agents allotments. It was originally proposed under static settings but has been adapteed to dynamic settings by partitioning hte agents into groups that exist in the system simultanously. At each timestep the VCG auction is rerun with the remaining resources.
* **E-Auction:** This method uses the solution to the standard secretary problem adapted to the multiple resources setting. The platform waits for $$\frac{n}{e}$$ fraction of the agents to arrive in the first phase and sets the reserve price as the highest valuation received for that resource in the first phase. The first agent to arrive in thesecond phase with a bid surpassing the reserve price is awarded the resource. This mechanism is aso truthful for settings in which agents do not misreport their arrival and departures to be later than and earlier than actual.
* **Online Ranked Competition Auction (ORCA):** The system extends on the earlier E-Auction by considering the possibility that some resources may be more coveted across the board by all agents and thus it makes sense to have differing thresholds in the multiple secretaries problem with less coveted resources having lower thresholds. These thresholds are solved using a dynamic programming approach resulting in the algorithm having similar truthfulness characteristics as the method above.

The above algorithms are compared to the offline optimal which is an omneiscent god-like algorithm which knows all the user valauations from the start, no matter when they enter the market. Once all valuations are known an optimization problem can be solved to get the best possible result. The ratio of the value extracted by the offline algorithm to that of any online algorithm is its competitive ratio. APSD and SDV have a competitive ratio in the order of number of agents, while E-Auction has a cometitive ratio of $$\mathrm{e}$$ and ORCA has the best competitive ratio of less than $$\mathrm{e}$$. The paper also compares the algorithms in differeing scenarios and finds that in scenarios with low competition SDV is the best performing method while in scenarios with high competition ORCA is the best performing method.

## [Assigning Tasks to Workers based on Historica Data: Online Task Assignment with Two-Sided Arrivals](http://karthikabinavs.xyz/papers/aamas2018.pdf)

This paper looks into the scenario where both sides of the market are dynamic rather than just one side. There are a couple of working assumptions:
* The arrival of workers and tasks can be inferred from past data into known independent distributions.
* The number of different distributions one side is far lesser than that on the other.

The paper contributes one adaptive and one non-adaptive approach. The adaptive approach changes its matching strategy depending on the type and the number of agents in the system ehile the non-adaptive matching strategy is decided before the start of the algorithm. The paper uses a stocastic tool called the Two-Stage Birth Death Process to draw parrallels with the problem and uses that to derive competitive ratios and hardness results such as theoretically maximum possible competitive ratio. The following are the pertinent observations:
* The non-adaptive greedy algorithm achieves a Competitve Ratio (CR) of 0.3 which is shown uing the stochastic process to be the maximum possible for a non-adaptive process. This beats a previous result of 0.25 which assumed random arrival order, thus demonstrating the value of using past data to infer arrival distributions.
* An adaptive greedy algorithm is shown to outperform the best non-adaptive algortihm using simulations and for a node-weighted relaxation of the problem (each agent has similar value over all resources) a linear program with tight constraints exploiting the same is used to achieve a CR of 0.34. Here again the stochastic tool is used to provide a theoretical bound of 0.58 indicating scope for improvement.

## [Matching with Externalities and Attitudes](https://pdfs.semanticscholar.org/968f/4062978213204ee15eae7143f218e275bdfc.pdf)

This is a largely theoretical paper that looks into the repurcussions of a blocking coalition (A subset of users that can all improve their utlities by deviating from the specified matching) imposing their deviations on the rest of the system in the presence of their differing attitudes to the rest. An additive model of externalities are assumed wherein the utlity of an agent is the sum of values of the matches it is a part of and the externalities arising due to the matches of other agents. The assumprion of the externalities depends on the attitude of the agents in the blocking coalition:
* **Neutral Attitude:** Agents in the blocking coalition assume that the rest will not react to their deviation.
* **Optimistic Attitude:** Agents in the blocking coalition assume that the rest will act to their own best interest.
* **pessimistic Attitude:** Agents in the vlocking coalition assume that the rest will act to punish them for their deviations.

The work looks into the questions of membership and non-emptiness i.e whether a given matching is stable under the given attitude and whether a given problem with a given attitude even has a stable matchig, respectively. The paper contributes the result that under assumptions of additive externalities only Gale-Shapely style pairwise stability questions of non-emptiness and membership can be answered in polynomial time. Also questions of membership can always be answered in polynomial time for optimistic attitudes, whether the stability be pairwise or setwise. All other combinations of the pproblem are computationally intractable.

<!---
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
-->

