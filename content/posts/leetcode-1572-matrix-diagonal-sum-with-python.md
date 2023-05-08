---
title: "LeetCode 1572: Matrix Diagonal Sum with Python"
date: 2023-05-08
categories:
  - programming
  - algorithms
tags:
  - python
  - leetcode
  - matrix
---

## Introduction

In this blog post, we'll discuss a problem from LeetCode called Matrix Diagonal Sum (Problem 1572). We'll explain the problem statement, requirements, and share a Python solution with comments for clarity.

## Problem Description

Given a square matrix `mat`, the task is to return the sum of the matrix diagonals.

- The primary diagonal is from the top-left to the bottom-right.
- The secondary diagonal is from the top-right to the bottom-left.

**Input**: A square matrix `mat` of integers (size n x n, where 1 <= n <= 100)

**Output**: An integer, representing the sum of the matrix diagonals.

**Example**:

```
Input: mat = [
[1, 2, 3],
[4, 5, 6],
[7, 8, 9]
]

Output: 25
```

## Solution

Our approach is to iterate through the matrix and sum the values on the two diagonals. Here's the Python code for our solution:

```python
class Solution:
    def diagonalSum(self, mat: List[List[int]]) -> int:
        sum = 0
        for i in range(len(mat)):
            sum += mat[i][i]
            sum += mat[i][len(mat)-i-1]

        if len(mat) % 2 == 1:
            sum -= mat[len(mat)//2][len(mat)//2]
        return sum
```

This solution has a time complexity of `O(n)`, where n is the number of rows (or columns) in the matrix.