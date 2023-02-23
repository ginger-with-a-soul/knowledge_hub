## Stack
```cpp
#include <iostream>
#include <stack>
#include <vector>

class Solution {
   public:
    int trap(std::vector<int>& height) {
        std::stack<unsigned int> left_borders;
        unsigned int n = height.size();
        unsigned int i = 0, j = 1;
        unsigned int current_left_height = 0, current_right_height = 0;
        unsigned int current_left_border_index = 0, left_border_height = 0, height_diff = 0;
        int water = 0;

        while (j < n) {
            current_left_height = height[i];
            current_right_height = height[j];

            if (current_left_height > current_right_height) {
                left_borders.push(i);
            }

            if (current_left_height < current_right_height) {
                while (!left_borders.empty()) {
                    current_left_border_index = left_borders.top();
                    left_border_height = height[current_left_border_index];
                    if (left_border_height <= current_right_height) {
                        left_borders.pop();
                        height_diff = left_border_height - height[i];
                        water += (j - current_left_border_index - 1) * height_diff;
                        height[i] += height_diff;
                    } else {
                        height_diff = current_right_height - height[current_left_border_index + 1];
                        water += (j - current_left_border_index - 1) * height_diff;
                        height[i] += height_diff;
                        height[current_left_border_index + 1] = current_right_height;
                        break;
                    }
                }
            }
            i++;
            j++;
        }

        return water;
    }
};
```
Memory complexity is `O(n)` (staircase-like example where every number is a left border), while time complexity is `O(n)` because we do only 1 array pass.
## Two pointers
```cpp
#include <iostream>
#include <stack>
#include <vector>

class Solution {
   public:
    int trap(std::vector<int>& height) {
        unsigned int left_max = 0, right_max = 0;
        unsigned int left = 0, right = height.size() - 1;
        unsigned int water = 0;

        while (left < right) {
            if (height[left] <= height[right]) {
                if (height[left] >= left_max) {
                    left_max = height[left];
                } else {
                    water += left_max - height[left];
                }
                left++;
            } else {
                if (height[right] >= right_max) {
                    right_max = height[right];
                } else {
                    water += right_max - height[right];
                }
                right--;
            }
        }
        return water;
    }
};
```
***Main idea*** is to remember that the water capacity for the current tile depends on its left and right borders - min of those. When iterating, we should always iterate the one that is smaller from the 2 heights - as the capacity depends on the smaller and not the larger one.
***The other very important idea*** to remember is that no **CURRENT** highest left, or right side can contain ANY water as in the current traversal it is currently the highest tile - left or right from it there is no higher tile, thus the water would leak that way.

[Leet code](https://leetcode.com/problems/trapping-rain-water/solution/)
[[Interview problems#Hard]]