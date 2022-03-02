Jupyter 默认浏览器调整

在文件jupyter_notebook_config.py中，找到

```bash
## Specify what command to use to invoke a web browser when opening the notebook.
#  If not specified, the default browser will be determined by the `webbrowser`
#  standard library module, which allows setting of the BROWSER environment
#  variable to override it.

#c.NotebookApp.browser = ''
```

添加如下代码，将浏览器设为chrome：

```bash
import webbrowser
webbrowser.register('chrome', None, webbrowser.GenericBrowser(u'C:/Program Files (x86)/Google/Chrome/Application/chrome.exe'))
c.NotebookApp.browser = 'chrome'
```

————————————————
版权声明：本文为CSDN博主「luckywizard」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/luckywizard/article/details/102655407