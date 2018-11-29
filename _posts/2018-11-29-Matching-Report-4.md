---
layout: post
title: Matching Algorithms Paper Review IV
author: Indraneil Paul

---


<div class="message" style="text-align: justify">
  In this review we start looking at papers that lay out the scenario of matching with location based rights and constraints and also what until recently, the current state of the field was.  
</div>

## [Optimization for Dynamic Ride Sharing: A Review](https://ac.els-cdn.com/S0377221712003864/1-s2.0-S0377221712003864-main.pdf?_tid=2581bb98-1ee8-4d6f-b11f-fa9d2ff613d5&acdnat=1543500873_8d41329cd7eaa699ad574004ae92ff34)

This survey paper details the various kinds of ride-sharing scenarios such as single rider single driver, multiple rider single driver, etc as well as the various complications that arise in dynamic matching scenarios such as predicting future requests and handling detours for new closeby requests.

The work also points out that solutions that optimize system-wide objectives do not necessarily give the users the best experience. It thus mentions that a system planner must choose between one of several objectives such as minimizing system-wide travel time, minimizing average waiting time for users, etc.

The paper also mentions a few open challenges:
* Building critical market mass. This has been addressed in later papers on market thickness which will be discussed in a later post
* Allowing the user a choice between several matches rather than just assigning them a ride, which still seems to be an open problem.

## [One to One Matching Problems with Location Restrictions](https://cdn.uclouvain.be/public/Exports%20reddot/core/documents/coredp2015_54.pdf)

This paper introduces a novel combination of ideas into a well known matching problem - the roommate problem. Agents are subject to location constraints brought about not by their preferences over locations but by the scarcity of viable matching locations. This is a direct result of the location ownership model that the paper considers wherein, once matched in a specific room, two roommates have effective collective ownership of that room and no other agent can get in that room without the explicit approval of at least one of the two agents.

The paper develops two stability concepts with respect to this new model:
* Direct Stability: Under this notion a coalition looking to deviate from a given match can only change the assignments of people in the locations wherein both the owners of a room belong in the coalition. In effect, this means that the match of a non-coalition member can only be changed by his partner (who is part of the coalition), moving to an emplty slot or one completely controlled by colition agents. If such a deviation is not possible, then no other matching directly dominates the given matching and the matching is directly stable.
* Exchange Stability: Under this notion a coalition looking to deviate from a given match can reassign the partners of non-menbers by exchanging amonst themselves and also relocate to spots completely owned by coalition members in addition to unopccupied slots. This in effect requires only the permission of one of the owners of a room to change its mapping. If such a deviation is not possible, then no other matching exchange dominates the given matching and the matching is exchange stable. Coalition Exchange stability is a refinement of Direct Stability such that if a matching is directy stable, it is also coalition exchange stable.

The work finally refers to another notion of dominance called indirect dominance in which a match indirectly dominates another match when it can be obtained from the other match by a series of successively directly dominant intermediate matches. The largest possible group of matches, such that no match in the group indirectly dominates another match in the group and no match outside the group indirectly dominates a match in the group, is called the Farsighted Stable Set. Similarly, the largest possible group of matches, such that no match in the group exchange dominates another match in the group and no match outside the group exchange dominates a match in the group, is called the Exchange Stable Set. The appendix of the paper goes into the relation between the two stable sets with further mathematical rigour. 

## [Risk Averse Matchings over Uncertain Graph Databases](https://arxiv.org/pdf/1801.03190.pdf)

This paper looks into the problem of maximal matchings over graphs whose edge weights are uncertain. Usually matching strategies seek to maximize expected utlity without regards to the variance in the outcome. This paper seeks to efficiently find the maximal utility matching that respects a certain variance bound which can be uselful in use cases where the user cares more about worst case rather than average case performance. The edge weights are are drawn from a probability distribution with a known mean and variance. Although not directly applied to matching with location considerations, this method would lend itself well to such a setting where the distributions of the various edges can be modelled using a preference order ot some distance based penalty.

Having sorted the edges by their ratio of reward to risk, their approach uses a binary search technique to greedily yield a risk bounded matching that is guaranteed to be at least a third as good as the offline optimal (where the distributions are collapsed and the actual rewards are known beforehand). The work is also extended to be compatible with hypergraphs with probabilistic hyperedges. 

