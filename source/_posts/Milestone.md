---
title: 博客里程碑
date: 2018-12-11 19:48:40
tags:
	- Milestone
---


## 数据结构与算法
	
###	基本十大排序算法
	
	冒泡排序、快速排序、归并排序、插入排序、基数排序、桶排序、堆排序等。

###	二叉树
-	普通二叉树
-	B树
-	B+树


###	红黑树(AVL树)

	插入平衡、删除平衡，节点的分裂、合并


### jdk中的算法与数据结构
	
-	HashMap、LinkedHashMap、ConcurrentHashMap、HashTable
-	集合类，List，LinkedList、ArrayList、CopyOnWriteArrayList
-	队列，ArrayBlockingQueue、LinkedBlockingQueue、SynchronousQueue、DelayQueue
	Deque, 双端队列,环形队列
-	链表

### concurrent包

	并发比较难理解，易出错。需要单独拿出来学习理解。
	CountDownLatch
	ForkJoinPool
	CAS操作(CompareAndSet（CompareAndSwap），ABA问题，version可以解决。)

## JVM底层原理

### java为什么能跨平台

	基于栈的数据操作。可跨平台。
	基于寄存器的数据操作。不可跨平台。优点：寄存器的操作比栈快。如：Google的arm架构和Android手机的架构系统。

### 内存模型

-	新生代
-	年轻代
-	永久代
from区，to区

### 垃圾回收策略

-	标记清除法
-	复制算法
-	分代收集

## 设计模式

-	策略模式
-	工厂模式
-	抽象工厂模式
-	门面模式
-	适配器模式
-	桥接模式
-	责任链模式
-	事件模式
-	CQRS模式(命令和查询分离)
-	观察者模式
-	代理模式




### Spring中的设计模式

-	策略模式（认证策略：cookie策略，session策略）
-	责任链模式（Spring security的过滤器链验证）
-	代理模式（AOP）
-	观察者模式（listener）


## Spring源码解析

-	IOC
-	AOP
-	Spring Session
-	Spring Security
-	Spring MVC
...


## Mybatis源码解析

	基于责任链模式来实现功能，基于插件interceptor拦截Executor、statment、ResultSet实现功能增强



## 数据库

### Innodb 和 myisam
	
	Innodb 索引和数据分离
	myisam索引和数据一起存放

### 索引原理
-	hash索引
-	B+树索引
	
	索引最大左匹配原则
	
### 索引优化
-	区分度越高的，使用越多的字段越应该放在最左边。如：时间。
-	不建议对取值范围小的列做索引。
	原因：二叉树的查找值越多查找区分度越大。最后没有区分度的值会退化为O(n)复杂度的顺序查找。
	
	

### 并发访问控制方案

-	乐观锁
	
	添加version版本控制

-	悲观锁

	select for update。不建议使用。最优情况会锁住一行，如果没有走索引，最坏情况会锁住整个表，直到事务提交。

	

### 大数据量，高可用方案

-	主从高可用，读写分离
-	分库分表

	按日期分、用户id的hash值分
-	跨库分页

-	数据库中间件
	
	sql路由、改写、聚合操作、join操作等。


## 全文检索

###	倒排索引
	正常查找都是基于词，去文档中查找。倒排索引对文档进行分词，记录词对应的文档。
	查询时先做分词，再去做文档查找和匹配。
	
###	Lucene
	
###	Elastic Search 

	Kibana、Logstash




## BI（商业智能）

-	power BI

-	ETL（数据转换、清洗工具）

-	维表、事实表分析，数据详情，钻取

-	自己实现一个BI



## 微服务架构

-	Spring Boot + dubbo
-	Spring Cloud
-	自建微服务(grpc + gateway)



## 前后端分离

### 架构
	nginx 反向代理，负载均衡
	Swagger 接口文档管理，Umock模拟数据，前后端分离开发
	OAuth2.0登录。统一认证服务器

### 后端
	Restful Api

### 前端
	vue（可参考饿了么的element-ui）


## 分布式

###	分布式数据一致性
	
	paxos

###	分布式事务

	两阶段提交

###	分布式锁

	基于redis
	基于zookeeper
	
### 分布式系统架构解耦合
	消息队列 rabbitMQ
	

## 机器学习，数据挖掘
	
### 分类
	决策树、贝叶斯
	
### 聚类
	k-means
	
### 递归神经网络
	RNN

### 时间序列预测
	LSTM
	



## 网络安全

- SQL注入
- XSS
- CSRF
- TCP 洪流攻击(syn报文重放)
- TCP 报文不确认ack, 占用连接


## 运维
	（后边拆分到spring Cloud里和自建微服务里）

- 日志系统	- ELK
- 调用链路	- zipkin
- 集群监控	- jmx监控收集到ELK中
- 负载均衡	- 客户端/服务端
- docker容器集群部署


## 其它

-	正则表达式
