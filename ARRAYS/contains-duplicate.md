# Contains Duplicate Problem - Complete Solutions Guide

## Problem Statement
Given an integer array `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.

**Example 1:**
- Input: `nums = [1,2,3,1]`
- Output: `true`
- Explanation: The element 1 occurs at indices 0 and 3.

**Example 2:**
- Input: `nums = [1,2,3,4]`
- Output: `false`
- Explanation: All elements are distinct.

## Solution 1: Brute Force Approach

### Algorithm Explanation
The brute force approach checks every pair of elements in the array to see if any two elements are equal. We use nested loops where the outer loop picks each element and the inner loop compares it with all subsequent elements.

### Code Implementation
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        int n = nums.size();
        
        // Check every pair of elements
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (nums[i] == nums[j]) {
                    return true;  // Found duplicate
                }
            }
        }
        
        return false;  // No duplicates found
    }
};
```

### Step-by-Step Tracing
Let's trace through Example 1: `nums = [1,2,3,1]`

```
Initial: nums = [1, 2, 3, 1], n = 4

i=0 (nums[0] = 1):
  j=1: nums[0] vs nums[1] → 1 vs 2 → Not equal
  j=2: nums[0] vs nums[2] → 1 vs 3 → Not equal  
  j=3: nums[0] vs nums[3] → 1 vs 1 → Equal! Return true

Result: true (duplicate found)
```

For Example 2: `nums = [1,2,3,4]`
```
Initial: nums = [1, 2, 3, 4], n = 4

i=0 (nums[0] = 1):
  j=1: 1 vs 2 → Not equal
  j=2: 1 vs 3 → Not equal
  j=3: 1 vs 4 → Not equal

i=1 (nums[1] = 2):
  j=2: 2 vs 3 → Not equal
  j=3: 2 vs 4 → Not equal

i=2 (nums[2] = 3):
  j=3: 3 vs 4 → Not equal

All pairs checked, no duplicates found.
Result: false
```

## Solution 2: Hash Set Approach (Optimized)

### Algorithm Explanation
We use an unordered set to keep track of elements we've seen. As we iterate through the array, we check if the current element is already in the set. If it is, we've found a duplicate. If not, we add it to the set and continue.

### Code Implementation
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> seen;
        
        for (int num : nums) {
            // If element already exists in set, we found a duplicate
            if (seen.find(num) != seen.end()) {
                return true;
            }
            // Add current element to set
            seen.insert(num);
        }
        
        return false;  // No duplicates found
    }
};
```

### Step-by-Step Tracing
Let's trace through Example 1: `nums = [1,2,3,1]`

```
Initial: nums = [1, 2, 3, 1], seen = {}

Step 1: num = 1
  - Check if 1 in seen: No
  - Insert 1 into seen
  - seen = {1}

Step 2: num = 2
  - Check if 2 in seen: No
  - Insert 2 into seen
  - seen = {1, 2}

Step 3: num = 3
  - Check if 3 in seen: No
  - Insert 3 into seen
  - seen = {1, 2, 3}

Step 4: num = 1
  - Check if 1 in seen: Yes! → Return true

Result: true (duplicate found)
```

For Example 2: `nums = [1,2,3,4]`
```
Initial: nums = [1, 2, 3, 4], seen = {}

Step 1: num = 1 → seen = {1}
Step 2: num = 2 → seen = {1, 2}
Step 3: num = 3 → seen = {1, 2, 3}
Step 4: num = 4 → seen = {1, 2, 3, 4}

All elements processed, no duplicates found.
Result: false
```

## Solution 3: Set Size Comparison Approach

### Algorithm Explanation
This approach creates a set from the input vector and compares the size of the set with the original vector. If they have different sizes, it means there were duplicates in the original vector (since sets only store unique elements).

### Code Implementation
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        set<int> s(nums.begin(), nums.end());
        return s.size() != nums.size();
    }
};
```

### Step-by-Step Tracing
Let's trace through Example 1: `nums = [1,2,3,1]`

```
Initial: nums = [1, 2, 3, 1], nums.size() = 4

Step 1: Create set from nums
  - set<int> s(nums.begin(), nums.end())
  - s = {1, 2, 3} (duplicates automatically removed)
  - s.size() = 3

Step 2: Compare sizes
  - s.size() != nums.size() → 3 != 4 → true

Result: true (duplicate found)
```

For Example 2: `nums = [1,2,3,4]`
```
Initial: nums = [1, 2, 3, 4], nums.size() = 4

Step 1: Create set from nums
  - s = {1, 2, 3, 4}
  - s.size() = 4

Step 2: Compare sizes
  - s.size() != nums.size() → 4 != 4 → false

Result: false (no duplicates)
```

## Time and Space Complexity Comparison

| Approach | Time Complexity | Space Complexity | Explanation |
|----------|----------------|------------------|-------------|
| **Brute Force** | O(n²) | O(1) | Nested loops compare every pair of elements. No extra space needed. |
| **Hash Set (Optimized)** | O(n) | O(n) | Single pass through array. Hash set operations are O(1) on average. Worst case space is O(n) if all elements are unique. |
| **Set Size Comparison** | O(n log n) | O(n) | Creating set from vector takes O(n log n) time due to sorting in balanced BST. Space complexity is O(n) for the set. |

## Summary

### When to Use Each Approach:

1. **Brute Force**: 
   - When memory is extremely limited
   - For very small arrays where the simplicity is preferred
   - Educational purposes to understand the basic approach

2. **Hash Set (Recommended)**:
   - Best overall performance with O(n) time complexity
   - When you need the fastest solution for large datasets
   - Most practical approach for real-world applications

3. **Set Size Comparison**:
   - When you want a concise, one-liner solution
   - When code readability is prioritized over performance
   - For medium-sized datasets where the O(n log n) complexity is acceptable

The **Hash Set approach** is generally the most efficient and practical solution for this problem, offering the best balance of time complexity and code clarity.
