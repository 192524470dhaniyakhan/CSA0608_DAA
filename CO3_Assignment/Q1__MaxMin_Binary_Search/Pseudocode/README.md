QUESTION 1: MAXIMUM AND MINIMUM USING DIVIDE AND CONQUER

Algorithm: MaxMin(A, low, high)

1. If low = high:
      Return A[low], A[low]

2. If high = low + 1:
      If A[low] < A[high]:
          Return A[high], A[low]
      Else:
          Return A[low], A[high]

3. mid = (low + high) / 2

4. (max1, min1) = MaxMin(A, low, mid)

5. (max2, min2) = MaxMin(A, mid + 1, high)

6. Maximum = max(max1, max2)

7. Minimum = min(min1, min2)

8. Return Maximum, Minimum


QUESTION 1: BINARY SEARCH

Algorithm: BinarySearch(A, key)

1. low = 0
2. high = length(A) - 1

3. While low <= high:

      mid = (low + high) / 2

      If A[mid] = key:
          Return mid

      Else if A[mid] < key:
          low = mid + 1

      Else:
          high = mid - 1

4. Return -1


TIME COMPLEXITY:
Max-Min: O(n)
Binary Search: O(log n)

SPACE COMPLEXITY:
Max-Min: O(log n)
Binary Search: O(1)
