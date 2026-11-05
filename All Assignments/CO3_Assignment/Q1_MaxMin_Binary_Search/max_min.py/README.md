
def find_max_min(arr):
    comparisons = 0
    min_candidates = []
    max_candidates = []

    n = len(arr)

    if n == 0:
        return None, None, 0

    i = 0

    # Compare elements in pairs
    while i + 1 < n:
        comparisons += 1

        if arr[i] < arr[i + 1]:
            min_candidates.append(arr[i])
            max_candidates.append(arr[i + 1])
        else:
            min_candidates.append(arr[i + 1])
            max_candidates.append(arr[i])

        i += 2

    # Handle an odd remaining element
    if i < n:
        min_candidates.append(arr[i])
        max_candidates.append(arr[i])

    # Find minimum among smaller elements
    minimum = min_candidates[0]
    for x in min_candidates[1:]:
        comparisons += 1
        if x < minimum:
            minimum = x

    # Find maximum among larger elements
    maximum = max_candidates[0]
    for x in max_candidates[1:]:
        comparisons += 1
        if x > maximum:
            maximum = x

    return maximum, minimum, comparisons


arr = [12, 5, 8, 20, 3, 15]

maximum, minimum, count = find_max_min(arr)

print("Array:", arr)
print("Maximum element:", maximum)
print("Minimum element:", minimum)
print("Total comparisons:", count)
