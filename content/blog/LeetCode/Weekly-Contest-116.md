+++
author = "Bowen She"
categories = ["Leetcode"]
tags = ["Stack", "Dynamic Programming", "Set", "HashMap"]
date = "2018-12-28"
description = "Solutions in weekly contest 116"
featured = "pic01.jpg"
featuredalt = "Pic 1"
featuredpath = "/img/2014/04"
linktitle = ""
title = "LeetCode Weekly Contest 116"
type = "post"

+++

# Maximum Width Ramp
🔗 [LC962](https://leetcode.com/problems/maximum-width-ramp/)

Given an array A of integers, a ramp is a tuple (i, j) for which i < j and A[i] <= A[j].  The width of such a ramp is j - i.

Find the maximum width of a ramp in A.  If one doesn't exist, return 0.


```shell
> Example 1:
Input: [6,0,8,2,1,5]
Output: 4
Explanation:
The maximum width ramp is achieved at (i, j) = (1, 5): A[1] = 0 and A[5] = 5.

> Example 2:
Input: [9,8,1,0,1,9,4,0,4,1]
Output: 7
Explanation:
The maximum width ramp is achieved at (i, j) = (2, 9): A[2] = 1 and A[9] = 1.
```

Note:
```
2 <= A.length <= 50000
0 <= A[i] <= 50000
```

# Algorithm

Naive brute force solution will be comparing all the (i, j) pairs to find the maximum width of the ramp j - i. The time complexity will be O(N^2). It's not good since the length of the input A could be 50000. O(N^2) could result in a big number O(2.5x10^9). We don't want a solution with a O(10^9) complexity which is very time consuming. So we must find a better algorithm with O(NlogN) or O(N) time complexity.

The O(NlogN) could indicate sorting of the whole array but it doesn't work in this case because indexes matter(we need the start and end index of the ramp and sorting will mix up the indexes). So we need to find a data structure which doesn't break the index order. Stack is a great option here. To reduce the total times of comparison, preprocessing the array is required. The logic behind preprocessing is that suppose we have a large number at index ***j***, then no matter which start index ***i (i < j)*** we choose, any number at ***k(i < k < j)*** smaller than ***A[j]***, its ramp width ***k - i*** will be smaller than ***j - i*** if the ramp exists(***A[i] <= A[j]***). Thus, starting from the end, we only need to traverse the array find those numbers larger than the previous largest number before the traversal hits them. The indexes of these numbers are stored in the stack. The indexes are decreasing in the stack while the corresponding values of the indexes are increasing. Only these indexes are the potential candidate for the end index of the maximum width ramp.

Then we traverse the array from the beginning to find the start index of the ramp which results in maximum width.

# solution
```python
class Solution:
    def maxWidthRamp(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        stack = []
        res = 0
        for i in range(len(A))[::-1]:
            if not stack or A[i] > A[stack[-1]]:
                stack.append(i)

        for i, a in enumerate(A):
            while stack and a >= A[stack[-1]]:
                res = max(res, stack.pop() - i)

        return res

```

# Complexity
T O(n)    
S O(n)

# Minimum Area Rectangle
🔗 [LC939](https://leetcode.com/problems/minimum-area-rectangle/)

Given a set of points in the xy-plane, determine the minimum area of a rectangle formed from these points, with sides parallel to the x and y axes.

If there isn't any rectangle, return 0.

```shell
Example 1:

Input: [[1,1],[1,3],[3,1],[3,3],[2,2]]
Output: 4
Example 2:

Input: [[1,1],[1,3],[3,1],[3,3],[4,1],[4,3]]
Output: 2
```

Note:
```
1 <= points.length <= 500
0 <= points[i][0] <= 40000
0 <= points[i][1] <= 40000
All points are distinct.
```

# Algorithm

The rectangles consist of four points represented as ***(x1, y1), (x1, y2), (x2, y1) and (x2, y2)***. There are 4 free parameters ***(x1, x2, y1, y2)*** required to define a rectangle.

The most inefficient way to solve this question is to find any four points from the input to see if they consist of a rectangle. The time complexity will be ***O(C(n, 4)) = O(n^4)***. But if we choose any two points as ***(x1, y1)*** and ***(x2, y2)***, we determine if we have ***(x2, y1)*** and ***(x1, y2)*** in the input, the time complexity will be reduced to ***O(N^2)***.

```python
def minAreaRect(points):
    # all the points are distinct
    s = {tuple(p) for p in points}
    assert(len(s) == len(points), "The inputs have duplicate points, please check")
    res = float('inf')

    for (x1, y1) in s:
        for (x2, y2) in s:
          # the rectangle has to be parallel to xy-axis
            if x1 != x2 and y1 != y2:
                if (x1, y2) in s and (x2, y1) in s:
                    res = min(res, abs((x2 - x1) * (y2 - y1)))

    return res if res < float('inf') else 0
  ```
  However, there are a lot of duplicate computation since (x1, y1), (x2, y2) will be considered once and (x2, y2), (x1, y1) will be considered again. Thus, the improved implementation will be:

```python
def minAreaRect(points):
    # all the points are distinct
    s = {tuple(p) for p in points}
    assert(len(s) == len(points), "The inputs have duplicate points, please check")
    res = float('inf')
    seen = set()

    for (x1, y1) in s:
        for (x2, y2) in seen:
            if x1 != x2 and y1 != y2:
                if (x1, y2) in seen and (x2, y1) in seen:
                    res = min(res, abs((x2 - x1) * (y2 - y1)))
        seen.add((x1, y1))

    return res if res < float('inf') else 0
```
# Complexity
T O(n^2)    
S O(n)

# Minimum Area Rectangle II
🔗 [LC963](https://leetcode.com/contest/weekly-contest-116/problems/minimum-area-rectangle-ii/)

Given a set of points in the xy-plane, determine the minimum area of **any** rectangle formed from these points, with sides **not necessarily parallel** to the x and y axes.

If there isn't any rectangle, return 0.

# Algorithm
Main idea is that in a rectangle, the two diagonals have same length and same midpoint. We go through each pair of points, and put the pair in the bucket of (midpoint, length). Loop through each bucket and compute the areas.

# Solution
```python
from collections import defaultdict
import math

def sq_norm(p1,p2):
    return (p1[0] - p2[0]) ** 2 + (p1[1] - p2[1])**2

def area(p1,p2,p3):
    return math.sqrt(sq_norm(p1,p3) * sq_norm(p2,p3))

class Solution:
    def minAreaFreeRect(self, p):
        """
        :type points: List[List[int]]
        :rtype: float
        """

        ans = 1E9

        m = defaultdict(list)
        for p1 in p:
            for p2 in p:
                if p1 < p2:
                    mid = (p1[0]+p2[0], p1[1] + p2[1], sq_norm(p1, p2))
                    sf = m[mid]
                    for p3 in sf:
                        ans = min(area(p1, p2, p3), ans)
                    m[mid].append(p1)
        return ans if ans < 1E9 else 0
```
# Complexity
T O(n^2logn)    [📄](http://www.cs.uu.nl/research/techreps/repo/CS-1989/1989-10.pdf)       
S O(n^2)

# Least Operators to Express Number

Given a single positive integer ```x```, we will write an expression of the form ```x (op1) x (op2) x (op3) x ...``` where each operator op1, op2, etc. is either addition, subtraction, multiplication, or division ```(+, -, *, or /)```.  For example, with ```x = 3```, we might write ```3 * 3 / 3 + 3 - 3``` which is a value of 3.

When writing such an expression, we adhere to the following conventions:

The division operator ```(/)``` returns rational numbers.
There are no parentheses placed anywhere.
We use the usual order of operations: multiplication and division happens before addition and subtraction.
It's not allowed to use the unary negation operator ```(-)```.  For example, ```"x - x"``` is a valid expression as it only uses subtraction, but ```"-x + x"``` is not because it uses negation.
We would like to write an expression with the least number of operators such that the expression equals the given target.  Return the least number of operators used.

```
> Example 1:

Input: x = 3, target = 19
Output: 5
Explanation: 3 * 3 + 3 * 3 + 3 / 3.  The expression contains 5 operations.

> Example 2:

Input: x = 5, target = 501
Output: 8
Explanation: 5 * 5 * 5 * 5 - 5 * 5 * 5 + 5 / 5.  The expression contains 8 operations.

> Example 3:

Input: x = 100, target = 100000000
Output: 3
Explanation: 100 * 100 * 100 * 100.  The expression contains 3 operations.
```

# Algorithm
I didn't know how to solve this problem in the first place. I checked the [solution](https://leetcode.com/problems/least-operators-to-express-number/solution/) and read several times to fully understand it.

The algorithm behind this is based on the observation that if the target is ![img](https://latex.codecogs.com/gif.latex?x^{e}), the least operations we need is ![img](https://latex.codecogs.com/gif.latex?e). There is no point to write expressions like ```x * x * x / x``` because it strictly wastes more operations.

Thus, any magnitude k of x will cost k-1 operations except for magnitude 0. To express 1, we need ```x / x``` which costs 1 operation. For any target value, we can do its x-adic expansion as ![img](https://latex.codecogs.com/gif.latex?target = a_{n}x^n+a_{n-1}x^{n-1}+...+a_1x+a_0). The recursive expression is ![img](https://latex.codecogs.com/gif.latex?target = (..((b_n*x + b_{n-1})\*x+b_{n-2})\*...)\*x +b_0\)).

The most important insight is that for ```x = 10```, ```target = 7```, ```target = 0 + 7``` or ```target = 1 * 10 - 7```. There are two ways to express a digit ```r```at magnitude ```k``` of ```x```. It could be a positive number ```r``` or ```x - (x - r)``` at its own magnitude ```k```. The ```x``` part will increase the digit at magnitude ```k+1``` by 1. It leaves the digits at magnitude ```k``` to be a negative number ```r - x```. We need to use DP to record the total number of operations of these two situations and compare with each other in the end to decide the minimum.

# Solution
```python
def leastOpsExpressTarget(self, x, y):
  # k is the current magnitude
    pos = neg = k = 0

    while y:
        y, r = divmod(y, x)
        if k:
            pos, neg = min(pos + r * k, neg + (r + 1) * k), min(pos + (x - r) * k, neg + (x - r) * k + k - 2 * k)
        else:
            pos, neg = 2 * r, 2 * (x - r)
        k += 1

    return min(pos, k + neg) - 1

```

# Complexity:
T O(![img](https://latex.codecogs.com/gif.latex?log_xy))  
S O(1)
