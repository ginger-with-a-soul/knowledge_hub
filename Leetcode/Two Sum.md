## Double loop
```cpp
class Solution {
public:
    vector<unsigned char> twoSum(vector<int>& nums, int target) {
        unsigned short nums_len = nums.size();
        int current_target = 0;
        vector<unsigned char> return_vector = {};
        for (unsigned short i = 0u; i < nums_len; ++i) {
		    current_target = nums[i];
			for (unsigned short j = i + 1; j < nums_len; ++j) {
				if (current_target + nums[j] == target) {
					return_vector.push_back(i);
					return_vector.push_back(j);
				}
			}
        }
        return return_vector;
    }
};
```
Double loop, so the time complexity is `O(nums_len^2)`, and the memory complexity is constant `O(1)` because it does not require memory that depends on the size of the input.

## Hash table
```Python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
	    map = {}
	    for index, num in enumerate(nums):
			current_value = target - num
		    if current_value in map:
			    return [map[current_value], index]
		    map[num] = index
		return []

```
Using [hash table](https://www.baeldung.com/cs/hash-tables#:~:text=Furthermore%2C%20the%20average%20complexity%20to,regardless%20of%20the%20aimed%20operation.) we can firstly add all those elements to the table (`O(nums_len)`) and after that we can go over each element and (`O(1)` on average) and check the appropriate requirements. This requires two passes, but, we can do it even better. While we're adding the elements, we can check if we've already added its complement element before, giving us only one pass!

[[Interview problems#Easy]]