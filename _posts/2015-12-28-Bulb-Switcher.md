---
layout: post
title: 319.Bulb Switcher
tags:
- leetcode
---
### Difficulty: Medium

## Porblem

There are n bulbs that are initially off. You first turn on all the bulbs. Then, you turn off every second bulb. On the third round, you toggle every third bulb (turning on if it's off or turning off if it's on). For the nth round, you only toggle the last bulb. Find how many bulbs are on after n rounds.

Example:

Given n = 3. 

At first, the three bulbs are [off, off, off].

After first round, the three bulbs are [on, on, on].

After second round, the three bulbs are [on, off, on].

After third round, the three bulbs are [on, off, off]. 

So you should return 1, because there is only one bulb is on.


## Solution

这个问题其实就是一个数学问题，一个一个试，找出规律后你就会发现其实最后只会剩下平方数下标的灯泡会亮，例如：1，2，4，9，16...... 所以这一题就很简单了，直接对n开方，取整就是最后的结果，简单暴力。

### Code

{% highlight java %}
public class Solution {
    public int bulbSwitch(int n) {
        return (int)Math.sqrt(n);
    }
}
{% endhighlight %}
