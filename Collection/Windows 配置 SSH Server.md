---
title: Windows 配置 SSH Server
authors: Ethan Lin
year: 2024-07-07
tags:
  - 类型/笔记
  - 日期/2024-07-07
aliases:
  - Windows 配置 SSH Server
---
# MacOS 访问 Windows SSH Server 配置过程

## 安装 SSH Server



> 这里按照
> [这个博客](https://blog.csdn.net/tyustli/article/details/124151946)
>
> 或者
>
> [微软官方推荐的方法](https://learn.microsoft.com/zh-cn/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui)
>
> 安装 SSH Server

安装 SSH 主机

查看 SSH 状态

```powershell
Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
```

输出如下
```
Name  : OpenSSH.Client~~~~0.0.1.0
State : Installed

Name  : OpenSSH.Server~~~~0.0.1.0
State : Installed
```



安装 SSH 主机

```powershell
# Install the OpenSSH Client
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Install the OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

两者都会返回

```powershell
Path          :
Online        : True
RestartNeeded : False
```



## 配置 SSH



> 
>
> 这里用了百度的「文心一言」生成结果

在Windows 11上安装了SSH Client与SSH Server之后，要通过macOS的SSH访问该Windows 11系统，需要遵循一系列步骤来确保SSH服务正确配置，并且网络设置允许远程访问。以下是一个详细的步骤指南：

### 1. 确保Windows 11上的SSH Server已正确安装并启动

**安装SSH Server**：

- 打开Windows 11的“设置”应用。
- 选择“应用” -> “可选功能”。
- 点击“查看功能”按钮，搜索并选择“OpenSSH Server”，然后点击“安装”。

**启动SSH Server服务**：

- 打开PowerShell（以管理员身份）。
- 输入命令`Start-Service sshd`来启动SSH服务。
- （可选）设置SSH服务为开机自启：`Set-Service -Name sshd -StartupType 'Automatic'`。

### 2. 配置Windows 11的防火墙以允许SSH连接

- 在PowerShell中，输入以下命令来允许SSH服务的TCP 22端口通过防火墙：
  
    ```powershell
    netsh advfirewall firewall add rule name="OpenSSH-Server-In-TCP" dir=in action=allow protocol=TCP localport=22
    ```
    

### 3. 配置SSH Server（可选）

- SSH Server的配置文件通常位于`C:\ProgramData\ssh\sshd_config`。
- 使用文本编辑器（如Notepad++或Visual Studio Code，以管理员身份运行）打开此文件，并根据需要进行修改。例如，可以更改端口号、允许特定用户登录等。
- 修改后，保存文件并重启SSH服务以应用更改。

### 4. 在macOS上通过SSH连接到Windows 11

- 打开macOS的终端应用。
- 输入SSH连接命令，格式为`ssh 用户名@Windows11的IP地址`。例如，如果Windows 11的IP地址是`192.168.1.100`，且你要以`admin`用户身份登录，则命令为：
  
    ```bash
    ssh admin@192.168.1.100
    ```
    
- 如果Windows 11 SSH Server配置了不同的端口（非默认的22端口），则需要在IP地址后添加`-p 端口号`。例如，如果端口是2222，则命令为：
  
    ```bash
    ssh admin@192.168.1.100 -p 2222
    ```
    

### 5. 验证连接

- 如果一切设置正确，你将在macOS的终端中看到SSH连接的欢迎信息，并可能需要输入Windows 11用户的密码进行身份验证。
- 成功登录后，你就可以在macOS上通过SSH远程访问Windows 11系统了。

#### 注意事项

- 确保Windows 11系统和macOS设备都连接到了同一网络，或者通过VPN、端口转发等方式实现了网络互通。
- 如果在连接过程中遇到任何问题（如连接超时、权限拒绝等），请检查网络设置、防火墙规则、SSH Server配置以及用户权限等。
- 如果Windows 11系统位于NAT或防火墙之后，并且无法直接从外部网络访问，你可能需要配置端口转发或VPN来绕过这些限制。



### 6. 免密登录

1. 在客户端生成密钥对；
2. 在客户端的`~/.ssh`文件夹，打开 config 文件。在文件末尾追加以下内容：
```text
Host windowsserver
    HostName 【你的要访问的IP地址】
    User 【你的用户名】
    IdentityFile ~/.ssh/【你的私钥文件名称】
    PreferredAuthentications publickey
```
。
3. 将公钥文件分别复制到作为服务端的 Windows 设备的文件夹`C:\Users\【用户名】\.ssh`里，`C:\ProgramData\ssh`里。
4. 编辑作为服务端的 Windows 设备的文件夹`C:\ProgramData\ssh`的 `sshd_config` 文件（需要管理员权限。也可以编辑完之后保存到其他地方然后复制覆盖回来）。保证