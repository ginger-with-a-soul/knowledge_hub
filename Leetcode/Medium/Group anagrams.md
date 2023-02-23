[Leet code](https://leetcode.com/problems/group-anagrams/)

```Python
class Solution:
    def groupAnagrams(self, strs: list[str]) -%3E list[list[str]]:
        sorted_strs: dict = {}
        result: list[list[str]] = []

        # time complexity: n * O(str_len * 1) - radix sort
        for s in strs:
            lex_str = ''.join(sorted(s))
            if lex_str in sorted_strs:
                sorted_strs[lex_str].append(s)
            else:
                sorted_strs[lex_str] = [s]

        for k in sorted_strs:
            result.append(sorted_strs[k])

        return result
```
**Time complexity:**
**Memory complexity:**

[Radix sort complexity](https://www.simplilearn.com/tutorials/data-structure-tutorial/radix-sort#:~:text=The%20Radix%20sort%20algorithm%20works,counting%20sort%20as%20a%20subroutine.)
[Counting sort and radix sort](https://medium.com/nerd-for-tech/counting-sort-radix-sort-ccd9f77a00a2)

[[Interview problems#Medium]]