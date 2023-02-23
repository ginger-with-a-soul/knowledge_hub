[Leet code](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)
## Recursion
```Python
class Solution:
    def letterCombinations(self, digits: str) -> list[str]:
        if not digits:
            return []

        self.result: list[str] = []
        self.number_mapping: dict = {
            '2': ['a', 'b', 'c'],
            '3': ['d', 'e', 'f'],
            '4': ['g', 'h', 'i'],
            '5': ['j', 'k', 'l'],
            '6': ['m', 'n', 'o'],
            '7': ['p', 'q', 'r', 's'],
            '8': ['t', 'u', 'v'],
            '9': ['w', 'x', 'y', 'z'],
        }

        self.get_letter_combinations(digits, '')
        return self.result

    def get_letter_combinations(self, digits: str, current_result: str) -> None:

        if len(digits) == 0:
            # append returns None but we just use return so that we stop executing current iteration
            return self.result.append(current_result)

        current_digit: str = digits[0]

        for letter in self.number_mapping[current_digit]:
            self.get_letter_combinations(digits[1:], current_result + letter)
```
**Time complexity** is `O(4^n)` where `n` is the length of input - in the worst case scenario we can get an input `9999` and because a 9 maps to 4 letters, we would have `4 * 4 * 4 * 4` or in other words 4^4 = 4^n.
Memory complexity is `O(n)` for 1 recursive call.
[[Interview problems#Medium]]