---
title: "LeetCode 2466: Count Ways To Build Good Strings"
date: 2023-05-13
draft: false
tags: ["LeetCode", "Dynamic Programming", "Problem Solving"]
categories: ["Coding", "LeetCode"]
---

# Introduction

In this post, I am going to share my solution for the LeetCode problem 2466: Count Ways to Build Good Strings. This problem is a great exercise in dynamic programming and problem-solving skills.

## Problem Description

In this problem, we are given the integers `zero`, `one`, `low`, and `high`. We start with an empty string and at each step, we can perform one of the following:

- Append the character '0' `zero` times.
- Append the character '1' `one` times.

This process can be performed any number of times. 

A good string is a string constructed by the above process having a length between `low` and `high` (inclusive).

The task is to return the number of different good strings that can be constructed satisfying these properties. Since the answer can be large, we need to return it modulo 109 + 7.

## Solution

I solved this problem by using dynamic programming. 

```python
class Solution:
    def countGoodStrings(self, low: int, high: int, zero: int, one: int) -> int:
        # dp[i] is the number of different strings of length i
        dp = [1] + [0] * (high + max(zero, one))

        for i in range(high+1):
            if dp[i] == 0:
                # this length is not achievable
                continue
            dp[i+zero] = (dp[i] + dp[i+zero]) % (10**9+7)
            dp[i+one] = (dp[i] + dp[i+one]) % (10**9+7)
        
        return sum(dp[low:high+1]) % (10**9+7)
```

In the code above, I created an array dp where dp[i] represents the number of different strings of length i. The array is initialized with 1 at index 0 to represent the one way to get an empty string and with 0 for all other indices.

I used bottom-up tabulation to gradually fill the dp array. At each position i, if dp[i] is 0, we skip it as there's no way to achieve this length. If it's not 0, we can add dp[i] to both dp[i+zero] and dp[i+one] as there are dp[i] ways to arrive at length i+zero and i+one.

Finally, I returned the sum of the counts from dp[low] to dp[high+1] and took the result modulo 10**9+7.

This approach successfully solved the problem and passed all the tests on LeetCode.