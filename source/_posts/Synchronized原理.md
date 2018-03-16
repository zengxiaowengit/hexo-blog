---
title: Synchronized原理
date: 2018-01-24 17:57:48
tags:
	- 并发
---

## Synchronized可以在哪些地方使用？

	Synchronized可以在：
-	普通方法同步
```java
public synchronized void method(){
	...
}
```

-	静态方法同步
```java
public synchronized static void method(){
	...
}
```
-	代码块同步
```java
public void method(){
    ...
    synchronized(this){
    	...
    }
}

```

## Synchronized 原理
	
	每个对象有一个监视器锁（monitor）。当monitor被占用时就会处于锁定状态，线程执行monitorenter指令时尝试获取monitor的所有权，过程如下：
    
    1、如果monitor的进入数为0，则该线程进入monitor，然后将进入数设置为1，该线程即为monitor的所有者。
    
    2、如果线程已经占有该monitor，只是重新进入，则进入monitor的进入数加1.
    
    3.如果其他线程已经占用了monitor，则该线程进入阻塞状态，直到monitor的进入数为0，再重新尝试获取monitor的所有权。

	当synchronized作用在方法上时，锁住的便是对象实例（this）；当作用在静态方法时锁住的便是对象对应的Class实例。
	
	因为 Class数据存在于永久带，因此静态方法锁相当于该类的一个全局锁（通过方法上的ACC_SYNCHRONIZED标识符来完成）；
	
	当synchronized作用于某一个对象实例时，锁住的便是对应的代码块（通过指令monitorenter和monitorexit来完成）。
	
## 锁的执行机制

	自旋锁。
	CAS操作。（参看CAS的博客）属于一种乐观锁。
	




