# R语言处理字符串


## stringr包之字符串处理函数汇总
 

字符串拼接函数

str_c: 字符串拼接。  
str_join: 字符串拼接，同 str_c。  
str_trim: 去掉字符串的空格和 TAB(\t) str_pad: 补充字符串的长度  
str_dup: 复制字符串  
str_wrap: 控制字符串输出格式  
str_sub: 截取字符串  
str_sub<- 截取字符串，并赋值，同 str_sub

字符串计算函数

str_count: 字符串计数 str_length: 字符串长度
str_sort: 字符串值排序  
str_order: 字符串索引排序，规则同 str_sort

字符串匹配函数

str_split: 字符串分割  
str_split_fixed: 字符串分割，同 str_split  
str_subset: 返回匹配的字符串  
word: 从文本中提取单词  
str_detect: 检查匹配字符串的字符  
str_match: 从字符串中提取匹配组  
str_match_all: 从字符串中提取匹配组，同 str_match str_replace: 字符串替换  
str_replace_all: 字符串替换，同 str_replace str_replace_na: 把 NA 替换为 NA 字符串  
str_locate: 找到匹配的字符串的位置。  
str_locate_all: 找到匹配的字符串的位置, 同 str_locate str_extract: 从字符串中提取匹配字符  
str_extract_all: 从字符串中提取匹配字符，同 str_extract

字符串变换函数

str_conv: 字符编码转换  
str_to_upper: 字符串转成大写  
str_to_lower: 字符串转成小写, 规则同 str_to_upper str_to_title: 字符串转成首字母大写, 规则同 str_to_upper

 参数控制函数，仅用于构造功能的参数，不能独立使用。 

boundary: 定义使用边界  
coll: 定义字符串标准排序规则。  
fixed: 定义用于匹配的字符，包括正则表达式中的转义符 regex: 定义正则表达式

