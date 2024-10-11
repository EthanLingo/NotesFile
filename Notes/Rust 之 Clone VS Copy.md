---
title: Rust 之 Clone VS Copy
authors: Ethan Lin
year: 2024-09-27
tags:
  - 类型/笔记
  - 日期/2024-09-27
  - 来源/转载
  - 内容/编程/Rust
aliases:
  - Rust 之 Clone VS Copy
---
# Rust 之 Clone VS Copy



# 来源

> [Site Unreachable](https://uxiew.github.io/rust_study/%E7%AC%AC%2011%20%E7%AB%A0%20%E6%89%80%E6%9C%89%E6%9D%83%E5%92%8C%E7%A7%BB%E5%8A%A8%E8%AF%AD%E4%B9%89/11.5%20Clone%20VS%20Copy.html)




Rust 中的 Copy 是一个特殊的 trait，它给类型提供了“复制”语义。在 Rust 标准库里面，还有一个跟它很相近的 trait，叫作 Clone。很多人容易把这两者混淆，本节专门来谈一谈这两个 trait。

## 11.5.1 Copy 的含义 

Copy 的全名是`std::marker::Copy`。 请大家注意，std::marker 模块里面所有的 trait 都是特殊的 trait。目前稳定的有四个，它们是 `Copy`、`Send`、`Sized`、`Sync`。它们的特殊之处在于：它们是跟编译器密切绑定的，impl 这些 trait 对编译器的行为有重要影响。在编译器眼里，它们与其他的 trait 不一样。这几个 trait 内部都没有方法，它们的唯一任务是给类型打一个“标记”，表明它符合某种约定——这些约定会影响编译器的静态检查以及代码生成。

Copy 这个 trait 在编译器的眼里代表的是什么意思呢？简单点总结就是，如果一个类型 impl 了 Copy trait，意味着任何时候，我们都可以通过简单的内存复制（在 C 语言里按字节复制 memcpy）实现该类型的复制，并且不会产生任何内存安全问题。

一旦一个类型实现了`Copy trait`，那么它在变量绑定、函数参数传递、函数返回值传递等场景下，都是 copy 语义，而不再是默认的 move 语义。

下面用最简单的赋值语句`x = y`来说明 move 语义和 copy 语义的根本区别。move 语义是“剪切、粘贴”操作，变量 y 把所有权递交给了 x 之后，y 就彻底失效了，后面继续使用 y 就会出编译错误。而 copy 语义是“复制、粘贴”操作，变量 y 把所有权递交给了 x 之后，它自己还留了一个副本，在这句赋值语句之后，x 和 y 依然都可以继续使用。

在 Rust 里，move 语义和 copy 语义具体执行的操作，是不允许由程序员自定义的，这是它和 C++的巨大区别。这里没有赋值构造函数或者赋值运算符重载。move 语义或者 copy 语义都是执行的 memcpy，无法更改，这个过程中绝对不存在其他副作用。当然，这里一直谈的是“语义”，而没有涉及编译器优化。从语义的角度，我们要讲清楚，什么样的代码在编译器看来是合法的，什么样的代码是非法的。如果考虑后端优化，在许多情况下，不必要的内存复制实际上已经彻底优化掉了，大家不必担心执行效率的问题。也没有必要每次都把 move 或者 copy 操作与具体的汇编代码联系起来，因为场景不同，优化结果不同，生成的代码也是不同的。大家只需记住的是语义。

## 11.5.2 Copy 的实现条件 

并不是所有的类型都可以实现`Copy trait`。Rust 规定，对于自定义类型，只有所有成员都实现了 Copy trait，这个类型才有资格实现 Copy trait。

常见的数字类型、`bool`类型、共享借用指针`&`，都是具有`Copy`属性的类型。而`Box`、`Vec`、可写借用指针`&mut`等类型都是不具备`Copy`属性的类型。

对于数组类型，如果它内部的元素类型是`Copy`，那么这个数组也是 Copy 类型。

对于元组 tuple 类型，如果它的每一个元素都是`Copy`类型，那么这个 tuple 也是 Copy 类型。

struct 和 enum 类型不会自动实现 Copy trait。只有当 struct 和 enum 内部的每个元素都是 Copy 类型时，编译器才允许我们针对此类型实现 Copy trait。 比如下面这个类型，虽然它的成员是 Copy 类型，但它本身不是 Copy 类型：

rust

```
struct T(i32);

fn main() {
    let t1 = T(1);
    let t2 = t1;
    println!("{} {}", t1.0, t2.0);
}
```

1  
2  
3  
4  
5  
6  
7  

编译可见编译错误。原因是在`let t2 = t1;`这条语句中执行的是 move 语义。但是我们可以手动为它`impl Copy trait`，这样它就具备了 copy 语义。

我们可以认为，Rust 中只有 POD（ C++ 语言中的 Plain Old Data）类型才有资格实现`Copy trait`。 在 Rust 中，如果一个类型只包含 POD 数据类型的成员，并且没有自定义析构函数，那它就是 POD 类型。 比如：整数、浮点数、只包含 POD 类型的数组等，都属于 POD 类型；而 Box String Vec 等不能按字节复制的类型，都不属于 POD 类型。 但是，反过来讲，也并不是所有满足 POD 的类型都应该实现`Copy trait`，是否实现`Copy`取决于业务需求。

## 11.5.3 Clone 的含义 

Clone 的全名是`std::clone::Clone`。它的完整声明如下：

rust

```
pub trait Clone : Sized {
    fn clone(&self) -> Self;
    fn clone_from(&mut self, source: &Self) {
        *self = source.clone()
    }
}
```

1  
2  
3  
4  
5  
6  

它有两个关联方法，分别是`clone_from`和`clone`，`clone_from`是有默认实现的，依赖于`clone`方法的实现。`clone`方法没有默认实现，需要手动实现。

clone 方法一般用于“基于语义的复制”操作。所以，它做什么事情，跟具体类型的作用息息相关。 比如，对于 Box 类型，clone 执行的是“深复制”；而对于 Rc 类型，clone 做的事情就是把引用计数值加 1。

虽然 Rust 中的`clone`方法一般是用来执行复制操作的，但是如果在自定义的`clone`函数中做点别的什么工作，编译器也没办法禁止。 你可以根据需要在`clone`函数中编写任意的逻辑。

但是有一条规则需要注意：对于实现了`copy`的类型，它的`clone`方法应该跟`copy`语义相容，等同于按字节复制。

## 11.5.4 自动 derive 

绝大多数情况下，实现 Copy Clone 这样的 trait 都是一个重复而无聊的工作。因此，Rust 提供了一个 attribute，让我们可以利用编译器自动生成这部分代码。 示例如下：

rust

```
#[derive(Copy, Clone)]
struct MyStruct(i32);
```

1  
2  

这里的`derive`会让编译器帮我们自动生成`impl Copy`和`impl Clone`这样的代码。自动生成的`clone`方法，会依次调用每个成员的`clone`方法。

通过 derive 方式自动实现 Copy 和手工实现 Copy 有微小的区别。 当类型具有泛型参数的时候，比如`struct MyStruct<T>{}`，通过 derive 自动生成的代码会自动添加一个`T:Copy`的约束。

目前，只有一部分固定的特殊 trait 可以通过 derive 来自动实现。将来 Rust 会允许自定义的 derive 行为，让我们自己的 trait 也可以通过 derive 的方式自动实现。

## 11.5.5 总结 

Copy 和 Clone 两者的区别和联系如下。

- Copy 内部没有方法，Clone 内部有两个方法。
    
- Copy trait 是给编译器用的，告诉编译器这个类型默认采用 copy 语义，而不是 move 语义。 `Clone trait`是给程序员用的，我们必须手动调用 clone 方法，它才能发挥作用。
    
- Copy trait 不是想实现就能实现的，它对类型是有要求的，有些类型不可能`impl Copy`。 而`Clone trait`则没有什么前提条件，任何类型都可以实现（ unsized 类型除外，因为无法使用 unsized 类型作为返回值）。
    
- Copy trait 规定了这个类型在执行变量绑定、函数参数传递、函数返回等场景下的操作方式。 即这个类型在这种场景下，必然执行的是“简单内存复制”操作，这是由编译器保证的，程序员无法控制。 Clone trait 里面的 clone 方法究竟会执行什么操作，则是取决于程序员自己写的逻辑。一般情况下，clone 方法应该执行一个“深复制”操作，但这不是强制性的，如果你愿意，在里面启动一个人工智能程序都是有可能的。
    
- 如果你确实不需要 Clone trait 执行其他自定义操作（绝大多数情况都是这样），编译器提供了一个工具，我们可以在一个类型上添加`#[derive(Clone)]`， 来让编译器帮我们自动生成那些重复的代码。编译器自动生成的`clone`方法非常机械，就是依次调用每个成员的`clone`方法。
    
- Rust 语言规定了在`T:Copy`的情况下，Clone trait 代表的含义。即：当某变量`t:T`符合`T:Copy`时，它调用`t.clone()`方法的含义必须等同于“简单内存复制”。 也就是说，`clone`的行为必须等同于`let x = std::ptr::read(&t);`，也等同于`let x = t;`。当`T:Copy`时，我们不要在`Clone trait`里面乱写自己的逻辑。 所以，当我们需要指定一个类型是 Copy 的时候，最好使用`#[derive(Copy, Clone)]`方式，避免手动实现`Clone`导致错误。
    

[](https://github.com/uxiew/rust_study/edit/main/docs/%E7%AC%AC%2011%20%E7%AB%A0%20%E6%89%80%E6%9C%89%E6%9D%83%E5%92%8C%E7%A7%BB%E5%8A%A8%E8%AF%AD%E4%B9%89/11.5%20Clone%20VS%20Copy.md)

