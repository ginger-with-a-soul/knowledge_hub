## Iterative
```Python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        previous_node: ListNode = None

        while head:
            current_node = head
            head = head.next
            current_node.next = previous_node
            previous_node = current_node

        return previous_node
```

## Recursive
```Python
class Solution:

    def reverseList(self, head: ListNode) -> ListNode:
        return self.recursive(head, None)

    def recursive(self, head, previous) -> ListNode:
        if not head:
            return previous
        
        current = head.next
        head.next = previous

        return self.recursive(current, head)
```

[Leet code](https://leetcode.com/problems/reverse-linked-list/)
[[Interview problems#Easy]]