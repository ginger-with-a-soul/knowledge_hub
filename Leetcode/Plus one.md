```cpp
#include <vector>

class Solution {
   public:
    std::vector<int> plusOne(std::vector<int> &digits) {
        unsigned short vec_len = digits.size() - 1;

        for (int i = vec_len; i >= 0; --i) {
            if (digits[i] == 9) {
                digits[i] = 0;
            } else {
                digits[i] += 1;
                return digits;
            }
        }
        digits.push_back(0);
        digits[0] = 1;
        return digits;
    }
};
```
Every time we encounter _9_ we set it to 0 to simulate adding one. The first time we do not, we just increment the number by one and return because our job is done. If we happen to get a sequence like _99_, that is the only case when we need to expand our array by one, so we do it by pushing to back 0 and setting the front number to 1 since we cannot push 1 to the front with vectors.

[[Interview problems#Easy]]