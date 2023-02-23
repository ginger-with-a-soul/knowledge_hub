[Leet code](https://leetcode.com/problems/rotate-image/)

## Mathematical
```Python
class Solution:
    def rotate(self, matrix: list[list[int]]) -> None:
        n: int = len(matrix[0])

        # fixes the main diagonal to be correct
        matrix.reverse()

        # everything that's now left is to swap upper triangular with lower triangular matrix
        i: int = 0
        j: int = 1

        while i < n - 1:
            while j < n:
                matrix[i][j] = matrix[i][j] + matrix[j][i]
                matrix[j][i] = matrix[i][j] - matrix[j][i]
                matrix[i][j] = matrix[i][j] - matrix[j][i]
                j += 1
            i += 1
            j = i + 1
```
**Time complexity:** `O(1)`
**Memory complexity:** `O(1)` because we're doing **everything** in place.

For a clockwise rotation, first we reverse the order of rows and that gives us the correct main diagonal. After that we just swap the elements on upper and lower triangular matrix with each other and indices work out just great.
For an anti-clockwise rotation, the algo remains the same with an exception in first step where now we reverse the of columns.
[[Interview problems#Medium]]