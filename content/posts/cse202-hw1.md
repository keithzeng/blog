---
title: "CSE202 HW1"
date: 2019-01-26T13:30:38-08:00
categories: ["algorithm"]
series: ["greedy"]
tags: ["CSE202", "HW"]
draft: true
---
[HW Link](https://cseweb.ucsd.edu/classes/wi19/cse202-a/hw1.pdf)

## Problem 1 (KT 4.2a)##
YES. T is still the MST for new instance.

Proof by contraction

- Assume original MST is T and new MST is T'
- $T \neq T'$, at least one edge is different
- $\exists$ $e_1 \in T$ and $e_2 \in T'$, whose $cost(e_1) < cost(e_2)$ and $cost^2(e_1) > cost^2(e_2)$
- However, the above mathematical expression doesn't hold

## Problem 2 (KT 4.2b)##
No. The P is no longer the shortest path for new instance.

![Diargram](/img/cse202/hw1.2.png)
As we can see, in the Dijkastra's algorithm, the edge e(s,t) is the shortest path with cost = 7. After squaring the cost, the shortest path P' = s -> a -> t instead, with cost of 32. So $P' \neq P$.

## Problem 3 (KT 17)##

### Algorithm: ###

1. Let $I = \\{I_1, I_2, ..., I_n\\}$ and best = 0
1. Sort I based on the finish time, f(i)
1. for i in n
  - let $R = I \setminus \\{I_j | i \neq j$ and $I_i \cap I_j \neq \emptyset\\}$
  - let num_of_jobs = perfome regular interval scheduling algorithm on R
  - best = max(best, num_of_jobs + 1)

### Time complexity anaylysis:###

Step 2, sorting takes $O(nlogn)$.\
Step 3, the for loops takes $O(n^2)$ overall, since looping through intervals takes O(n), pruning + regular interval scheduling algorithm takes O(n)
So time complexity = $O(nlogn + n^2)$ = $O(n^2)$.

### Space complexity analysis: ###

We don't need any extra space since we sorted in place.\
So space complexity = O(1).

### Proof of Optimality: ###
**Claim:**\
The algorithm above provides the optimal solution.\

**Proof:**\
Let's say the optimal solution is S\*, which contains a $I_i$. Since above algorithm is brute force algorithm go through each job, we are guranteed that when are checing the optimal number for $I_i$ the number is updated.

## Problem 4 ##
### Algorithm: ###

Let $J = \\{J_1, J_2, ..., J_n\\}$, where $J_i$ contains $c_i$ and $p_i$\
then sort J based on $c_i$\
Let H = maxheap sorted on J's profit\
Let $C = C_0$\
Let z = 0

loop add_job:\
while $z \leq n$ and $c_z \leq C$

1. push $J_z$ to H
1. $J \setminus \\{J_z\\}$
1. $z \gets z + 1$


while k > 0 and H is not empty

1. $J_x$ = extractMax from H
1. $C \gets C + p_x$
1. execute loop add_job
1. $k \gets k - 1$

### Proof of Optimality: ###
**Claim:**\
The gready algorithm above produces the optimal capital, C\*.\

**Proof:**\
Let's say in particular loop, when we have capital C, we chooses a different $J_y$ instead of $J_x$. Since $J_x$ is obtained from the top of the heap, it implies that $p_y \leq p_x$, also the new capital $C + p_y \leq C + p_x$. Subsequently, in third step, when we consider add the jobs whose cost are smaller than the current capital, the new heap $H' \in H$, which indicates that our algorithm stays ahead in every step afterward.

#### Time Complexity: ####

1. Sorting takes O(nlogn).
1. Extractmax takes retrievl + deletion = O(1) + O(logn) = O(logn). For k loops, complexity = O(klogn).
1. The loop add_job execute exactly n times, $\sum_i^n log(n!) = O(nlogn)$.
1. So overall = O(nlogn + klogn) = O(nlogn), since $k \leq n$

### Space Complexity: ###

O(n) for storing all the projects in the heap.

## Problem 5 ##

### Algorithm: ###

sort $T = \\{t_1, t_2, ..., t_n\\}$ in decreasing order\
sort $W = \\{w_1, w_2, ..., w_n\\}$ in decreasing order\

Let i = 1, pointer for T\
Let j = 1, pointer for W\
Let result = {}\

while $i \leq n$

1. If $t_i$ / $w_j$ $\leq D$
  - $i \gets i + 1$
  - $j \gets j + 1$
  - result + {i, j}
2. else
  - $i \gets i + 1$

### Proof of Optimality: ###
**Claim:**\
The above algorithm produces the optimal assignment, R.

**Proof:**\
Assume there is a better assignment R', where |R'| > |R|.\
This can happen by either case:

1. R' = R + {i, j} 
1. R' have different arrangement of pairs that vacant a machine to take on another task, resulting more tasks to be taken

For case 1, let's say in step i, our algorithm rejects the task because $t_i$ / $w_j$ $\leq D$, but R' takes this pair {i, j}. This will be a violation to the statement and moreover this machine can't complete the task on time.

For case 2, the only way that R' and R will take on different arrangement is when R decides to take the pair {i, j} but R' decides to ignore the $t_i$. This have vacated the $w_j$, we now have |R| > |R'|. In the next round, $w_j$ can take the $t_i$$\tiny{+}$$_1$. In the meantime R could either take new pair {i+1, j+1} or rejects it dues to insufficient time, therefore |R| $\geq$ |R'| in every step.

