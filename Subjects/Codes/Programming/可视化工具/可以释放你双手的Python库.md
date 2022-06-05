#来源/转载 #资料 

[[Python]]
[[GUI]]
[[PyAutoGUI]]

# 可以释放你双手的Python库
===============

[![mars](https://pic1.zhimg.com/v2-5fa2e3417dc7a7ddf297e658fcd48f57_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/mars-15-29)

[mars](https://www.zhihu.com/people/mars-15-29)

爱运动、爱读书的技术狗。

​关注他

575 人赞同了该文章
PyAutoGUI库
----------

**你想彻底释放双手，让电脑帮你完成鼠标操作和键盘操作？**

**让电脑帮你完成GUI的自动任务？**

那本文就是为你量身打造的，实现办公自动化的Python程序库。

本文中所有代码全部经过验证，使用的开发环境是Python 3.8。

PyAutoGUI是一个跨平台GUI自动化Python模块。用于以编程方式控制鼠标和键盘。

本文按照如下顺序进行组织：

1.  安装
2.  鼠标控制功能
3.  键盘功能功能

1.安装
----

在Windows平台上， 在cmd命令窗口中输入：

```python
>>>pip install pyautogui
```

pyautogui会自动安装它依赖的模块，包括PyTweening，PyScreeze，PyGetWindow，PymsgBox和MouseInfo。

安装完毕后，调用如下语句，不会报错。

```python
>>> import pyautogui
```

2\. 鼠标控制功能
----------

这一小节按照如下的顺序进行展开。

-   屏幕和鼠标位置
-   鼠标移动
-   鼠标拖拽
-   鼠标点击

**2.1 屏幕和鼠标位置**
---------------

在介绍鼠标控制功能前，首先介绍屏幕和鼠标位置，**因为鼠标的控制功能都是基于屏幕像素点进行的。**

我们的屏幕是由很多像素点组成的。以我的显示器为例进行说明。我的显示分辨率是1920×1080，左上角就是（0，0），右下角就是（1919，1079），x轴坐标按照从左往右的顺序递增，y轴坐标按照从上往下的顺序递增。

```text
0,0       X 增加 -->
+---------------------------+
|                           | Y 增加
|                           |     |
|   1920 x 1080 screen      |     |
|                           |     V
|                           |
|                           |
+---------------------------+ 1919, 1079
```

屏幕分辨率大小由size()函数作为两个整数的元组返回，当前鼠标位置可以通过position()函数返回。

```python
>>> pyautogui.size()
Size(width=1920, height=1080)
>>> pyautogui.position()
Point(x=897, y=309)
```

要检查X，Y坐标是否在屏幕上，可以调用onScreen()函数。

```python
>>> pyautogui.onScreen(0,0)
True
>>> pyautogui.onScreen(1920,1080)
False
>>> pyautogui.onScreen(1919,1079)
True
```

2.2 鼠标移动
--------

鼠标移动的方法包括两种：绝对坐标和相对坐标。

使用moveTo()函数，会将鼠标光标移至你传递的X和Y整数坐标，即移动到绝对坐标位置

```python
# 将鼠标光标移动到(200,300)
>>> pyautogui.moveTo(200,300)
# 将鼠标光标移动到(400,500)
>>> pyautogui.moveTo(400,500)
```

使用move()函数，会将鼠标光标移动到相对于当前位置的像素点上，即移动到相对坐标位置。

```python
# 将鼠标光标左移100个像素点
>>> pyautogui.move(-100,0)
# 将鼠标光标右移100个像素点
>>> pyautogui.move(100,0)
# 将鼠标光标上移200个像素点
>>> pyautogui.move(0,-200)
# 将鼠标光标下移200个像素点
>>> pyautogui.move(0,200)
```

除了可以设置鼠标光标位置，还可以设置持续时间和缓动功能，这两个参数使鼠标移动更有趣。这两个参数可以控制鼠标移动到目的地的时间和速度。正常情况下，鼠标是以恒定的速度向目的地移动。第3个参数是控制持续时间（单位秒），第4个参数是控制移动节奏，在持续时间不变的情况下，不同位置的移动速度不一样。

```python
pyautogui.easeInQuad        #开始慢，结束快
pyautogui.easeOutQuad       #开始块，结束慢
pyautogui.easeInOutQuad     #开始块，结束块，中间慢
pyautogui.easeInBounce      #结束时反弹
pyautogui.easeInElastic     #结束时是橡皮筋
```

参考下面的例子。

```python
# 将当前鼠标光标移动到位置(400,500),持续时间是2秒，移动开始慢，结束时快
>>> pyautogui.moveTo(400,500,2,pyautogui.easeInOutQuad)
# 将当前鼠标光标向右移动400个像素点，持续时间是2秒，移动开始块，结束时慢
>>> pyautogui.move(400,0,2,pyautogui.easeOutQuad)
```

2.3 鼠标拖拽
--------

鼠标拖拽的方式包括两种：绝对坐标和相对坐标。

使用dragTo()函数和drag()函数可以实现鼠标拖拽功能。dragTo()函数使用绝对坐标，将当前鼠标光标选中的东西移动到指定的光标位置；drag()函数使用相对坐标，将当前鼠标光标选中的东西移动到相对于当前位置的像素点上，即移动到相对坐标位置。

除了之外，它们还有一个参数button，这个参数可以被设置成‘left’，‘middle’，‘right’，表示在拖拽的过程中按下哪个鼠标键。

```python
# 将当前光标位置的东西移动到(100,200)处，在拖动的过程中按住鼠标左键。
>>> pyautogui.dragTo(100,200,button='left')
# 将当前光标位置的东西向下移动100个像素点，在拖动的过程中按住鼠标左键。
>>> pyautogui.drag(100,0,button='left')
```

鼠标拖拽具有和鼠标移动一样的参数。第3个参数和第4个参数的作用和鼠标移动的参数效果一样。参考下面的例子。例子的效果如GIF所示。

```python
# 将当前光标位置的东西向右移动400个像素点，持续时间2秒，开始快，结束慢。
>>> pyautogui.drag(400,0,2,pyautogui.easeOutQuad)
```

![](https://pic3.zhimg.com/v2-ad596ed5a134ca40b867885a17d37fce_b.jpg)

2.4 鼠标点击
--------

通过调用click()函数可以模拟鼠标在当前位置单击鼠标左键，”点击“的定义是按下按钮后将其释放。

```python
>>> pyautogui.click()
```

除了在当前位置点击，还可以点击指定的坐标位置。在click()函数中传入X坐标和Y坐标。

```python
>>> pyautogui.click(100,300)
```

鼠标点击默认使用鼠标左键，也可以通过传递参数，指定使用那个鼠标键。参数包括'left'，‘middle’， ‘right’。

```python
# 用鼠标左键，点击（100，300)的位置
>>> pyautogui.click(100,300,button='right')
# 用鼠标右键，点击当前位置
>>> pyautogui.click(button='middle')
```

click默认点击一次，如果要实现多次点击，可以将整数传递给clicks参数，还可以将整数或浮点数设置给interval参数，以指定两次点击之间的暂停时间（以秒为单位）。

```python
# 用鼠标左键点击2次，间隔时间0.25秒
>>> pyautogui.click(clicks=2,interval=0.25)
```

3 键盘控制功能
--------

键盘控制功能包括输入字符串、按下键盘上的键、热键。

3.1 输入字符串
---------

输入字符串使用的是write()函数。

```python3
>>> pyautogui.write("Hello World!")
```

3.2 模拟按键
--------

模拟按键使用的press()函数、keyDown()、keyUp()函数。

调用press()函数，从它传递一个字符串pyautogui.KEYBOARD\_KEYS，例如enter、f1、esc等等。

```python3
>>> pyautogui.press('f11')
```

下表是KEYBOARD\_KEYS，这些参数可以传递给press()函数，和接下来要介绍的keyDown()，keyUp()和hotKey()函数。

```python
['\t', '\n', '\r', ' ', '!', '"', '#', '$', '%', '&', "'", '(',
')', '*', '+', ',', '-', '.', '/', '0', '1', '2', '3', '4', '5', '6', '7',
'8', '9', ':', ';', '<', '=', '>', '?', '@', '[', '\\', ']', '^', '_', '`',
'a', 'b', 'c', 'd', 'e','f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o',
'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', '{', '|', '}', '~',
'accept', 'add', 'alt', 'altleft', 'altright', 'apps', 'backspace',
'browserback', 'browserfavorites', 'browserforward', 'browserhome',
'browserrefresh', 'browsersearch', 'browserstop', 'capslock', 'clear',
'convert', 'ctrl', 'ctrlleft', 'ctrlright', 'decimal', 'del', 'delete',
'divide', 'down', 'end', 'enter', 'esc', 'escape', 'execute', 'f1', 'f10',
'f11', 'f12', 'f13', 'f14', 'f15', 'f16', 'f17', 'f18', 'f19', 'f2', 'f20',
'f21', 'f22', 'f23', 'f24', 'f3', 'f4', 'f5', 'f6', 'f7', 'f8', 'f9',
'final', 'fn', 'hanguel', 'hangul', 'hanja', 'help', 'home', 'insert', 'junja',
'kana', 'kanji', 'launchapp1', 'launchapp2', 'launchmail',
'launchmediaselect', 'left', 'modechange', 'multiply', 'nexttrack',
'nonconvert', 'num0', 'num1', 'num2', 'num3', 'num4', 'num5', 'num6',
'num7', 'num8', 'num9', 'numlock', 'pagedown', 'pageup', 'pause', 'pgdn',
'pgup', 'playpause', 'prevtrack', 'print', 'printscreen', 'prntscrn',
'prtsc', 'prtscr', 'return', 'right', 'scrolllock', 'select', 'separator',
'shift', 'shiftleft', 'shiftright', 'sleep', 'space', 'stop', 'subtract', 'tab',
'up', 'volumedown', 'volumemute', 'volumeup', 'win', 'winleft', 'winright', 'yen',
'command', 'option', 'optionleft', 'optionright']
```

press()函数实际上是模拟按下一个键，然后释放它，其实就是keyDown()和keyUp()函数的包装。这些函数可以自己调用。

```python
import pyautogui

pyautogui.keyDown('ctrl')
pyautogui.keyDown('shift')
pyautogui.keyUp('shift')
pyautogui.keyUp('ctrl')
```

调用结果就是，输入法切换成功。

3.3 热键
------

为了方便快捷地按下热键或键盘快捷键，`hotkey()`可以传递几个键字符串，这些字符串将按顺序按下，然后以相反的顺序释放。

3.2节中的切换输入法，可以输入如下代码：

```text
pyautogui.hotkey('ctrl', 'shift')
```

---

学习python基础很重要，这里推荐几本书供大家学习。

[

![](https://pic2.zhimg.com/v2-db17951a4131d0c37d29365825aca4fd_hd.jpg)

Python编程 从入门到实践 第2版(图灵出品)

京东

¥ 74.50

去购买​









](https://union-click.jd.com/jdc?e=jdext-1312277645061799936-0&p=AyIGZRhfFwQbAVAfUhYyEgddE1kVABc3EUQDS10iXhBeGlcJDBkNXg9JHUlSSkkFSRwSB10TWRUAFxgMXgdIMktHIXsNflxMZxdPOEgAUV0XcjJMQkQLWStbHAIQD1QaWxIBIgdUGlsRBxEEUxprJQIXNwd1g6O0yqLkB4%2B%2FjcePwitaJQIVBlEcXxUAFAdRElIlAhoDZc31gdeauIyr%2FsOovNLYq46cqca50ytrJQEiXABPElAeEgVVGFgTBBUCURpcFQQaD10ZXAkDIgdUGlkRBRcAVx41EAITBlQcXRICGmlXGloXAxEBVRpaJQIiBGVFNRRREQ8BEgkUbEheCUAORlURaVESUxIHFQBRK1kUAxAF)

[

![](https://pic2.zhimg.com/v2-267521ff9d1f687bdc6f8d1d686d184b_hd.jpg)

零基础学Python（全彩版）Python3.8 全新升级

京东

¥ 69.80

去购买​









](https://union-click.jd.com/jdc?e=jdext-1312278445368135680-0&p=AyIGZRhfFwQbAVAfUhYyEgRXH1kdAhY3EUQDS10iXhBeGlcJDBkNXg9JHUlSSkkFSRwSBFcfWR0CFhgMXgdIMhV7F1ojEHtJZyocOm8KEHoebAVUdEQLWStbHAIQD1QaWxIBIgdUGlsRBxEEUxprJQIXNwd1g6O0yqLkB4%2B%2FjcePwitaJQIVBlEcXxUGFQRXElIlAhoDZc31gdeauIyr%2FsOovNLYq46cqca50ytrJQEiXABPElAeEgVVGFgTCxcCURlcHAIQA1ISWgkDIgdUGlkRBRcAVx41EAITBlQcXRICGmlXGloXAxEBVRpaJQIiBGVFNRRREVQCH1IcbEheCUACQV0VaVESUxMGGgddK1kUAxAF)

编辑于 11-18