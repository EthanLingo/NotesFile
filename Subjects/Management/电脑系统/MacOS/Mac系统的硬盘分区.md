#来源/转载 
#知识 

[[Mac]]
[[硬盘分区]]

Mac系统支持如下三种硬盘分区:

-   **GUID**

    是基于Intel处理器苹果电脑使用的新的分区表, 也叫GUID Partition Table, GPT，是EFI标准的一个部分，详见[WikiPedia的解释：GUID Parttion Table](http://en.wikipedia.org/wiki/GUID_Partition_Table) 。

    在Intel处理器Mac电脑上可以使用GUID和APM分区表硬盘来启动机器，GUID是苹果建议使用的分区表格式。

    对于使用时间机器备份的硬盘，只能使用GUID格式的分区表。

    在PowerPC处理器机器上不能做启动盘，要用APM分区表格式，见下.

-   **APM**

    是Apple的标准，是Apple Partition Map的缩写，对于基于PowerPC的电脑，硬盘只能使用这种分区表格式才能作为系统启动盘。如果在分区中安装Universal Binary码的OS X系统, 基于Intel的电脑也可以从这样的分区表的启动分区硬盘启动.

    如果考虑到系统兼容性(PowerPC和Intel-based)，那么硬盘应该使用这种分区表格式.

-   **MBR**

 Master Boot Record的缩写, 实际上是指硬盘上的第一个磁盘块。MBR是比较古老的标准，有诸多限制，比如最多支持4个主分区等，由于PC兼容机的广泛使用，以及微软一直没有放弃使 用，所以这种分区表格式还在PC世界存在。如果在苹果机上给硬盘使用这种分区表格式，一般都是应用在外置硬盘或者Ｕ盘上, 这样可以照顾到PC机使转移数据更方便. Mac的OS X系统不能从这种的分区表格式的硬盘上启动系统.