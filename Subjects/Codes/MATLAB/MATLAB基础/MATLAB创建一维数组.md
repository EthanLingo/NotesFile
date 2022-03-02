MATLAB创建一维数组的5种方法：直接输入法，步长生成法，转置法，定数线性采样法linspace(a,b,n)，定数对数采样法logspace(a,b,n)。



1. 第一，直接输入法创建一维行数组。在命令行窗口（Command Window）输入如下代码：A=[pi,2*pi,exp(1),3,2^3]，然后回车得到一维行数组。

   A =3.1416  6.2832  2.7183  3.0000  8.0000

   其中创建数组时用[ ]将数字括起来，逗号或者空格用于创建行数组，分号用于创建列数组。

   ![MATLAB创建一维数组的5种方法](https://exp-picture.cdn.bcebos.com/e6ae36066b0192dd1b014a471a87031c98c0f095.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

2.  2

    第二，直接输入法创建一维列数组。在命令行窗口（Command Window）输入如下代码：A=[pi;2*pi;exp(1);3;2^3]，然后回车得到一维列数组。

    A =

    3.1416

    6.2832

    2.7183

    3.0000

    8.0000

    其中分号用于创建列数组。

    ![MATLAB创建一维数组的5种方法](https://exp-picture.cdn.bcebos.com/bfa52adaf05e4a234f3002a91dd818196020e295.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

3.  3

    第三，步长生成法创建一维行数组。在命令行窗口（Command Window）输入如下代码：A=0:1:2*pi，然后回车得到一维行数组。

    A =0   1   2   3   4   5   6

    其中步长生成法的通用格式为a:inc:b，a,b为数组首尾的数字，inc为间隔。

    ![MATLAB创建一维数组的5种方法](https://exp-picture.cdn.bcebos.com/bab5c45872dade49244e77e226042e6816e9d595.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

4.  4

    第四，步长生成法创建一维列数组。在命令行窗口（Command Window）输入如下代码：A=[0:1:2*pi]'，然后回车得到一维列数组。

    A =

    0

    1

    2

    3

    4

    5

    6

    其中步长生成法创建列数组就是添加一个单引号，该单引号将原本的行数组转置为列数组。

    ![MATLAB创建一维数组的5种方法](https://exp-picture.cdn.bcebos.com/d9a8d2d2bb665159d601ec9e8fe23ea23b42c795.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

5.  5

    第五，定数线性采样法创建一维数组。在命令行窗口（Command Window）输入如下代码：A=linspace(10,20,6)，然后回车得到一维数组。

    A =10  12  14  16  18  20

    其中定数线性采样法的通用格式为linspace(a,b,n)，a,b表示数组首尾的数字，n表示线性采样个数。若用定数线性采样法linspace(a,b,n)生成一维列数组，只需加个单引号，即linspace(a,b,n)'

    ![MATLAB创建一维数组的5种方法](https://exp-picture.cdn.bcebos.com/0d55dc7bd2828689c2074b0565f97fbd4d7c379a.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)

6.  6

    第六，定数对数采样法创建一维数组。在命令行窗口（Command Window）输入如下代码：A=logspace(1,5,3)，然后回车得到一维数组。

    A =10    1000   100000

    其中定数对数采样法的通用格式为logspace(a,b,n)，a,b表示数组首尾的数字（10的a/b指数），n表示对数采样个数。若用定数对数采样法logspace(a,b,n)生成一维列数组，只需加个单引号，即logspace(a,b,n)'

    ![MATLAB创建一维数组的5种方法](https://exp-picture.cdn.bcebos.com/e076d77622bc7dc5be26d7eb5e460596b914299a.jpg?x-bce-process=image%2Fresize%2Cm_lfit%2Cw_500%2Climit_1%2Fquality%2Cq_80)