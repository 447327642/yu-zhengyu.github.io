---
layout: post
title: 总结(V) List review --- List 题目总结
tags:
- Algorithm Summary
---

List的题目可以说是我做的最不好的。并不是说不会方法，而是有时候边界条件的检查让我们可能很难在15分钟之内做到bug free。所以我这里举出一些常用的手法，到时候大家可以直接背下来，直接用。当然你也可以现场画图，但是我觉得那样时间就慢了。

***
### 1. Reverse a list in place

不用多余的空间，翻转一个链表，这个其实一开始我是觉得挺有难度的，因为每次我都记不住，所以我这次就直接记下了，免得到时候用着又来查。

####code[java]

{% highlight java %}

public ListNode reverseList(ListNode head) {
    if(head==null) return head;
    ListNode temp1= head.next;
    ListNode temp2= null;
    head.next=null;
    while(temp1!=null){
        temp2=temp1.next;
        temp1.next=head;
        head=temp1;
        temp1=temp2;
    }
    return head;
}              
{% endhighlight %}

***
### 2. find the middle of linked list

高频率用到，主要的方法就是用一个runner指针。这个技巧也会用在寻找一个链表中是否有回路。

####code[java]

{% highlight java %}

public static ListNode getMiddleOfList(ListNode l) {
	ListNode fast = l;
	ListNode slow = l;
	ListNode prev = null;
	while(fast != null && fast.next != null) {
		prev = slow;
		slow = slow.next;
		fast = fast.next.next;
	}
	
	return slow;
}

{% endhighlight %}

上面代码基本包含了奇偶的情况，有这种题就大胆往上写，绝对不出错。

***






