---
title: "LeetCode 1964: Find the Longest Valid Obstacle Course at Each Position"
date: 2023-05-07
draft: false
tags: ["LeetCode", "Python", "Dynamic Programming", "Binary Search", "Longest Increasing Subsequence"]
categories:
  - LeetCode
---

In this blog post, we'll discuss how to solve LeetCode problem 1964: Find the Longest Valid Obstacle Course at Each Position. The problem statement is as follows:

> You are given an array of integers `obstacles`. There is an obstacle course that you can play where the rules are:
>
> - You must do the course in the order it is given (i.e., you must go from the first obstacle to the last).
> - You can only jump from an obstacle with height less than or equal to the next obstacle.
> - Your score is the length of the longest valid subarray of obstacles you can jump through in a single run.
>
> Return an array `ans` where `ans[i]` is the length of the longest obstacle course you can jump through ending at the `i-th` obstacle.

We will solve this problem using a variation of the Longest Increasing Subsequence (LIS) algorithm, along with dynamic programming and binary search.

## Solution

The key insight is that if we list the minimum heights for each valid course length, the heights should form a non-decreasing sequence. Hence, we can use binary search on it.

Here's the Python solution based on our discussion:

```python
import bisect
from typing import List

class Solution:
    def longestObstacleCourseAtEachPosition(self, obstacles: List[int]) -> List[int]:
        minHeightsForCourseLen = [0]
        res = []
        for n in obstacles:
            idx = bisect.bisect_right(minHeightsForCourseLen, n)
            res.append(idx)

            if idx == len(minHeightsForCourseLen):
                minHeightsForCourseLen.append(n)
            else:
                minHeightsForCourseLen[idx] = min(minHeightsForCourseLen[idx], n)
        return res
```

The time complexity of this solution is `O(n * log(n))`, where n is the length of the input array obstacles.

We hope this post helps you understand how to solve LeetCode 1964: Find the Longest Valid Obstacle Course at Each Position. Happy coding!