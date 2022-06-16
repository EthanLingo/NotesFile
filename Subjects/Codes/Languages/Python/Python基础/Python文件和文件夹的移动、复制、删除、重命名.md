# Python文件和文件夹的移动、复制、删除、重命名

python中对文件和文件夹进行移动、复制、删除、重命名，主要依赖os模块和shutil模块，要死记硬背这两个模块的方法还是比较困难的，可以用一个例子集中演示文件的移动、复制、删除、重命名，用到的时候直接查询就行。

```python
`#文件、文件夹的移动、复制、删除、重命名`

`#导入shutil模块和os模块`

`import shutil,os`

`#复制单个文件`

`shutil.copy("C:\\a\\1.txt","C:\\b")`

`#复制并重命名新文件`

`shutil.copy("C:\\a\\2.txt","C:\\b\\121.txt")`

`#复制整个目录(备份)`

`shutil.copytree("C:\\a","C:\\b\\new_a")`

`#删除文件`

`os.unlink("C:\\b\\1.txt")`

`os.unlink("C:\\b\\121.txt")`

`#删除空文件夹`

`try:`

    `os.rmdir("C:\\b\\new_a")`

`except Exception as ex:`

    `print("错误信息："+str(ex))#提示：错误信息，目录不是空的`

`#删除文件夹及内容`

`shutil.rmtree("C:\\b\\new_a")`

`#移动文件`

`shutil.move("C:\\a\\1.txt","C:\\b")`

`#移动文件夹`

`shutil.move("C:\\a\\c","C:\\b")`

`#重命名文件`

`shutil.move("C:\\a\\2.txt","C:\\a\\new2.txt")`

`#重命名文件夹`

`shutil.move("C:\\a\\d","C:\\a\\new_d")`
```
