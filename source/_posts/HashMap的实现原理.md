---
title: HashMap的实现原理
date: 2018-01-24 18:33:44
tags:
	- jdk
	
---

## 原理
	
	Java中最常用的两种结构是数组和模拟指针(引用)，
	几乎所有的数据结构都可以利用这两种来组合实现。
	HashMap也是如此。实际上HashMap是一个“链表散列”。
	如下是它的数据结构： 
![](/image/hashmap.jpeg)


## put操作

	1、根据key获取到对应的hash值。如果key为null，则调用putForNullKey，将hash值设置为0
	2、如果hash值处不存在Entry，则put，返回；
	3、如果hash值处已经存在Entry，则以链表的方式遍历，是否存在key冲突。
	   key冲突则用传入的value覆盖掉旧的value，同时把旧的value返回。
	   否则在table[hash]的位置插入Entry，把它的next指向原来在该位置的Entry。

## get操作

	1、根据key计算对应的hash值（null hash值为0）。
	2、
	
