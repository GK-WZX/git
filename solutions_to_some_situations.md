# 一些情况的的处理

## 修改文件名或删除一个文件情况

* 问题：
	1. 重命名文件或删除文件之后，使用命令`git status`会显示
		1. `delete: 原文件名`
		2. `Untrack files: 新文件名`（如果是重命名文件）
* 解决：
	1. 方法一：
		* 执行命令`git rm <old file name>`将原跟踪文件删除
		* 正常提交即可
	2. 方法二：
		* 删除：`git rm <file name>`删除工作区和跟踪的文件，并提交的暂存区
		* 重命名：`git mv <old file name> <new file name>`修改文件名，并提交到暂存区

