[Leet code](https://leetcode.com/problems/subsets/description/)
## Recursion
```Python
class Solution:
    def subsets(self, nums: list[int]) -> list[list[int]]:
        self.result: list[list[int]] = []
        self.get_subsets(nums, [])

        return self.result

    def get_subsets(self, nums: list[int], current_nums: list[int]) -> None:
        self.result.append(current_nums)

        if len(nums) == 0:
            return

        for (i, num) in enumerate(nums):
            copy_current_nums = current_nums[:]
            copy_current_nums.append(num)
            self.get_subsets(nums[i+1:], copy_current_nums)
```

**Time complexity** of subset generation is `O(2^n)` where `n` is the number of elements. Intuitively, one subset can contain a specific element `i` or it not, thus we can say that the element `i` is included or not - e.i 0 or 1. Because of that, for `n` elements, every can be 0 and 1, so the number of subsets is `2^n`. In this implementation, because we're copying `current_nums` in every iteration and there are `2^n` iterations and `current_nums`, in the worst case scenario, can be of length `n`, our time complexity is `O(n * 2^n)`. 
**Memory complexity**: each recursive call gets `nums` and `current_nums` and those in total have `n` elements, and we create a copy of `current_nums` and that, in the worst case scenario, can be of length `n`, thus our memory complexity for all recursive calls is `O(num_of_rec_calls * 2 * n)`.

There is also one very interesting solution that uses **Binary masks and operations** and can be found [here](https://leetcode.com/problems/subsets/solutions/464411/subsets/?orderBy=most_votes).

[[Interview problems#Medium]]
