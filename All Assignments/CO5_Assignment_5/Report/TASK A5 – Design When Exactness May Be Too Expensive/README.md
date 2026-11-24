
---

# TASK A5 – DESIGN WHEN EXACTNESS MAY BE TOO EXPENSIVE
## Set Cover

### Introduction

The Set Cover problem is a combinatorial optimisation problem in which a collection of candidate emergency centres must be selected to cover all emergency-response zones.

Each emergency centre can serve a specific subset of zones.

The objective is to select the minimum number of centres so that every zone is covered.

### A5.1 – Exact Perspective

An exact combinatorial search can identify the optimal solution by examining possible combinations of emergency centres.

**Proposed Approach:**

1. Start with all available emergency centres.
2. Generate possible combinations of centres.
3. Check whether each combination covers all emergency zones.
4. Calculate the number of centres in each valid combination.
5. Keep track of the combination containing the minimum number of centres.
6. Return the minimum-size combination after examining the possibilities.

**Example:**

Consider four emergency zones:

Z = {Z1, Z2, Z3, Z4}

Candidate emergency centres:

| Emergency Centre | Zones Covered |
|---|---|
| C1 | Z1, Z2 |
| C2 | Z2, Z3 |
| C3 | Z3, Z4 |
| C4 | Z1, Z4 |

One possible valid solution is:

Selected Centres = {C1, C3}

These two centres cover all four zones.

Therefore, the minimum number of centres for this example is 2.

**Why Does Exact Search Become Problematic?**

If there are m candidate emergency centres, the total number of possible subsets is:

2^m

As the number of candidate centres increases, the number of combinations grows exponentially.

This makes exhaustive search computationally expensive for large instances.

Therefore, exact search is suitable for small problems, while approximation algorithms are useful for larger problems.

### A5.2 – Approximation Design

**Proposed Approach: Greedy Set Cover Algorithm**

The greedy approach repeatedly selects the emergency centre that covers the largest number of currently uncovered zones.

The algorithm continues until all zones are covered.

**Input:**
- Set Z containing all emergency zones.
- Set C containing all candidate emergency centres.
- Each centre has a corresponding set of zones it can cover.

**Output:**
- Selected emergency centres that cover all zones.

### Pseudocode

```text
ALGORITHM GreedySetCover(Z, C)

BEGIN

    UncoveredZones ← Z

    SelectedCentres ← EMPTY SET

    WHILE UncoveredZones is not EMPTY DO

        BestCentre ← NULL

        MaximumCoverage ← 0

        FOR each Centre in C DO

            CurrentCoverage ←
                Number of zones in
                (Centre covers INTERSECTION UncoveredZones)

            IF CurrentCoverage > MaximumCoverage THEN

                MaximumCoverage ← CurrentCoverage

                BestCentre ← Centre

            END IF

        END FOR

        IF BestCentre = NULL THEN

            RETURN FAILURE

        END IF

        ADD BestCentre to SelectedCentres

        REMOVE all zones covered by BestCentre
        from UncoveredZones

    END WHILE

    RETURN SelectedCentres

END
```

### Explanation of the Greedy Algorithm

1. Initially, all emergency zones are marked as uncovered.
2. The selected-centre list is initially empty.
3. The algorithm examines every available emergency centre.
4. It calculates how many currently uncovered zones each centre can serve.
5. The centre covering the largest number of uncovered zones is selected.
6. All zones covered by the selected centre are removed from the uncovered list.
7. The process repeats until no uncovered zones remain.
8. If no available centre can cover a remaining zone, the algorithm returns FAILURE.
9. The selected centres are returned as the final cover.

### Example of Greedy Selection

Consider the following emergency zones:

Z = {Z1, Z2, Z3, Z4}

| Centre | Zones Covered |
|---|---|
| C1 | Z1, Z2, Z3 |
| C2 | Z2, Z4 |
| C3 | Z3, Z4 |

**Greedy Selection Trace:**

| Step | Selected Centre | Newly Covered Zones | Remaining Zones |
|---|---|---|---|
| Initial | None | None | Z1, Z2, Z3, Z4 |
| 1 | C1 | Z1, Z2, Z3 | Z4 |
| 2 | C2 | Z4 | None |

