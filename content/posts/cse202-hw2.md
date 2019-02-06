---
title: "CSE202 HW2"
date: 2019-02-05T13:01:30-08:00
categories: ["algorithm"]
series: ["divide and conquer"]
tags: ["cse202", "hw"]
draft: true
---
[HW Link](https://cseweb.ucsd.edu/classes/wi19/cse202-a/hw2.pdf)

## Problem 1 (KT 5.2)

We will need to modify the merge-and-count function, everything else stays the same as regular inversion algorithm.

merge-and-count(A, B):

1. i = 1, j = 1, where i is pointer to A, j is pointer to B
1. count = 0, lenA = length(A), lenB = length(B)
1. sorted = {}
1. While $i \leq lenA$ and $j \leq lenB$:
  - if (A[i] $\leq$ B[j])
     - sorted = sorted + {A[i]}
     - $i \gets i + 1$
  - else
     - sorted = sorted + {B[j]}
     - $j \gets j + 1$
1. append remaining A or append remaining B to sorted
1. While $i \leq lenA$ and $j \leq lenB$:
  - if (A[i] $\leq$ 2B[j]), means no significant inversion
     - $i \gets i + 1$
  - else
     - $j \gets j + 1$
     - $count \gets count + (lenA - i + 1)$
1. return (sorted, count)

### Proof

Instead of looping once for original inversion problem, we here loop twice. One for making the element sorted, and one for counting number of *significant inversion*. Our conquer step will take O(2n), which is still O(n), so T(n) = 2T(n/2) + O(n) still holds. Thus the overall algorithm is still $O(\log n)$.

## Problem 2

### part (a)

Since there are 4 addition, 2 substractions, and 3/2 n byte shift each level.

We have following

\begin{align}
T(n) & = 3T(n / 2) + 3n / 2 + 6\newline
  & = 3(3T(n / 4) + 3n / 4 + 6) + 3n/2 + 6
\end{align}

Then the general fomula at each level i is equal

$$
T(n) = 3^k T(n / 2^k) + n\sum\_{i=1}^k (3 / 2)^i + 6\sum\_{i=1}^k 3^i
$$

### part (b)

### part \(c)

## Problem 3

### Algorithm 1:

Basic Idea: for each vertex v, find the two longest paths orginate from v.

We need to create a adjacency matrix or neighbor list for each v.

Alg(T):

- Let adj = {neighbors[i], where i = 1 to n}
- Let diameter = 0
- Let visited = {}
- for v in V
  - loop through neighbors[i] and calculate the distance, tag vertex to be visited along the way to avoid travel back
  - $maxDist_v$ = sum of two longest paths (or just one)
  - diameter = max($diameter$, $maxDist_v$)
- return diameter

### Complexity

#### Time
Building adjacency matrix takes O(n). For each loop, we will take O(n) to visit possibly all the vertices. By looping n times, we have $O(n^2)$. Overall we have $O(n^2 + n) = O(n^2)$

#### Space
We will at most store 2n vertices in adj and n status in visited. So the overall space is O(n).

Where

- V = vertices of graph
- T = graph
- m = number of edges
- n = number of vertices

### Algorithm 2 (Improve of Algorithm):

Idea: we have done a lot of repeated work to find the disitance between different iterations. We can see that the maximum diameter should be either on subtrees from current vertex or span across different subtree (including current vertex). We can recursively split the problem into k subgroups and perform the calculation.

Alg(T):

- Let adj = {neighbors[i], where i = 1 to n}
- Let global variable diameter = 0
- Let visited = {}
- Let x = an abitary vertex in V.
- DFS(x, adj, visited)
- return diameter

DFS(x, adj, visited):

- if visited[x] return
- Let longestDist = 0, secondLongestDist = 0
- set x to be visited
- for neighbor in adj[x]:
  - find the longestDist and secondLongestDist
- diameter = max (longestDist + secondLongestDist, diameter)
- return longestDist

### Complexity

#### Time
Building adjacency matrix takes O(n). For the n loops, we basically split the vertices into groups of neighbors. Let's assume without loss of generality that at each vertex we split into k groups, so T(n) = kT(n/k) + O(1). Based on master theorem, this is O(n) complexity. Alternatively, we can see that the algorithm visit each node exactly 1 time. Overall we have $O(n + n) = O(n)$

#### Space
Same as above, so space complexity is O(n).

### Proof
**Claim 1:** The algorithm cover all the paths possible and return the diameter of the tree.

Assuem the contary, the return value is not the diameter, which means there is a path has longer distance than diameter. Let's call this path $P_uv$. Let's assume z is the root vertext of this path. There are two possible cases

- our original solution contains z
- our original solution doesn't contains z

Let's define our path to be $P_xy$.\

If our original solution contains z, then at the step when we try to find the two longest paths, we would've pick $P\_{uv}$. We ended up choose our $P\_{xy}$ because $P\_{xz}$ and $P_yz$ is the two longest path, so $P_uz$ < ($P\_{xz}$, $P\_{yz}$) and $P\_{vz}$ < ($P\_{xz}$, $P\_{yz}$), so $P\_{uz} + P\_{zv} < P\_{xz} + P\_{zy}$. So $P\_{uv}$ can't be the diameter. 

If our original solution doesn't contain z, then mistep happens in the other step. However, if the $P_uv$ is the true diameter, in the vertex $a \neq z$, the diameter value will not be replaced by the new value, therefore $P\_{uv}$ is again not true diameter.

**Claim 2:** The longest path lies between two leaf nodes.

If this is not the case, we can always extend the path with additional nodes to make it longer.

## Problem 4

