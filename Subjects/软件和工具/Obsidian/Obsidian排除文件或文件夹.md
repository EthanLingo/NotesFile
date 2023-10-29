# Obsidian排除文件或文件夹
Files and directories are only considered for synchronization if they pass all filter rules: They have to match **at least one** entry in the include list and **none** of the entries in the exclude list as presented in the filter configuration dialog.   
 

-   Each list item must be a file or directory path **relative** to the selected base directories.
-   Multiple items must be separated by **|** or a **new line**.
-   Wild cards ***** and **?** may be used: ***** means zero or more characters while **?** represents exactly one character.
-   File matching is **case-insensitive**

  

#解决 
tags: #内容/Obsidian 


### Example: Match items of a folder pair

_The following filter phrases assume a folder pair C:\\Source <-> D:\\Target and can be used for the include as well as exclude filter._   
 

Filter description

Filter phrase

Single file C:\\Source**\\file.txt**

`\file.txt`

Single folder C:\\Source**\\SubFolder**

`\SubFolder\`

All files (and folders) named **thumbs.db**

`*\\thumbs.db`

All files (and folders) starting with the **Z** character

`*\\z*`

All ***.tmp** files located in C:\\Source\\**SubFolder**

`\SubFolder\*.tmp`

Files and folders containing **temp** somewhere in their path

`*temp*`

Multiple entries separated by vertical bar

`*.tmp | *.doc | *.bak`

All subdirectories of the base directories

`*\`

***.txt** files located in subdirectories of base directories

`\*\*.txt`

  

### Example: Exclude a sub folder except for certain files

Set up **two folder pairs** with the same source and target paths but with **distinct local filters**:  
Folder pair 1: `_local exclude_ filter \SubFolder\`
Folder pair 2: `_local include_ filter \SubFolder\*.txt`