**Final Selected Centres:**

{C1, C2}

**Total Centres Used:** 2

All emergency zones are covered successfully.

### A5.3 – What Have We Sacrificed?

There is an important difference between finding a feasible cover and proving that the cover is optimal.

**1. Finding a Feasible Cover**

A feasible cover means that every emergency zone is covered by at least one selected emergency centre.

The greedy algorithm can produce such a solution efficiently when a complete cover exists.

However, the selected centres may not always represent the minimum possible number.

**2. Proving Minimum Number of Centres**

Proving optimality requires demonstrating that no other combination of emergency centres can cover all zones using fewer centres.

An exact algorithm can establish this by examining the relevant combinations and finding the minimum-size cover.

The greedy algorithm does not generally provide an exact minimum-size solution.

### Comparison: Exact vs Greedy Approach

| Feature | Exact Algorithm | Greedy Approximation |
|---|---|---|
| Search Strategy | Examines combinations | Selects the best immediate choice |
| Solution Quality | Optimal | May be non-optimal |
| Search Effort | Exponential in the worst case | Generally lower |
| Scalability | Limited for large instances | More suitable for large instances |
| Optimality Guarantee | Yes | No guarantee of exact optimality |

### Complexity Analysis

Let:

- m = Number of candidate emergency centres.
- n = Number of emergency zones.

**Exact Algorithm:**

Worst-case time complexity: O(2^m × (m + n))

The algorithm may examine all possible centre combinations and check their coverage.

**Greedy Algorithm:**

Using a straightforward implementation that repeatedly scans all centres and their zone lists, the worst-case time complexity is O(n × m × n), assuming each centre covers at most n zones.

This is polynomial compared with exhaustive search.

### Final Result

The Set Cover problem was analysed using exact combinatorial search and a greedy approximation strategy. The exact approach can identify the minimum number of emergency centres but becomes computationally expensive as the number of candidates increases. The greedy approach selects the centre covering the largest number of uncovered zones and provides a feasible cover more efficiently, although it does not always guarantee an optimal solution.
```

<badge color="success">PART A COMPLETED</badge>

---

## Your assignment progress

<box border radius="lg" padding={3} gap={3}>
  <title size="lg">Part A – 25 Marks</title>
  <row justify="between">
    **A1 – Graph Colouring**
    <icon name="check-circle-filled" color="success"/>
  </row>
  <row justify="between">
    **A2 – Subset Sum**
    <icon name="check-circle-filled" color="success"/>
  </row>
  <row justify="between">
    **A3 – Backtracking Pattern**
    <icon name="check-circle-filled" color="success"/>
  </row>
  <row justify="between">
    **A4 – Complexity Classes**
    <icon name="check-circle-filled" color="success"/>
  </row>
  <row justify="between">
    **A5 – Set Cover**
    <icon name="check-circle-filled" color="success"/>
  </row>
  <divider color="subtle"/>
  <title color="success" size="2xl">5 / 5</title>
  <text color="secondary" size="xs">All Part A tasks prepared. Part A still needs to be included in the final consolidated PDF.</text>
</box>

## Next: Part B – Python implementation

Now we'll start putting actual Python programs into your GitHub folders.

Our first file will be:

<box border radius="lg" padding={3} gap={2}>
  <row align="center" gap={2}>
    <icon name="folder" color="#E5A33B"/>
    **Source_Code**
  </row>
  <box padding={{left:4}} gap={2}>
    <row align="center" gap={2}>
      <icon name="folder" color="#E5A33B"/>
      **Task_B1_Graph_Colouring**
    </row>
    <box padding={{left:4}}>
      <row align="center" gap={2}>
        <icon name="file-code" color="#3B82F6"/>
        **graph_colouring.py**
      </row>
      <row align="center" gap={2}>
        <icon name="file-text" color="secondary"/>
        **README.md**
      </row>
    </box>
  </box>
</box>

B1 will include:
- Graph colouring using backtracking.
- Search nodes and candidate assignments.
- Rejected branches and backtracks.
- Maximum search depth.
- Three validation tests.
- Input-order vs degree-based vertex ordering.
- Performance comparison tables.

**Let's move to B1 now, bro!** ❤️
