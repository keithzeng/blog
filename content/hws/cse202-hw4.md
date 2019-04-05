---
title: "CSE202 HW4"
date: 2019-03-03T18:34:16-08:00
categories: ["algorithm"]
series: ["np"]
tags: ["hw", "cse202"]
draft: false
---

## Problem 1: Balanced Simple Path

### Idea

To prove Balanced Simple Path(BSP) is NP-Complete, we need to do following:

1. Prove that BSP $\in$ NP.
2. Choose a problem Y that is known to be NP-complete
3. Consider an arbitrary instance $s_Y$ of problem Y, and show how to construct, in polynomial time, an instance $s_X$ of problem X that satisfies the following properties:
  - If $s_Y$ is a “yes” instance of Y, then $s_X$ is a “yes” instance of X
  - If $s_X$ is a “yes” instance of X, then $s_Y$ is a “yes” instance of Y.

We decide to prove  Hamiltonian Path $\leq_p$ BSP

### Reduction

The Hamiltonian Path is a path that visit all the vertices exactly once. Now in a graph G with n nodes, we will need to visit n different nodes to complete the Hamiltonian Path. To reduce Hamiltonian Path to BSP we need to impose this constraint. Since BSP contains only -1 and 1 edges, let's assign all the edges in G with weight 1. Now a Hamiltonian Path will have total weight of n - 1 exactly since visiting n nodes requires n - 1 edges. Adding the constraint is pretty easy if we can connect the G with a long tail of n - 1 edges of weight -1, making the total weight of BSP 0.

For BSP Algorithm, the inputs are G, s, and t. We need to define a start node s and terminal node t in G. However, Hamiltonian Path can start at any node and end at any node. We can either try all the $n^2$ possible combination, or we do some trick to avoid finding the start node and end node. We add an source node labeled as s and direct edge from s to all the nodes in G with weight 1. Now, the total path weight will equal to n. Then we also create sink node $t_1$, where all the nodes direct an edge with weight of -1 to it. By adding these extra nodes and edges, we add the flexibility of that Hamiltonian Path can start at any node and end at any node. Then we need more nodes behind the $t_1$ to make the a long tail of total n nodes with weight -n as described earlier to control number of vertices visit. Finally, the last node of the long tail is labeled as t.

Let's say this is the original graph G

![hw4.1](/img/cse202/hw4.1.png)

With addition of n + 1 nodes, 3n - 1 edges, we got the new G' as follow

![hw4.1b](/img/cse202/hw4.1b.png)

The blue edges with weight 1 connect s to all the nodes in the G to make all the nodes as potential starting node for Hamiltonian path. The red edges with weight -1 connect all the nodes to the head node $t_1$ of tail is to make them a potential end node for Hamiltonian Path. All the tail node along with t is to force the constraint that all vertices should be visited exactly once.

### Correctness

**Prove that BSP $\in$ NP.**

Given a certificate - a path in order, we can easily check if this path is BSP in O(p(n)) by making sure each vertex is visited exactly once and the sum of the edges in the path is equal to 0. If a problem can be verify in polynomial time to the input size, then the problem is in NP. Therefore BSP $\in$ NP.

**Prove Hamiltonian Path $\leq_p$ BSP**

We choose a NP-Complete problem - Hamiltonian Path, and reduce its problem to BSP. To convert from G to G' for BSP algorithm, we connect s node to all the node, then all the nodes to tail node, and construct additional nodes to control the navigation of the path. The construction takes about O(3n) or O(n), therefore it is polynomial time conversion.

**Prove $s_X$ and $s_Y$ Return Same Answer**

We claim that the BSP will return true to G' only if G contains a Hamiltonian Path. It's easy to see that Hamiltonian path visit all the nodes exactly once, when the BSP execute on G' will visit the same nodes in the G exactly once as well as in BSP. Any detour from Hamiltonian path will increase or decrease the path sum resulting a nonzero weight when reach the t node, leading the BSP Algorithm to return false. Conversely, all the BSP's that BSP Algorithm return true can be converted to Hamiltonian path by removing all the negative edges and facilitator nodes. Thus, we prove that these two problems are equivalent.

