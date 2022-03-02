#来源/转载 
#笔记 

[[MATLAB]]
[[部署环境]]

1. 如果已经用校园认证的激活程序或者序列号激活过的话，在卸载之前，需要先“反激活，（官网指南里要求这个步骤，可能是考虑到有些许可证是限制激活设备总数吧）
2. 反激活之后，先直接从应用程序中把 MATLAB 的文件夹整个删除（2018 以上的版本应该是/ Polyspace，日版本是/ Mathworks 文件夹）;
3. 删除应用程序后，还有部分缓存、配置之类琐碎文件，如果以后不再安装 MATLAB，想彻底清理干净，可以按这个 list 逐一排查：
```bash
~/Library/Application Support
~/Library/Caches
~/Library/Containers
~/Library/Cookies
~/Library/Launchagents
~/Library/Logs
~/Library/Preferences
~/Library/Preferencepanes
```