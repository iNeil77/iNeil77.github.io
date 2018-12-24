---
layout: post
title: Matching Algorithms Paper Review V
author: Indraneil Paul

---


<div class="message" style="text-align: justify">
  This post covers a few recent results in one-sided matching markets that reveal that low-latency solutions to matching problems may not always be the way to go. Making agents wait so as to increase their options can lead to inproved matches and increased social welfare in general.  
</div>

## [Thickness and Information in Dynamic Matching Markets](https://ipl.econ.duke.edu/seminars/system/files/seminars/1392.pdf)

This paper details the improvements observed in social welfare and reduction in number of agents leaving the market (perishing) by making agents wait for their matches rather than matching them immediately as they enter the market. Agents need to be matched urgently only when they become critical (in urgent need of leaving the market). These results are derived for varying levels of agent impatience (which is encoded as a utility discounted with time). The implicit assumption is that there exists a central broker with a certain time horizon who can detect critical agents and match them if possible. The paper contrasts two different models:
* **Greedy:** The algortihm maatches agents as soon as they enter the market
* **Patient ($\alpha$):** The algorithm matches agents only as they become critical. Optionally non-critical agents may be matched at a rate determined by a parameter ($\alpha$)

The work shows that under certain bounds on $\alpha$, the loss of the patient algortihm isn't much worse than the best possible with an omneiscent broker. This allows an acceleration of the patient algorithm with only minimal degradation in performance. The comparative performance of the two methods are shown under differing rates of impatience. Under some low bounds of impatience, all parameterizations of the patient algorithm are always shown to outperform the greedy one. Additionally, under some medium bounds on impatience, some parameterization of the patient algorithm is shown to outperform the greedy variant. 

Most interestingly, the advantage of the patient algorithm over the greedy one seems to stem entirely from the advantage in information. This is reinforced by the fact that divergence in the performance of the two methods seems to be largely governed by the time horizon that the central broker possesses. When the broker is unable to indentify critical agents, the advantage of the patient algorithm is negligible. On the other hand the difference in performance is maximum when the broker is omneiscent and has an infinite time horizon, allowing it to plan matches from the start.

## [Competing Dynamic Matching Markets](https://www.cs.cmu.edu/~sandholm/competingMatchingMarkets.amma15.pdf)

This paper extends the aforementioned work by considering the scenario in which the two kinds of markets co-exist and compete against one another. Agents are split into three pools, with one participating exclusively in the greedy pool, one participating exclusively in the patient pool and the rest participating in both the markets.

The patient market is once again shown to be the single best solution. However, the presence of a competing greedy market that hurts the usage of the patient market (thickness) produces the worst possible result of all, with the resultant performance being inferior to that of even a purely greedy approach. This in turn enforces an incentive structure wherein in the presence of a competing greedy market, a patient market is forced to switch to a greedy mechanism of operation.
