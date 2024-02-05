---
title: 安卓开发之路：Kotlin null 详解
date: 2023-07-02
abbrlink: d27106dd
categories:
  - [ 经验分享,安卓 ]
tags:
  - [教程]
  - [ 安卓]
desc: 在Kotlin中，null是一个重要的概念。
recommend: true
cover: https://p.wzsco.top/7ad1d87c36e184f2e978e215619c7971.png/cover
---
> 参考来自：https://www.c-sharpcorner.com/article/kotlin-null-safety/

## 前言

在Kotlin中，null是一个重要的概念。相比于Java中的null，Kotlin对null做了更严格的控制，这使得在Kotlin中出现空指针异常的可能性更小。探讨Kotlin中的null，包括其定义、解决方案以及在实际项目中的应用。

## Kotlin中的null

在Kotlin中，null是一个特殊的值，它表示一个变量或表达式没有被初始化或者没有有效的值。Kotlin中的null拥有Java中的null的所有特性，例如可以被赋值给任何引用类型的变量，可以作为函数的返回值等。与Java不同的是，在Kotlin中，null是一个类型，而不仅仅是一个值。这意味着，如果一个变量可以为null，那么它的类型需要被声明为可为空的类型。

在Kotlin中，可为空的类型使用“?”来表示。例如，可以将变量声明为可为空的字符串类型，如下所示：

```kotlin
var str: String? = null
```

在这个例子中，str变量被声明为可为空的字符串类型。由于它的类型中包含了“?”，因此它可以被赋值为null。

## 空安全调用操作符

Kotlin中的空安全调用操作符（?.）是一种方便的方式来检查一个变量是否为null。它可以被用于访问一个对象的属性或方法，而不必担心对象是否为null。如果对象为null，那么表达式将返回null，而不是抛出NullPointerException。

例如，假设我们有一个可为空的字符串变量str，它包含一个非空字符串。我们可以使用空安全调用操作符来访问其length属性，如下所示：

```kotlin
val length = str?.length
```

如果str为null，那么表达式将返回null。否则，它将返回str的length属性的值。

## Elvis操作符

Elvis操作符（?:）是另一种方便的方式来处理null。它被用于提供一个默认值，当一个表达式为null时，它将返回默认值。例如，假设我们有一个可为空的字符串变量str，我们想要获取它的长度，如果它为null，我们想要默认长度为0。我们可以使用Elvis操作符来完成这个任务，如下所示：

```kotlin
val length = str?.length ?: 0
```

如果str为null，那么表达式将返回0。否则，它将返回str的length属性的值。

## 非空断言操作符

非空断言操作符（!!）是一种非常强大的操作符，它被用于告诉Kotlin编译器，我们确信某个变量不会为null。当我们使用非空断言操作符时，如果变量为null，那么将抛出NullPointerException异常。

例如，假设我们有一个可为空的字符串变量str，我们确定它不为null。我们可以使用非空断言操作符来访问其length属性，如下所示：

```kotlin
val length = str!!.length
```

如果str为null，那么表达式将抛出NullPointerException异常。否则，它将返回str的length属性的值。

非空断言操作符应该谨慎使用。因为它会在编译时消除null检查，从而增加了出现NullPointerException异常的风险。通常情况下，应该优先考虑使用空安全调用操作符和Elvis操作符。

## lateinit关键字

在某些情况下，我们可能需要在声明变量时不初始化它，而是在稍后的某个时候初始化它。在Kotlin中，我们可以使用lateinit关键字来实现这个目的。lateinit关键字告诉Kotlin编译器，我们会稍后初始化这个变量，因此它可以不被初始化。

使用lateinit关键字有以下限制：

- 只能用于类成员变量，不能用于局部变量或函数参数
- 只能用于非空类型，不能用于可为空的类型
- 必须在使用该变量之前进行初始化，否则会抛出UninitializedPropertyAccessException异常

例如，我们可以将下面的类成员变量声明为可使用lateinit关键字的字符串类型：

```kotlin
lateinit var str: String
```

在稍后的某个时候，我们可以初始化这个变量：

```kotlin
str = "hello world"
```

在初始化之前，我们不能使用这个变量，否则会抛出UninitializedPropertyAccessException异常。

## 结论

在Kotlin中，null是一个非常重要的概念，它可以帮助我们避免许多空指针异常。Kotlin提供了许多有用的工具来处理null，例如空安全调用操作符、Elvis操作符和lateinit关键字。当我们使用这些工具时，应该谨慎使用非空断言操作符，因为它可能会导致NullPointerException异常。通过正确使用这些工具，我们可以编写更加健壮和安全的代码。