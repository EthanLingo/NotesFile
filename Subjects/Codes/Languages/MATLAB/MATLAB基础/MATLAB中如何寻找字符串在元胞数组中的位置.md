# MATLAB中如何寻找字符串在元胞数组中的位置

\>> a={'asda' 'asdas' 'werwe' 'reasd'} ; % 建立元胞数组

id=ismember(a,'werwe') % 查找 

id = 

0 0 1 0 % 返回的索引值 

\>>a(id) % 取出找到的值


ans = 

'werwe'
