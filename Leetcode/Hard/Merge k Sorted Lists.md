[Leet code](https://leetcode.com/problems/merge-k-sorted-lists/)
```cpp
#include <algorithm>
#include <iostream>
#include <vector>

struct ListNode {
    int val;
    ListNode* next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode* next) : val(x), next(next) {}
};

class Solution {
   public:
    void merge_two_lists(ListNode* l1, ListNode* l2) {
        if (l2 == nullptr) {
            return;
        }

        if (l1 == nullptr) {
            l1 = l2;
            return;
        }

        ListNode* dummy = new ListNode();
        ListNode* root = new ListNode();
        bool first_pass = true;

        while (l1 != nullptr && l2 != nullptr) {
            if (l1->val <= l2->val) {
                dummy->next = l1;
                l1 = l1->next;
            } else {
                dummy->next = l2;
                l2 = l2->next;
            }

            if (first_pass) {
                first_pass = false;
                root = dummy->next;
            }

            dummy = dummy->next;
        }

        if (l1 == nullptr) {
            dummy->next = l2;
        }

        if (l2 == nullptr) {
            dummy->next = l1;
        }

        l1 = root;
    }

    ListNode* mergeKLists(std::vector<ListNode*>& lists) {
        if (lists.empty()) {
            return nullptr;
        }

        ListNode* result = new ListNode();

        for (ListNode* node : lists) {
            merge_two_lists(result, node);
        }

        return result->next;
    }
};
```
**Time complexity:** O(n) where n is the total number of 
**Memory complexity:** O(1) is you don't count the return value linked list
[[Interview problems#Hard]]