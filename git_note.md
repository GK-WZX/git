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
