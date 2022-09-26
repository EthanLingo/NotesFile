# 清理Xcode缓存


tags: #日期/2022-09-26 #类型/笔记 #来源/转载 #内容/整理 


Xcode生成的缓存文件, 删除后下次编译会再次生成, 可以清理

`~/Library/Developer/Xcode/DerivedData/`

真机调试产生的一堆对iOS设备支持的文件,可以删除不需要的版本

`~/Library/Developer/Xcode/iOS DeviceSupport/`

APP 打包的ipa历史版本，可以定期清理

`~/Library/Developer/Xcode/Archives`

打印的日志，可以定期清理

`~/Library/Developer/Xcode/iOS Device Logs/`

模拟器的数据，可以定期清理

`~/Library/Developer/CoreSimulator/Devices/`

模拟器缓存数据，不用的可以定期清理

`~/Library/Developer/CoreSimulator/Caches/`

 APP 打包的app icon历史版本，可以定期清理

`~/Library/Developer/Xcode/Products/`

文件缓存，可以定期清理

`~/Library/Developer/Xcode/DocumentationCache/`


————————————————

> 来源：
版权声明：本文为CSDN博主「惟爱妮」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/u012907783/article/details/126623430