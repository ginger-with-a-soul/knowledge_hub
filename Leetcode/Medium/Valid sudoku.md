[Leet code](https://leetcode.com/problems/valid-sudoku/)

```Python
class Solution:
    def isValidSudoku(self, board: list[list[str]]) -> bool:

        storage: set = set()

        for r in range(9):
            for c in range(9):
                x = board[r][c]
                if x != '.':
                    row: str = x + ' row ' + str(r)
                    column: str = x + ' col ' + str(c)
                    both: str = x + ' row ' + \
                        str(int(r/3)) + ' col ' + str(int(c/3))
                    if row in storage or\
                       column in storage or\
                       both in storage:
                        return False
                    storage.add(row)
                    storage.add(column)
                    storage.add(both)

        return True
```
**Memory complexity**: O(numbers_as_strings + encoding)
**Time complexity**: O(size(board))


The main idea is to keep just one big set and to encode our solutions as strings that describe what element (number) we have, and in what row/col and both (used for subproblem check). For the subproblem, we encode every small square by giving it a unique row/column index by int dividing current row/column by 3.

Write out the execution on paper and it will become clear.

[[Interview problems#Medium]]