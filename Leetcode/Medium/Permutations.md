## Backtracking
```Python
class Solution:

    def permute(self, nums: list[int]) -> list[list[int]]:
        solutions: list[list[int]] = []

        self.get_permutation(solutions, [], nums)

        return solutions

    def get_permutation(self, solutions: list[list[int]], solution: list[int], nums: list[int]) -> list[int]:

        if len(nums) == 0:
            solutions.append(solution)

        for i in range(len(nums)):
            nums_copy = nums[:]
            solution_copy = solution[:]
            nums_copy.remove(nums[i])
            solution_copy.append(nums[i])
            self.get_permutation(solutions,
                                                           solution_copy,
                                                           nums_copy
                                                           )
```

`solutions` Holds all solutions for our input `nums`
`solutions` contains our current solution and in every function call to `get_permutation` we transfer exactly one integer from our current `nums` to `solutions` thus getting an invariant that is _in every function call to `get_permutation`_ we are one step closer to our current solution because `nums` gets smaller by 1 element and `solutions` gets bigger by that 1 element.

[Leet code](https://leetcode.com/problems/permutations/description/)
[[Interview problems#Medium]]
