# Q1: Maximum and Minimum using Divide and Conquer

def max_min(arr, low, high):

    if low == high:
        return arr[low], arr[low]

    if high == low + 1:
        if arr[low] > arr[high]:
            return arr[low], arr[high]
        else:
            return arr[high], arr[low]

    mid = (low + high) // 2

    max1, min1 = max_min(arr, low, mid)
    max2, min2 = max_min(arr, mid + 1, high)

    maximum = max(max1, max2)
    minimum = min(min1, min2)

    return maximum, minimum


# Binary Search

def binary_search(arr, key):
    low = 0
    high = len(arr) - 1

    while low <= high:
        mid = (low + high) // 2

        if arr[mid] == key:
            return mid
        elif arr[mid] < key:
            low = mid + 1
        else:
            high = mid - 1

    return -1


# Main Program

arr = [7, 2, 9, 1, 5, 8, 3]

maximum, minimum = max_min(arr, 0, len(arr) - 1)

print("Maximum:", maximum)
print("Minimum:", minimum)

sorted_arr = sorted(arr)
key = 5

result = binary_search(sorted_arr, key)

print("Sorted Array:", sorted_arr)
print("Search Element:", key)

if result != -1:
    print("Element found at index:", result)
else:
    print("Element not found")
