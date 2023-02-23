## DFS
```Python
def DFS(self, node: TreeNode, depth: int) -> int:
	if not node:
		return depth

	return max(DFS(node.left, depth + 1), DFS(node.right, depth + 1))

DFS(node, 0)
```
DFS approach solves the problem by diving the tree into left and right subtrees and finding the max of the depth between those two. In general, when using recursion it is good to think about the solution by only thinking about the most basic case and not go into detail - if the basic case works, the more complex case probably will. Thinking about it this way, we are able to type-out the solution quickly.

Both time and memory complexities are `O(n)` where `n` is the number of nodes. Memory complexity comes from recursion that uses `n` stack frames.

## BFS
```Python
def BFS(self, node: TreeNode) -> int:
        if not node:
            return 0

        depth: int = 0

        bfs_queue: Queue = Queue()
        bfs_queue.put(node)

        while not bfs_queue.empty():

            depth += 1
            current_queue_size: int = bfs_queue.qsize()

            for _ in range(current_queue_size):
                current_node: TreeNode = bfs_queue.get()

                if current_node.left:
                    bfs_queue.put(current_node.left)
                if current_node.right:
                    bfs_queue.put(current_node.right)

        return depth
```
The key idea here is to increment `depth` only when you're done with all the nodes currently in queue. Time and memory complexities are again `O(n)`.

[Leet code](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
[[Interview problems#Easy]]