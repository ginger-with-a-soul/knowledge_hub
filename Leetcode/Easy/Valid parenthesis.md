```cpp
#include <stack>
#include <string>

class Solution
{
public:
    bool isValid(std::string str)
    {
        std::stack<char> s;

        for (char c : str)
        {
            if (c == '(' || c == '{' || c == '[')
            {
                s.push(c);
            }
            else
            {
                char top_char = s.top();
                if (s.empty() || (top_char == '(' && c != ')') || (top_char == '{' && c != '}') || (top_char == '[' && c != ']'))
                {
                    return false;
                }
                s.pop();
            }
        }

        return s.empty();
    }
};
```

Another elegant solution would be for every _opening bracket_ to only push its _closing bracket_ to the [stack](https://www.geeksforgeeks.org/stack-data-structure/) and then when a closing bracket is our current char, we can ask if the top of the stack is that same char, if it is then we found a match, and we can take the top off. 

[[Interview problems#Easy]]