---
layout: post
title:  "62.Unique Paths"
date:   2015-12-28 18:35:22 -0500
categories: code
---
### Difficulty: Medium

## Porblem

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?
## Solution


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
