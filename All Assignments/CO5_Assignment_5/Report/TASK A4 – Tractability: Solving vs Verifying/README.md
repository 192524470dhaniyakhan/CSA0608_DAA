
---

# TASK A4 – TRACTABILITY: SOLVING vs VERIFYING
## P, NP, NP-Complete and NP-Hard

### Introduction

Computational problems are classified based on how efficiently they can be solved and how efficiently a proposed solution can be verified.

The major complexity classes are:

**1. P (Polynomial Time):**

P contains decision problems that can be solved by a deterministic algorithm in polynomial time.

Examples include shortest path and minimum spanning tree.

**2. NP (Nondeterministic Polynomial Time):**

NP contains decision problems for which a proposed solution can be verified in polynomial time.

**3. NP-Complete:**

A problem is NP-Complete if:
- It belongs to NP.
- Every problem in NP can be reduced to it in polynomial time.

**4. NP-Hard:**

A problem is NP-Hard if every problem in NP can be reduced to it in polynomial time. It does not necessarily have to belong to NP.

### Complexity Classification of Problems

| Problem | What Constitutes a Solution? | Efficient Verification? | Complexity Classification | Reason |
|---|---|---|---|---|
| Shortest Path | A path between two vertices with minimum total weight | Yes | P | Can be solved using polynomial-time shortest-path algorithms. |
| Minimum Spanning Tree | A spanning tree connecting all vertices with minimum total edge weight | Yes | P | Can be solved using Kruskal's or Prim's algorithm in polynomial time. |
| Subset Sum – Decision Version | A subset whose elements add up to the target value | Yes | NP-Complete | A proposed subset can be checked in polynomial time, and the decision problem is NP-Complete. |
| Hamiltonian Cycle – Decision Version | A cycle visiting every vertex exactly once and returning to the starting vertex | Yes | NP-Complete | A proposed cycle can be verified in polynomial time, but finding one is computationally difficult in general. |
| Travelling Salesperson – Decision Version | A tour visiting every city with total cost not exceeding a given threshold | Yes | NP-Complete | A proposed tour and its total cost can be verified in polynomial time. |
| Travelling Salesperson – Optimisation Version | A minimum-cost tour visiting every city exactly once | Yes | NP-Hard | Finding the optimal tour is an optimisation problem and is NP-Hard. |

### Explanation of Each Problem

**1. Shortest Path**

The shortest-path problem finds the minimum-cost path between two vertices in a weighted graph.

Algorithms such as Dijkstra's algorithm can solve the problem in polynomial time under its applicable edge-weight assumptions.

Therefore, it belongs to P.

**2. Minimum Spanning Tree**

A minimum spanning tree connects all vertices of a connected, weighted, undirected graph with minimum total edge weight and without cycles.

Kruskal's and Prim's algorithms solve this problem in polynomial time.

Therefore, it belongs to P.

**3. Subset Sum – Decision Version**

The problem determines whether a subset of given integers has a sum equal to a specified target.

A proposed subset can be verified by calculating its sum and comparing it with the target.

The decision version is NP-Complete.

**4. Hamiltonian Cycle – Decision Version**

The problem determines whether a graph contains a cycle that visits every vertex exactly once and returns to the starting vertex.

A proposed cycle can be checked by verifying its edges and ensuring that every vertex appears exactly once.

The problem is NP-Complete.

**5. Travelling Salesperson – Decision Version**

The decision version determines whether a tour exists whose total travelling cost is less than or equal to a specified limit.

A proposed tour can be verified by calculating its total cost.

The decision problem is NP-Complete.

**6. Travelling Salesperson – Optimisation Version**

The optimisation version aims to find the minimum-cost tour among all possible tours.

Since finding the optimal tour is computationally difficult, this version is NP-Hard.

### Inquiry 1 – Why is "Difficult to Solve" Not an Adequate Definition of NP?

"Difficult to solve" is not an accurate definition of NP because NP is defined based on the ability to verify a proposed solution in polynomial time.

A problem may be easy or difficult to solve, but if a proposed solution can be verified efficiently, it can belong to NP.

NP does not mean that a problem is necessarily difficult to solve.

For example, every problem in P also belongs to NP because a solution can be verified efficiently.

### Inquiry 2 – Why Is the Distinction Between Decision and Optimisation Important?

A decision problem asks whether a solution exists that satisfies a given condition, usually with a YES or NO answer.

An optimisation problem aims to find the best possible solution, such as the minimum cost or maximum value.

The distinction is important because NP-Completeness is formally defined for decision problems.

For example:

- TSP Decision Version: Determines whether a tour exists with cost less than or equal to a given threshold. It is NP-Complete.
- TSP Optimisation Version: Finds the minimum-cost tour. It is NP-Hard.

The distinction helps in understanding the computational difficulty and selecting appropriate algorithms.

### Complexity Summary

| Complexity Class | Main Property | Example |
|---|---|---|
| P | Solvable in polynomial time | Shortest Path |
| NP | Solutions verifiable in polynomial time | Subset Sum |
| NP-Complete | In NP and NP-Hard | Hamiltonian Cycle |
| NP-Hard | At least as hard as every problem in NP | TSP Optimisation |

### Final Result

The six computational problems were analysed and classified into P, NP-Complete and NP-Hard categories. The distinction between solving and verifying was explained. The importance of decision and optimisation versions was also demonstrated using the Travelling Salesperson Problem.
