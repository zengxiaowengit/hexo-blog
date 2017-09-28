title: kotlin学习之Java对比
date: 2017-09-28 12:00:00
tag: 
- kotlin
- java
---
Kotlin 非常具有代表性，具有简明性和独特的表达能力，同时易于“并发编程”。
不过，Java8有一个巨大的进步，就是Stream API以及lambda表达式的引入，编程的思维有一定的进步，代码量一定程度减少，但是还不够。
Kotlin 的优势体现在哪里？为何 Java 程序员要转向 Kotlin？
<!-- more -->

# Hello World!
```kotlin
    fun main(args: Array<String>) {
        println("Hello Kotlin!")
    
        sayHello("World")
    }
    
    fun sayHello(name: String) {
        println("Hello $name!")
    }
```

#集合框架
- sortedBy/groupBy使用
- firstOrNull，注意如果集合为空，不能用first
- any，filter使用
- toMap
- associateBy
- map to
- associate
- 使用.filterNotNull()
    
    举个例子
```kotlin
data class User(val name: String, val age: Int)

val users = listOf(User("A", 1), User("B", 2), User("C", 3), User("D", 3))

fun main(args: Array<String>) {
    users.sortedBy { it.age }.reversed().forEach {
        println(it)
    }

    users.groupBy { it.age }.forEach {
        println(it)
    }

    println(users.any { it.age > 1 })

    users.filter { it.age > 4 }.first()
    println(users.filter { it.age > 4 }.firstOrNull())

    println(users.associateBy { it.name })

    println(users.map { it.name to it.age }.toMap())

    println(users.associate { it.name to it })

    users.map { it.name }
    println(users.filterNotNull())
}

```
# 方法扩展
    这应该可以评为最强大的功能。
```kotlin
fun Any.printIt() = println(this.toString())

fun main(args: Array<String>) {
    "abc".printIt()
    1L.printIt()
    User("ABC", 1).printIt()
}
```    

# 属性get/set 的使用
```kotlin
class Page {
    var page: Int = 1
        set(value) {
            if (value == null) {
                throw IllegalArgumentException()
            }
            if (value < 1) {
                throw IllegalArgumentException()
            }
            field = value
        }
    var size: Int = 20
        get() = field * 20

    override fun toString(): String {
        return "Page(page=$page, size=$size)"
    }

}

fun main(args: Array<String>) {
    val page = Page()
    page.page = -1
    page.size = 2
    page.printIt()
}
```

# 更方便的方法重载
```kotlin
@JvmOverloads
fun show(name: String, age: Int = 1, gender: String = "男") {
    println("name=$name, age=$age, gender=$gender")
}

fun main(args: Array<String>) {
    show("A")
    show("A", 2)
    show("A", 3, "男")
    show("A", gender = "男")
}
```
# 静态方法使用
```kotlin
class Helper {
    companion object {
        fun showSomething() {
            println("Something")
        }
    }
}

fun main(args: Array<String>) {
    Helper.showSomething()
}
```
# 一些小点
- == 相当于equals
- isNullOrBlank, string可以判断null
- ?:操作。避免Java烦人的 NullPointerException😠

```kotlin
fun main(args: Array<String>) {
    val str1 = "abc"
    val str2 = String("abc".toByteArray())

    println(str1 == str2)
    println(str1 === str2)

    var str3: String? = null
    println(str3.isNullOrBlank())

    println(str3 ?: "empty string")

    str3 = "1"
    str3?.let { print(it) }
}
```
- if/else try/cache when，比switch强大太多
```kotlin
fun main(args: Array<String>) {
    val a = 1
    val b = 2
    val c = if (a > b) a else b
    println(c)

    val d = when(a) {
        1 -> 10
        2 -> 20
        else -> 0
    }
    println(d)
}
```
- 变长参数 array to vargs
```kotlin
fun printAll(vararg str: Any) {
    str.forEach {
        println(it)
    }
}

fun main(args: Array<String>) {
    printAll("1", "2", "3")
    printAll()

    val abc = listOf("a", "b", "c")
    printAll(*abc.toTypedArray())
}
```
- ?.let{}使用，减少null判断
```kotlin
//Java
if (account.mobile != null) {
    account.mobile = "*****"
}
// kotlin一行搞定
account.mobile?.let { it = "******" }
```
- 多行字符串，写SQL爽不爽！
```kotlin
fun main(args: Array<String>) {
    val str = """
        a
        b
        c
    """

    str.printIt()
}

```
- 字符串插值
```kotlin
val a = "world"
println("hello $a")
```
- try-with-resource的kotlin版本更容易
```kotlin
//源码
@InlineOnly
public inline fun <T : Closeable?, R> T.use(block: (T) -> R): R {
    var closed = false
    try {
        return block(this)
    } catch (e: Exception) {
        closed = true
        try {
            this?.close()
        } catch (closeException: Exception) {
        }
        throw e
    } finally {
        if (!closed) {
            this?.close()
        }
    }
}

//用法
var connection:Connection
connection.use{
    //...
}
```