[Leet code](https://leetcode.com/problems/sort-colors/description/)

```Python
class Solution:

    def dutch_partition(self, nums: list[int]) -> None:
        red, white, blue = 0, 0, len(nums) - 1

        while white <= blue:
            if nums[white] == 0:
                nums[white], nums[red] = nums[red], nums[white]
                white += 1
                red += 1
            elif nums[white] == 1:
                white += 1
            else:
                nums[white], nums[blue] = nums[blue], nums[white]
                blue -= 1

    def sortColors(self, nums: list[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """

        self.dutch_partition(nums)
```
**Time complexity:** O(n)
Memory complexity: O(1)

[[Interview problems#Medium]]