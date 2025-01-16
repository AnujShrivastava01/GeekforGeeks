---
Difficulty: Medium  
Source: 160 Days of Problem Solving  
Tags:
  - Arrays
  - Map
---

# 🚀 _Day 9. Count Subarrays with Given XOR_ 🧠


The problem can be found at the following link: [Problem Link](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/hashing-gfg-160/problem/count-subarray-with-given-xor)



## 💡 **Problem Description:**

Given an array of integers `arr[]` and an integer `k`, count the number of subarrays whose XOR is equal to `k`.



## 🔍 **Example Walkthrough:**

### **Example 1**

**Input:**  
`arr = [4, 2, 2, 6, 4], k = 6`  
**Output:**  
`4`  

**Explanation:**  
The subarrays having XOR of their elements as `6` are:  
1. `[4, 2]`  
2. `[4, 2, 2, 6, 4]`  
3. `[2, 2, 6]`  
4. `[6]`

Hence, the output is `4`.



### **Example 2**

**Input:**  
`arr = [5, 6, 7, 8, 9], k = 5`  
**Output:**  
`2`  

**Explanation:**  
The subarrays having XOR of their elements as `5` are:  
1. `[5]`  
2. `[5, 6, 7, 8, 9]`

Hence, the output is `2`.



## **Constraints**

- $`1 ≤ arr.size() ≤ 10^5`$
- $`0 ≤ arr[i] ≤ 10^5`$
- $`0 ≤ k ≤ 10^5`$



## 🎯 **My Approach:**

The problem is solved using the **Prefix XOR** technique combined with a **Hash Map** for efficient subarray counting.  

1. **Key Observations**:  
   - Let `XOR(A, B)` represent the XOR of elements in subarray `[A...B]`.  
   - If the XOR of a subarray `[i...j]` equals `k`, then:  
     $\( \text{XOR(0, i-1)} \oplus \text{XOR(0, j)} = k \)$.  
     Rearranging gives:  
     $\( \text{XOR(0, i-1)} = \text{XOR(0, j)} \oplus k \)$.  

2. **Algorithm Steps**:  
   - Traverse the array while maintaining a **Prefix XOR** (`prefXOR`) of all elements encountered so far.
   - Use a hash map to store the frequency of each `prefXOR` value encountered.
   - For each element, calculate:  
     $\( \text{TargetXOR} = \text{prefXOR} \oplus k \)$.  
     If `TargetXOR` exists in the hash map, it means there are subarrays ending at the current index whose XOR equals `k`.
   - Add these counts to the result.
   - Finally, update the hash map with the current `prefXOR`.



## 🕒 **Time and Auxiliary Space Complexity** 

- **Expected Time Complexity:**  
  $\( O(n) \)$, where `n` is the size of the array. We traverse the array once, and each hash map operation (insertion or lookup) takes $\( O(1) \)$ on average.

- **Expected Auxiliary Space Complexity:**  
  $\( O(n) \)$, as we store up to `n` unique `prefXOR` values in the hash map.


## 📝 **Solution Code**

## Code (C++)

```cpp
class Solution {
public:
    long subarrayXor(vector<int> &arr, int k) {
        long res = 0, prefXOR = 0;
        unordered_map<int, int> mp;
        for (int val : arr) {
            prefXOR ^= val;
            res += mp[prefXOR ^ k] + (prefXOR == k);
            mp[prefXOR]++;
        }
        return res;
    }
};

```
