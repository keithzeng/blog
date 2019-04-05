---
title: "CSE202 HW5"
date: 2019-03-10T20:16:19-07:00
categories: ["algorithm"]
series: ["approximation"]
tags: ["approximation"]
draft: true
---

## Problem 1: Load Balancing

Let $T^\*$ denotes the optimal time, $M_i$ denotes the last machine that we place the job with time $t_j$, $T_i$ denotes the total time for $M_i$, m denotes number of machine, and n denotes number of jobs.

We know that
\begin{equation}
T^\* \geq \frac{1}{m} \sum_{k=1}^{n} t_k
\end{equation}

\begin{equation}
T^\* \geq \max_k t_k
\end{equation}

![hw5.1](/img/cse202/hw5.1.png)

As we see from the diagram above, at the last step, when we place the $t_j$ on $M_i$, $M_i$ has the lowest load at that time. At that time, $M_i$ has $T_i - t_j$ load and all other machines has $T_k \geq T_i - t_j$, so we got following expression. Also notice that the sum of load of all the machine is equal to the sum of all the job's time.

\begin{align\*}
m(T_i - t_j) + t_j &\leq \sum\_{k=1}^m T_k = \sum\_{k=1}^n t_k \newline
T_i - t_j + \frac{t_j}{m} &\leq \frac{1}{m} \sum_k t_k \newline
\end{align\*}

Plug in eq (1), we got
\begin{align\*}
T_i - t_j + \frac{t_j}{m} &\leq T^\* \newline
T_i &\leq T^\* + (1 - \frac{1}{m}) t_j\newline 
\end{align\*}

Plug in eq (2), we got
\begin{align\*}
T_i &\leq T^\* + (1 - \frac{1}{m}) T^\*\newline
&= (2 - \frac{1}{m})T^\*
\end{align\*}

## Problem 2: Center Selection

### Part (a)

For 1 run of experiment for a n = 50 and k = [1,5,10,15,20,30,40,45,50], there isn't a consistent way to determine which ALGO is better. For k = 10, ALGO1 gives lower r(C,S) than ALGO2's. For k = 15, ALGO2 produces lower r(C,S) than ALGO1.

Run 1
![hw5.2a_sinlge](/img/cse202/hw5.2a_single.png)

For a different run, for both k = 10 and 15, ALGO2 produces lower r(C,S). 

Run 2
![hw5.2a_sinlge2](/img/cse202/hw5.2a_single2.png)

However, one may observe from the above diagrams, for higher value of k, it seems like ALGO2 outperform ALGO1 consistently. Therefore, I decided to execute 100 runs of experiment for n = 50 and k = [1,5,10,15,20,30,40,45,50], then I average the $r^2$ of these 100 runs, I produces a trend diagram that the average of $r^2$ of ALGO2 is consistently lower than ALGO1's for k > 1 value. The diagram is shown below

![hw5.2a](/img/cse202/hw5.2a.png)

The reason that when k = 1, ALGO1 outperform ALGO2 is that the ALGO2's first point was chosen arbitrarily while ALGO1 choose the center point that r(C,S) is minimize. Due to this reason， k = 1 is not a good indicator of performance.

We also test different combination of n and k shown below:

n = 10, k = [1,2,3,4,5,6,7,8,9,10]

![hw5.2a_n10](/img/cse202/hw5.2a_n10.png)

n = 20, k = [1,5,10,15,20]

![hw5.2a_n20](/img/cse202/hw5.2a_n20.png)

n = 30, k = [1,5,10,15,20,25,30]

![hw5.2a_n30](/img/cse202/hw5.2a_n30.png)

n = 40, k = [1,5,10,15,20,25,30,35,40]

![hw5.2a_n40](/img/cse202/hw5.2a_n40.png)


### Part (b)

If we allow k to be a small value, we can obtain instance of points that ALGO1 is better than ALGO2.

points = [(16, 7), (9, 16), (7, 17), (14, 2), (8, 2), (12, 0), (5, 0), (16, 10), (12, 7), (5, 4), (4, 4), (18, 7), (1, 5), (1, 1), (14, 16), (9, 12), (8, 7), (3, 18), (1, 2), (14, 12)]

k = 5

<center>

|  ALGO |                       C                       |$r^2$|
|:-----:|:---------------------------------------------:|:---:|
| ALGO1 |   [(8, 7), (9, 16), (12, 7), (5, 4), (8, 2)]  |  40 |
| ALGO2 | [(16, 7), (3, 18), (1, 1), (14, 16), (12, 0)] |  64 |

</center>

![hw5.2b1](/img/cse202/hw5.2b1.png)
![hw5.2b2](/img/cse202/hw5.2b2.png)

### Part (c\)

points = [(6, 11), (15, 18), (5, 13), (7, 16), (3, 16), (16, 19), (11, 7), (8, 7), (0, 18), (12, 15), (4, 13), (4, 9), (16, 10), (7, 5), (15, 13), (13, 3), (7, 18), (19, 10), (17, 1), (6, 16)]

k = 5

<center>

|  ALGO |                       C                       |$r^2$|
|:-----:|:---------------------------------------------:|:---:|
| ALGO1 | [(8, 7), (7, 18), (11, 7), (15, 13), (17, 1)] |  49 |
| ALGO2 | [(15, 13), (0, 18), (17, 1), (7, 5), (7, 16)] |  37 |

</center>

![hw5.2c1](/img/cse202/hw5.2c1.png)
![hw5.2c2](/img/cse202/hw5.2c2.png)

