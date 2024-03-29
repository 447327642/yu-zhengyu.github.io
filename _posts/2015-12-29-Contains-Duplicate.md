---
layout: post
title: 217. Contains Duplicate
tags:
- leetcode
---
### Difficulty: Easy

## Porblem

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.


## Solution

这个问题非常简单，我的做法就是直接把数组放到set当中就好，然后看set的长度和原数组的长度是否相等，如果相等，就说明没有重复的元素，不相等说明有重复元素。

### Code[python]

{% highlight python %}
class Solution:
    # @param {integer[]} nums
    # @return {boolean}
    def containsDuplicate(self, nums):
        b = set(nums)
        if len(b) < len(nums):
            return True
        return False
{% endhighlight %}

当然，如果对空间上有所要求，比如说，不能用额外的空间的话。那我们首先要对数组进行排序。那么时间上的话最快也就是O(nlogn)，然后遍历一遍，看看nums[i] == nums[i-1]是否成立。当然，有时候还有一些题目问在一个链表上，是否有重复元素。那么，我的做法就是用两个指针去做，时间上是O(n2).
