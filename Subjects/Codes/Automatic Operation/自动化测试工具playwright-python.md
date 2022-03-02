[[Python]]
[[自动化测试]]


#资料 
#来源/转载 
#教程 

大家好，我是boy哥。

相信玩过爬虫的朋友都知道`selenium`，一个自动化测试的神器工具。写个`Python`自动化脚本解放双手基本上是常规的操作了，爬虫爬不了的，就用自动化测试凑一凑。

虽然`selenium`有完备的文档，但也需要一定的学习成本，对于一个纯小白来讲还是有些门槛的。

最近，微软开源了一个项目叫「`playwright-python`」，简直碉堡了！这个项目是针对`Python`语言的纯自动化工具，连代码都不用写，就能实现自动化功能。

![](https://pic1.zhimg.com/v2-93debcd9a93746fb10b1e74d8a0ae13c_b.jpg)

可能你会觉得有点不可思议，但它就是这么厉害。下面我们一起看下这个神器。

1\. Playwright介绍
----------------

`Playwright`是一个强大的Python库，仅用一个API即可自动执行`Chromium`、`Firefox`、`WebKit`等主流浏览器自动化操作，并同时支持以无头模式、有头模式运行。

Playwright提供的自动化技术是绿色的、功能强大、可靠且快速，支持`Linux`、`Mac`以及`Windows`操作系统。

  

![](https://pic4.zhimg.com/80/v2-81f3228d91e2c3b398c6474d1fafa60b_1440w.jpg)

2\. Playwright使用
----------------

### 安装

`Playwright`的安装非常简单，两步走。

```text
# 安装playwright库
pip install playwright

# 安装浏览器驱动文件（安装过程稍微有点慢）
python -m playwright install
```

上面两个pip操作分别安装：

-   安装Playwright依赖库，需要Python3.7+  
    
-   安装Chromium、Firefox、WebKit等浏览器的驱动文件  
    

### 录制

使用`Playwright`无需写一行代码，我们只需手动操作浏览器，它会录制我们的操作，然后自动生成代码脚本。

下面就是录制的命令`codegen`，仅仅一行。

```text
# 命令行键入 --help 可看到所有选项
python -m playwright codegen
```

`codegen`的用法可以使用`--help`查看，如果简单使用就是直接在命令后面加上url链接，如果有其他需要可以添加`options`。

```python3
python -m playwright codegen --help
Usage: index codegen [options] [url]

open page and generate code for user actions

Options:
  -o, --output <file name>  saves the generated script to a file
  --target <language>       language to use, one of javascript, python, python-async, csharp (default: "python")
  -h, --help                display help for command

Examples:

  $ codegen
  $ codegen --target=python
  $ -b webkit codegen https://example.com
```

options含义：

-   \-o：将录制的脚本保存到一个文件  
    
-   \--target：规定生成脚本的语言，有`JS`和`Python`两种，默认为Python  
    
-   \-b：指定浏览器驱动

比如，我要在`baidu.com`搜索，用`chromium`驱动，将结果保存为`my.py`的`python`文件。

```python3
python -m playwright codegen --target python -o 'my.py' -b chromium https://www.baidu.com
```

命令行输入后会自动打开浏览器，然后可以看见在浏览器上的一举一动都会被自动翻译成代码，如下所示。

![](https://pic2.zhimg.com/v2-2e4a3d1766b77c3374baeb95ac0429f1_b.jpg)

结束后自动关闭浏览器，保存生成的自动化脚本到py文件。

```python3
from playwright import sync_playwright

def run(playwright):
    browser = playwright.chromium.launch(headless=False)
    context = browser.newContext()

    # Open new page
    page = context.newPage()

    page.goto("https://www.baidu.com/")

    page.click("input[name=\"wd\"]")

    page.fill("input[name=\"wd\"]", "jingdong")

    page.click("text=\"京东\"")

    # Click //a[normalize-space(.)='京东JD.COM官网 多快好省 只为品质生活']
    with page.expect_navigation():
        with page.expect_popup() as popup_info:
            page.click("//a[normalize-space(.)='京东JD.COM官网 多快好省 只为品质生活']")
        page1 = popup_info.value
    # ---------------------
    context.close()
    browser.close()

with sync_playwright() as playwright:
    run(playwright)
```

此外，`playwright`还提供了同步和异步的API接口，文档如下。

> 链接：[https://microsoft.github.io/playwright-python/index.html](https://link.zhihu.com/?target=https%3A//microsoft.github.io/playwright-python/index.html)

### 同步

下面示例代码：依次打开三个浏览器，前往baidu搜索，截图后退出。

```python3
from playwright import sync_playwright

with sync_playwright() as p:
    for browser_type in [p.chromium, p.firefox, p.webkit]:
        browser = browser_type.launch()
        page = browser.newPage()
        page.goto('https://baidu.com/')
        page.screenshot(path=f'example-{browser_type.name}.png')
        browser.close()
```

### 异步

异步操作可结合`asyncio`同时进行三个浏览器操作。

```python3
import asyncio
from playwright import async_playwright

async def main():
    async with async_playwright() as p:
        for browser_type in [p.chromium, p.firefox, p.webkit]:
            browser = await browser_type.launch()
            page = await browser.newPage()
            await page.goto('http://baidu.com/')
            await page.screenshot(path=f'example-{browser_type.name}.png')
            await browser.close()

asyncio.get_event_loop().run_until_complete(main())
```

### 移动端

更厉害的是，`playwright`还可支持移动端的浏览器模拟。 下面是官方文档提供的一段代码，模拟在给定地理位置上手机`iphone 11 pro`上的`Safari`浏览器，首先导航到`maps.google.com`，然后执行定位并截图。

```python3
from playwright import sync_playwright

with sync_playwright() as p:
    iphone_11 = p.devices['iPhone 11 Pro']
    browser = p.webkit.launch(headless=False)
    context = browser.newContext(
        **iphone_11,
        locale='en-US',
        geolocation={ 'longitude': 12.492507, 'latitude': 41.889938 },
        permissions=['geolocation']
    )
    page = context.newPage()
    page.goto('https://maps.google.com')
    page.click('text="Your location"')
    page.screenshot(path='colosseum-iphone.png')
    browser.close()
```

另外，还可以配合`pytest`插件一起使用，感兴趣可以自己试一下。

3\. 总结
------

`playwright`相比已有的自动化测试工具有很多优势，比如： 

-   跨浏览器，支持Chromium、Firefox、WebKit 
-   跨操作系统，支持Linux、Mac、Windows 
-   可提供录制生成代码功能，解放双手 
-   可用于移动端

目前存在的缺点就是生态和文档还不是非常完备，比如没有API中文文档、没有较好的教程和示例供学习。不过相信，随着知道的人越来越多，未来会越来越好。

> GitHub链接：[https://github.com/microsoft/playwright-python](https://link.zhihu.com/?target=https%3A//github.com/microsoft/playwright-python)  
> 开源组织：Microsoft

**原创不易，欢迎点赞、在看、分享。**

**开源项目精选，关注我的原创公众号：GitHuboy**