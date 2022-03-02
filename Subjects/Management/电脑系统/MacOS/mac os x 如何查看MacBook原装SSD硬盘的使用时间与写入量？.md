作者：小谢  
链接：https://www.zhihu.com/question/24479810/answer/903982914  
来源：知乎  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。  
  

分两个情况：

### 一、如果题主不差钱，或者只是看一下（例如购买二手macbook时）：

下载SMART Utility或者DriveDX中的任意一个，都收费，但都免费试用十几天。有图形界面UI非常友好。

如果是买二手电脑，先下载好保存到优盘中，接头的时候直接打开，就不用再现场下载了。

### 二、如果题主差钱，但是而我一样能折腾：

推荐下载使用smartmontools，命令行工具，但是功能完整。

Homebrew用户可以用

```text
brew install smartmontools
```

然后在smartctl所在目录打开terminal终端（或者把smartctl拖入终端窗口），先使用--smart (-s)命令打开S.M.A.R.T监控：

```text
smartctl -s on disk0
```

然后使-a命令查看状态：


#教程 #来源：转载 

[[Mac]]
[[管理硬件]]


```text
smartctl -a disk0
```

如果是通过Homebrew安装的，应该位于/usr/local/sbin/smartctl，如果环境变量已经配置可以直接打开终端使用。

结果如下：

```text
=== START OF SMART DATA SECTION ===
SMART overall-health self-assessment test result: PASSED

SMART/Health Information (NVMe Log 0x02)
Critical Warning:                   0x00
Temperature:                        43 Celsius
Available Spare:                    91%
Available Spare Threshold:          2%
Percentage Used:                    0%
Data Units Read:                    20,551,382 [10.5 TB]
Data Units Written:                 9,906,876 [5.07 TB]
Host Read Commands:                 29,998,493
Host Write Commands:                17,633,126
Controller Busy Time:               0
Power Cycles:                       337
Power On Hours:                     7
Unsafe Shutdowns:                   21
Media and Data Integrity Errors:    0
Error Information Log Entries:      0
```

[编辑于 2019-11-21](//www.zhihu.com/question/24479810/answer/903982914)