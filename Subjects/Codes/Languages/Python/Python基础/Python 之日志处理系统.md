---
title: Python 之日志处理系统
authors: Ethan Lin
year: 2024-04-23
tags:
  - 类型/AI问答笔记
  - 日期/2024-04-23
  - 内容/编程语言/Python
  - 内容/计算机系统
  - 内容/日志系统
---
# Python 之日志处理系统




> [!attention]
> 以下由AI回答，不保证正确性！



在Python的日志系统中，主要涉及到以下几个对象：  

- Logger：日志记录器。这是日志系统的核心对象，它提供了应用程序可以直接使用的接口。  
- Handler：日志处理器。决定将日志记录发送到合适的目的地输出。目的地可以是很多种，例如控制台、文件、HTTP GET/POST，SMTP等。每个logger可以添加零个或者多个handler。  
- Formatter：日志格式化器。指定了日志记录的最终顺序、结构和内容。  
- Filter：日志过滤器。提供了更精细的设备来决定要输出哪些日志记录。  

这些对象之间的交互关系如下：  

- 当你在应用程序中调用`logging.debug()`、`logging.info()`等函数时，Python会创建一个`LogRecord`对象，然后将这个对象传递给Logger对象处理。  
- Logger对象会查看这个LogRecord对象的级别，如果级别足够高（比如Logger的级别设置为INFO，那么只有INFO级别及以上的LogRecord会被处理），Logger就会将这个LogRecord传递给它的所有Handler对象。  
- 每个Handler对象也有一个级别，它会忽略级别低于这个级别的LogRecord。如果LogRecord的级别足够高，Handler就会使用它的Formatter将这个LogRecord转换为文本，然后将这个文本输出到它的目的地。  
- Filter可以被Logger或者Handler使用，它可以提供更复杂的算法来决定是否输出一个LogRecord。如果Filter决定这个LogRecord需要被输出，它就会被传递给下一个Filter，或者被Handler处理。如果Filter决定这个LogRecord不需要被输出，那么它就会被丢弃。  
- Logger和Handler之间的交互关系可以简单地理解为：Logger生成日志记录，然后将日志记录传递给Handler，Handler将日志记录输出到特定的目的地。

这就是Python日志系统中的对象以及它们之间的交互关系。