From the given graph, we can see that $a \rightarrow d \rightarrow b \rightarrow c$ is the only Hamiltonian Path, thus $s_Y$ = 'YES'. When we run BSP algorithm on G', s, and t, we also get $s_X$ = 'YES', and the only SBP is $s \rightarrow d \rightarrow b \rightarrow c \rightarrow t_1 \rightarrow t_2 \rightarrow t_3 \rightarrow t$. Conversely, the reverse has to be true. When we return $s_X$ = 'YES', there is way to visit all the vertices then $s_Y$ is also 'YES'.

## Problem 2: (KT 8.7): 4-Dimensional Matching

Do there exist n 4-tuples from C so that no two have an element in common?

If $\exists S \subseteq C$ and $|S| = n$ that no conflict in all the four coordinates, then YES.

### Idea

To prove 4-Dimensional Matching(4DM) is NP-Complete, we need to do following:

1. Prove that 4DM $\in$ NP.
2. Choose a problem Y that is known to be NP-complete
3. Consider an arbitrary instance $s_Y$ of problem Y, and show how to construct, in polynomial time, an instance $s_X$ of problem X that satisfies the following properties:
  - If $s_Y$ is a “yes” instance of Y, then $s_X$ is a “yes” instance of X
  - If $s_X$ is a “yes” instance of X, then $s_Y$ is a “yes” instance of Y.

We decide to prove  3-Dimensional Matching(3DM) $\leq_p$ 4DM

### Reduction

To reduce 3DM to 4DM without affecting the original 3DM, we can simply pad the all the tuples from C with a duplicate of 3rd coordinate, resulting of the form ($w_j, x_k, y_l, y_l$). This can be achieve in O(p(|n|)) for any input. Let's call this new collection C', and define Z = Y. Supplying C' and W, X, Y, and Z to the 4DM will solve the 3DM.

### Correctness

**Prove that 4DM $\in$ NP.**

Given a certificate of n tuples of length 4, or array of n x 4, we can check the solution in polynomial time. To make sure each element appear 1 time only, we can use set to record the appearance. To make sure tuple exist in C, if we use adjacency matrix, then we can access the element in O(1) time, so it takes total time of O(n). So, the verification takes polynomial time to the input size. Therefore 4DM $\in$ NP.

**Prove 3DM $\leq_p$ 4DM**

We convert the C to C' by duplicating the 3rd element of the tuple, this can be achieve in O(|C|) time, which |C| can be at most $n^3$. The conversion takes O(p(n)), which fulfill the requirement.

**Prove $s_X$ and $s_Y$ Return Same Answer**

We claim if there is solution to 3DM there is solution to 4DM with C'. Suppose that S is the solution to the 3DM and S' is solution to the 4DM. It's easy to see that by padding all the $t=(w_j, x_k, y_l) \in S$ with the $y_l$, we get the S', because the C' passed into the 4DM was manipulated this way and Z = Y. Conversely, the tuple $t' = (w_j, x_k, y_l, z_m) \in S'$  can be can be converted to $t \in S$ by simply dropping the last element of the tuple. This can be done so because last element of $t' \in S'$ will not affect how W, X, and Y match. This essentially shows that $s_X$ = 'YES' then $s_Y$ = 'YES' and when $s_Y$ = 'YES' then $s_X$ = 'YES'. Based on the evidences shown above, we have proved that 4DM is NP-Complete Problem.

## Problem 3: Domino Tiling

### Idea

Since domino is 1 x 2 rectangle, we will need to use it to cover two adjacent squares. Now, there are two ways of squares to be adjacent, either vertically or horizontally, or same as up-down and left-right. Since the question impose the constraint that if the square is cover by one domino that we cannot overlay another one. Therefore each square can be covered with 1 domino only.

Looking at these two possible orientations of domino, we can see that these two squares' index sum must be in odd and even combo, i.e. (i,j) if i + j is odd, then i + 1 + j = even. Therefore, we can split the squares into two sets A and B, where A contains all the odd index sum squares and B contains all the even index sum squares. We treat each square as a node, then we draw an edge between elements from A and elements from B if they are adjacent. By adding the edge with weight 1, this problem essentially boils down to the bipartite matching problem G(V, E), where $V = A \cup B$, and E = edges between A and B. We can find a solution, if we can find a perfect matching between A and B. We can easily convert bipartite problem into a network flow problem by adding s and t node, and also send flow of unit 1 from s to all the elements in A and then from all the elements from B to t. After running the network flow algorithm, we will get the maximum flow which will equals to number of matching |M| we can get.

