#  Binary Search
[704. Binary Search](https://leetcode.com/problems/binary-search/)

Focus on the right boundary and its update:

Ensure that all updates stay within the valid search interval, without exceeding boundaries or revisiting already searched ranges.

## Two main solutions:

1: Left-Closed, Right-Closed Interval [left, right]

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l = 0
        r = len(nums) - 1
        while l <= r:
            m = l + (r - l) // 2
            if nums[m] > target:
                r = m - 1
            elif nums[m] < target:
                l = m + 1
            else:
                return m
        return -1

```

2: Left-Closed, Right-Open Interval [left, right)

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l = 0
        r = len(nums)
        while l < r:
            m = l + (r - l) // 2
            if nums[m] > target:
                r = m
            elif nums[m] < target:
                l = m + 1
            else:
                return m
        return -1
```

## Summary of these two solutions:

| Aspect | [left, right]| [left, right)|
| ------ | ------ | ------ |
| Initial right value | n - 1 | n |
| While loop condition | l <= r | l < r |
| Right boundary update | r = m - 1 | r = m |
