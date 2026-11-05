1. Aim
To design and implement a Divide-and-Conquer algorithm to find the maximum and minimum elements in an array using a tournament-based comparison strategy and compare its performance with the conventional method.
2. Algorithm Design
The Divide-and-Conquer approach divides the array into pairs of elements.
- Compare each pair to identify the smaller and larger elements.
- Store the smaller elements in a minimum candidate list.
- Store the larger elements in a maximum candidate list.
- Find the minimum from the minimum candidate list.
- Find the maximum from the maximum candidate list.
- Return both results.
This reduces the number of comparisons compared with independently finding the maximum and minimum.
