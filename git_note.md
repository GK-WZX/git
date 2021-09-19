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

8. 比较文件差异
	1. `git diff [文件名]`
		* 比较工作区和暂存区中该文件的差异
	2. `git diff [本地库中的历史版本] [文件名]`
		* 比较工作区和历史版本中该文件的差异
	3. 不指定文件名的情况下，将比较所有文件

## 分支管理

1. 什么是分支？
	* 在版本控制过程中，使用多条线同时推进多个任务。
2. 分支的好处？
	* 同时并行推进多个功能开发，提高开发效率。
	* 各个分支在开发过程中，如果某一分支开发失败，不会对其他分支有任何影响，失败的分支删除重新开始即可。
3. 分支操作
  1. 创建分支

  	```shell 
  	git branch [分支名]
  	```

  2. 查看分支

  	```shell
  	git branch -v
  	```

  3. 切换分支

  	```shell
  	git checkout [分支名]
  	```

  4. 合并分支
  	1. 第一步：切换到接受修改的分支（增加新内容的分支）上

  		```shell
  		git checkout [分支名]
  		```
  	
  	2. 第二步：执行merge命令
  		```shell
  		git merge [有新内容的分支]
  		```

  5. 删除分支

     ```shell
     git branch -d [分支名]
     ```

  6. 解决冲突

    * 冲突的表现
    * 冲突的解决
    	1. 第一步：编辑文件，删除特定符号
    	2. 第二步：把文件修改到满意的程度，保存退出
    	3. `git add [文件名]`
    	4. `git commit -m "日志信息"
    		* 注意：此时commit一定不能带具体的文件名
## 远程库

1. 远程库别名
	* 查看别名
		```shell
		git remote -v
		```

	* 创建别名
		```shell
		git remote add [别名] [远程库地址]
		```
		![alias](./imgs/alias_01.png)
	
	* 删除别名
		```shell
		git remote rm [别名]
		```
	
	* 重命名别名
		```shell
		git remote rename [old name] [new name]
		```

	* 更改远程库的url
		```shell
		git remote set-url [old url] [new url]
		```
	
	* 远程库地址
		1. 不带token:`https://github.com/<user_name>/<repo_name>.git
			* 例如：`https://github.com/guoke2017/git.git`
		2. 带token:`https://<token>@github.com/<user_name>/<repo_name>.git
			* 例如：`https://ghp_sdF6QFsopUCtjcqb4MxzSgVVFU40UJQWv@github.com/guoke2017/git.git`

2. 推送
	* 命令
		```shell
		git push [远程库地址或别名] [远程库分支]
		```
	* Note
		* 当远程库地址不带有token时，每次push都要输入用户名和token
		* 可以将token写进远程库地址中，这样就不用每次都输入token了

3. 克隆
	* 命令
		```shell
		git clone [远程库地址]
		```
	* 作用
		1. 完整的把库下载到本地
		2. 创建origin远程库的别名
		3. 初始化本地库

4. 邀请团队成员
	1. 团队负责人github的仓库界面中，选“settings” -> “Manage access” -> “Invite a collaborator”
		![settings](./imgs/邀请_settings.png)
		![ManageAccess](./imgs/邀请_ManageAccess.png)
