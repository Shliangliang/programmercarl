#  Squares of a Sorted Array
[977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

## Two main solutions:

1: Calculated then Sort

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        for i in range(len(nums)):
            nums[i] *= nums[i]
        nums.sort()
        return nums

```

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        return sorted(x*x for x in nums)
```

2: Two Pointers from Opposite Ends
```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        res = [float('inf')] * len(nums)
        l = 0
        r = len(nums) - 1
        i = len(nums) - 1
        while l <= r:
            if nums[l] ** 2 <= nums[r] ** 2:
                res[i] = nums[r] ** 2
                r -= 1
            else:
                res[i] = nums[l] ** 2
                l += 1
            i -= 1
        return res
```
