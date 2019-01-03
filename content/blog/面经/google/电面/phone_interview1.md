+++
author = "Bowen She"
categories = ["面经"]
tags = ["狗家", "电面", "Iterator"]
date = "2018-12-17"
description = "一亩三分地Google电面整理 P1"
featured = "google-01.png"
featuredalt = "Google 01"
featuredpath = "/img/面经/Google"
linktitle = ""
title = "狗家电面 Part 01"
type = "post"

+++
***Disclaimer: The following resources are from 1point3acre.com(以下资源来自一亩三分地)***

# Find next clock time

🚩 [原帖](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=466107&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3046%5D%5Bvalue%5D%3D1%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D2%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline)

***Similiar question***:
🔗 [LeetCode 31 Next Permutation](https://leetcode.com/problems/next-permutation/)

Given the clock time in string format "xx:xx" as the input, e.g. "22:12", find the closest clock time which is larger than the input time. All the inputs are valid.

### Example 1

**Input**: "22:12"

**Output**: "22:21"

### Example 2:

**Input**: "13:09"

**Output**: "19:03"

### Example 3:

**Input**: "23:59"

**Output**: "23:59"

**Explanation**:
Since there is no time larger than "23:59", we return the original time.

## Solution
**1. Brute Force**

Since all the input time strings are valid, there are only 4 numbers in each time string. We can find all permutations of the input time and find the next closest time which is valid(*hour in range [0, 24), minute in range [0, 60) at the sam time*) and larger than it.

Time complexity: O(4!)

Space complexity: O(4!)

```python
import itertools
import sys

class Solution:
    def findNextClockTime(self, time):
        hour, minute = time.split(':')
        numbers = hour + minute
        distance = sys.maxsize
        target = int(numbers)
        ans = numbers

        """
        itertools.permutation will return a list,
        each item in the list is a tuple.
        """
        for p in itertools.permutations(numbers):
            p = ''.join(p)
            # ignore the original time
            if p != numbers:
                n = int(p)
                # decide if the time is valid
                h = n / 100
                m = n % 100
                if 0 <= h < 24 and 0 <= m < 60:
                    if n > target and n - target < distance:
                        ans = p

        # return ans in a correct time string format
        return ans[:2] + ':' + ans[2:]
```

**2. Next lexicographical permutation algorithm**

This problem can be expanded to a more general question, **find the next lexicographical permutation of a string** with some restriction to make the string valid. Let's cosnider about the string without any restriction first. If the string length is ```n```, the brute force solution will be **O(n!)** which is less acceptable. In this 🔗 [post](https://www.nayuki.io/page/next-lexicographical-permutation-algorithm), it brings up a **O(n)** time in-place **O(1)** space solution For more concise explanation, check 🔗 [the Leetcode 31 Solution](https://leetcode.com/problems/next-permutation/solution/).

```python
class Solution:
    def nextPermutation(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        # find pivot
        pivot = -1
        for i in range(len(nums)-2, -1, -1):
            if nums[i] < nums[i+1]:
                pivot = i
                break

        # find the rightmost number larger than pivot      
        if pivot != -1:
            for i in range(len(nums)-1, pivot, -1):
                if nums[i] > nums[pivot]:
                    nums[i], nums[pivot] = nums[pivot], nums[i]
                    break
        # reverse
        nums[pivot+1:] = nums[pivot+1:][::-1]

        return
```

----

# K Empty Slots
🔗 [LeetCode 683](https://leetcode.com/problems/k-empty-slots/)

There is a garden with N slots. In each slot, there is a flower. The N flowers will bloom one by one in N days. In each day, there will be exactly one flower blooming and it will be in the status of blooming since then.

Given an array flowers consists of number from 1 to N. Each number in the array represents the place where the flower will open in that day.

For example, flowers[i] = x means that the unique flower that blooms at day i will be at position x, where i and x will be in the range from 1 to N.

Also given an integer k, you need to output in which day there exists two flowers in the status of blooming, and also the number of flowers between them is k and these flowers are not blooming.

If there isn't such day, output -1.

### Example 1

```
Input:
flowers: [1,3,2]
k: 1

Output: 2
Explanation: In the second day, the first and the third flower have become blooming.
```
### Example 2:

```
Input:
flowers: [1,2,3]
k: 1
Output: -1
```

### Note:
```
The given array will be in the range [1, 20000].
```

## Solution
The brute force way is for each day, we change the status of the new blooming flower, and check if there are two flowers satisfy the condition.

The naive solution looks like this:
```python
def kEmptySlots(self, flowers, k):
  def isExist(blooming, k):
      # e: number of empty slots
      e = 0
      cnt = 0

      for b in blooming:
          if b:
              # if this is the first blooming flower we find
              if cnt == 0:
                  cnt += 1
              # if two blooming flowers exists
              else:
                  if e == k:
                      return True
              e = 0
          else:
              e += 1

      return False

  N = len(flowers)
  blooming = [False] * (N + 1)
  for i, flower_idx in enumerate(flowers):
      blooming[flower_idx] = True
      if isExist(blooming, k):
          return i+1

  return -1
```

We got TLE for it, so how do we solve this problem more time efficiently? We don't need to check all the status of flowers for each day. We only need to check if any neighbor of the new blooming flower has k distance in between. Thus, it's wise to **keep the track of the already blooming flowers with a sorted list and use Binary Search to find the neighbors of added flower**.

💡 *check the useful package tools explained in the code comments*

```python
import bisect

class Solution:
    def kEmptySlots(self, flowers, k):
        """
        :type flowers: List[int]
        :type k: int
        :rtype: int
        """
        blooming = []
        # enumerate(list, 1) 1-based-index crazy!!
        for day, flower in enumerate(flowers, 1):
            # bisect will do the BS and return the leftmost possible position if duplicate elements are present
            i = bisect.bisect(blooming, flower)
            neighbors = []
            if i > 0:
                neighbors.append(blooming[i - 1])
            if i < len(blooming):
                neighbors.append(blooming[i])
            for neighbor in neighbors:
                if abs(flower - neighbor) == k + 1:
                    return day
                # insertion in list takes O(n) time cost but insertion's O(n) is a very fast o(n)
                # since it's implemented in C and only has to shift data
            blooming.insert(i, flower)
        return -1
```
We can use Binary Indexed Tree data structure to get rid of list so that the insertion could be reduced to **O(log(n))**. So the total time cost will be **O(nlog(n))**. We don't implement it here but we will talk about BIT in a seperate post later.

*Wait..*

Can we be faster? Did we utilize all the conditions in the problem description?
You can always try **inverse thinking** if someone wants to challenge you. We've seen that the garden contains **flowers** and for each day, only one flower blooms. Thus, after N days, the gardens will be full of blossom. **Why don't we start with the full blossom state, and reversely traverse the flowers list to discard flowers, and check if there exist k empty consecutive slots on some day?** The return value should be the smallest day that satisfies the condition that k empty slots present because in the normal order, we want to find the earliest day when the condition is exactly met. To quickly discard nodes in a list, we intuively think of **linkedList** since deletion in linkedlist is O(1). We use ```left``` and ```right``` to keep track of its nearest neighbors. Then the total time complexity is **O(n)**. *Crazy!!!*

> 💡 "You have to remember what's added but you can forget what's deleted. That's why deletion is more efficient in this case."

```python
class Solution:
    def kEmptySlots(self, flowers, k):
        """
        :type flowers: List[int]
        :type k: int
        :rtype: int
        """
        N = len(flowers)
        garden = [[i-1, i+1] for i in range(N)]
        garden[0][0] = None
        garden[N-1][1] = None
        ans = -1

        for i in range(N - 1, -1, -1):
            # change to 0-based index
            cur = flowers[i] - 1
            left, right = garden[cur]

            if left != None and cur - left == k + 1:
                ans = i + 1
                # print("ans: %d" % ans)
            elif right != None and right - cur == k + 1:
                ans = i + 1
            if left != None:
                garden[left][1] = right
            if right != None:
                garden[right][0] = left

        return ans
```

Yet, I just found that a less tricky and more intuitive solution with pruning technique has less runtime. **Great simulation of emply invervals for each day.**

```python
class Solution:
    """
    T: O(n*n/k/k)
    S: O(n)
    """
    def kEmptySlots(self, flowers, k):
        """
        :type flowers: List[int]
        :type k: int
        :rtype: int
        """
        n = len(flowers)
        emptys = {(1, n)}

        for d, x in enumerate(flowers):
            for i, j in emptys:
                if i <= x <= j:
                    emptys.discard((i, j))

                    if i != 1 and x - i == k:
                        return d + 1
                    elif x - i > k:
                        emptys.add((i, x - 1))

                    if j != n and j - x == k:
                        return d + 1
                    elif j - x > k:
                        emptys.add((x + 1, j))

                    break

        return -1
```

Yet another sliding window O(n) 🔗[Solution](https://leetcode.com/problems/k-empty-slots/discuss/107931/JavaC%2B%2B-Simple-O(n)-solution) for it. Crazy!!

```python
class Solution:
    def kEmptySlots(self, flowers, k):
        """
        :type flowers: List[int]
        :type k: int
        :rtype: int
        """
        # slide window solution
        # day -> position; position -> day
        # we want to find a sliding window of size k that every flower inside has not bloomed yet which means for any
        # flower inside the window[l, r], its blooming day x is later than p[i] and p[j]
        N = len(flowers)
        p = [0] * N

        for day, flower in enumerate(flowers):
            p[flower-1] = day + 1

        l = 0
        r = k + 1
        ans = N+1
        i = l + 1
        while r < N:
            if  i == r:
                # Once we find a solution, we don't stop
                # we need to find the earliest day
                ans = min(max(p[l], p[r]), ans)
                l = i
                r = l + k + 1
            else:
                if p[l] > p[i] or p[r] > p[i]:
                    l = i
                    r = l + k + 1
            i += 1

        return ans if ans != N + 1 else -1
```

It's amazing to see a problem with so many solutions. It's probably why Google use this question in the OA interview frequently.

## Follow Up
lc354 lc 630
Find largest day, the connected
leetcode找的是连续空缺花的size，现在是求连续有花 ，最晚的日期。
https://leetcode.com/problems/k-empty-slots/discuss/190918/A-good-followup-question

---
🚩 [原帖](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=465608&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3046%5D%5Bvalue%5D%3D1%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D2%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline)

# Profitable Schemes
🔗 [LeetCode 879](https://leetcode.com/problems/profitable-schemes/)

There are G people in a gang, and a list of various crimes they could commit.

The i-th crime generates a profit[i] and requires group[i] gang members to participate.

If a gang member participates in one crime, that member can't participate in another crime.

Let's call a profitable scheme any subset of these crimes that generates at least P profit, and the total number of gang members participating in that subset of crimes is at most G.

How many schemes can be chosen?  Since the answer may be very large, return it modulo 10^9 + 7.

```
Example 1:

Input: G = 5, P = 3, group = [2,2], profit = [2,3]
Output: 2
Explanation:
To make a profit of at least 3, the gang could either commit crimes 0 and 1, or just crime 1.
In total, there are 2 schemes.
Example 2:

Input: G = 10, P = 5, group = [2,3,5], profit = [6,7,8]
Output: 7
Explanation:
To make a profit of at least 5, the gang could commit any crimes, as long as they commit one.
There are 7 possible schemes: (0), (1), (2), (0,1), (0,2), (1,2), and (0,1,2).
```

Note:
```
1 <= G <= 100
0 <= P <= 100
1 <= group[i] <= 100
0 <= profit[i] <= 100
1 <= group.length = profit.length <= 100
```

# Algorithm

It's very similar to the backpack problem. If you consider group array as weights and profit array as value, the problem will be converted into finding all the schemes to get value P without exceeding the weight limit G.

Thus we can solve it by using DP.

# solution
```python
def profitableSchemes(self, G, P, group, profit):
    dp = [[0 for _ in range(G+1)] for _ in range(P+1)]

    dp[0][0] = 1

    assert(len(g) == len(p), "the length of group and profits are not equal, please check!")

    for g, p in zip(group, profit):
        for i in range(P+1)[::-1]:
            for j in range(G+1)[::-1]:
                if j >= g:
                      dp[min(i + p, P)][j] += dp[i][j - g]

    return sum(dp[P]) % (10 ** 9 + 7)

```

---
问知不知道二叉树，给一个二叉树根结点，现在知道这个二叉树不合法，原因是有一条多余的边，让删除这条边。比如，

```
     A
   /  \
  B    C
/  \ /  
D    E
```

上面的树连接情况是这样：A -> B, A -> C, B -> D, C -> E, B -> E

那么删除C -> E or B -> E 都是可以的。
注意：这里只给root结点，跟LC某道带edge的题不太一样。

Follow up:

现在换成带val的BST了，要求删掉多余那一条边之后，仍然保证是BST。

---
🚩 [原帖](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=465117&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3046%5D%5Bvalue%5D%3D1%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D2%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline)

问了以前项目的api， ml

BQ：
1. 为什么申请这个职位
2. 最喜欢的编程语言， 为什么是这个语言？


算法题目：🔗 [Leetcode 271](https://leetcode.com/problems/encode-and-decode-strings/description/)

Solution:

特殊符号， 比如‘#’作delimiter

Followup：如果不用特殊符号，怎么做？

对每个字符串这样编码： 字符串长度+‘ &nbsp; ’+原字符串（用字符串长度规定切割位置， 用空格或其它非数字字符作长度与原字符串的分割符）

---
🚩 [原帖](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=464930&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3046%5D%5Bvalue%5D%3D1%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D2%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline)

 给出两个比特流，一个短，一个长，要求在长的里搜索匹配短的。一开始有点蒙，后来在提示下想到转化成字符串，但是由长度不是八的整数倍，觉得很复杂，没有写完。估计挂了。

 KMP?

Boyce Morle?

 Rabin Carp?

 ---

 🚩 [原帖](https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=464676&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3046%5D%5Bvalue%5D%3D1%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D2%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline)

算法题目：🔗 [Leetcode 443](https://leetcode.com/problems/string-compression/description/)

Run Length Decoder

给一个encode过的int array， 其实就是compress过的， 比如 【1，1，1，2，2，3】 -》 【3，1，2，2，1，3】.  Generally, [a,a,a,b,c,c] - > [3,a,1,b,2,c]

写一个decoder， 把compress的array转换回去。

Follow up:

🔗 [Leetcode 604](https://leetcode.com/problems/design-compressed-string-iterator/description/)

decode完的array可能超出memory，所以要写写一个 Run length Iterator, 有hasNext() and next() 这两个function
