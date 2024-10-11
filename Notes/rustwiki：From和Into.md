---
title: rustwiki：From和Into
authors: Ethan Lin
year: 2024-09-27
tags:
  - 类型/笔记
  - 日期/2024-09-27
  - 来源/转载
  - 内容/编程/Rust
aliases:
  - rustwiki：From和Into
---

# rustwiki：From和Into




# 来源

> 




辨析



# [`From` 和 `Into`](https://rustwiki.org/zh-CN/rust-by-example/conversion/from_into.html#from-%E5%92%8C-into)

[`From`](https://rustwiki.org/zh-CN/std/convert/trait.From.html) 和 [`Into`](https://rustwiki.org/zh-CN/std/convert/trait.Into.html) 两个 trait 是内部相关联的，实际上这是它们实现的一部分。如果我们能够从类型 B 得到类型 A，那么很容易相信我们也能够把类型 B 转换为类型 A。

## [`From`](https://rustwiki.org/zh-CN/rust-by-example/conversion/from_into.html#from)

[`From`](https://rustwiki.org/zh-CN/std/convert/trait.From.html) trait 允许一种类型定义 “怎么根据另一种类型生成自己”，因此它提供了一种类型转换的简单机制。在标准库中有无数 `From` 的实现，规定原生类型及其他常见类型的转换功能。

比如，可以很容易地把 `str` 转换成 `String`：

`let my_str = "hello"; let my_string = String::from(my_str);`

也可以为我们自己的类型定义转换机制：

## [`Into`](https://rustwiki.org/zh-CN/rust-by-example/conversion/from_into.html#into)

[`Into`](https://rustwiki.org/zh-CN/std/convert/trait.Into.html) trait 就是把 `From` trait 倒过来而已。也就是说，如果你为你的类型实现了 `From`，那么同时你也就免费获得了 `Into`。

使用 `Into` trait 通常要求指明要转换到的类型，因为编译器大多数时候不能推断它。不过考虑到我们免费获得了 `Into`，这点代价不值一提。

[](https://rustwiki.org/zh-CN/rust-by-example/conversion.html "Previous chapter")
