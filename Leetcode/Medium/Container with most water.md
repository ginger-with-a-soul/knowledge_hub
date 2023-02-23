## Two pointers
```cpp
#include <algorithm>
#include <vector>

class Solution {
   public:
    int maxArea(std::vector<int>& height) {
        unsigned int num_of_items = height.size();
        unsigned long max_area = 0;
        unsigned int current_height = 0;
        unsigned int height_left = 0;
        unsigned int height_right = 0;

        for (unsigned int i = 0, j = num_of_items - 1; i < j;) {
            height_left = height[i];
            height_right = height[j];
            current_height = std::min(height_left, height_right);
            max_area = std::max(max_area, current_height * (j - i));

            while (current_height >= height[i] && i < j) i++;
            while (current_height >= height[j] && i < j) j--;
        }

        return max_area;
    }
};
```
The main idea to be taken from here is to recognize the **exact** condition when we can get an area bigger than the current one: we know that in every iteration, our base is getting smaller, thus, to get a bigger area our side **has to** get larger than the current one. Because of that, we can skip all the elements where the height is smaller or equal to the height of the current side.
The other way to do this - a bit slower, is to iterate one-by-one and calculate the area every time.
Time complexity for both of these is still `O(num_of_elements)` but in the first approach we skip unnecessary area computation. Memory complexity is constant.

[Leet code](https://leetcode.com/problems/container-with-most-water/)
[[Interview problems#Medium]]