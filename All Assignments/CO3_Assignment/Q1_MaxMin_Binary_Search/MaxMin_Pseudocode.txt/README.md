ALGORITHM: MAXIMUM AND MINIMUM USING TOURNAMENT METHOD

Step 1: Start.

Step 2: Read the array A of size n.

Step 3: Initialize two empty lists:
        MIN_CANDIDATES
        MAX_CANDIDATES

Step 4: Compare elements in pairs.

Step 5: For each pair:
        If first element < second element:
            Add first element to MIN_CANDIDATES.
            Add second element to MAX_CANDIDATES.
        Otherwise:
            Add second element to MIN_CANDIDATES.
            Add first element to MAX_CANDIDATES.

Step 6: If one element remains:
        Add it to both candidate lists.

Step 7: Find the minimum from MIN_CANDIDATES.

Step 8: Find the maximum from MAX_CANDIDATES.

Step 9: Display maximum and minimum.

Step 10: Stop.
