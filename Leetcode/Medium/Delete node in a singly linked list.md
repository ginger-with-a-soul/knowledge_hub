## Logical problem
```Python
class Solution:
    def deleteNode(self, node):
        node.val = node.next.val
        node.next = node.next.next
```
Instead of deleting the current node (which cannot be done since we do not have a list head), we are "deleting" the node by replacing it with the next one since we know that our node is not the end node. This can be viewed as corrupting the current node.

[Leet code](https://leetcode.com/problems/delete-node-in-a-linked-list/)
[[Interview problems#Medium]]
