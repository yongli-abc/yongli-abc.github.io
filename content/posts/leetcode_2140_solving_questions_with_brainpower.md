---
title: "LeetCode 2140: Solving Questions With Brainpower"
date: 2023-05-12
draft: false
tags: ["Algorithms", "Dynamic Programming", "LeetCode"]
categories: ["Programming", "Python", "LeetCode"]
---

In this post, we will solve LeetCode problem 2140, titled ["Solving Questions With Brainpower"](https://leetcode.com/problems/solving-questions-with-brainpower/description/). This problem is a great example of applying dynamic programming to a practical scenario.

## Problem Description

Given a 0-indexed 2D integer array questions where questions[i] = [points_i, brainpower_i], the array describes the questions of an exam. You have to process the questions in order and make a decision whether to solve or skip each question. Solving question i will earn you points_i points but you will be unable to solve each of the next brainpower_i questions. If you skip question i, you get to make the decision on the next question.

## Python Solution

Here's a Python solution using dynamic programming:

```python
class Solution:
    def mostPoints(self, questions: List[List[int]]) -> int:
        n = len(questions)
        dp = [0] * n + [0]

        for i in range(n-1, -1, -1):
            p_no_take = dp[i+1]
            p_take = questions[i][0]
            if i + questions[i][1] + 1 < n:
                p_take += dp[i+questions[i][1]+1]
            dp[i] = max(p_no_take, p_take)
        return dp[0]
```

In the code above, we first initialize a DP array, dp, with an extra 0 at the end. Then, we iterate backwards through the list of questions. For each question, we calculate the maximum points we could get if we don't take this question (p_no_take), and the maximum points we could get if we do take this question (p_take). We update dp[i] to be the maximum of these two values.

Finally, we return dp[0], which represents the maximum points we can earn for the entire exam.