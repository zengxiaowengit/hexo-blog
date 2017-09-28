title: kotlin学习之高阶函数
date: 2017-07-17 15:48:53
tag: 
- kotlin

---

kotlin的高阶函数主要有：

also, let, run, map,filter,apply。

下面对他们做一个比较。

<!-- more -->

## 针对对象

    apply:无it，使用this。可以直接调用该对象的方法，处理之后返回该对象this。
    let:参数it，闭包返回
    also:
    run:无it，使用this。闭包返回
    use:参数it，闭包返回


##针对集合
kotlin有专门针对集合遍历的高阶函数。

    filter:顾名思义，是用来过滤集合中的元素的。表达式为true才添加入结果集。结果为list
    map   :遍历所有元素，闭包返回。结果为list
