---
title: Golang语言实践笔记之快速开始一个Go程序
layout: post
comments: true
language: chinese
category: [golang]
keywords: golang
description: golang语言实践
---

通过学习go实践代码学习golang的基本数据结构和语法

<!-- more -->

### 提到的Golang语法和数据结构

* main函数保存在名为main的包里。如果main函数不在main包里，构建工具就不会生成可执行文件。
* 一个包定义一组编译过的代码，包的名字类似命名空间，可以用来间接访问包内声明的标识符。
* 所有处于同一个文件夹里的代码文件，必须使用同一个包名。按照惯例，包和文件夹同名。
* 使用下划线导入包，这个技术是为了让Go语言对包做初始化操作，但是并不使用包里的标识符。为了让程序的可读性更强，Go编译器不允许声明导入某个包却不使用。下划线让编译器接受这类导入，并且调用对应包内的所有代码文件里定义的init函数。
* 程序中每个代码文件里的init函数都会在main函数执行前调用。
* 变量没有定义在任何函数作用域内，会被当成包级别变量。变量名是以小写字母开头的。
* Go语言中，标识符要么从包里公开，要么不从包里公开。当代码导入一个包时，程序可以直接访问这个包中任意一个公开的标识符。这些标识符以大写字母开头。以小写字母开头的标识符是不公开的，不能被其他包中的代码直接访问。但是，其他包可以间接访问不公开的标识符。例如，一个函数可以返回一个未公开类型的值，那么这个函数的任何调用者，哪怕调用者不是在这个包里声明的，都可以访问这个值。
* map是Go语言里的一个引用类型，需要使用make来构造。如果不先构造map并将构造后的值赋值给变量，会在试图使用这个map变量时收到出错信息。这是因为map变量默认的零值是nil。
* 在Go语言中，所有变量都被初始化为其零值。对于数值类型，零值是0；对于字符串类型，零值是空字符串；对于布尔类型，零值是false；对于指针，零值是nil。对于引用类型来说，所引用的底层数据结构会被初始化为对应的零值。但是被声明为其零值的引用类型的变量，会返回nil作为其值。
* 使用简化变量声明运算符，在调用make的同时声明并初始化该通道变量。根据经验，如果需要声明初始值为零值的变量，应该使用var关键字声明变量；如果提供确切的非零值初始化变量或者使用函数返回值创建变量，应该使用简化变量声明运算符。
* 在Go语言中，通道（channel）和映射（map）与切片（slice）一样，也是引用类型，不过通道本身实现的是一组带类型的值，这组值用于在goroutine之间传递数据。通道内置同步机制，从而保证通道安全。
* 在Go语言中，所有的变量都以值的方式传递。因为指针变量的值是所指向的内存地址，在函数间传递指针变量，是在传递这个地址值，所以依旧被看作以值的方式在传递。
* Go语言支持闭包，因为有了闭包，函数可以直接访问到那些没有作为参数传入的变量。匿名函数并没有拿到这些变量的副本，而是直接访问外层函数作用域中声明的这些变量本身。
* 命名接口的时候，也需要遵循Go语言的命名惯例。如果接口类型只包含一个方法，那么这个类型的名字以er结尾。如果接口类型内部声明了多个方法，其名字需要与其行为关联。
* 如果要让一个用户定义的类型实现一个接口，这个用户定义的类型要实现接口类型里声明的所有方法。
* 空结构在创建实例时，不会分配任何内存。这种结构很适合创建没有任何状态的类型。
* 如果声明函数的时候带有接收者，则意味着声明了一个方法。这个方法会和指定的接收者的类型绑在一起。因为大部分方法在被调用后都需要维护接收者的值的状态，所以一个最佳实践是将方法的接收者声明为指针，对于不需要分配内存的类型来说，由于不需要维护状态，所以不需要指针类型的接收者。
* 与直接通过值或者指针调用方法不同，如果通过接口类型的值调用方法，规则有很大不同。使用指针作为接收者声明的方法，只能在接口类型的值是一个指针的时候被调用。使用值作为接收者声明的方法，在接口类型的值为值或者指针时，都可以被调用。


### 代码地址
[快速开始一个Go程序](https://github.com/jingliming/code/tree/master/chapter2/sample)
## 小结
* 每个代码文件都属于一个包，而包名应该与代码文件所在的文件夹同名
* Go语言提供了多种声明和初始化变量的方式。如果变量的值没有初始化，编译器会将变量初始化为零值
* 使用指针可以在函数间或者goroutine间共享数据
* 通过启动goroutine和使用通道完成并发和同步
* Go语言提供了内置函数来支持Go语言内部的数据结构
* 标准库包含很多包，能做很多很有用的事情
* 使用Go接口可以编写通用的代码和框架

