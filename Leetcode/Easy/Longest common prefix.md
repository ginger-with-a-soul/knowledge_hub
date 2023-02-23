```cpp
#include <string>
#include <vector>

class Solution
{
public:
    std::string longestCommonPrefix(std::vector<std::string> &strs)
    {
        unsigned short num_strs = strs.size();
        std::string current_string = "";
        std::string previous_string = "";

        if (num_strs == 1)
        {
            return strs[0];
        }

        unsigned char longest_common_prefix_size = strs[0].size();
        for (unsigned char i = 1; i < num_strs; ++i)
        {
            current_string = strs[i];
            previous_string = strs[i - 1];

            for (unsigned char j = 0; j < longest_common_prefix_size; ++j)
            {
                if (current_string[j] != previous_string[j])
                {
                    longest_common_prefix_size = j;
                    break;
                }
            }

            // early stopping when we detect that the current string has no common prefix with the previous string
            if (longest_common_prefix_size == 0)
            {
                return "";
            }
        }

        return strs[0].substr(0, longest_common_prefix_size);
    }
};
```
It is obvious that we have to go through every word, thus we have to have at least `O(num_words)` time complexity. Next, we know that our LCP will be `<=` in size to the shortest string in our vector of strings (`minString`). Depending on the implementation, we can use this knowledge and not go to the end of each new string that is larger than our current LCP, but rather stopping when we hit the LCP. In the **worst case** scenario, our time complexity will be `O(total_num_of_chars)` and that will happen **when all our words are identical**. 

### Vertical slice
```cpp
#include <string>
#include <vector>

class Solution
{
public:
    std::string longestCommonPrefix(std::vector<std::string> &strs)
    {
        unsigned char num_strs = strs.size();

        if (num_strs == 1)
        {
            return strs[0];
        }

        std::string first_word = strs[0];
        unsigned char first_word_len = strs[0].size();

        for (unsigned short i = 0; i < first_word_len; ++i)
        {
            char current_char = first_word[i];
            for (unsigned short j = 1; j < num_strs; ++j)
            {
	            // i starts from 0 and size from 
                if (i == strs[j].size() || current_char != strs[j][i])
                {
                    return first_word.substr(0, i);
                }
            }
        }
        return first_word;
    }
};
```

A very interesting solution to this problem is not to go string by string, but rather to take the first string and then go char by char through that string and check all the other strings if they on that current char position have the same char. This is better than our last solution in the situation when we have a lot of identical strings, but only the last string is shorter. The last algorithm would go through whole identical strings and only when it hits the last string, it would adjust the LCP. This implementation would adjust LCP as soon as we get the first char that is different, thus not having to go through whole identical strings!

Another interesting take would be to use the [Prefix trees](https://leetcode.com/problems/implement-trie-prefix-tree/solution/), but to create it, we would need to go through our `total_num_of_chars` so we won't consider it here.
[[Interview problems#Easy]]