---
layout: post
title:  "41.First Missing Positive"
date:   2015-12-28 17:35:22 -0500
categories: code
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

![Image sanpshot]({{ site.url }}/assets/41_1.png)

这个题目我其实不是很理解，基本原理就是桶排序。每当 ```A[i]!= i+1``` 的时候,就把```A[i] 与 A[A[i]-1] 交换```，一直到当```A[i] == A[A[i]-1]```。这里借助网上一个朋友的图来说明这个过程。


基本上这个思路还可以去做这样的题目： 从1~n中找出那个重复的数字，有就返回该数字，没有就返回-1，时间是O(n), 空间是O(1).

基本上这个思路还可以去做这样的题目： 从1~n中找出那个重复的数字，有就返回该数字，没有就返回-1，时间是O(n), 空间是O(1).

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


