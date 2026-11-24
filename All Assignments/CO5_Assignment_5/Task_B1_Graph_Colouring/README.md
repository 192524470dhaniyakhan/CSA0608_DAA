
# PART A – ALGORITHMIC DESIGN AND PSEUDOCODE

# TASK A1 – DESIGN A CONSTRAINT-AWARE SEARCH
## Graph Colouring for Cloud-Service Deployment

### A1.1 – Model the Search Problem

**Input:**
- A graph G = (V, E).
- V represents the set of services.
- E represents conflicts between services.
- K represents the maximum number of available server groups (colours).

**Output:**

A valid assignment of colours to all vertices such that no two adjacent vertices have the same colour, using at most K colours.

If no valid assignment exists, the algorithm returns FAILURE.

**Decision Made at Each Stage:**

At each stage, the algorithm selects an unassigned vertex and assigns one of the available colours.

**Constraint:**

Two adjacent vertices must not receive the same colour.

**Goal Condition:**

All vertices must be assigned valid colours without violating any constraints.

### A1.2 – Define the Search State

The search state maintains:

1. The graph containing vertices and edges.
2. The current colour assigned to each vertex.
3. The number of available colours.
4. The number of vertices already assigned.

**Search Tree Node:**

Each node represents a partial assignment of colours to the vertices.

For example:

- Root: No vertices are assigned.
- Level 1: One vertex is assigned a colour.
- Level 2: Two vertices are assigned colours.
- Final level: All vertices are successfully coloured.

### A1.3 – Define the Pruning Condition

A partial assignment is rejected if the selected vertex has an adjacent vertex that already contains the same colour.

The algorithm does not explore that branch further because it violates the graph-colouring constraint.

If none of the available colours is valid for the selected vertex, the algorithm performs backtracking.

### A1.4 – Complete Pseudocode

**Algorithm: GraphColouring**

**Input:** Graph G = (V, E), Number of colours K

**Output:** Valid colouring or FAILURE

```
ALGORITHM GraphColouring(G, K)

BEGIN

    FOR each vertex v in V DO
        Colour[v] ← 0
    END FOR

    IF BACKTRACK(1) = TRUE THEN
        RETURN Colour
    ELSE
        RETURN FAILURE
    END IF

END


ALGORITHM BACKTRACK(index)

BEGIN

    IF index > NumberOfVertices THEN
        RETURN TRUE
    END IF

    vertex ← V[index]

    FOR colour ← 1 TO K DO

        feasible ← TRUE

        FOR each neighbour u of vertex DO

            IF Colour[u] = colour THEN
                feasible ← FALSE
                BREAK
            END IF

        END FOR

        IF feasible = TRUE THEN

            Colour[vertex] ← colour

            IF BACKTRACK(index + 1) = TRUE THEN
                RETURN TRUE
            END IF

            Colour[vertex] ← 0

        END IF

    END FOR

    RETURN FALSE

END
```

**Explanation:**

1. Initially, all vertices are uncoloured.
2. The algorithm selects the next unassigned vertex.
3. It checks each available colour.
4. A colour is accepted only if no adjacent vertex has the same colour.
5. The selected colour is assigned to the vertex.
6. The algorithm recursively explores the next vertex.
7. If a later assignment fails, the previous colour is removed.
8. The algorithm tries another available colour.
9. If all vertices are coloured, SUCCESS is returned.
10. If no valid assignment is possible, FAILURE is returned.

### A1.5 – Trace the Search

**Example Graph:**

Consider five vertices:

V = {A, B, C, D, E}

Edges:

E = {(A,B), (B,C), (C,A), (C,D), (D,E)}

Number of available colours:

K = 2

Available colours:

- Colour 1 = Red
- Colour 2 = Blue

**Initial Colour Assignment:**

| Vertex | Colour |
|---|---|
| A | Unassigned |
| B | Unassigned |
| C | Unassigned |
| D | Unassigned |
| E | Unassigned |

**Search Trace:**

| Step | Vertex | Attempted Colour | Decision |
|---|---|---|---|
| 1 | A | Red | Accepted |
| 2 | B | Red | Rejected (A-B conflict) |
| 3 | B | Blue | Accepted |
| 4 | C | Red | Rejected (A-C conflict) |
| 5 | C | Blue | Rejected (B-C conflict) |
| 6 | C | None available | Backtrack |
| 7 | B | Undo Blue | Backtrack |
| 8 | B | Red | Rejected (A-B conflict) |
| 9 | A | Undo Red | Backtrack |
| 10 | A | Blue | Explored symmetrically; failure |

**Observation:**

Vertices A, B and C form a triangle. A triangle requires at least three different colours. Therefore, the graph cannot be coloured using only two colours.

Vertices D and E are not reached because the algorithm fails while assigning vertex C.

**Result:**

The backtracking algorithm correctly identifies that the given graph cannot be coloured using two colours.

### Time Complexity Analysis

Let:

- V = Number of vertices.
- E = Number of edges.
- K = Number of available colours.

**Worst-Case Time Complexity:**

O(K^V × (V + E))

The algorithm may explore up to K choices for each of V vertices. Each feasibility check examines adjacent vertices.

**Space Complexity:**

O(V + E)

This includes graph storage, colour assignments and recursive call stack.

### Final Result

The graph-colouring problem was modelled using a graph and solved using recursive backtracking. Constraint checking and pruning were used to reject invalid assignments. The search trace demonstrated how the algorithm explores candidate colours, rejects conflicting choices and performs backtracking when no valid assignment is possible.

