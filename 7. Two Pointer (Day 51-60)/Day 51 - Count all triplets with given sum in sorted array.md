---
Difficulty: Medium  
Source: 160 Days of Problem Solving  
Tags:
  - two-pointer-technique
  - Hash
---

# 🚀 _Day 1. Count all triplets with given sum in sorted array_ 🧠


The problem can be found at the following link: [Problem Link](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/two-pointer-technique-gfg-160/problem/count-all-triplets-with-given-sum-in-sorted-array)

## 💡 **Problem Description:**

You are given a sorted array `arr[]` of size `n` and an integer `target`. Your task is to count the number of triplets `(i, j, k)` such that:  
- `i < j < k`  
- `arr[i] + arr[j] + arr[k] == target`

## 🔍 **Example Walkthrough:**

**Input:**  
`arr[] = [-3, -1, -1, 0, 1, 2]`, `target = -2`  
**Output:**  
`4`  
**Explanation:**  
The triplets are:  
- `arr[0] + arr[3] + arr[4] = -3 + 0 + 1 = -2`  
- `arr[0] + arr[1] + arr[5] = -3 + (-1) + 2 = -2`  
- `arr[0] + arr[2] + arr[5] = -3 + (-1) + 2 = -2`  
- `arr[1] + arr[2] + arr[3] = -1 + (-1) + 0 = -2`



**Input:**  
`arr[] = [-2, 0, 1, 1, 5]`, `target = 1`  
**Output:**  
`0`  
**Explanation:**  
No triplet adds up to `1`.



### Constraints:
- $`3 ≤ arr.size() ≤ 10^3`$
- $`-10^5 ≤ arr[i], target ≤ 10^5`$



## 🎯 **My Approach:**

1. **Two-Pointer Technique in a Sorted Array**:  
   To efficiently solve the problem, we use the two-pointer approach in a sorted array:
   - Iterate through the array, treating each element as the first element of a potential triplet.
   - Use two pointers (`left` and `right`) to find the other two elements that satisfy the required sum.
   - If the current sum matches the target, count all unique combinations while handling duplicates.

2. **Handling Duplicates**:  
   - If `arr[left] == arr[right]`, count all combinations formed by the elements between `left` and `right`.
   - If duplicates exist in either pointer range, skip them while counting.

3. **Steps:**
   - Fix the first element (`arr[i]`) and use two pointers for the remaining subarray.
   - Calculate the sum of the triplet. If it equals the target:
     - Count the combinations and adjust pointers to skip duplicates.
   - If the sum is smaller than the target, move the left pointer.
   - If the sum is larger, move the right pointer.



## 🕒 **Time and Auxiliary Space Complexity** 

- **Expected Time Complexity:** O(n²), where `n` is the size of the array. The outer loop iterates through each element, and the two-pointer traversal for each element takes O(n) time in the worst case.
- **Expected Auxiliary Space Complexity:** O(1), as we only use a constant amount of additional space for variables.

## 📝 **Solution Code**

## Code (C++)

```cpp
class Solution {
public:
    int countTriplets(vector<int>& arr, int target) {
        int n = arr.size(), res = 0;
        for (int i = 0; i < n - 2; ++i) {
            int left = i + 1, right = n - 1;
            while (left < right) {
                int sum = arr[i] + arr[left] + arr[right];
                if (sum < target) {
                    ++left;
                } else if (sum > target) {
                    --right;
                } else {
                    if (arr[left] == arr[right]) {
                        int count = right - left + 1;
                        res += (count * (count - 1)) / 2;
                        break;
                    } else {
                        int cnt1 = 1, cnt2 = 1;
                        while (left + 1 < right && arr[left] == arr[left + 1]) ++left, ++cnt1;
                        while (right - 1 > left && arr[right] == arr[right - 1]) --right, ++cnt2;
                        res += cnt1 * cnt2;
                        ++left;
                        --right;
                    }
                }
            }
        }
        return res;
    }
};
```

