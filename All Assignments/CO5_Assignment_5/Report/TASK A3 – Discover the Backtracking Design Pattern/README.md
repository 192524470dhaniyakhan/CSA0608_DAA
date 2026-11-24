
---

# TASK A3 – DISCOVER THE BACKTRACKING DESIGN PATTERN

## A3.1 – Identify the Common Pattern

Backtracking is an algorithmic technique used to solve problems by constructing solutions step by step. Whenever a selected choice violates a constraint or cannot lead to a valid solution, the algorithm goes back to the previous decision and tries another possibility.

The three problems considered are:

1. N-Queens
2. Subset Sum
3. Graph Colouring

### Comparison of Backtracking Components

| Backtracking Component | N-Queens | Subset Sum | Graph Colouring |
|---|---|---|---|
| State | Positions of queens on the chessboard | Current subset and sum | Current colour assigned to each vertex |
| Decision Variable | Row or column position of a queen | Current array element | Current vertex |
| Candidate Choices | Available columns | Include or Exclude | Available colours |
| Feasibility Test | No two queens attack each other | Current sum does not exceed target (positive numbers) | Adjacent vertices must have different colours |
| Goal Condition | All N queens are placed | Subset sum equals target | All vertices are coloured |
| Pruning Condition | Queen placement causes an attack | Current sum exceeds target | Colour conflicts with an adjacent vertex |
| Undo Operation | Remove the queen from its position | Restore the previous subset and sum | Remove the assigned colour |

### Explanation

Although these problems have different objectives, they follow the same computational approach.

- N-Queens places queens while checking row, column and diagonal restrictions.
- Subset Sum selects or rejects elements while checking the required sum.
- Graph Colouring assigns colours while avoiding conflicts between connected vertices.

All three algorithms construct a solution incrementally, check constraints and reject invalid branches before exploring them further.

## A3.2 – Design a Generic Backtracking Framework

**Algorithm: GenericBacktracking**

**Input:** Initial problem state.

**Output:** A valid solution or FAILURE.

### Pseudocode

``` id="genericbt"
ALGORITHM BACKTRACK(State)

BEGIN

    IF GoalCondition(State) = TRUE THEN
        RETURN SUCCESS
    END IF

    CandidateList ← GenerateCandidates(State)

    FOR each Candidate in CandidateList DO

        IF Feasible(State, Candidate) = TRUE THEN

            Apply(State, Candidate)

            IF BACKTRACK(State) = SUCCESS THEN
                RETURN SUCCESS
            END IF

            Undo(State, Candidate)

        END IF

    END FOR

    RETURN FAILURE

END
```

### Explanation of the Framework

1. **Goal Condition:** Checks whether the current state represents a complete valid solution.
2. **Generate Candidates:** Produces possible choices for the next decision.
3. **Feasibility Test:** Checks whether a candidate satisfies the problem constraints.
4. **Apply:** Adds the selected candidate to the current state.
5. **Recursive Exploration:** Continues searching for a complete solution.
6. **Undo:** Restores the previous state if the selected candidate does not lead to a solution.
7. **Failure:** Returns FAILURE when no candidate produces a valid solution.

### Applications

The generic framework can represent all three problems:

- N-Queens: Candidates are possible queen positions.
- Subset Sum: Candidates are Include and Exclude decisions.
- Graph Colouring: Candidates are available colours.

The framework changes only the candidate-generation, feasibility and goal-checking procedures according to the problem.

## A3.3 – Explain the Role of Undo

The Undo operation is an important part of backtracking because it restores the previous search state after an unsuccessful decision.

Without Undo, the effects of an earlier decision would remain in the search state and could affect later choices.

### Example: Graph Colouring

Consider a graph with three vertices A, B and C.

Suppose:

- A is assigned Red.
- B is assigned Blue.
- The algorithm attempts to assign a colour to C.

If the selected colour for C causes a conflict, the algorithm must remove that assignment and return to the previous state.

If Undo is omitted:

1. The incorrect colour assignment remains.
2. Future choices are evaluated using an invalid state.
3. Other valid colour combinations may be missed.
4. The algorithm may incorrectly report that no solution exists.

Therefore, Undo ensures that every new candidate is explored from the correct previous state.

### Complexity Analysis

The time complexity of a backtracking algorithm depends on the number of candidate choices and the depth of the search tree.

In the worst case, if each level has b possible choices and the search depth is d:

**Time Complexity:** O(b^d)

**Space Complexity:** O(d) for the recursive search stack, excluding problem-specific state storage.

### Final Result

The common backtracking design pattern was identified using N-Queens, Subset Sum and Graph Colouring. A generic recursive backtracking framework was developed. The importance of the Undo operation was demonstrated through graph colouring, showing how restoring the previous state helps maintain correctness during recursive exploration.
