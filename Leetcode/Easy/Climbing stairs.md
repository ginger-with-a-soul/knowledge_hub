## Naive recursion
```Python
class Solution:
	def climbStairs(self, n: int) -> int:
		return self.recursive_step(n, 0)

def recursive_step(self, n: int, total: int) -> int:

	if total == n:
		return 1
	
	if total == n + 1:
		return 0
	
	left_step: int = self.recursive_step(n, total + 1)
	right_step: int = self.recursive_step(n, total + 2)  
	
	return left_step + right_step
```

## Memoization
```Python
class Solution:

def climbStairs(self, n: int) -> int:
	self.results: list = [-1 for _ in range(n + 2)]
	return self.recursive_step(n, 0)
	
def recursive_step(self, n: int, total: int) -> int:

	if total == n:
		return 1

  

	if total == n + 1:
		return 0

	if self.results[total + 1] != -1:
		left_step: int = self.results[total + 1]
	else:
		left_step: int = self.recursive_step(n, total + 1)
		self.results[total + 1] = left_step

	if self.results[total + 2] != -1:
		right_step: int = self.results[total + 2]
	else:
		right_step: int = self.recursive_step(n, total + 2)
		self.results[total + 2] = right_step
  
	return left_step + right_step
```

## Dynamic programming
```Python
class Solution:
	def climbStairs(self, n: int) -> int:

	one: int = 1
	two: int = 1
	
	for i in range(n - 1):
		tmp = two
		two = one + tmp
		one = tmp
		
	return two
```

Write down this problem as a tree for a smaller input (`n = 4` for example). A branch is the size of a step you took (1 or 2) from the current node, and a node represents on which staircase number you're currently on. 
You will see that a recursive algo is pretty obvious, thus you should look for redundancy in calculations for the reoccurring nodes. Once you find those, [memoization](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/) should be your next step. 
After that, you should look for a pattern on how does the number of solutions changes when you're in node `n, n-1, ..., 0`, just count the number of solutions for each node. Then you'll be able to see a pattern on how that solution number changes.

[[Interview problems#Easy]]