Assume that we have 3x3 matrix with
\begin{bmatrix}
F & T & F \newline
F & T & T \newline
F & F & T \newline
\end{bmatrix}

Then we will have diagram of

![hw4.3](/img/cse202/hw4.3.png)

### Algorithm

ALGO(S):

- Let n = length of S
- Let A = $\emptyset$
- Let B = $\emptyset$
- for i from 0 to n - 1
  - for j from 0 to n - 1
     - if i + j = odd number
         - add i * n + j to A
     - else i + j = even number
         - add i * n + j  to B
- Let E = $\emptyset$
- for a in A
  - for neighbor in a's 4 neighbors
  - if S[neighbor] = T
     - E $\gets$ E $\cup$ {e(a,neighbor)}
- $G_{bipartite} = G(A \cup B, E)$
- G = convertToNetworkFlow($G_{bipartite}$)
- M = networkFlowALGO(G)
- if M = $|A \cup B|$ / 2
  - return true
- else
  - return false

### Correctness

The matching between A and B are Bipartite matching, since any match will exclude the element from matching with another one. Also we draw the edge only when they are adjacent to each other, preventing domino being splitted. Bipartite graph also impose the constraint that matching happens in different sets. The edge represents the domino that cover the squares one from each set. Further more, the bipartite matching also exclude the matching of 1 node to multiple other nodes, the capacity = 1 in network flow graph nicely impose this constraint. This is crucial for determine the feasibility with the return flow M (number of domino).

At the end, the flow return form the networkFlowALGO is exactly number of domino that can cover 2 squares. We check its equality with EXP = $|A \cup B|$ / 2. The idea is very simple since we have $|A \cup B|$ many squares, we need exactly $|A \cup B|$ / 2 dominoes to cover all these squares. If the M doesn't equate to the EXP, we cannot cover all the squares, thus returning false. On the other hand, if we got M to be EXP, we can cover all the squares, thus returning true.

### Complexity

The Ford-Fulkerson Algorithm has time complexity of O(|E||V|). In our case we have have at most $n^2$ nodes in our V, and |E| is at most 4|V| since there are 4 neighbors for each square, so $|E| = 4n^2$ and $|V| = n^2$, then the time complexity for our algorithm is O($n^4$). Space will be O($n^4$) if we use adjacency matrix to represent the graph of $n^2$ nodes.

### Data Structure

Simple 2-dimensional array should be sufficient to fulfill the need.

## Problem 4: (KT 10.9): MaxCut for trees

### Idea

We choose a random node r as the root of the tree. For each node v $\in$ V, we define a tree $T_v$ along with $n_v$ which is number of nodes under the subtree $T_v$. Now we can split the $T_v$ into two sets X, Y in any ratio, and one of them must contains the v, the cut is dependent on how we place the v. If we place the v in X, and its children in Y, we create a cut equals to the sum of edges. Now if v is place along with its children, there will be no cut associated with v. Lastly, if v is placed with one of its children, we create a cut equals to one of the edge. This observation has helped us in creating subproblem for this graph.

Let's assume that v $\in$ X and $|X| = k$. Let's define OPT(v, k) to be the maximum cut for the partition that contains v with size k and $1 \leq k \leq n_v$. The OPT(v, k) can be determined as follow