### Part (d)

**Claim**

ALGO1 is not a good approximation algorithm, since $\gamma$ is not bounded.

**Proof**

We can easily get $\gamma  = 2$ for simple example shown below.

![hw5.2dk2](/img/cse202/hw5.2dk2.png)

For k = 2, the optimum solution will be selecting the midpoint between H1 and H2, producing r = d/2.

![hw5.2dk2opt](/img/cse202/hw5.2dk2opt.png)

For ALGO1, we will pick either point producing r = d. Thus, r = 2OPT.

![hw5.2dk2alg](/img/cse202/hw5.2dk2alg.png)

We can also show $\gamma = 3$ as well for the example shown below.

![hw5.2dk3](/img/cse202/hw5.2dk3.png)

For k = 3, the optimum solution will be selecting H2, H5 and H7, producing r = d/4.

![hw5.2dk3opt](/img/cse202/hw5.2dk3opt.png)

For ALGO1, the first point selected will be H6, then we can pick any point because all the choices will result r = d. Let's say that we pick H5. For next point the only point that will decrease the r is H7, so we pick H7. The final r is 3d/4, which is 3OPT.

![hw5.2dk3alg](/img/cse202/hw5.2dk3alg.png)

Moreover, we can come up with generic case that show that $\gamma$ can be any value.

![hw5.2dgen](/img/cse202/hw5.2dgen.png)

For k = 3, the optimal centers choices are H1, H2, and h4, resulting r = 1.

![hw5.2dgen_opt](/img/cse202/hw5.2dgen_opt.png)

For ALGO1, we will select either H2 or H3. Let's say that we select H2 first resulting r = $\gamma + 1$. Then the next point we can either select H3 or H4 to improve the r to $\gamma$. Let's say we select H3, resulting r = $\gamma$. At last, we can select either H1 or H4 without improving the r, resulting r = $\gamma$. Because $\gamma$ can be any value, then ALGO1 can be any multiple of the OPT.

![hw5.2dgen_alg](/img/cse202/hw5.2dgen_alg.png)

## Problem 3: Hitting Set (KT 11.4))

### Idea

We have

$$A = \\{a_1, ... a_n\\}$$

$$w = \\{w_i ... w_n\\}\ \forall \ a_i \in A \text{ and } w_i \geq 0$$

$$B_i \subset A\ \forall i = 1...m$$

$$H \subseteq A \text{ where }  H \cap B_i \neq \emptyset$$

$$b = \max_i |B_i|$$

Goal:

$$\text{Min} \sum_{a_i \in H}w_i$$

We can convert above problem into linear program optimization problem, where we use x to represent the whether or not to include the $a_i$ or not just like vertex cover.

### Algorithm

Objective function:

$$\text{Min} \sum_{i = 1}^{n} w_i x_i$$

Under constraints:

\begin{equation}\tag{1}0 \leq x_i \leq 1 \ \forall i = 1,...n\end{equation}

\begin{equation}\tag{2}\sum_{i: a_i \in B_j}x_i \geq 1 \ \forall j = 1,...m\end{equation}

Solution:

$$S = \\{a_i | x_i \geq \frac{1}{b}\\}$$

### Correctness

Let $x^\*$ denotes the x vectors that satisfy above problem, and let $w\_{LP}$ denotes the value of the objective function

$$w\_{LP} = w^Tx^\* = \sum\_{i = 1}^{n} w_i x^\*_i$$

**Claim 1**

H is a hitting set.

**Proof**

To be a hitting set, H need to have nonempty intersection with all $B\_j$. Since our constraint 2 is $\sum_{ai \in B_j} x_i \geq 1$ and $|B_j| \leq b$, there are at least 1 element $x_i \geq \frac{1}{b}$. By the choice of our solution, we will select at least 1 element from each $B_j$, therefore H is a hitting set.

**Claim 2**

$w(S) \leq bw\_{LP}$

**Proof**

We define that 
$$w\_{LP} = w^Tx^\* = \sum\_{i = 1}^{n} w_i x^\*_i$$

Plug in $x^\*_i \geq \frac{1}{b}$

\begin{align\*}
w\_{LP} &= \sum\_{i = 1}^{n} w_i x^\*_i \newline
&\geq \sum\_{i = 1}^{n} w_i \frac{1}{b} = \frac{1}{b} \sum\_{i = 1}^{n} w_i\newline
&\geq \frac{1}{b} \sum\_{a_i \in S}^{n} w_i \newline
&= \frac{1}{b} \sum\_{a_i \in S}^{n} w_i \newline
&= \frac{1}{b} w(S) \newline
\end{align\*}

So we obtain
$$ w(S) \leq b w\_{LP}$$

**Claim 3**

$w\_{LP} \leq w(S^\*)$

**Proof**

Let $S^\*$ be the optimal solution, and set $x_i = 1$ if $a_i \in S^\*$ 0 otherwise. This x still satisfy the original constraint 1 and 2. Also, we know that the minimum of Linear Programing is not larger than the minimum of Integer Program (11.23), the following relation is established.

\begin{align\*}
w\_{LP} &\leq \sum\_{i = 1}^n w_i x_i \newline
&= \sum\_{a_i \in S^\*} w_i \newline
&=  w(S^\*) \newline
\end{align\*}

So 
$$w\_{LP} \leq w(S^\*)$$

Therefore, we have

$$ w(S) \leq b w\_{LP} \leq b w(S^\*)$$

[^algo]: Algorithm Design by Jon Kleinber, Eva Tardos 