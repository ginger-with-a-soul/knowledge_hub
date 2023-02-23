## Mathematical
```Python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next


class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        carry_over: int = 0
        node = head = ListNode(0)

        while l1 or l2 or carry_over:
            result: int = carry_over
            if l1:
                result += l1.val
                l1 = l1.next
            if l2:
                result += l2.val
                l2 = l2.next
            carry_over, result = divmod(result, 10)
            node.next = ListNode(val=result)
            node = node.next

        return head.next
```

[[Interview problems#Medium]