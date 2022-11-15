## Binary search
```Python
class Solution:
    def mySqrt(self, x: int) -> int:
        l: int = 0
        r: int = int(x / 2) + 1
        m: int = (l + r) / 2

        while l + 1 < r:
            m = int((l + r) / 2)
            power: int = m * m
            if power == x:
                return m
            if power > x:
                r = m
            else:
                l = m
        # fixes the problem where x is equal to the sqrt of right boundary
		return r if r * r == x else l
		
		# this would be if we did not want to round it down but to round
		# it to the closest integer	
        #return l if abs(l * l - x) < abs(r * r - x) else r
```
The main thing to note here is that the right boundary can mathematically be proven to be this exact value. The proof can be given using mathematical induction but just for the sake of intuitive understanding, consider this:
`x/2 * x/2 >= x`, some examples:
```
x = 4 => 4/2 * 4/2 >= 4
x = 5 => 5/2 * 5/2 >= 5
. . .
x = 10 => 10/2 * 10/2 >= 10
```
As we can see, this is a non-descending array so if it works for smaller inputs, intuitively speaking - it will work for every larger input.

Since we are using **Binary search**, the time complexity is `O(logr)` and the memory complexity is constant - `O(1)`.

[[Interview problems#Easy]]
