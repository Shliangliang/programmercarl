#  Spiral Matrix II
[59. Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/)


## Solution:

- Normalize the update ranges for all four directions in a clockwise spiral:

  - Use Left-Closed, Right-Open intervals: [left, right)

  - Loop count is loop = n // 2, representing the number of full layers (rings) to traverse

  - offset starts from 1 and increases with each loop to define current layer bounds

  - If n is odd, the center element needs to be filled separately after all layers




```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        nums = [[0] * n for _ in range(n)]
        startx, starty = 0, 0
        loop, mid = n // 2, n // 2
        cnt = 1

        for offset in range(1, loop + 1):
            for j in range(starty, n - offset):             # left → right
                nums[startx][j] = cnt
                cnt += 1
            for i in range(startx, n - offset):             # top → bottom
                nums[i][n - offset] = cnt
                cnt += 1
            for j in range(n - offset, starty, -1):         # right → left
                nums[n - offset][j] = cnt
                cnt += 1
            for i in range(n - offset, startx, -1):         # bottom → top
                nums[i][starty] = cnt
                cnt += 1
            startx += 1
            starty += 1
        
        if n % 2 != 0:
            nums[mid][mid] = cnt
        
        return nums

```

# 🌀 Spiral Matrix II Summary

## 🔧 Key Components

| Component       | Purpose                                                                 |
|----------------|-------------------------------------------------------------------------|
| `nums`         | 2D matrix of size `n x n` to store result                                |
| `cnt`          | Counter starting from 1 to `n^2`, assigned to `nums[][]`                 |
| `loop`         | Number of full layers (or rings) to iterate: `loop = n // 2`            |
| `offset`       | Distance from the outer border, increases by 1 after each layer         |
| `startx`/`starty` | Starting coordinate of current layer’s top-left corner                |
| `mid`          | Middle coordinate: `mid = n // 2`, used if `n` is odd                   |

---

## 🔁 Loop Logic (One Spiral Layer per Loop)

- For each `offset` in `range(1, loop + 1)`:
  1. Move → : Fill top row from left to right
  2. Move ↓ : Fill right column from top to bottom
  3. Move ← : Fill bottom row from right to left
  4. Move ↑ : Fill left column from bottom to top
- After each loop, move the starting point inward by 1 (`startx += 1`, `starty += 1`)
- If `n` is odd, fill center cell separately: `nums[mid][mid] = cnt`

---

## 📐 Range and Update Table

| Direction        | Range Used                        | Indices Involved                             | nums[][] Update                          |
|------------------|-----------------------------------|-----------------------------------------------|------------------------------------------|
| Left → Right     | `range[starty, n - offset)`       | Row: `startx`, Col: `starty → n - offset - 1` | `nums[startx][j] = cnt`                  |
| Top → Bottom     | `range[startx, n - offset)`       | Col: `n - offset`, Row: `startx → n - offset - 1` | `nums[i][n - offset] = cnt`         |
| Right → Left     | `range[n - offset, starty, -1)`   | Row: `n - offset`, Col: `n - offset → starty + 1` | `nums[n - offset][j] = cnt`         |
| Bottom → Top     | `range[n - offset, startx, -1)`   | Col: `starty`, Row: `n - offset → startx + 1` | `nums[i][starty] = cnt`                 |
| Center (odd `n`) | —                                 | Single cell: `nums[mid][mid]`                 | `nums[mid][mid] = cnt`                  |

> 📌 Note: `range[a, b)` is left-closed, right-open: includes `a`, excludes `b`

---

## ✅ Example

For `n = 3`, layers:
- `loop = 1`
- main loop fills outer ring
- `mid = 1`, so fill `nums[1][1]` with final `cnt`
