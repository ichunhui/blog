---
title: 一篇文章让你彻底掌握 Scala
categories:
  - 编程
tags:
  - 编程
  - scala
abbrlink: efbdcb14
date: 2021-04-14 15:27:00
---

# Scala 入门

> Scala 是大数据领域的热门语言，如：Akka、Kafka，所以，想要学习大数据顶级开源项目的源码，有必要具备一定的 Scala 基础。

<!-- TOC depthFrom:2 depthTo:3 -->

- [1. 基本语法](#1-基本语法)
- [2. 注释](#2-注释)
- [3. 变量](#3-变量)
  - [3.1. 变量类型声明](#31-变量类型声明)
- [4. 数据类型](#4-数据类型)
- [5. 数组](#5-数组)
- [6. 逻辑控制语句](#6-逻辑控制语句)
  - [6.1. 条件语句](#61-条件语句)
  - [6.2. 循环语句](#62-循环语句)
  - [6.3. 模式匹配](#63-模式匹配)
- [7. 运算符](#7-运算符)
- [8. 方法与函数](#8-方法与函数)
- [9. 闭包](#9-闭包)
- [10. 集合](#10-集合)
  - [10.1. 迭代器](#101-迭代器)
- [11. 类和对象](#11-类和对象)
- [12. Trait](#12-trait)
- [13. 异常](#13-异常)
- [14. 输入输出](#14-输入输出)
  - [14.1. 读取用户输入](#141-读取用户输入)
  - [14.2. 读取文件内容](#142-读取文件内容)
- [15. 包](#15-包)
  - [15.1. 定义包](#151-定义包)
  - [15.2. 引用](#152-引用)
  - [15.3. 访问修饰符](#153-访问修饰符)
- [16. 参考资料](#16-参考资料)

<!-- /TOC -->

## 1. 基本语法

Scala 基本语法需要注意以下几点：

- **区分大小写** - Scala 是大小写敏感的。
- **类名** - 对于所有的类名的第一个字母要大写。示例：`class MyFirstScalaClass`
- **方法名称** - 所有的方法名称的第一个字母用小写。示例：`def myMethodName()`
- **程序文件名** - 程序文件的名称应该与对象名称完全匹配(新版本不需要了，但建议保留这种习惯)。示例: 假设"HelloWorld"是对象的名称。那么该文件应保存为'HelloWorld.scala"
- **`def main(args: Array[String])`** - Scala 程序从 `main()` 方法开始处理，这是每一个 Scala 程序的强制程序入口部分。
- 一行中只有空格或者带有注释，Scala 会认为其是空行，会忽略它。标记可以被空格或者注释来分割。
- Scala 是面向行的语言，语句可以用分号（;）结束或换行符。

## 2. 注释

Scala 类似 Java 支持单行和多行注释。

【示例】单行和多行注释

```scala
object HelloWorld {
  /*
   * 这是我的第一个 Scala 程序
   * 以下程序将输出'Hello World!'
   */
  def main(args: Array[String]) {
    println("Hello, world!") // 输出 Hello World
  }
}
```

## 3. 变量

在 Scala 中，使用关键词 `var` 声明变量，使用关键词 `val` 声明常量。

【示例】声明变量

```scala
var myVar : String = "Foo"
var myVar : String = "Too"
```

【示例】声明常量

```scala
val myVal : String = "Foo"
```

### 3.1. 变量类型声明

变量的类型在变量名之后等号之前声明。定义变量的类型的语法格式如下：

```scala
// 声明变量类型
var VariableName : DataType [=  Initial Value]
// 声明常量类型
val VariableName : DataType [=  Initial Value]
```

在 Scala 中声明变量和常量不一定要指明数据类型，在没有指明数据类型的情况下，其数据类型是通过变量或常量的初始值推断出来的。所以，如果在没有指明数据类型的情况下声明变量或常量必须要给出其初始值，否则将会报错。

```scala
var myVar = 10;
val myVal = "Hello, Scala!";
val xmax, ymax = 100
```

## 4. 数据类型

Scala 与 Java 有着相同的数据类型：

| 数据类型 | 描述                                                                                                |
| :------- | :-------------------------------------------------------------------------------------------------- |
| Byte     | 8 位有符号补码整数。数值区间为 -128 到 127                                                          |
| Short    | 16 位有符号补码整数。数值区间为 -32768 到 32767                                                     |
| Int      | 32 位有符号补码整数。数值区间为 -2147483648 到 2147483647                                           |
| Long     | 64 位有符号补码整数。数值区间为 -9223372036854775808 到 9223372036854775807                         |
| Float    | 32 位, IEEE 754 标准的单精度浮点数                                                                  |
| Double   | 64 位 IEEE 754 标准的双精度浮点数                                                                   |
| Char     | 16 位无符号 Unicode 字符, 区间值为 U+0000 到 U+FFFF                                                 |
| String   | 字符序列                                                                                            |
| Boolean  | true 或 false                                                                                       |
| Unit     | 表示无值，和其他语言中 void 等同。用作不返回任何结果的方法的结果类型。Unit 只有一个实例值，写成()。 |
| Null     | null 或空引用                                                                                       |
| Nothing  | Nothing 类型在 Scala 的类层级的最底端；它是任何其他类型的子类型。                                   |
| Any      | Any 是所有其他类的超类                                                                              |
| AnyRef   | AnyRef 类是 Scala 里所有引用类(reference class)的基类                                               |

上表中列出的数据类型都是**对象**，也就是说 scala 没有 java 中的原生类型。在 scala 是可以对数字等基础类型调用方法的。

## 5. 数组

Scala 数组声明的语法格式：

```scala
// 方式一
var z:Array[String] = new Array[String](3)
// 方式二
var z = new Array[String](3)
```

## 6. 逻辑控制语句

### 6.1. 条件语句

【示例】条件语句

```scala
object IfDemo {
  def main(args: Array[String]) {
    var x = 30;

    if (x == 10) {
      println("X 的值为 10");
    } else if (x == 20) {
      println("X 的值为 20");
    } else if (x == 30) {
      println("X 的值为 30");
    } else {
      println("无法判断 X 的值");
    }
  }
}
```

### 6.2. 循环语句

和 Java 一样，Scala 支持 `while`、`do ... while`、`for` 三种循环语句。

```scala
object WhileDemo {
  def main(args: Array[String]) {
    // 局部变量
    var a = 10;

    // while 循环执行
    while (a < 20) {
      println("Value of a: " + a);
      a = a + 1;
    }
  }
}
```

**scala 不支持 `break` 和 `continue`**。但是，可以通过 `Breaks` 对象来进行循环控制。

```scala
import scala.util.control._

object BreakDemo {
  def main(args: Array[String]) {
    var a = 0;
    var b = 0;
    val numList1 = List(1, 2, 3, 4, 5);
    val numList2 = List(11, 12, 13);

    val outer = new Breaks;
    val inner = new Breaks;

    outer.breakable {
      for (a <- numList1) {
        println("Value of a: " + a);
        inner.breakable {
          for (b <- numList2) {
            println("Value of b: " + b);
            if (b == 12) {
              inner.break;
            }
          }
        } // 内嵌循环中断
      }
    } // 外部循环中断
  }
}
```

### 6.3. 模式匹配

scala 的 `match` 对应 Java 里的 `switch`，但是写在选择器表达式之后。即： **选择器 match {备选项}。**

```scala
/**
  * @author peng.zhang
  */
object MatchDemo {
  def main(args: Array[String]) {
    println(matchTest("two"))
    println(matchTest("test"))
    println(matchTest(1))
    println(matchTest(6))

  }

  def matchTest(x: Any): Any = x match {
    case 1      => "one"
    case "two"  => 2
    case y: Int => "scala.Int"
    case _      => "many"
  }
}
```

## 7. 运算符

Scala 含有丰富的内置运算符，包括以下几种类型：

- 算术运算符：`+`、`-`、`*`、`/`、`%`
- 关系运算符：`==`、`!=`、`>`、`<`、`>=`、`<=`
- 逻辑运算符：`&&`、`||`、`!`
- 位运算符：`~`、`&`、`|`、`^`、`<<`、`>>`、`>>>` （无符号右移）
- 赋值运算符：`=`

## 8. 方法与函数

Scala 有方法与函数，二者在语义上的区别很小。

Scala 中的方法跟 Java 的类似，方法是组成类的一部分。

Scala 中的函数则是一个完整的对象，Scala 中的函数其实就是继承了 Trait 的类的对象。

Scala 中使用 `val` 语句可以定义函数，`def` 语句定义方法。

【示例】

```scala
class Test {
  def m(x: Int) = x + 3
  val f = (x: Int) => x + 3
}
```

## 9. 闭包

闭包是一个函数，返回值依赖于声明在函数外部的一个或多个变量。

闭包通常来讲可以简单的认为是可以访问一个函数里面局部变量的另外一个函数。

如下面这段匿名的函数：

```scala
val multiplier = (i:Int) => i * 10
```

函数体内有一个变量 i，它作为函数的一个参数。如下面的另一段代码：

```scala
val multiplier = (i:Int) => i * factor
```

在 multiplier 中有两个变量：i 和 factor。其中的一个 i 是函数的形式参数，在 multiplier 函数被调用时，i 被赋予一个新的值。然而，factor 不是形式参数，而是自由变量，考虑下面代码：

```scala
var factor = 3
val multiplier = (i:Int) => i * factor
```

这里我们引入一个自由变量 factor，这个变量定义在函数外面。

这样定义的函数变量 multiplier 成为一个"闭包"，因为它引用到函数外面定义的变量，定义这个函数的过程是将这个自由变量捕获而构成一个封闭的函数。

```scala
object ClosureDemo {
  def main(args: Array[String]) {
    println("muliplier(1) value = " + multiplier(1))
    println("muliplier(2) value = " + multiplier(2))
  }

  var factor = 3
  val multiplier = (i: Int) => i * factor
}
```

## 10. 集合

Scala 集合支持 List、Set、Map、元祖、Option。

```scala
// 定义整型 List
val x = List(1,2,3,4)

// 定义 Set
val x = Set(1,3,5,7)

// 定义 Map
val x = Map("one" -> 1, "two" -> 2, "three" -> 3)

// 创建两个不同类型元素的元组
val x = (10, "Runoob")

// 定义 Option
val x:Option[Int] = Some(5)
```

### 10.1. 迭代器

迭代器 it 的两个基本操作是 **next** 和 **hasNext**。

调用 **it.next()** 会返回迭代器的下一个元素，并且更新迭代器的状态。

调用 **it.hasNext()** 用于检测集合中是否还有元素。

```scala
object Test {
   def main(args: Array[String]) {
      val it = Iterator("Baidu", "Google", "Runoob", "Taobao")

      while (it.hasNext){
         println(it.next())
      }
   }
}
```

## 11. 类和对象

类是对象的抽象，而对象是类的具体实例。类是抽象的，不占用内存，而对象是具体的，占用存储空间。类是用于创建对象的蓝图，它是一个定义包括在特定类型的对象中的方法和变量的软件模板。

```scala
class Point(val xc: Int, val yc: Int) {
  var x: Int = xc
  var y: Int = yc

  def move(dx: Int, dy: Int) {
    x = x + dx
    y = y + dy
    println("x 的坐标点 : " + x);
    println("y 的坐标点 : " + y);
  }
}

class Location(override val xc: Int, override val yc: Int, val zc: Int)
    extends Point(xc, yc) {
  var z: Int = zc

  def move(dx: Int, dy: Int, dz: Int) {
    x = x + dx
    y = y + dy
    z = z + dz
    println("x 的坐标点 : " + x);
    println("y 的坐标点 : " + y);
    println("z 的坐标点 : " + z);
  }
}

object Test {
  def main(args: Array[String]) {
    val loc = new Location(10, 20, 15);

    // 移到一个新的位置
    loc.move(10, 10, 5);
  }
}
```

## 12. Trait

Scala Trait(特征) 相当于 Java 的接口，实际上它比接口还功能强大。

与接口不同的是，它还可以定义属性和方法的实现。

一般情况下 Scala 的类只能够继承单一父类，但是如果是 Trait(特征) 的话就可以继承多个，从结果来看就是实现了多重继承。

```scala
trait Equal {
  def isEqual(x: Any): Boolean

  def isNotEqual(x: Any): Boolean = !isEqual(x)
}

class Point(xc: Int, yc: Int) extends Equal {
  var x: Int = xc
  var y: Int = yc

  def isEqual(obj: Any) =
    obj.isInstanceOf[Point] &&
      obj.asInstanceOf[Point].x == x
}

object Test {
  def main(args: Array[String]) {
    val p1 = new Point(2, 3)
    val p2 = new Point(2, 4)
    val p3 = new Point(3, 3)

    println(p1.isNotEqual(p2))
    println(p1.isNotEqual(p3))
    println(p1.isNotEqual(2))
  }
}
```

## 13. 异常

Scala 抛出异常的方法和 Java 一样，使用 `throw` 关键词。

【示例】抛出异常

```scala
throw new IllegalArgumentException
```

【示例】捕获异常

```scala
import java.io.{FileNotFoundException, FileReader, IOException}

object Test {
  def main(args: Array[String]) {
    try {
      val f = new FileReader("input.txt")
    } catch {
      case ex: FileNotFoundException => {
        println("Missing file exception")
      }
      case ex: IOException => {
        println("IO Exception")
      }
    } finally {
      println("Exiting finally...")
    }
  }
}
```

## 14. 输入输出

### 14.1. 读取用户输入

使用 `scala.io.StdIn.readLine()` 方法读取用户输入

```scala
object StdInDemo {
  def main(args: Array[String]) {
    print("请输入内容: ")
    val line = StdIn.readLine()

    println("你输入的是: " + line)
  }
}
```

### 14.2. 读取文件内容

```scala
object SourceDemo {
  def main(args: Array[String]) {
    println("文件内容为:")

    Source.fromFile("test.txt").foreach {
      print
    }
  }
}
```

## 15. 包

### 15.1. 定义包

Scala 使用 `package` 关键字定义包，在 Scala 将代码定义到某个包中有两种方式：

第一种方法和 Java 一样，在文件的头定义包名，这种方法就后续所有代码都放在该包中。 比如：

```scala
package com.runoob
class HelloWorld
```

第二种方法有些类似 C#，如：

```scala
package com.runoob {
  class HelloWorld
}
```

### 15.2. 引用

Scala 使用 `import` 关键字引用包。

```
import java.awt.Color  // 引入Color

import java.awt._  // 引入包内所有成员

def handler(evt: event.ActionEvent) { // java.awt.event.ActionEvent
  ...  // 因为引入了java.awt，所以可以省去前面的部分
}
```

import 语句可以出现在任何地方，而不是只能在文件顶部。import 的效果从开始延伸到语句块的结束。这可以大幅减少名称冲突的可能性。

如果想要引入包中的几个成员，可以使用 selector（选取器）：

```
import java.awt.{Color, Font}

// 重命名成员
import java.util.{HashMap => JavaHashMap}

// 隐藏成员
import java.util.{HashMap => _, _} // 引入了util包的所有成员，但是HashMap被隐藏了
```

> **注意：**默认情况下，Scala 总会引入 java.lang._ 、 scala._ 和 Predef.\_，这里也能解释，为什么以 scala 开头的包，在使用时都是省去 scala.的。

### 15.3. 访问修饰符

Scala 访问修饰符基本和 Java 的一样，分别有：private，protected，public。

如果没有指定访问修饰符，默认情况下，Scala 对象的访问级别都是 public。

Scala 中的 private 限定符，比 Java 更严格，在嵌套类情况下，外层类甚至不能访问被嵌套类的私有成员。

```scala
class Outer {

  class Inner {
    private def f() {
      println("f")
    }

    class InnerMost {
      f() // 正确
    }

  }

  (new Inner).f() //错误
}
```

## 16. 参考资料

- [Scala 官网](https://www.scala-lang.org/)
- [Scala 菜鸟教程](https://www.runoob.com/scala/scala-tutorial.html)
