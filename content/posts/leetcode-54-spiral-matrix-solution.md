---
title: "LeetCode 54: Spiral Matrix Solution"
date: 2023-05-09
tags: ["coding", "python", "algorithm", "leetcode"]
categories: ["coding", "solution", "programming"]
---

## Problem: LeetCode 54: Spiral Matrix

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

## Approach

The idea is to use a 'seen' set to keep track of the elements we've already visited. We use a `while true` loop with two pointers to iterate through the matrix, checking boundaries and turning around when needed. We also check if the next element is in the 'seen' set. The loop terminates when the size of the 'seen' set equals the total number of elements in the matrix, which means we have visited all elements.

## Solution

Here is the Python solution:

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        m = len(matrix)
        n = len(matrix[0])
        s = m * n
        seen = set()

        dir = [(0,1),(1,0),(0,-1),(-1,0)]

        i = j = 0
        d = 0
        res = []
        while True:
            res.append(matrix[i][j])
            seen.add((i,j))
            ni = i + dir[d][0]
            nj = j + dir[d][1]

            if ni < 0 or ni >= m or nj < 0 or nj >= n or (ni,nj) in seen:
                d = (d+1) % len(dir)
                i += dir[d][0]
                j += dir[d][1]
            else:
                i = ni
                j = nj
            if len(res) == s:
                return res 
```


The solution starts by initializing the size of the matrix and an empty 'seen' set. It then defines the directions of movement in a clockwise spiral order. The while loop continues until we've visited all elements in the matrix. Within the loop, it adds the current element to the result list and the 'seen' set, then it calculates the next position. If the next position is out of bounds or already seen, it changes direction and moves one step; otherwise, it moves to the next position.

This solution is simple and efficient, with a time complexity of `O(mn)`, where m and n are the dimensions of the matrix. It's a good example of how we can use a 'seen' set to avoid revisiting elements in a matrix traversal problem.
