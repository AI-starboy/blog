+++
author = "Bowen She"
categories = ["Leetcode"]
tags = ["Dynamic Programming"]
date = "2018-12-16"
description = "Starting from the base knapsack problem, solve a set of related ones to it."
featured = "knapsack-01.jpg"
featuredalt = "knapsack"
featuredpath = "/img/LeetCode/knapsack"
linktitle = ""
title = "Knapsack Problem Summary"
type = "post"
+++

# Classic Knapsack Problem

Given a set of items, each with a weight and a value, determine the number of each item to include in a collection so that the total weight is less than or equal to a given limit and return the largest possible value which can be collected.

It derives its name from the problem faced by someone who is constrained by a fixed-size knapsack and must fill it with the most valuable items.

The problem often arises in resource allocation where there are financial constraints.

The mathematic way to describe this problem is as below:
![](/img/LeetCode/knapsack/knapsack-02.png)

Needlees to say the brute force solution is to try all possible subsets T, we use Dynamic Programming to solve this classic problem.

Dynamic programming is a method for solving optimization problems.

**The idea**: Compute the solutions to the subsub-problems
once and store the solutions in a table, so that they
can be reused (repeatedly) later.

**Remark**: We trade space for time.


## LeetCode 416 Partition Equal Subset Sum

Given a non-empty array containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

Note:

1. Each of the array element will not exceed 100.
2. The array size will not exceed 200.

Example 1:
```
Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

Example 2:

```
Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```