1. v = leaf node, OPT(v, 1) = 0
1. v contains 1 child subtree of $T_a$, $OPT(v, k) = \max(OPT(a, k - 1), w(v, a) + OPT(a, n_a - (k - 1)) \forall 1 \leq k \leq n_v$
1. v contains 2 children, $T_a$ and $T_b$, $OPT(v, k) = \max\_{0\leq l \leq k - 1, r = k - 1 - l} \max(OPT(a, l), w(v, a) + OPT(a, n_a - l)) + \max(OPT(b, r), w(v, b) + OPT(b, n_b - r))$

The base case, case 1, is trivial, since a leaf node has no edge, so we have cut of 0. For case 2, if we have only 1 child, we can either place it along with its child a, thus the OPT(v, k) = OPT(a, k - 1) with one size less or we place v on the other set generating a cut of w(v, a) + $OPT(a, n_a - (k - 1))$ by selecting $n_a - (k - 1)$ nodes with a. Now if the v has two subtrees, we need to check all the possible cases, where we pick l nodes from the left subtree, and correspondingly r = k - 2 from right subtree. Therefore, we need to check all the possible selection of nodes from left child, ranging from 0 to k - 1.

Notes: one caveat is that the expression contains OPT(v, 0) is meaningless and the any expression contains OPT(v, 0) should be evaluated to 0, i.e. w(v, a) + OPT(a, 0) should evaluate to 0.

### Algorithm

ALGO(T(V, E), n):

- Let OPT = array of n x n
- Let size = array of n
- Let pick an arbitrary node r as the root
- Build the OPT from the bottom level first
- for v in level's node
  - if v is leaf node
     - size[v] = 1
     - OPT(v, 1) = 0
  - else if v has 1 subtree, $T_a$
     - size[v] = size[a] + 1
     - for k from 1 to size[v]
         - $OPT(v, k) = \max(OPT(a, k - 1), w(v, a) + OPT(a, n_a - (k - 1))$
  - else v has 2 subtree, $T_a$ and $T_b$
     - size[v] = size[a] + size[b] + 1
     - for k from 1 to size[v]
         - Let maxSoFar = 0
         - for l from 0 to k - 1
             - let r = k - 1 - l
             - curMax = $\max(OPT(a, l), w(v, a) + OPT(a, n_a - l))$
             - $+ \max(OPT(b, r), w(v, b) + OPT(b, n_b - r))$
             - maxSoFar = max(maxSoFar, curMax)
         - $OPT(v, k)$ = maxSoFar
  - level = level - 1

return OPT(r, n / 2)

### Correctness

**Leaf Node**

The base case is trivial, since if there is only 1 node, there is no edge which means there is no cut.


**Nonleaf Node**

For current k and $T_v$, assume that for all $1 \leq t \leq k - 1$ and all descendants of v have valid OPT value. We can prove by induction that all our algorithm return the correct value. We need to prove this for two cases, if $T_v$ has one child or two children.

**Single Child $T_a$**

If we want the partition that contains v has size k, we can either place v along with a. If we place v with a, we need k - 1 more nodes on $T_a$, this intuitively leads to the formula
$$OPT(v, k) = OPT(a, k - 1)$$
or if we place v on the other set, we will now have cut of w(v, a) cut plus the maximum cut by picking n - (k - 1) nodes on $T_a$. This will leave exactly k - 1 node in $T_a$ to be place with v. This will lead to the formula of following 
$$OPT(v, k) = w(v, a) + OPT(a, n_a - (k - 1))$$

We have consider all the possible scenario in the placement of v, and we need to pick max of the two to fulfill the definition of OPT(v, k).

**Two Children $T_a$ and $T_b$**

Now for the case of two children, if we want to fulfill the requirement of picking k - 1 nodes with v, we have $n^2$ possible scenario. We can pick 0 from $T_a$ or k - 1 from $T_b$, 1 from $T_a$ or k - 2 from $T_b$, etc. Therefore, we need a double for loop for checking all the possible ways. We can pick 0 node from left child $T_a$ or k - 1 nodes in right child $T_b$. Now assume that we are selecting l nodes from left and r = k - 1 - l nodes from right, we can optimize each side individually by either place it along with its child or not. For left child, we get

$$LEFT = \max(OPT(a, l), w(v, a) + OPT(a, n_a - l))$$

For right child, we get

$$RIGHT =  \max(OPT(b, r), w(v, b) + OPT(b, n_b - r))$$

Using a double for loops, we can check all the possible choices ensuring we get the right value for current v and k.

$$OPT(v, k) = \max\_{0\leq l \leq k - 1, r = k - 1 - l} LEFT + RIGHT$$

### Complexity
For every node, we have two nested loop and can potentially by as big as n, where n is the number of vertices. Since we have n nodes, we have to time complexity of $O(n^3)$. For space, we use $O(n^2)$ for OPT array.

### Data Structure

Simple array will suffice if all the vertices are encoded with number.
We use two arrays, which one is for storing the OPT for each v and k, and another one for the size of each subtree.

[^algo]: Algorithm Design by Jon Kleinber, Eva Tardos 