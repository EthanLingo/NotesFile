tags: #来源/转载 
#资料 
#笔记 
#解决 

[[Python]]
[[配置Python]]

# 配置Python

## 安装Python

## 删除Python

### MacOS

正如开篇所言，Mac 自带的 Python 已经能够满足我们的需要了，因此很多同学在安装完 Python 之后，又想要将其删除，或者称之为卸载。对于删除 Python，我们首先要知道其具体都安装了什么，实际上，在安装 Python 时，其自动生成：

-   Python framework，即 Python 框架；
-   Python 应用目录；
-   指向 Python 的连接。

对于 Mac 自带的 Python，其框架目录为：

-   `System/Library/Frameworks/Python.framework`

而我们安装的 Python，其（默认）框架目录为：

-   `/Library/Frameworks/Python.framework`

接下来，我们就分别（在 Mac 终端进行）删除上面所提到的三部分。

**第 1 步，删除框架**：

-   `sudo rm -rf /Library/Frameworks/Python.framework/Versions/x.x`

**第 2步，删除应用目录**：

-   `sudo rm -rf "/Applications/Python x.x"`

**第 3 步，删除指向 Python 的连接**：

```bash
cd /usr/local/bin/
ls -l /usr/local/bin | grep '../Library/Frameworks/Python.framework/Versions/x.x' | awk '{print $9}' | tr -d @ | xargs rm
```

至此，我们已经成功删除 Python 的相关文件，其中`x.x`为 Python 的版本号。