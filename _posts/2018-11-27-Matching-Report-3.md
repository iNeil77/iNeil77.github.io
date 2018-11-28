---
layout: post
title: Matching Algorithms Paper Review III
author: Indraneil Paul

---


<div class="message" style="text-align: justify">
In this post we look at an interesting application motivating dynamic matching - Kidney Exchanges. The stakes being that of life and death, we need to squeeze every bit of efficiency off the system. Prior-free algorithms usually perform unacceptably in this domain. However encoding distributional information in deterministic algorithms ususally involves solving for sample trajectories over future time periods, which can turn computationally prohiitive very quickly. The paper we discuss involves assigning importance potentials to the elements of the graph over which the matching is to be done, post which at runtime an offline mechanism is run in the weighted graph.
</div>

## [Dynamic Matching via Weighted Myopia with Application to Kidney Exchange](https://www.cs.cmu.edu/~sandholm/dynamicMatchingViaWeightedMyopia.aaai12.pdf)

The model considers two kinds of users - patient donor pairs and altruistic donors. Patient donor pairs exchange with other such pairs to form disjoint cycles while altruisitc donors can trigger chains in the graph. Various blood types have differing latitudes with regards to the number of different agents they can exchange with. The algorithm allows for a central planner across time who ca observe when an agent gets critical and is about to leave the market. The algorithm thus assigns potentials to graph elements which allows it to sacrifice lower valued elements in immediate requirement matchings when an agent becomes critical and save the more versatile elements for later to trigger larger chains or cycles, when the opportunity presents itself.

The weights are learnt by the model during a training phase using a well known integer solver called ParamILS which is run over 1500 synthetically generated graphs with realistic agent expiration rates simulated. The solver tries to maximize the number of matches and the graph element weights are set as the learnable parameters. Once the weights are learnt, at every moment of criticality, the method solves the weighted graph using a branch-and-price solver which has been shown to be able to solve the NP-Hard problem to optimality for upto 10,000 agents.

Finally, the authors demonstrate how potentials may be learnt for arbitrarily complex graph structures, thus improving theoretical performance. There are a few pathological examples wherein additionally learning edge potentials significantly outperforms learning just vertex potentials, additionally learning cycle potentials significantly outperforms learning just edge and vertex potentials and so on. These however, quickly become computationally intractable and the authors show demonstrable improvements from existing methods using just vertex potentials.