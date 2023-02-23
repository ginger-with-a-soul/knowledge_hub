## Two pointers
```cpp
#include <Cvector>

class Solution
{
public:
    int removeDuplicates(vector<int> &nums)
    {
        unsigned short unique_position = 0;
        unsigned short nums_len = nums.size();

        for (unsigned short i = 1; i < nums_len; ++i)
        {
            if (nums[i] != nums[unique_position])
            {
                unique_position += 1;
                nums[unique_position] = nums[i];
            }
        }

        return unique_position + 1;
    }
};
```

The first pointer start from the second element and iterates through the whole array, while the second pointer stays on the last position where we've written our unique element.

Time complexity is `O(nums_len)` because we have to iterate through the whole array.

[[Interview problems#Easy]]