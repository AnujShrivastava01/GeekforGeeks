---
Difficulty: Medium  
Source: 160 Days of Problem Solving  
Tags:
  - Arrays  
  - Greedy  
---

# 🚀 _Day 9. Minimize the Heights II_ 🧠

The problem can be found at the following link: [Problem Link](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/arrays-gfg-160/problem/minimize-the-heights3351)

## 💡 **Problem Description:**

Given an array `arr[]` denoting the heights of N towers and a positive integer `K`, you are required to perform one of the following operations for each tower:

- Increase the height of the tower by `K`
- Decrease the height of the tower by `K`

Your task is to find out the minimum possible difference between the height of the tallest and shortest towers after performing the operations on each tower.

**Note:**
- It is compulsory to either increase or decrease the height of the tower by `K` for each tower.
- After the operation, the resultant array should not contain any negative integers.

## 🔍 **Example Walkthrough:**

**Input:**  
`k = 2, arr[] = {1, 5, 8, 10}`  
**Output:**  
`5`  

**Explanation:**  
After performing the operations, the modified heights will be `{3, 3, 6, 8}`. The difference between the largest and smallest heights is `8 - 3 = 5`.

**Input:**  
`k = 3, arr[] = {3, 9, 12, 16, 20}`  
**Output:**  
`11`  

**Explanation:**  
After performing the operations, the modified heights will be `{6, 12, 9, 13, 17}`. The difference between the largest and smallest heights is `17 - 6 = 11`.

### Constraints:
- `1 ≤ k ≤ 10^7`
- `1 ≤ n ≤ 10^5`
- `1 ≤ arr[i] ≤ 10^7`

## 🎯 **My Approach:**

1. **Greedy Approach**:
   - Sort the array of heights.
   - The goal is to minimize the difference between the tallest and shortest towers after performing the operations.
   - For each tower, choose whether to increase or decrease the height in such a way that the difference is minimized.
   - Calculate the difference between the modified tallest and shortest tower.

2. **Steps**:
   - Sort the array of heights.
   - Iterate through the array and try both options (increase or decrease) for each tower.
   - Track the minimum possible difference between the maximum and minimum tower heights after modifying the heights.

## 🕒 **Time and Auxiliary Space Complexity** 📝

- **Expected Time Complexity:** `O(n log n)`, where `n` is the size of the array. Sorting the array takes `O(n log n)`, and the rest of the operations are linear.
- **Expected Auxiliary Space Complexity:** `O(n)`, as we store the modified heights in an auxiliary space.

## 📝 **Solution Code**

## Code (C++)

```cpp
class Solution {
public:
    int getMinDiff(vector<int>& arr, int k) {
        int n = arr.size();
        vector<pair<int, int>> modifiedHeights;
        vector<int> frequency(n, 0);

        for (int i = 0; i < n; i++) {
            if (arr[i] - k >= 0) {
                modifiedHeights.emplace_back(arr[i] - k, i);
            }
            modifiedHeights.emplace_back(arr[i] + k, i);
        }

        sort(modifiedHeights.begin(), modifiedHeights.end());

        int left = 0, right = 0, covered = 0, minDifference = INT_MAX;

        while (right < modifiedHeights.size()) {
            if (frequency[modifiedHeights[right].second]++ == 0) {
                covered++;
            }

            while (covered == n) {
                minDifference = min(minDifference, modifiedHeights[right].first - modifiedHeights[left].first);

                if (--frequency[modifiedHeights[left].second] == 0) {
                    covered--;
                }
                left++;
            }
            right++;
        }

        return minDifference;
    }
};
```
