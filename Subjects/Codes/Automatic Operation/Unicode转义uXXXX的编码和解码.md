
# Unicode转义(\\uXXXX)的编码和解码
#笔记 
tags: #来源/转载 
#资料 
#类型/解决

[[编码]]
[[解码]]
[[Unicode]]
[[JS]]
[[Java]]
[[C#]]


**在涉及Web前端开发时, 有时会遇到`\uXXXX`格式表示的字符, 其中`XXXX`是16进制数字的字符串表示形式, 在js中这个叫Unicode转义字符, 和`\n` `\r`同属于转义字符. 在其他语言中也有类似的, 可能还有其它变形的格式.**

多数时候遇到需要解码的情况多点, 所以会先介绍解码decode, 后介绍编码encode.

下文会提供Javascript下不同方法的实现和简单说明, 会涉及到正则和位运算的典型用法.

## **_1_**|**_0_****Javascript的实现**

### **_1_**|**_1_****解码的实现**

function decode(s) {
    return unescape(s.replace(/\\\\(u\[0-9a-fA-F\]{4})/gm, '%$1'));
}

`unescape`是用来处理`%uXXXX`这样格式的字符串, 将`\uXXXX`替换成`%uXXXX`后`unescape`就可以处理了.

### **_1_**|**_2_****编码的实现**

function encode1(s) {
    return escape(s).replace(/%(u\[0\-9A-F\]{4})|(%\[0\-9A-F\]{2})/gm, function($0, $1, $2) {
        return $1 && '\\\\' + $1.toLowerCase() || unescape($2);
    });
}

和解码中相对应, **使用`escape`编码, 然后将`%uXXXX`替换为`\uXXXX`,** 因为`escape`还可能把一些字符编码成`%XX`的格式, 所以这些字符还需要使用`unescape`还原回来.

**`escape`编码结果`%uXXXX`中的`XXXX`是大写的, 所以后面的`replace`只处理大写的`A-F`.**

### **_1_**|**_3_****另一种编码的实现**

不使用正则和`escape`

function encode2(s) {
    var i, c, ret = \[\],
        pad = '000';
    for (i = 0; i < s.length; i++) {
        c = s.charCodeAt(i);
        if (c > 256) {
            c = c.toString(16);
            ret\[i\] = '\\\\u' + pad.substr(0, 4 - c.length) + c;
        } else {
            ret\[i\] = s\[i\];
        }
    }
    return ret.join('');
}

遍历字符串中的字符, 那些`charCode`大于256的会转换成16进制字符串`c.toString(16)`, 如果不足4位则左边补0`pad.substr(0, 4 - c.length)`. 结尾将遍历的结果合并成字符串返回.

unicode解码网站（字符转化成\\uxxxx）：[http://www.msxindl.com/tools/unicode16.asp](http://www.msxindl.com/tools/unicode16.asp)

## **_2_**|**_0_****C#的实现** 

### **_2_**|**_1_****解码的实现**

static Regex reUnicode = new Regex(@"\\\\u(\[0-9a-fA-F\]{4})", RegexOptions.Compiled);
public static string Decode(string s)
{
return reUnicode.Replace(s, m =>
{
short c;
if (short.TryParse(m.Groups\[1\].Value, System.Globalization.NumberStyles.HexNumber, CultureInfo.InvariantCulture,out c))
{
return "" + (char)c;
}
return m.Value;
});
}

正则和js中的一样, 将`XXXX`转换以16进制`System.Globalization.NumberStyles.HexNumber`解析为`short`类型, 然后直接`(char)c`就能转换成对应的字符, `"" + (char)c`用于转换成字符串类型返回.

由于正则中也有`\uXXXX`, 所以需要写成`\\uXXXX`来表示匹配字符串`\uXXXX`, 而不是具体的字符.

上面使用到了Lambda, 需要至少dotnet 4的SDK才能编译通过, 可以在dotnet 2下运行.

### **_2_**|**_2_****编码的实现**

static Regex reUnicodeChar = new Regex(@"\[^\\u0000-\\u00ff\]", RegexOptions.Compiled);
public static string Encode(string s)
{
return reUnicodeChar.Replace(s, m => string.Format(@"\\u{0:x4}", (short)m.Value\[0\]));
}

 和C#的解码实现正好相反, 0-255之外的字符, 从`char`转换成`short`, 然后`string.Format`以16进制, 至少输出4位.

## **_3_**|**_0_****Java的实现**

### **_3_**|**_1_****解码的实现**

和C#相似的, 使用正则

static final Pattern reUnicode = Pattern.compile("\\\\\\\\u(\[0-9a-zA-Z\]{4})");
 
public static String decode1(String s) {
Matcher m = reUnicode.matcher(s);
StringBuffer sb = new StringBuffer(s.length());
while (m.find()) {
m.appendReplacement(sb,
Character.toString((char) Integer.parseInt(m.group(1), 16)));
}
m.appendTail(sb);
return sb.toString();
}

[Java语言](https://www.baidu.com/s?wd=Java%E8%AF%AD%E8%A8%80&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)没有内嵌正则语法, 也没有类似C#的`@"\u1234"`原始形式字符串的语法, 所以要表示正则中匹配`\`, 就需要`\\\\`, 其中2个是用于Java中字符转义, 2个是正则中的字符转义.

Java语言中没有设计函数或者委托的语法, 所以它的正则库提供的是`find` `appendReplacement` `appendTail`这些方法的组合, 等价于js和C#中的`replace`.

这里使用`StringBuffer`类型是由于`appendReplacement`只接受这个类型, `StringBuffer`有线程安全的额外操作, 所以性能差一点. 也许第三方的正则库能把API设计的更好用点.

`Integer.parseInt(m.group(1), 16)`用于解析为`int`类型, 之后再`(char)`, 以及`Character.toString`转换成字符串.

### **_3_**|**_2_** **解码的另一种实现**

 因为`StringBuffer`的原因, 不使用正则的实现

public static String decode2(String s) {
StringBuilder sb = new StringBuilder(s.length());
char\[\] chars = s.toCharArray();
for (int i = 0; i < chars.length; i++) {
char c = chars\[i\];
if (c == '\\\\' && chars\[i + 1\] == 'u') {
char cc = 0;
for (int j = 0; j < 4; j++) {
char ch = Character.toLowerCase(chars\[i + 2 + j\]);
if ('0' <= ch && ch <= '9' || 'a' <= ch && ch <= 'f') {
cc |= (Character.digit(ch, 16) << (3 - j) \* 4);
} else {
cc = 0;
break;
}
}
if (cc > 0) {
i += 5;
sb.append(cc);
continue;
}
}
sb.append(c);
}
return sb.toString();
}

手工做就是麻烦很多, 代码中也一坨的符号.

遍历所有字符`chars`, 检测到`\u`这样的字符串, 检测后续的4个字符是否是16进制数字的字符表示. 因为`Character.isDigit`会把一些其它语系的数字也算进来, 所以保险的做法`'0' <= ch && ch <= '9'`.

`Character.digit`会把`0-9`返回为`int`类型的0-9, 第2个参数是16时会把`a-f`返回为`int`类型的10-15.

剩下的就是用`|=`把各个部分的数字合并到一起, 转换成char类型. 还有一些调整遍历位置等.

### **_3_**|**_3_****编码的实现**

考虑到Java正则的杯具, 还是继续手工来吧, 相对解码来说代码少点.

public static String encode(String s) {
StringBuilder sb = new StringBuilder(s.length() \* 3);
for (char c : s.toCharArray()) {
if (c < 256) {
sb.append(c);
} else {
sb.append("\\\\u");
sb.append(Character.forDigit((c >>> 12) & 0xf, 16));
sb.append(Character.forDigit((c >>> 8) & 0xf, 16));
sb.append(Character.forDigit((c >>> 4) & 0xf, 16));
sb.append(Character.forDigit((c) & 0xf, 16));
}
}
return sb.toString();
}

对应于上文Java编码的实现正好是反向的实现, 依旧遍历字符, 遇到大于256的字符, 用位运算提取出4部分并使用`Character.forDigit`转换成16进制数对应的字符.

剩下就是`sb.toString()`返回了.

## **_4_**|**_0_****总结**

-   编码从逻辑上比解码简单点.
-   对付字符串, js还是最顺手的, 也方便测试.
-   位运算的性能很高.
-   Java的正则库设计的很不方便, 可以考虑第三方.
-   Java的语法设计现在看来呆板, 落后, 也没有js那种灵活.
-   上文Java的非正则实现可以写成等价的C#代码.

 转：  https://blog.csdn.net/testcs\_dn/article/details/88532460