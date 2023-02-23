# Backtracking
```Python
class Solution:
    def generateParenthesis(self, n: int) -> list[str]:

        self.solution: list[str] = []
        self.get_parenthesis('', n, n)

        return self.solution

    def get_parenthesis(self, current_str: str, left: int, right: int) -> None:

        if left == 0 and right == 0:
            self.solution.append(current_str)

        if left > right:
            return

        if left > 0:
            self.get_parenthesis(current_str + '(', left - 1, right)
        if right > 0:
            self.get_parenthesis(current_str + ')', left, right - 1)
```

[Leet code](https://leetcode.com/problems/generate-parentheses/)
[[Interview problems#Medium]]
