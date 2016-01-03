---
layout: post
title: 总结(III) BackTrack Review --- 回溯法题目总结
tags:
- Algorithm Summary
---

这种题目出现的频率还是比较高的，一般如果遇到题目类似于：排列组合，有多少个子类，subset等等。基本上都是同一套路，有暴力求解的意思，就是一个一个试，但是试的策略有所不同。如果遇到是数字的排列的情况，需要在求解之前进行排序。

***
### 78. Subsets： Given a set of distinct integers, nums, return all possible subsets.

这题是典型的用回溯法的题目，我当时用的是python做的。因为这题是求子集，所以注意一下空集也算进去。下面直接上代码。

####code[python]

{% highlight python %}

class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        result = []
        nums.sort()
        self.dfs(nums, 0, [], result)
        return result
        
    def dfs(self, nums, index, temp, result):
        result.append(temp)
        for i in range(index, len(nums)):
            self.dfs(nums, i + 1, temp + [nums[i]], result)
              
{% endhighlight %}

