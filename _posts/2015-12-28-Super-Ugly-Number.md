---
layout: post
title:  313.Super Ugly Number
tags:
- leetcode
---
### Difficulty: Medium

## Porblem

Write a program to find the nth super ugly number.

Super ugly numbers are positive numbers whose all prime factors are in the given prime list primes of size k. For example, ```[1, 2, 4, 7, 8, 13, 14, 16, 19, 26, 28, 32]``` is the sequence of the first 12 super ugly numbers given ```primes = [2, 7, 13, 19]``` of size 4.

## Solution

这个问题的解法其实和```Ugly NumberII```差不多，我们拿当factor是```[2, 3, 5]```来当例子。如果我们把这些丑陋数字列出来的话，我们能发现其中的规律：

(1) 1×2, 2×2, 3×2, 4×2, 5×2, …

(2) 1×3, 2×3, 3×3, 4×3, 5×3, …

(3) 1×5, 2×5, 3×5, 4×5, 5×5, …

所以，其实我们只要每一次对前一个丑陋数乘上相应的factor，然后从中取出最小的一个数就好。然后相应的下标+1. ```这里注意，如果有不止一个最小的数，那么所有数的下标都应该+1，在下做这题的时候就犯了这个错误，结果总会出现重复的数字。```

### Code

{% highlight java %}
import java.util.Vector;
public class Solution {
    public int nthSuperUglyNumber(int n, int[] primes) {
        int size = primes.length;
        int[] clist = new int[size];
        int[] result = new int[n];
        result[0] = 1;
        for(int i = 1; i < n; i++){
            int minnum = Integer.MAX_VALUE;
            Vector<Integer> templist = new Vector<Integer>();
            for(int j = 0; j < size; j++) {
                int temp = primes[j] * result[clist[j]];
                templist.add(temp);
                if(temp < minnum) {
                    minnum = temp;
                }
            }
            for(int p = 0; p < templist.size(); p++)
                if(templist.get(p) == minnum)
                    clist[p]++;
            result[i] = minnum;
        }
        return result[n - 1];
    }
}
{% endhighlight %}
