[Leet code](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)

```cpp
#include <algorithm>
#include <iostream>
#include <vector>

class Solution {
   public:
    int strStr(std::string haystack, std::string needle) {
        std::string combined = needle + '$' + haystack;

        unsigned needle_len = needle.length();
        std::vector<unsigned> z_array = create_z_array(combined, needle_len);

        for (auto i = 0; i < z_array.size(); ++i) {
            if (z_array[i] == needle_len) {
                return i - needle_len - 1;
            }
        }
        return -1;
    }

    std::vector<unsigned> create_z_array(std::string text, unsigned needle_len) {
        std::vector<unsigned> z_array(text.length(), 0);

        unsigned window_end = 0;

        for (auto i = 1, j = 0, k = i, matches = 0; i < text.length(); ++i, j = 0, k = i, matches = 0) {
            while (k < text.length()) {
                if (text[k++] != text[j++]) {
                    break;
                }
                matches += 1;
            }

            z_array[i] = matches;
            // optimization for the leetcode problem of a classical z algo
            if (matches == needle_len) {
                return z_array;
            }
            window_end = std::min((unsigned long)matches + i - 1, text.length() - 1);

            j = 1;
            while (i + 1 < window_end && i + 1 + z_array[j] < window_end) {
                z_array[++i] = z_array[j++];
            }
        }

        return z_array;
    }
};
```
**Time complexity:** 0(n + m) where n is the len of the needle and m the len of the haystack
**Memory complexity:** O(n + m)

This implementation of pattern matching is based on the ***Z-algorithm***, and explanation for it [can be found here](https://www.youtube.com/watch?v=CpZh4eF8QBw&t=3s). Time complexity is the best theoretically possible, as well as KMP's which has the same memory and time complexities.

The other popular algorithms for this type of problem are **sliding window technique** and **KMP**.

[[Interview problems#Medium]]]