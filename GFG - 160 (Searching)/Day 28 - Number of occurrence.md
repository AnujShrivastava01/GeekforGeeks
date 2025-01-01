---
Difficulty: Easy  
Source: 160 Days of Problem Solving  
Tags:
  - Arrays
  - Searching
---

# 🚀 _Day 1. Number of Occurrences_ 🧠

The problem can be found at the following link: [Problem Link](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/searching-gfg-160/problem/number-of-occurrence2259)


## 💡 **Problem Description:**

Given a sorted array `arr[]` and a number `target`, determine the number of occurrences of `target` in the array.  

If the number does not exist in the array, return `0`.

## 🔍 **Example Walkthrough:**

**Input:**  
`arr[] = [1, 1, 2, 2, 2, 2, 3], target = 2`  
**Output:**  
`4`  

**Explanation:**  
`2` occurs 4 times in the array.

**Input:**  
`arr[] = [1, 1, 2, 2, 2, 2, 3], target = 4`  
**Output:**  
`0`  

**Explanation:**  
`4` is not present in the array.

**Input:**  
`arr[] = [8, 9, 10, 12, 12, 12], target = 12`  
**Output:**  
`3`  

**Explanation:**  
`12` occurs 3 times in the array.

### Constraints:
- $`1 ≤ arr.size() ≤ 10^6`$
- $`1 ≤ arr[i] ≤ 10^6`$
- $`1 ≤ target ≤ 10^6`$



## 🎯 **My Approach:**

1. **Binary Search for Boundaries:**  
   - Since the array is sorted, we can leverage binary search to efficiently locate the first and last occurrence of the target.
   - Two binary search calls are made: one to find the lower bound and another for the upper bound.  
   - The difference between the indices of these two boundaries gives the count of occurrences.

2. **Steps:**  
   - Perform a binary search to find the first occurrence of the target.  
   - Perform another binary search to find the last occurrence of the target.  
   - Subtract the indices of these two boundaries and add `1` to calculate the count.  
   - If the target is not present, return `0`.



## 🕒 **Time and Auxiliary Space Complexity** 

- **Expected Time Complexity:** O(log n), as binary search operates in logarithmic time.  
- **Expected Auxiliary Space Complexity:** O(1), as only a constant amount of additional space is used.  

## 📝 **Solution Code**

## Code (C)

```c
int countFreq(int arr[], int n, int target) {
    int low = 0, high = n - 1;
    while (low < high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] < target)
            low = mid + 1;
        else
            high = mid;
    }

    if (arr[low] != target)
        return 0;

    int first = low;
    high = n - 1;
    while (low < high) {
        int mid = low + (high - low + 1) / 2;
        if (arr[mid] > target)
            high = mid - 1;
        else
            low = mid;
    }

    int last = high;
    return last - first + 1;
}
```



## Code (C++)

```cpp
class Solution {
public:
    int countFreq(const vector<int>& arr, int target) {
        auto lower = lower_bound(arr.begin(), arr.end(), target);
        auto upper = upper_bound(lower, arr.end(), target);
        return (lower != arr.end() && *lower == target) ? (upper - lower) : 0;
    }
};
```

