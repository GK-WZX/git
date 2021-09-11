# git笔记

## 初始化

1. 创建一个文件夹，进入该文件夹之下，执行以下命令将会把这个文件夹变成一个本地仓库并初始化。
	
	```shell
	git init
	```
2. 命令执行之后将会在该目录下生成一个隐藏文件夹`.git`，其中包含该仓库的信息文件。

## 设置签名

1. 形式
	* usrname:guoke
	* email:goodMorning@qq.com
2. 作用
	* 区分不同开发人员的身份
3. 辨析
	* 这里设置的签名和登录远程库（代码托管中心）的账号密码没有任何关系。：
4. 命令
	* 项目级别/仓库级别：仅在当前本地库范围内有效
		```shell
		git config user.name guoke
		git config user.email goodMorning@qq.com
		```
		* 信息可在`./.git/config`文件中查看
	* 系统用户级别：登录当前操作系统的用户范围（全局范围）
		```shell
		git config --global user.name guoke
		git config --global user.email goodMorning@qq.com
		```
		* 信息可在`~/.gitconfig`文件中查看
	* 级别优先级
		* 两者都有时：项目级别优先于系统用户级别
		* 只有其一时：使用存在的那个签名
		* 两个都没有时：不允许，git操作会出错。

## 基本操作

1. 状态查看操作
	* 命令
		```shell
		git status
		```
	* 作用
		* 查看工作区和暂存区的状态
2. 添加操作
	* 命令
		```shell
		git add [file name]
		```
	* 作用
		* 将工作区的“新建/修改”添加到暂存区
3. 提交操作
	* 命令
		```shell
		git commit -m "commit message" [file name]
		```
	* 作用
		* 将暂存区的内容提交到本地库
4. 查看历史记录
	1. `git log`
		* 多屏显示控制方式
			* 空格向下翻页
			* b 向上翻页
			* q 退出
	2. `git log --pretty=oneline`
	3. `git log --oneline`
	4. `git reflog`
		* HEAD@{移动到该版本需要的步数}
5. 前进后退
	1. 本质
		HEAD指针指向各个版本，版本的前进回退本质就是HEAD指针指向不同的版本。
	2. 基于索引值操作[推荐]
		```shell
		git reset --hard [局部索引值]
		```

	3. 使用^符号：只能后退
		```shell
		# 一个^符号代表后退一步，n个^表示后退n步
		git reset --hard HEAD^
		```

	4. 使用~符号：只能后退
		```shell
		# 后退n步
		git reset --hard HEAD~n
		```

6. reset命令三个参数命令对比
	* `--soft`参数
		* 仅仅在本地库移动HEAD指针
	* `--mixed`参数
		* 在本地库移动HEAD指针
		* 重置暂存区
	* `--merge`参数
		* 在本地库移动HEAD指针
		* 重置暂存区
		* 重置工作区

7. 删除文件并找回
	1. 删除文件并已经提交到本地库
		```shell
		# 直接会回退到删除前的版本号
		git reset --hard [索引值]
		```
	
	2. 删除文件并已经提交到暂存区
		```shell 
		# 用本地库的文件刷新暂存区和工作区内容
		git reset --hard HEAD
		```

	3. 删除文件但没有提交到暂存区和本地库
		```shell 
		# 用本地库的文件刷新暂存区和工作区内容
		git reset --hard HEAD
		```
