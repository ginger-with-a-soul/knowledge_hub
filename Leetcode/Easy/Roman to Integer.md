## Hash table
```cpp
#include <unordered_map>
#include <string>

class Solution
{
public:
    int romanToInt(std::string s)
    {
        // I 1 V 5 X 10 L 50 C 100 D 500 M 1000 int total = 0;

        std::unordered_map<char, unsigned short> map = {
            {'I', 1},
            {'V', 5},
            {'X', 10},
            {'L', 50},
            {'C', 100},
            {'D', 500},
            {'M', 1000}};

        char previous_char = 'K';
        unsigned short total = 0;
        for (char c : s)
        {
            total += map[c];
            if (previous_char != 'K')
            {
                if (map[previous_char] < map[c])
                {
                    total -= 2 * map[previous_char];
                }
            }

            previous_char = c;
        }

        return total;
    }
};
```
Time complexity is `O(n)`. 
The other very cool solution is to replace every occurrence of `IV` with `IIII` and so on, but this would yield higher complexity.
We could also use **stack**, where we would check if an item currently on top is `<` than the one we're currently dealing with and if it is, we would subtract those two and remove the top element and add that subtraction result. In the end, we would just go through the stack and add up its elements.

[[Interview problems#Easy]]
