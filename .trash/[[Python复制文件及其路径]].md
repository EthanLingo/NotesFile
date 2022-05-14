
本文实例讲述了python实现复制整个目录的方法。分享给大家供大家参考。具体分析如下：

python有一个非常好用的目录操作类库shutil，通过这个库可以很简单的复制整个目录及目录下的文件

```python
import shutil
#复制文件
shutil.copyfile('listfile.py', 'd:/test.py')
#复制目录
shutil.copytree('d:/temp', 'c:/temp/')
#其余可以参考shutil下的函数
```
