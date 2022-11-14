## Morris traversal
```Python
# TODO: type it out
```
_[Morris traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/solution/)_  ([video explanation](https://www.youtube.com/watch?v=YA-nB2wjVcI&t=703s))is the most optimal algorithm for binary tree traversal for all 3 types of traversals (preorder, inorder and postorder). Time complexity of Morris traversal is `O(n)` which is the same as recursive for example, but what's better than recursive is memory complexity which is `O(1)`. Another advantage is that we do not need recursion.

##  Recursion
```Python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right


class Solution:
    def __init__(self):
        self.result: list[int] = []

    def inorderTraversal(self, root: TreeNode) -> list[int]:
        self.recursive_traversal(root)
        return self.result

    def recursive_traversal(self, root: TreeNode) -> int:

        if root:

            self.recursive_traversal(root.left)
            self.result.append(root.val)
            self.recursive_traversal(root.right)
```

[Tree traversals](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)

[[Interview problems#Easy]]