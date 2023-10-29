---
title: "Solving LeetCode Problem 2090 - K Radius Subarray Averages"
date: 2023-06-20
categories: ["LeetCode", "Python", "Algorithm"]
tags: ["prefix sum", "arrays"]
draft: true
---

In this post, we will solve problem 2090 from LeetCode titled "K Radius Subarray Averages". This problem provides an interesting use case of prefix sum arrays in handling subarray sum related problems.

## Problem Statement

The problem states that we're given a 0-indexed array `nums` of `n` integers and an integer `k`. The k-radius average for a subarray of `nums` centered at some index `i` with the radius `k` is the average of all elements in `nums` between the indices `i - k` and `i + k` (inclusive). If there are fewer than `k` elements before or after the index `i`, then the k-radius average is `-1`. We need to build and return an array `avgs` of length `n` where `avgs[i]` is the k-radius average for the subarray centered at index `i`.

## Solution

A prefix sum array can be very helpful in solving this problem. It allows us to compute the sum of any subarray in constant time, once the prefix sum array is computed. 

Here is the Python code for the solution:

```python
class Solution:
    def getAverages(self, nums: List[int], k: int) -> List[int]:
        presum = [nums[0]]
        for i in range(1, len(nums)):
            presum.append(presum[i-1] + nums[i])
        ans = [-1] * len(nums)
        for i in range(len(nums)):
            if i - k < 0 or i + k >= len(nums):
                continue
            if i-k-1 >= 0:
                ans[i] = (presum[i+k] - presum[i-k-1]) // (2 * k + 1)
            else:
                ans[i] = presum[i+k] // (2 * k + 1)
        return ans
```

In this code, we first compute the prefix sum array. Then for each valid index i, we calculate the sum of elements in the range [i-k, i+k] using the prefix sum array and compute the average. The average is computed using integer division as specified in the problem statement.

That's all for this post. Stay tuned for more problem solutions from LeetCode.

