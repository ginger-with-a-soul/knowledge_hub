[Leet code](https://leetcode.com/problems/median-of-two-sorted-arrays/)
```cpp
#include <algorithm>
#include <climits>
#include <iostream>
#include <vector>

class Solution {
   public:
    double findMedianSortedArrays(std::vector<int>& nums1, std::vector<int>& nums2) {
        int len_X = nums1.size();
        int len_Y = nums2.size();

        if (len_X > len_Y) {
            return findMedianSortedArrays(nums2, nums1);
        }

        int left = 0;
        int right = len_X;

        while (left <= right) {
            // we want to have half of the total elemets in these partitions combined
            int partition_point_X = (left + right) / 2;
            // pp_X + pp_Y = (len_X + len_Y + 1) / 2
            int partition_point_Y = (len_X + len_Y + 1) / 2 - partition_point_X;

			// if on the left side of partition_point_X there is 0 elements, we take that the element value for that non-existing element is -INF
            int left_X = partition_point_X == 0 ? INT_MIN : nums1[partition_point_X - 1];
            int right_X = partition_point_X == len_X ? INT_MAX : nums1[partition_point_X];

            int left_Y = partition_point_Y == 0 ? INT_MIN : nums2[partition_point_Y - 1];
            int right_Y = partition_point_Y == len_Y ? INT_MAX : nums2[partition_point_Y];


			// we compare the largest el. in the left partition of X with the smalles el. in the right partition of Y and vice versa
            if (left_X <= right_Y && left_Y <= right_X) {
                // cuts found
                if ((len_X + len_Y) % 2) {
                    return (double)std::max(left_X, left_Y);
                } else {
                    return (std::max(left_X, left_Y) + std::min(right_X, right_Y)) / 2.0;
                }
            } else if (left_X > right_Y) {
                right = partition_point_X - 1;
            } else {
                left = partition_point_X + 1;
            }
        }
        std::__throw_invalid_argument("Input arrays invalid");
    }
};

int main() {
    Solution s = Solution();
    std::vector<int> nums1 = {1, 2, 3};
    std::vector<int> nums2 = {2, 3, 4};
    try {
        std::cout << s.findMedianSortedArrays(nums1, nums2) << std::endl;
    } catch (std::invalid_argument& e) {
        std::cout << e.what() << std::endl;
    }
}

```
**Time complexity:** O(min(len_X, len_Y)) since we use [[binary search]] on smaller array to find a perfect _cut_ position.
**Memory complexity:** O(1).

You can find a great video explanation [here](https://www.youtube.com/watch?v=LPFhl65R7ww).

[[Interview problems#Hard]]