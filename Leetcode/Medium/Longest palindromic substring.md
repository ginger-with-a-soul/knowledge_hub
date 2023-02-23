[Leet code](https://leetcode.com/problems/longest-palindromic-substring/)

```cpp

#include <algorithm>
#include <iostream>
#include <string>
#include <vector>

// Manacher's algorithm
// Rules:
// 1. Totally contained under current palindrome - NOT A CENTER
//      -> because it's not a center we can just insert already found palindrom length
// 2. Current palindrome expands untill the end of input - STOP PROCESSING
// 3. Palindrome expands till right edge and it's mirror is a proper prefix - IS A CENTER
//      -> it's a center because we need to continue evaluation from it because our larger palindrom only gave us
//      -> info up to that point and our proper palindrom from that center will be >= of the last good info
// 4. Palindrome expands till right edge and it's mirror expands beyond left edge - NOT A CENTER
//      -> it's not a new center because it's mirror goes beyond our current palindrom meaning that the mismatch
//      -> happened on the right or in other words, the lenght of our palindrom in that case is < than its mirror

class Solution {
   public:
    std::string longestPalindrome(std::string s) {
        std::string odd_s = "";
        odd_s.push_back('$');
        int s_len = s.length();
        for (int i = 0; i < s_len; ++i) {
            odd_s.push_back(s[i]);
            odd_s.push_back('$');
        }

        std::vector<int> palindrom_array = manacher(odd_s);

        // for (int i = 1; i < palindrom_array.size(); i += 1) {
        // std::cout << palindrom_array[i];
        // std::cout << " ";
        // }
        // std::cout << std::endl;

        int position = 0;
        int current_max = 0;
        int array_len = palindrom_array.size();
        for (int i = 0; i < array_len; ++i) {
            if (current_max < palindrom_array[i]) {
                current_max = palindrom_array[i];
                position = i;
            }
        }

        std::cout << position << " " << current_max << std::endl;

        int center = position / 2;
        int len = current_max / 2;

        return s.substr(center - len / 2, len);
    }

    std::vector<int> manacher(std::string s) {
        int string_len = s.length();
        std::vector<int> array(string_len, 1);

        int left_window_position = 0;
        int right_window_position = 0;
        int middle_window_position = 0;
        int matches = 1;

        for (int i = 1; i < string_len; ++i) {
            matches = 1;
            if (left_window_position <= i && i <= right_window_position) {
                int mirrored_center = middle_window_position - (i - middle_window_position);
                int left_mirror_position = mirrored_center - (array[mirrored_center] / 2);
                int right_mirror_position = mirrored_center + (array[mirrored_center] / 2);

                if (left_mirror_position < left_window_position) {
                    array[i] = right_window_position - middle_window_position + 1;
                } else {
                    matches = array[mirrored_center];
                    int tmp = right_mirror_position;
                    right_window_position = middle_window_position + (right_mirror_position - left_mirror_position);
                    if (right_window_position == middle_window_position) {
                        right_window_position += 1;
                    }
                    left_window_position = middle_window_position + (middle_window_position - tmp);

                    while (left_window_position - 1 >= 0 && right_window_position + 1 < string_len) {
                        if (s[left_window_position - 1] != s[right_window_position + 1]) {
                            break;
                        }
                        matches += 2;
                        left_window_position -= 1;
                        right_window_position += 1;
                    }
                }

            } else {
                for (int l = i - 1, r = i + 1; l >= 0 && r < string_len; --l, ++r) {
                    if (s[l] != s[r]) {
                        break;
                    }
                    matches += 2;
                }

                left_window_position = i - (matches / 2);
                right_window_position = i + (matches / 2);
                middle_window_position = i;
            }
            array[i] = matches;
            // std::cout << array[i] + " ";

            if (right_window_position == string_len - 1) {
                break;
            }
        }

        return array;
    }
};

int main() {
    Solution s = Solution();
    std::cout << s.longestPalindrome("ccc") << std::endl;
}
```
**Time complexity:** 0(n)
**Memory complexity:** O(2n-1)

The Manacher's algo is a non-trivial algorithm that is hard to code in 45 minutes during an interview, so it should only be explained as an idea, but the coding solution should be some of the other (worse time complexity) algorithms.

A detailed video explanation can be found [here](https://www.youtube.com/watch?v=V-sEwsca1ak).

[[Interview problems#Medium]]