```cpp
class Solution {
   public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        short int k = m + n - 1;

        n -= 1;
        m -= 1;
        while (m >= 0 && n >= 0) {
            if (nums1[m] >= nums2[n]) {
                nums1[k--] = nums1[m--];
            } else {
                nums1[k--] = nums2[n--];
            }
        }

        while (m >= 0) {
            nums1[k--] = nums1[m--];
        }

        while (n >= 0) {
            nums1[k--] = nums2[n--];
        }
    }
};
```
The main idea is to start from the back and fill the large array with the biggest number every time. Thus, that is a loop invariant, instead of finding the smallest number and filling the big array from the front.
It is very important to remember that sorting from the front is the same as reverse sorting from the back!

[[Interview problems#Easy]]