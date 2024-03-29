---
layout: post
title: 62.Unique Paths
tags:
- leetcode
---

### Difficulty: Medium

## Porblem

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

## Solution


这题比较简单，也是我比较后悔的一题，因为人生中第一次面试就是面试这题。这题其实就是最简单的DP做法即可。采用缓存备忘的形式避免重复计算。当然也可以用自底向上的方法，转移方程就是：当前坐标的path数 = 上坐标的path数 + 左坐标的path数。

公式：path = f[m][n-1] + f[m-1][n].


### Code[python]

{% highlight python %}

class Solution(object):
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        tt = [[-1 for i in range(0, n+1)] for j in range(0, m+1)]
        temp = self.conunt(m, n, tt)
        return temp
        
    def conunt(self, m, n, tt):
        if tt[m][n] != -1:
            return tt[m][n]
        if m == 1 or n == 1:
            return 1
        else:
            tt[m][n] = self.conunt(m - 1, n, tt) + self.conunt(m, n - 1, tt)
            return tt[m][n]
{% endhighlight %}
