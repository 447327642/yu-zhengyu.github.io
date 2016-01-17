---
layout: post
title: 总结(IX) Java Interview --- java面试二三事
tags:
- Algorithm Summary
---

自己本来是个python的程序员，然而来了CMU后都被带成java程序员了，没办法了，现在面试也以Java为主，不过其实各个语言也是相通的。那么接下来我就收集一些JAVA面试时候会问的奇奇怪怪的问题吧。

### 用最少的code写一个函数，要求会把栈用光。
当时第一次遇到这种问题，我本身吓了一跳。不过其实这题是考你基础知识，就是栈和堆的问题。一般来收，所有的对象都是存放到堆中的，而指向对象的reference是存在栈里面的，函数调用，一开始也会放进栈。那么，用光栈最快的方法就是进行递归调用。下面上代码

####code[java]
{% highlight java %}
public class Useupstack {
	public static void main(String[] args) {
		help();
	}
	
	public static help() {
		help();
	}
}

{% endhighlight %}

***

#### follow up: 如果是用完堆里面的函数呢？？
这个也是基础知识的考察，那么，因为java里面不方便对内存直接调用，所以这里我们用C++来进行解答。
我们知道，C++可以任意对内存进行控制，那么我们就可以用C++的malloc函数来进行内存操作。

####code[C++]
{% highlight c++ %}

include <stdlib.h>
include <unistd.h>

int main(int argc, char** argv)
{
    while(1)
    {
        malloc(1024 * 4);
        fork();
    }
}

{% endhighlight %}