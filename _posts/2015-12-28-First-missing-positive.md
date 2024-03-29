---
layout: post
title:  41.First Missing Positive
tags:
- leetcode
---
### Difficulty: Hard

## Porblem

Given an unsorted integer array, find the first missing positive integer.

For example,

Given ```[1,2,0]``` return ```3```,

and ```[3,4,-1,1]``` return ```2```.

Your algorithm should run in O(n) time and uses constant space.


## Solution

这个题目我其实不是很理解，基本原理就是桶排序。每当 ```A[i]!= i+1``` 的时候,就把```A[i] 与 A[A[i]-1] 交换```，一直到当```A[i] == A[A[i]-1]```。这里借助网上一个朋友的图来说明这个过程。```这里尤其注意一下两个数字交换的位置。我这里犯了N次错误。因为当你将nums[i]改变的时候，如果不事先保存下标，就很容易出错。所以保险的交换做法应该就像我这样做。如果你有更好的做法，可以提出```

<img src="http://yu-zhengyu.github.io/static/img/review/41_1.png" width=400>

这个题目我其实不是很理解，基本原理就是桶排序。每当 ```A[i]!= i+1``` 的时候,就把```A[i] 与 A[A[i]-1] 交换```，一直到当```A[i] == A[A[i]-1]```。这里借助网上一个朋友的图来说明这个过程。

这个题目现在终于比较理解了，其实就是把具体的数字放在指定的坐标就好。如果index为1的是不是在数组的 index 相对的位置上，如果不是，交换，然后一直交换到超出了该数组的范围或者已经交换到对了的情况。不知道这种算不算桶排序的思想。我觉得桶排序说得就太让人迷惑了。不如说，看数组中的数字和数组的下标是否相等即可。

### Code[java]
{% highlight java %}
public class Solution {
    public int firstMissingPositive(int[] nums) {
        int i = 0;
        int n = nums.length;
        while(i < n) {
            if(nums[i] > 0 && nums[i] <= n && nums[i] != i + 1 && nums[i] != nums[nums[i]- 1]) {
                int temp = nums[i];
                int temp2 = nums[nums[i]- 1];
                int tempindex = i;
                int tempindex2 = nums[i]- 1;
                nums[tempindex2] = temp;
                nums[tempindex] = temp2;
            }
            else
                i++;
        }
        
        for(int j = 0; j < n; j++) {
            if(nums[j] != j + 1)
                return j + 1;
        }
        return n + 1;
    }
}
{% endhighlight %}


