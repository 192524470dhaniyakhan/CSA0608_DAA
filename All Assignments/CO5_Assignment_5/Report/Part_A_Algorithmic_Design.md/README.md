
---

# TASK A2 – DON'T SEARCH WHAT CANNOT WORK
## Improve a Weak Subset-Sum Design

### A2.1 – Diagnose the Computational Waste

The given algorithm generates every possible subset before checking whether its sum equals the target value.

This approach causes unnecessary computational work because:

1. It generates all possible subsets, even when some subsets cannot produce the target.
2. It checks the sum only after generating a complete subset.
3. It does not eliminate invalid search branches early.
4. It performs unnecessary calculations for subsets that already exceed the target.

For a set containing n elements, the total number of possible subsets is:

2^n

Therefore, the worst-case time complexity is O(2^n × n) when each generated subset is summed separately.

### A2.2 – Redesign Using Backtracking

**Proposed Approach:**

The subset-sum problem can be improved using recursive backtracking.

Instead of generating every complete subset, the algorithm makes two decisions for each element:

1. Include the current element in the subset.
2. Exclude the current element from the subset.

Since all input numbers are positive, a branch can be terminated whenever the current sum exceeds the target.

**Algorithm: SubsetSumBacktracking**

**Input:**
- Array A containing positive integers.
- Target sum T.
- Number of elements N.

**Output:**
- TRUE if a subset with the required sum exists.
- FALSE otherwise.

**Pseudocode:**

```
ALGORITHM SubsetSum(A, N, T)

BEGIN

    RETURN BACKTRACK(1, 0)

END


ALGORITHM BACKTRACK(index, currentSum)

BEGIN

    IF currentSum = T THEN
        RETURN TRUE
    END IF

    IF currentSum > T THEN
        RETURN FALSE
    END IF

    IF index > N THEN
        RETURN FALSE
    END IF

    // Include the current element

    IF BACKTRACK(index + 1,
                 currentSum + A[index]) = TRUE THEN

        RETURN TRUE

    END IF

    // Exclude the current element

    IF BACKTRACK(index + 1,
                 currentSum) = TRUE THEN

        RETURN TRUE

    END IF

    RETURN FALSE

END
```

**Explanation:**

1. Initially, the current sum is zero.
2. The algorithm selects the first element.
3. It explores the Include decision.
4. If the target is not reached, it explores the Exclude decision.
5. If the current sum exceeds the target, the branch is immediately rejected.
6. If all elements are processed without reaching the target, the branch returns FALSE.
7. The algorithm continues until a valid subset is found or all possibilities are exhausted.

### A2.3 – Demonstrate Pruning

**Given Input:**

Set A = {3, 5, 7, 10}

Target T = 9

**Example of a Pruned Branch:**

| Step | Decision | Current Sum | Result |
|---|---|---:|---|
| 1 | Include 3 | 3 | Continue |
| 2 | Include 5 | 8 | Continue |
| 3 | Include 7 | 15 | Reject |
| 4 | Further exploration | 15 | Pruned |

**Explanation:**

When the algorithm includes 3, 5 and 7, the current sum becomes 15.

Since 15 is greater than the target value 9, the algorithm immediately terminates that branch.

Further exploration is unnecessary because all remaining numbers are positive. Adding more elements can only increase the sum.

**Valid Subset Example:**

{3, 5, 1} would reach 9 if 1 were present in the input. However, the given set does not contain 1.

For the actual input, the subset {3,  5} gives 8, and no subset produces 9.

Therefore, the algorithm returns FALSE.

### A2.4 – Challenge Your Pruning Rule

**Question:**

Suppose negative integers are now permitted. Does the pruning condition remain valid?

**Answer:**

No. The pruning condition is no longer valid when negative integers are permitted.

The original pruning condition assumes that all remaining elements are positive.

If negative numbers are allowed, a current sum that exceeds the target may later decrease after adding a negative number.

**Example:**

Set A = {12, -5, 2}

Target T = 9

If the algorithm first selects 12:

Current Sum = 12

Since 12 is greater than 9, the original algorithm would reject the branch.

However:

12 + (-5) + 2 = 9

A valid solution actually exists.

Therefore, pruning the branch when currentSum > Target would incorrectly eliminate a valid solution.

**Violated Assumption:**

The assumption that every remaining element is positive has been violated.

**Modification:**

When negative integers are allowed, the algorithm must use a different pruning strategy that considers the possible minimum and maximum sums of the remaining elements.

### Complexity Analysis

**Time Complexity:**

O(2^n)

In the worst case, the algorithm explores both Include and Exclude decisions for every element.

**Space Complexity:**

O(n)

The recursive call stack can grow up to n levels.

### Final Result

The inefficient subset-generation approach was redesigned using recursive backtracking. Include and Exclude decisions were introduced, and pruning was applied when the current sum exceeded the target. The analysis also demonstrated that this pruning condition is valid only when all input elements are positive.
