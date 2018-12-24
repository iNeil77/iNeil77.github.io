---
layout: post
title: Matching Algorithms Paper Review VI
author: Indraneil Paul

---


<div class="message" style="text-align: justify">
  In this post we explore recent experiments simulated on ridesharing data that detail how efficient it is viz-a-viz a centralized cab assignment system. 
</div>

## [The Efficiency of A Dynamic Decentralized Two-sided Matching Market](https://site.stanford.edu/sites/g/files/sbiybj8706/f/4698-s2search_match_03_2018_03.pdf)

The paper considers two kinds of vehicular matching problems:
* **Decentralized Model:** This model approximates a ride-hailing system. The system sends nearby rider requests to a driver and leaves it upto the driver to choose a rider
* **Centralized Model:** This model approximates a cab booking system. The centralized broker assigns matches to drivers.

Several simulations are run on both the models using both myopic (matches made immediately for centralized and driver taking closest request immediately for decentralized) as well as patient (matches being made after developing market thickness in centralized and driver waiting a stochastic amount of time before selecting in decentralized) heuristics. In the centralized system the patient version understandably improves both thickness and match rate of the market. In the decentralized system the patient version improves thicknes in the market but surprisingly leads to a lower number of matches. This is likely due to the forgone matches in the cases where a driver is in an underserved part of the city and forgoes a match for hope of a better one. The presence of a central broker enforcing matches ostensibly prevents this eventuality in a centralized market.

Finally it is shown that these conclusions are robust to a number of deviations in the model:
* An alternative strategy being used by drivers or brokers such as selecting the second best match
* An alternative strategy being used by drivers or brokers such as following a patient approach but turning greedy just before leaving the market unmatched
* Each driver having differing tolerances to the maximum viable match distance

## [We Are on the Way: Analysis of On-Demand Ride-Hailing Systems](http://public.kenan-flagler.unc.edu/2017msom/SIGs/Service%20Operations%20SIG/Feng%20Kong%20Wang%202017%20We%20are%20on%20the%20way%20-%20On%20Demand%20Ride-Hailing%20Systems.pdf)

This work largely looks at a simplified stylized version of a similar problem. The model considers a cirular road on which a fixed number ofdrivers keep moving at a constant pace. The drivers arrive uniformly along the circle with the arrival rates of passengers modelled by a poisson distribution and their trip durations being modelled by an exponential distribution. Two models of cab hailing are considered:
* **Ride-Hailing:** One can call a taxi from a certain position and the request is assigned to the closest driver.
* **Streeet-Hailing:** One can sit in a taxi only when it passes by him on the circle.

Additionally, both one-way (ride-hailing taxis move only clockwise) and two-way systems (ride-hailing taxis move clockwose and counter-clockwise) are considered. Street-hailing taxis always move clockwise and only pick passengers up when they drive past them. Simulations are run for varying levels of congestion (by varying the poisson distribution parameters) and a few important observations are made:

* In the street-hailing system average wait-time rises monotonocally with congestion levels. This system is best for reducing waiting time during sparse and medium supply of drivers.
* In the one-way ride hailing system wait-times initially increase with congestion, then decrease for medium congestion levels and then increase again. This is thought to be due to commited assigned drivers missing out on closer but later-arriving passengers. This system is best for reducing waiting time during driver oversupply.
* All of the aforementioned observations regarding waiting times hold true for two-way ride-hailing systems but are less prominent.
* Finally a ride-hailing system operating on a radius limit with which requests are accepted seems to perform best in all cases regarding waiting times. The authors also propose a heuristic based method for deriving a good radius figure that allows for a reasonable bound on waiting times.
