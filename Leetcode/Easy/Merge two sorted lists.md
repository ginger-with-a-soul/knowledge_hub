## Iterative method
```cpp
struct ListNode {
	int val;
	ListNode* next;
	ListNode() : val(0), next(nullptr) {}
	ListNode(int x) : val(x), next(nullptr) {}
	ListNode(int x, ListNode* next) : val(x), next(next) {}
};

class Solution {
   public:
	ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
		if (!list1) {
			return list2;
		}

		if (!list2) {
			return list1;
		}

		ListNode* root = new ListNode();
		ListNode* tmp = new ListNode();
		bool first_pass = true;

		while (list1 != nullptr && list2 != nullptr) {
			if (list1->val <= list2->val) {
				root->next = list1;
				list1 = list1->next;
			} else {
				root->next = list2;
				list2 = list2->next;
			}
			root = root->next;
			if (first_pass) {
				first_pass = false;
				tmp = root;
			}
		}

		if (list1 == nullptr) {
			root->next = list2;
		}

		if (list2 == nullptr) {
			root->next = list1;
		}

		return tmp;
	}
};
```
Time complexity is `O(n + m)` where n is the len of the first list and m the len of the second list. Memory complexity is `O(1)` because we only use two extra objects.
We could also use the recursive approach, but that would yield worse memory complexity.

[[Interview problems#Easy]]