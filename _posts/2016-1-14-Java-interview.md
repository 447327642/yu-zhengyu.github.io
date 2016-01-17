---
layout: post
title: 总结(IX) Java Interview --- java面试二三事
tags:
- Algorithm Summary
---

自己本来是个python的程序员，然而来了CMU后都被带成java程序员了，没办法了，现在面试也以Java为主，不过其实各个语言也是相通的。那么接下来我就收集一些JAVA面试时候会问的奇奇怪怪的问题吧。

##[基础知识篇]

1. 什么是JVM
{% highlight java %}
JVM 就是java虚拟机。JVM 会把Java code编译为byte code， 然后执行这些byte code。所有系统都能够安装JAVA虚拟机，这也体现了Java程序的多平台执行优势。
{% endhighlight %}

***

2. OOPS 的重要概念。
{% highlight java %}
OOPS就是面向对象编程，主要包括以下4个概念：
1. Abstraction 抽象性
2. Polymorphism 多态
3. Inheritance 继承
4. Encapsulation 封装
{% endhighlight %}

***

3. Overloadding VS Overriding
{% highlight java %}
* Overloadding 发生在compile阶段，Overriding 发生在runtime阶段。
* Overloading是在同一个类中写同一个函数，只是参数的类型不同。而overriding一般会在子类中出现，并且重写的时候函数名字和参数类型是一样的。
* 返回类型，overloading 是可以自由定义，但是Overriding就必须和继承的父类保持一致。
* 你可以overloading一个static 类， 但是不能overriding一个static类。
{% endhighlight %}

***

4. static VS instance
{% highlight java %}
static method是一个类级别的方法，你可以直接调用它。但是instance方法是一个对象级别的方法，你必须首先创建一个引用指向它，然后再进行调用。
{% endhighlight %}

***

5. Stringbuilder, Stringbuffer, string 的区别
{% highlight java %}
* String是immutable，不可改变的。Stringbuilder 和 Stringbuffer 都是mutable的。
* Stringbuffer 是 synchronized，Stringbuilder 不是
* Stringbuilder 比 Stringbuffer 快。
* StringBuffer线程安全，且保证同步。Stringbuilder不保证线程同步。
* String也是线程安全的，因为它不能够改变。
{% endhighlight %}

***

6. Java是值传递还是引用传递
{% highlight java %}
当写函数的过程中，如果参数是基本类，如int或者double，那么我们会发现java是值传递。但是，在Java中对象作为参数传递时，是把对象在内存中的地址拷贝了一份传给了参数。所以，总体来说，都是pass by value。
{% endhighlight %}

***

7. Searialziation 和 Desearialziation。
{% highlight java %}
Searialziation 是将对象转化为数据流，方便对象能够在网络中进行传递。Desearialziation当然就是讲流转为对象了。
{% endhighlight %}

8. final, finally, and finalize
{% highlight java %}
* Final 能够修饰变量，方法和类。修饰变量，说明该变量不能再改变。修饰method，说明该方法不能被overridden。修饰class说明该类不能够被继承。

* finally是用在异常处理的情况。代码如果被写入了finally的块中，不管该段代码是否抛出异常，到最后finally块中的代码都必须执行。这个修饰一般用在关闭网络流，数据库或者输入输出流一类的处理。

* finalize是用在垃圾回收的过程。finalize会被垃圾回收调用，会在对象被抛弃之前清理所有的活动。java提供finalize()方法，垃圾回收器准备释放内存的时候，会先调用finalize()。
{% endhighlight %}

9. java如何创建多线程
{% highlight java %}
一般在java中，创建多线程有两种方法：
1. 继承Thread类；
重写run() 函数，然后调用start()函数。

public class simpleThread extends Thread {
	public void run() {
		// 写上你的task
		System.out.println("Hello");
	}
}

public class simple {
	public static void main(String[] agrs) {
		simpleThread t = new simpleThread();
		t.start();
	}
}

2. 实现Runnable接口。
方法和上面差不多，不过是实现接口，重写的函数还是run方法。

public class simpleThread implements Runnable {
	public void run() {
		// 写上你的task
		System.out.println("Hello");
	}
}

public class simple {
	public static void main(String[] agrs) {
		Thread t = new Thread( new simpleThread() );
		t.start();
	}
}


{% endhighlight %}


##[code 篇]

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

#include <stdlib.h>
#include <unistd.h>

void main(int argc, char** argv)
{
    while(1)
    {
        malloc(1);
    }
}

{% endhighlight %}

