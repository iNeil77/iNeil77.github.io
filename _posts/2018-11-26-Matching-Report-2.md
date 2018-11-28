---
layout: post
title: Matching Algorithms Paper Review II
author: Indraneil Paul

---


<div class="message" style="text-align: justify">
In this post we look at solutions to static matching problems under distributional constraints. A motivating example would be a school matching system wherein both students and schools have preference orders over one another and there exist constraints over student distribution such that the least coveted schools must get at least some set proportion of the number of students that the most coveted school gets. Additionally, each student can only be matched to one school.
</div>

## [Designing Matching Mechanisms under General Distributional Constraints](https://mpra.ub.uni-muenchen.de/78753/1/MPRA_paper_64000.pdf)

Before we can get into it a few notions need to be clarified:
* **Strategyproof:** A mechanism is strategyproof if misreporting ones prefernce order does not confer that agent any advantage in terms of the the match obtained.
* **Nonwasteful:** A mechanism is nonwasteful if it does not produce a matching where a student claims than empty seat in a school different from the one he is alloted and switching to the desired school would still lead to a matching that satisfies the distributional constraints.
* **Fairness:** A mechanism is fair if it never leads to a situation where a student and a school that are not matched would rather be matched with each other.

The notions of nonwastefulness and fairness together constitute stability in the Gale-Shapely sense and guarantee that rational agents will not try to deviate from determined matching. The paper goes into two existing algorithms:
* **Serial Dictatorship (SD):** In SD a common priority order is assumed among students which is dictated by a master list, with students ordered sequentially according to the master list. A student can be matched to the schools to which on matching they wont violate any constraints. The student can then choose the best among them. It is strategyproof and nonwasteful but unfair.
* **Artificial Cap Deffred Acceptance (ACDA):** In ACDA, the maximum quota of each school is artificially lowered such that the deferred acceptance run over the lowered quotas satisfied all constraints. It is strategyproof and fair.

This work introduces a method called Adaptive Deffered Acceptance (ADA) which is a round by round method that maintains a set called a forbidden list and starts with a separate complete list of students ranked by how desirable they are to the schools. Every round a set number of top students which is commensurate with the round number are taken off the ranked list and their matches are determined using the DA. If a valid match is obtained for all students, the method terminates. If not, the quotas are reduced by the number of students assigned and the we move onto the next round. If a school violates the distributional constraints, the its quota is set to zero and the currently matched students are removed from the student list and the lgorithm moves to the next round.

The ADA is strategyproof, nonwasteful and in fairness lies between the ACDA and the SD algorithms. The paper also proves an important result that there cannot be another method which is strategyproof and also dominates the ADA in all cases.

## [Strategyproof and Fair Matching Mechanism for Ratio Constraints](http://ifaamas.org/Proceedings/aamas2018/pdfs/p59.pdf)

The paper introduces a new algorithm called Quota Reduction Deferred Acceptance (QRDA) which solves the above stated problem by repeatedly applying the standard DA to sequentially reduced artificially imposed maximum quotas. This algorithms is strategyproof and fair and performs the best amongst all the mentioned algortihms in simulations. However, in some pathological cases this algorithm is shown to underperform ACDA.
