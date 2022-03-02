
# JavaScript处理JSON

JSON对象的两个方法：JSON.parse() 和 JSON.stringify() 通常用做JSON对象和字符串之间的相互转换

JSON.parse() 方法用于将一个 JSON 字符串转换为对象。

JSON.parse(text[, reviver])

参数说明：

text:必需， 一个有效的 JSON 字符串。
reviver: 可选，一个转换结果的函数， 将为对象的每个成员调用此函数。
返回值：

返回给定 JSON 字符串转换后的对象。

JSON.parse() 可以接受第二个参数，它可以在返回之前转换对象值。比如这例子中，将返回对象的属性值大写：


关于JSON语法，参考[[JSON]]