如果是使用deepin系统的应用商店安装的项目会自动创建快捷方式,但是自己安装的有些程序不会自动添加,所以需要手动添加.

## 一、进入/usr/share/applications

applications目录下保存了所有的快捷方式，可以仿照系统已有的快捷方式创建一个。

## 二、使用root权限添加一个.desktop后缀的文件

使用root权限添加一个".desktop"后缀的文件，如"deepin-editor.desktop"，编辑内容如下：

```text
[Desktop Entry]
Categories=Utility;TextEditor;
Comment=Simple and easy to use text editor
Exec=deepin-editor %F
GenericName=Text Editor
Icon=deepin-editor
MimeType=text/english;text/plain;text/x-makefile;text/x-c++hdr;text/x-c++src;text/x-chdr;text/x-csrc;text/x-java;text/x-moc;text/x-pascal;text/x-tcl;text/x-tex;application/x-shellscript;text/x-patch;text/x-adasrc;text/x-chdr;text/x-csrc;text/css;application/x-desktop;text/x-patch;text/x-fortran;text/html;text/x-java;text/x-tex;text/x-makefile;text/x-objcsrc;text/x-pascal;application/x-perl;application/x-perl;application/x-php;text/vnd.wap.wml;text/x-python;application/x-ruby;text/sgml;application/xml;model/vrml;image/svg+xml;application/json;
Name=Text Editor
StartupNotify=false
Type=Application
```

其中参数：

Categories：该应用程序的分类，系统会按照该参数对应用分组；

Comment：概要介绍

**Exec：启动脚本，可以附加参数**

GenericName：通用名，暂不知具体用途

Icon：图标对应的路径，图标支持 png 格式、svg 格式等，图标的推荐尺寸为 128x128

MimeType：关联的文件类型

**Name：显示名称**

StartupNotify：启动通知，暂不知具体用途

**Type：包括 3 种类型：Application、Link、Directory**

## **三、保存退出后，即可看到添加的快捷方式**

发布于 2020-09-05