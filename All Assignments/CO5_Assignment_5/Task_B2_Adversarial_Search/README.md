
# Task B2 – Engineer an Adversarial Input

## Objective

To investigate how two graphs with the same number of vertices and colours can produce different search behaviour in a backtracking algorithm.

## Algorithm Used

Recursive Graph Colouring using Backtracking.

## Experimental Configuration

- Number of vertices: 5
- Number of available colours: 2
- Search strategy: Original input order

## Graph A – Easy Input

Graph A is a path graph containing five vertices.

Edges:

(A,B), (B,C), (C,D), (D,E)

This graph is colourable using two colours.

## Graph B – Adversarial Input

Graph B is a cycle containing five vertices.

Edges:

(A,B), (B,C), (C,D), (D,E), (E,A)

This graph contains an odd cycle and cannot be coloured using only two colours.

## Prediction Before Execution

Graph B is expected to require more search because its odd cycle creates a conflict that cannot be resolved with two colours.

Unsuccessful branches are expected when the algorithm reaches the final vertex and discovers that both available colours conflict with its already-coloured neighbours.

Graph A is expected to find a valid colouring without backtracking.

## Experimental Results

| Measure | Graph A | Graph B |
|---|---:|---:|
| Search Nodes | 6 | 11 |
| Candidate Assignments | 7 | 18 |
| Rejected Branches | 2 | 8 |
| Backtracks | 0 | 8 |
| Maximum Search Depth | 5 | 5 |

## Interpretation

Graph A was successfully coloured using two colours without requiring backtracking.

Graph B could not be coloured using two colours. The algorithm explored alternative assignments and repeatedly encountered conflicts due to the odd cycle.

Graph B required more search nodes, candidate assignments and backtracks than Graph A.

## Investigation

Input size alone does not describe the computational effort required by a backtracking algorithm.

Even though both graphs contain the same number of vertices and use the same number of colours, their structures produce different search behaviours.

The important structural property of Graph B is its odd cycle. An odd cycle cannot be coloured using only two colours, causing the algorithm to explore and reject multiple assignments.

## Final Result

The experiment demonstrated that graph structure significantly influences backtracking performance. Graph B required more computational effort than Graph A despite having exactly the same number of vertices and available colours.

