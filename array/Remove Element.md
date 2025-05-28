#  Remove Element
[27. Remove Element](https://leetcode.com/problems/remove-element/description/)

## Three main solutions:

1: Brute Force (Element Shifting)

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i, l = 0, len(nums)
        while i < l:
            if nums[i] == val:
                # Shift all elements after index i one step to the left
                for j in range(i + 1, l):
                    nums[j - 1] = nums[j]
                l -= 1
                i -= 1
            i += 1
        return l

```

2: Two Pointers (Fast & Slow)

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        fast = slow = 0
        while fast < len(nums):
            if nums[fast] != val:
                nums[slow] = nums[fast]
                slow += 1
            fast += 1
        return slow
```

3: Two Pointers from Opposite Ends
```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        left, right = 0, len(nums) - 1
        while left <= right:
            # Skip non-val elements from the left
            while left <= right and nums[left] != val:
                left += 1
            # Skip val elements from the right
            while left <= right and nums[right] == val:
                right -= 1
            # If left < right, overwrite nums[left] with a valid element from the right
            if left < right:
                nums[left] = nums[right]
                left += 1
                right -= 1
        return left
```

## Summary of these solutions:

| Method                      | Keeps Order | Time Complexity | Space Complexity | Notes                             |
|----------------------------|-------------|------------------|-------------------|------------------------------------|
| Brute Force (Shifting)     | ✅ Yes      | O(n²)            | O(1)              | Simple but inefficient             |
| Fast & Slow Pointers       | ✅ Yes (partial)| O(n)             | O(1)              | Clean, efficient, recommended      |
| Opposite End Two Pointers  | ❌ No       | O(n)             | O(1)              | Best if order doesn’t matter       |
