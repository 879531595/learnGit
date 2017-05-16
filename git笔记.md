#第零部分 集中式vs分布式

###集中式版本控制系统:


版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。中央服务器就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家自己改，改完了，再放回图书馆。

集中式代表：CVS、SVN

集中式的缺点：是必须联网才能工作；集中式版本控制系统的中央服务器要是出了问题，所有人都没法干活了

###分布式版本控制系统：
没有“中央服务器”，每个人的电脑上都是一个完整的版本库，不需要联网

分布式的优点：分布式版本控制系统的安全性要高很多，因为每个人电脑里都有完整的版本库，某一个人的电脑坏掉了不要紧，随便从其他人那里复制一个就可以了。

分布式代表：	Git
	
	注意：以上版本控制系统都是开源系统
	



#第一部分 安装git后的配置操作

	使用git config -global 参数进行设置：
	设置用户名：git　config -global user.name  "username"
	设置邮箱  : git config　　-global user.email "xxx@qq.com"

注意：
	git config  –global 参数，有了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然你也可以对某个仓库指定的不同的用户名和邮箱。


#第二部分 git基本操作

###1、创建版本库（repository）

	定义：将目录变成git的管理仓库
	命令：git init 目录
	这样在目录下就会多一个.git的目录，这个目录是Git来跟踪管理版本的。

###2、将文件添加到版本库中

	第一步：使用命令 git add readme.txt添加到暂存区里面去。
	如下：git add readme.txt
	
	第二步：用命令 git commit告诉Git，把文件提交到仓库。
	如下：git commit -m "readme.txt提交" 
	-m 表示提交的注释

	git status:查看文件提交状态
	git diff 文件名 ：查看修改内容

diff 在Linux内命令，比较文本文件
	

###3.版本退回：	
	git log ：显示从最近到最远的日志
	git log --pretty=oneline 漂亮的显示从最近到最远的日志
	git reset --hard HEAD^ ：退回上一个版本
	git reset --hard HEAD^^ ：退回上上个版本
	git reset -–hard HEAD~100 ：退回前100个版本
	git reset -–hard 版本号 ：退出对应版本号版本

###4管理原理
	Git管理的是修改，当你用git add命令后，在工作区的第一次修改被
	放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存
	区，所以，git commit只负责把暂存区的修改提交了，也就是第一次
	的修改被提交了，第二次的修改不会被提交。
	
	git diff HEAD -- readme.txt命令可以查看工作区和版本库里面
	最新版本的区别

###5撤销修改
	命令：git checkout -- readme.txt
	意思就是，把readme.txt文在工作区的修改全部撤销。

	这里有两种情况：

	一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就
	回到和版本库一模一样的状态；
	一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修
	改就回到添加到暂存区后的状态。
	总之，就是让这个文件回到最近一次git commit或git add时的状态。

###6删除文件
	命令：git rm <文件名>:删除操作
		git commit - m 'remove file'：提交操作描述
	文件将会在版本库(repository)中被删除

#第三部分 远程仓库
					
（搭建运行Git的服务器）

###1、远程GitHub

第一步：创建SSH Key：

	ssh-keygen -t rsa -C "youremail@example.com"

就会在用户主目录下生产.ssh文件。里面有id_rsa和d_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人

第二步：将公钥 放在GitHub 网站上的“SSH Keys”页面
	
		
###2、添加远程库

第一步：首先你得有一个远程库
	在GitHub上创建一个远程库名字为MyRepository

第二步：把本地库和远程库相关联

在本地的MyRepository库下输入指令：

	git remote add origin git@github.com:879531595/MyRepository.git

879531595为自己的github账户名

origin是远程库名（git默认的叫法）

相关操作：

	git push -u origin master：将本地库的所有内容推送到远程库
	上（使用参数u时可能会报错，反正我是报错了，改为参数f后执行正常）

	当第一次上传成功后，之后就可以直接使用：
	git push origin master进行提交修好
###3、从远程库克隆

	命令：
	git clone git@github.com:879531595/test.git
	其中clone是表示克隆的参数
	git@github.com是github远程库
	879531595是自己在github上的账号
	test.git 是github上的库

执行命令后本地就会下载 github上的库
	

###注意：当第一次使用Git的clone和push 指令链接github时，会得到一个警告。这是应为第一次链接需要进行ssh的验证，你只需要输入yes回车即可
	
	

