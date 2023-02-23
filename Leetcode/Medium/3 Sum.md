[Leet code](https://leetcode.com/problems/3sum/)
```Python
class Solution:

    def threeSum(self, nums: list[int]) -> list[list[int]]:
        nums.sort()

        result: list[list[int]] = []

        for i, el in enumerate(nums):
            if el > 0:
                break

            if i > 0 and nums[i] == nums[i-1]:
                continue

            left_pointer: int = i + 1
            right_pointer: int = len(nums) - 1

            while left_pointer < right_pointer:
                sum: int = el + nums[left_pointer] + nums[right_pointer]
                if sum == 0:
                    left_pointer += 1
                    right_pointer -= 1
                    if nums[right_pointer] == nums[right_pointer + 1] and nums[left_pointer] == nums[left_pointer - 1] and left_pointer < right_pointer:
                        continue
                    result.append(
                        [el, nums[left_pointer-1], nums[right_pointer+1]])
                elif -1*(el + nums[left_pointer]) > nums[right_pointer]:
                    left_pointer += 1
                else:
                    right_pointer -= 1

        return result
```
**Time complexity:** 0(n\*n)
**Memory complexity:** 0(1)

[[Interview problems#Medium]]