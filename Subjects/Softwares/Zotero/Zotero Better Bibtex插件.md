# Zotero Better Bibtex插件

tags: #内容/办公 #内容/软件/Zotero #内容/科研管理 #类型/笔记 #发布/个人网站 


在使用Zotero插件Better Bibtex时，我使用自动导出bibtex文件与LaTex编辑器联动。关于cite key设置方面，目前觉得适合的几个可选设置如下：
- `[auth.auth.ea]_[year]_[Title:skipwords:clean:nopunctordash:select,1,3]`
	注解：
	- `[auth.auth.ea]`最多二作者，超过加ea字样；
	- `_`：下划线分隔；
	- `[year]`：年份；
	- `Title`：标题，且所有标题单词首字母大写。其中：
		- `skipwords`：忽略不重要单词，如The、Of等；
		- `clean`：清除不确定字符；
		- `nopunctordash`：删除标点符号与连接破折号；
		- `select,1,3`：仅使用从第一个单词开始的前三个单词，其余不作为cite key。
- `[auth.auth.ea]_[year]_[Title:skipwords:clean:nopunctordash]`
	注解：与上面设置项不同在于，标题使用所有单词。

此外，我选择了`jieba`分词选项，用于中文分词。

官方对于关键词之帮助参考：[Citation Keys :: Better BibTeX for Zotero](https://retorque.re/zotero-better-bibtex/citing/)
