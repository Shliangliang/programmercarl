#  Minimum Size Subarry Sum
[209. Minimum Size Subarry Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

Problem Summary

Given an array of positive integers nums and a positive integer s, return the minimal length of a contiguous subarray of which the sum is greater than or equal to s. If no such subarray exists, return 0.
## Two main solutions:

1: Brute force

Try every possible subarray starting from each index and stop once the sum reaches or exceeds s.

Time Complexity: O(n²)

Space Complexity: O(1)

Only need to define start point and the min_len initially
```python
class Solution:
    def minSubArrayLen(self, s: int, nums: List[int]) -> int:
        l = len(nums)
        min_len = float('inf')
        
        for i in range(l):
            cur_sum = 0
            for j in range(i, l):
                cur_sum += nums[j]
                if cur_sum >= s:
                    min_len = min(min_len, j - i + 1)
                    break
        
        return min_len if min_len != float('inf') else 0

```

2: Two Pointers (Sliding Window)

Use two pointers moving in the same direction to maintain a window whose sum is at least s. Shrink the window from the left when possible.

Time Complexity: O(n)

Space Complexity: O(1)

Recommended: Much more efficient for large inputs.

Initialize: left pointer, right pointer, min_len, cur_sum

Loop: Outer loop for the right pointer (end point), inner loop for the left pointer (start point) to move right

```python
class Solution:
    def minSubArrayLen(self, s: int, nums: List[int]) -> int:
        l = len(nums)
        left = 0
        right = 0
        min_len = float('inf')
        cur_sum = 0 
        
        while right < l:
            cur_sum += nums[right]
            
            while cur_sum >= s: 
                min_len = min(min_len, right - left + 1)
                cur_sum -= nums[left]
                left += 1
            
            right += 1
        
        return min_len if min_len != float('inf') else 0
```

## ✅ Summary Table

| Approach                     | Time Complexity | Space Complexity | Loop Structure                                           | Preserves Order | Comment                         |
|-----------------------------|------------------|-------------------|----------------------------------------------------------|------------------|----------------------------------|
| Brute Force                 | O(n²)            | O(1)              | Outer loop on `i` (start), inner loop on `j` (end)       | ✅ Yes           | Simple but slow for large input |
| Two Pointers (Sliding Window) | O(n)           | O(1)              | Outer loop on `right` (expand), inner loop on `left` (shrink) | ✅ Yes           | Efficient and recommended        |
