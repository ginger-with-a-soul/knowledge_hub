## Two pointers
```Python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next


class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        fast_head: ListNode = head
        slow_head: ListNode = head

        for i in range(n):
            fast_head = fast_head.next

        if not fast_head:
            return head.next

        while fast_head.next != None:
            fast_head = fast_head.next
            slow_head = slow_head.next

        slow_head.next = slow_head.next.next

        return head
```
This problem is pretty easy to solve in 2 passes or by using extra memory. To solve it in 1 pass and w/out any extra memory, we have to use ***two pointers***. Since we do not know the pointer to the last element, the only thing we can do is to set both pointers to the starting element. The catch here is to figure out that if we first move `fast_pointer` by `n` positions (where n represents nth element from the back) and only then we start moving both pointers until the `fast_pointer` is ON the last element (not after it), our `slow_pointer` will end up on the element just before our nth, for example:
```
1 -> 2 -> 3 -> 4 -> 5 (and n = 2)

 1 -> 2 -> 3 -> 4 -> 5
|fp| 
|sp|

 1 -> 2 -> 3 -> 4 -> 5
|sp|	  |fp|

 1 -> 2 -> 3 -> 4 -> 5
          |sp|	    |fp|

```

[Leet code](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
[[Interview problems#Medium]]