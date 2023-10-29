
# 卸载 Visual Studio for Mac


---
title: 卸载 Visual Studio for Mac
authors: Ethan Lin
year:
tags:
  - 日期/2022-09-26 
  - 类型/笔记 
  - 来源/转载
---



适用范围：![yes](https://learn.microsoft.com/zh-cn/visualstudio/mac/media/yes-icon.png?view=vsmac-2022)Visual Studio for Mac ![no](https://learn.microsoft.com/zh-cn/visualstudio/mac/media/no-icon.png?view=vsmac-2022)Visual Studio

可使用此指南通过导航到相关部分来单独卸载 Visual Studio for Mac 中的每个组件。 建议使用[卸载脚本](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-scripts)部分提供的脚本来卸载所有内容。

本文适用于 Visual Studio for Mac。 如果要查找有关 VS Code 的信息，请参阅 [Visual Studio Code 设置](https://code.visualstudio.com/docs/setup/setup-overview)。

 备注

我们想详细了解你为何要卸载 Visual Studio for Mac，便于我们进行改进。 请花几分钟的时间[分享你的反馈](https://aka.ms/vs/mac/uninstallsurvey)。 谢谢！

## [卸载脚本](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-scripts)

[[卸载 Visual Studio for Mac#终极卸载脚本：]]


可使用两个脚本来卸载计算机上的 Visual Studio for Mac 以及所有组件：

-   [Visual Studio 和 Xamarin 脚本](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#visual-studio-for-mac-and-xamarin-script)
-   [.NET Core 脚本](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#net-core-script)

以下部分提供有关下载和使用脚本的信息。

### [Visual Studio for Mac 和 Xamarin 脚本](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#visual-studio-for-mac-and-xamarin-script)

可通过使用[卸载脚本](https://raw.githubusercontent.com/MicrosoftDocs/visualstudio-docs/master/mac/resources/uninstall-vsmac.sh)一次性卸载 Visual Studio 和 Xamarin 组件。

卸载脚本中包含本文中出现的大部分命令。 由于可能存在外部依赖项，因此脚本中省略了三个主要部分。 要删除此内容，请跳转到下面的相关部分，并手动删除：

-   **[卸载 Mono](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-mono-sdk-mdk)**
-   **[卸载 Android AVD](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-android-avd)**
-   **[卸载 Android SDK 和 Java SDK](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-android-sdk-and-java-sdk)**

要运行脚本，请执行以下步骤：

1.  右键单击脚本并选择“另存为”以在 Mac 上保存文件。
    
2.  打开“终端”，并将工作目录更改为下载脚本的位置：
    
    Bash复制
    
    ```
    cd /location/of/file
    ```
    
3.  使脚本可执行，并通过 sudo 运行它：
    
    Bash复制
    
    ```
    chmod +x ./uninstall-vsmac.sh
    sudo ./uninstall-vsmac.sh
    ```
    
4.  最后，删除卸载脚本，并删除停靠位置中的 Visual Studio for Mac（如果有）。
    

### [.NET Core 脚本](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#net-core-script)

.NET Core 的卸载脚本位于 [dotnet cli 存储库](https://raw.githubusercontent.com/dotnet/cli/master/scripts/obtain/uninstall/dotnet-uninstall-pkgs.sh)

要运行脚本，请执行以下步骤：

1.  右键单击脚本并选择“另存为”以在 Mac 上保存文件。
    
2.  打开“终端”，并将工作目录更改为下载脚本的位置：
    
    Bash复制
    
    ```
    cd /location/of/file
    ```
    
3.  使脚本可执行，并通过 sudo 运行：
    
    Bash复制
    
    ```
    chmod +x ./dotnet-uninstall-pkgs.sh
    sudo ./dotnet-uninstall-pkgs.sh
    ```
    
4.  最后，删除 .NET Core 卸载脚本。
    

## [手动删除 Visual Studio for Mac](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#manually-removing-visual-studio-for-mac)

如果想要手动删除 Visual Studio for Mac 及其依赖项（而不是使用上一部分的脚本），请遵循本部分总结的步骤。

从 Mac 中卸载 Visual Studio 的第一步是在“应用程序”目录中找到 Visual Studio 应用，并将其拖动到回收站。 或者，控件单击并选择“移到回收站”，如下图所示：

![Screenshot showing how to uninstall Visual Studio for Mac application.](https://learn.microsoft.com/zh-cn/visualstudio/mac/media/vsmac-2022/move-vsmac-application-to-trash.png?view=vsmac-2022)

删除此应用捆绑包会删除 Visual Studio for Mac，但文件系统上可能仍有其他文件（例如 Xamarin SDK、.NET SDK 或 iOS 开发工具）。

要删除 Visual Studio for Mac 的所有痕迹，请在终端运行以下命令：

Bash复制

```
sudo rm -rf "/Applications/Visual Studio.app"
rm -rf ~/Library/Caches/VisualStudio
rm -rf ~/Library/Preferences/VisualStudio
rm -rf ~/Library/Preferences/Visual\ Studio
rm -rf ~/Library/Logs/VisualStudio
rm -rf ~/Library/VisualStudio
rm -rf ~/Library/Preferences/Xamarin/
rm -rf ~/Library/Application\ Support/VisualStudio
```

可能还要删除以下包含各种 Xamarin 文件和文件夹的目录。 但是，此目录包括 Android 签名密钥。 有关详细信息，请参阅[卸载 Android SDK 和 Java SDK](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-android-sdk-and-java-sdk) 部分：

Bash复制

```
rm -rf ~/Library/Developer/Xamarin
```

## [卸载 Mono SDK (MDK)](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-mono-sdk-mdk)

Mono 是 Microsoft .NET Framework 的开放源代码实现，可供所有 Xamarin 产品（Xamarin.iOS、Xamarin.Android 和 Xamarin.Mac）使用，让用户能使用 C# 开发这些平台。

 警告

除 Visual Studio for Mac 之外，还有其他应用程序使用 Mono，例如 Unity。 卸载 Mono 前，请确保 Mono 上没有其他依赖项。

若要从计算机删除 Mono Framework，请在终端运行以下命令：

Bash复制

```
sudo rm -rf /Library/Frameworks/Mono.framework
sudo pkgutil --forget com.xamarin.mono-MDK.pkg
sudo rm -rf /etc/paths.d/mono-commands
```

## [卸载 Xamarin.Android](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-xamarinandroid)

安装和使用 Xamarin.Android 时需要许多必备项，例如 Android SDK 和 Java SDK。

使用以下命令删除 Xamarin.Android：

Bash复制

```
sudo rm -rf /Developer/MonoDroid
rm -rf ~/Library/MonoAndroid
sudo pkgutil --forget com.xamarin.android.pkg
sudo rm -rf /Library/Frameworks/Xamarin.Android.framework
```

### [卸载 Android SDK 和 Java SDK](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-android-sdk-and-java-sdk)

开发 Android 应用程序需要 Android SDK。 要完全删除 Android SDK 的所有部分，请在 ~/Library/Developer/Xamarin/ 中找到相关文件，并将其移到回收站 。

 警告

请注意，Visual Studio for Mac 生成的 Android 签名密钥位于 `~/Library/Developer/Xamarin/Keystore` 中。 请务必适当备份，或避免在要保留密钥存储时删除此目录。

不必卸载 Java SDK (JDK)，因为它已预先打包为 Mac OS X/macOS 的一部分。

### [卸载 Android AVD](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-android-avd)

 警告

除 Visual Studio for Mac 之外，还有其他应用程序使用 Android AVD 和这些附加 Android 组件，如 Android Studio。 删除此目录可能会导致 Android Studio 中的项目中断。

要删除任何 Android AVD 和其他 Android 组件，请使用以下命令：

Bash复制

```
rm -rf ~/.android
```

要仅删除 Android AVD，请使用以下命令：

Bash复制

```
rm -rf ~/.android/avd
```

## [卸载 Xamarin.iOS](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-xamarinios)

Xamarin.iOS 支持使用 C# 或 F# 通过 Visual Studio for Mac 开发 iOS 应用程序。

在终端使用以下命令从文件系统删除所有 Xamarin.iOS 文件：

Bash复制

```
rm -rf ~/Library/MonoTouch
sudo rm -rf /Library/Frameworks/Xamarin.iOS.framework
sudo rm -rf /Developer/MonoTouch
sudo pkgutil --forget com.xamarin.monotouch.pkg
sudo pkgutil --forget com.xamarin.xamarin-ios-build-host.pkg
sudo pkgutil --forget com.xamarin.xamarin.ios.pkg
```

## [卸载 Xamarin.Mac](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-xamarinmac)

可使用以下两个命令分别删除 Mac 上的产品和许可证，进而从计算机上删除 Xamarin.Mac：

Bash复制

```
sudo rm -rf /Library/Frameworks/Xamarin.Mac.framework
rm -rf ~/Library/Xamarin.Mac
```

## [卸载工作簿和检查器](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-workbooks-and-inspector)

从版本 1.2.2 开始，可通过在终端中运行以下命令卸载 Xamarin Workbooks 和 Inspector：

Bash复制

```
sudo /Library/Frameworks/Xamarin.Interactive.framework/Versions/Current/uninstall
```

需要在旧版本手动删除以下项目：

-   在 `"/Applications/Xamarin Workbooks.app"` 删除 Workbooks 应用
-   在 `"Applications/Xamarin Inspector.app"` 删除 Inspector 应用
-   删除加载项：`"~/Library/Application Support/XamarinStudio-6.0/LocalInstall/Addins/Xamarin.Interactive"` 和 `"~/Library/Application Support/XamarinStudio-6.0/LocalInstall/Addins/Xamarin.Inspector"`
-   在 `/Library/Frameworks/Xamarin.Interactive.framework` 和 `/Library/Frameworks/Xamarin.Inspector.framework` 删除 Inspector 和支持文件

## [卸载 Xamarin Profiler](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-the-xamarin-profiler)

Bash复制

```
sudo rm -rf "/Applications/Xamarin Profiler.app"
```

## [卸载 Visual Studio 安装程序](https://learn.microsoft.com/zh-cn/visualstudio/mac/uninstall?view=vsmac-2022#uninstall-the-visual-studio-installer)

使用以下命令删除 Xamarin 通用安装程序的所有痕迹：

Bash复制

```
rm -rf ~/Library/Caches/XamarinInstaller/
rm -rf ~/Library/Caches/VisualStudioInstaller/
rm -rf ~/Library/Logs/XamarinInstaller/
rm -rf ~/Library/Logs/VisualStudioInstaller/
rm -rf ~/Library/Preferences/Xamarin/
rm -rf "~/Library/Preferences/Visual Studio/"
```

---



# 终极卸载脚本：

```shell
#!/bin/sh

# Uninstall Visual Studio for Mac
echo "Uninstalling Visual Studio for Mac..."

sudo rm -rf "/Applications/Visual Studio.app"
rm -rf ~/Library/Caches/VisualStudio
rm -rf ~/Library/Preferences/VisualStudio
rm -rf ~/Library/Preferences/Visual\ Studio
rm -rf ~/Library/Logs/VisualStudio
rm -rf ~/Library/VisualStudio
rm -rf ~/Library/Preferences/Xamarin/
rm -rf ~/Library/Application\ Support/VisualStudio
rm -rf ~/Library/Application\ Support/VisualStudio/7.0/LocalInstall/Addins/

# Uninstall Xamarin.Android
echo "Uninstalling Xamarin.Android..."

sudo rm -rf /Developer/MonoDroid
rm -rf ~/Library/MonoAndroid
sudo pkgutil --forget com.xamarin.android.pkg
sudo rm -rf /Library/Frameworks/Xamarin.Android.framework


# Uninstall Xamarin.iOS
echo "Uninstalling Xamarin.iOS..."

rm -rf ~/Library/MonoTouch
sudo rm -rf /Library/Frameworks/Xamarin.iOS.framework
sudo rm -rf /Developer/MonoTouch
sudo pkgutil --forget com.xamarin.monotouch.pkg
sudo pkgutil --forget com.xamarin.xamarin-ios-build-host.pkg


# Uninstall Xamarin.Mac
echo "Uninstalling Xamarin.Mac..."

sudo rm -rf /Library/Frameworks/Xamarin.Mac.framework
rm -rf ~/Library/Xamarin.Mac


# Uninstall Workbooks and Inspector
echo "Uninstalling Workbooks and Inspector..."

if [ -f "/Library/Frameworks/Xamarin.Interactive.framework/Versions/Current/uninstall" ]; then
    sudo /Library/Frameworks/Xamarin.Interactive.framework/Versions/Current/uninstall
fi


# Uninstall the Visual Studio for Mac Installer
echo "Uninstalling the Visual Studio for Mac Installer..."

rm -rf ~/Library/Caches/XamarinInstaller/
rm -rf ~/Library/Caches/VisualStudioInstaller/
rm -rf ~/Library/Logs/XamarinInstaller/
rm -rf ~/Library/Logs/VisualStudioInstaller/

# Uninstall the Xamarin Profiler
echo "Uninstalling the Xamarin Profiler..."

sudo rm -rf "/Applications/Xamarin Profiler.app"

echo "Finished Uninstallation process."
```