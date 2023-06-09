#### 名词解释

高级语言：

是一种独立于机器，面向过程或对象的语言，高级语言相对低级语言有较高的可读性，更易理解。

高级语言并不是特指的某一种具体的语言，而是包括很多编程语言，如流行的java，c，c++，C#，pascal，python易语言，中文版的C语言等等，这些语言的语法、命令格式都不相同。

低级语言：低级语言就是**机器语言**，是直接用二进制代码指令表达的计算机语言，指令是用0和1组成的一串代码，它们有一定的位数，并分成若干段，各段的编码表示不同的含义，

编译器：

简单讲，编译器就是将一种语言（通常为高级语言）翻译为另一种语言，通常为低级语言”的程序

源代码 → 预处理器 → 编译器→ 目标代码)→ 链接器 → 可执行程序

汇编指令：汇编指令是汇编语言中使用的一些操作符和助记符，还包括一些伪指令（如assume，end），汇编指令同机器指令一一对应。每一种CPU都有自己的汇编指令集。例如：add，and....

机器码：

计算机直接使用的程序语言，其语句就是机器指令码，由1和0构成的指令。

#### 编译，链接，安装，运行

预处理：主要是进行***\*文本替换、宏展开、删除注释\****这类简单工作，使.c文件转换成.i文件

编译就是把高级语言变成计算机可以识别的2进制语言，由编译程序Compiler（编译器）将源代码编译成若干个目标模块，翻译成机器语言。.i文件转换成.s文件

汇编：.s文件转换成.o文件

链接：由链接程序Linker将编译后形成的一组目标模块，以及所需库函数链接在一起，形成一个完整的装入模块(可执行文件)；.o文件转换成.elf文件（可执行）

可执行文件：pc端有.exe，.elf，.pe

安装：可执行文件只有被装载到内存以后才能被CPU执行，由装入程序Loader将装入模块装入内存运行；

![20170611205306090](C:/Users/zhangjiejie666/Desktop/star%E9%AA%8C%E6%94%B6/git%E7%AC%94%E8%AE%B0/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/20170611205306090.png)

#### 操作系统和文本编辑器

操作系统：Windows，Linux

文本编辑器：记事本，vscode，vim，pad++

#### *VScode*

主界面：菜单栏，活动栏，侧栏，状态栏，面板，编辑器板块，搜索栏，源代码管理，扩展

搭建c/c++语言环境

完成简单代码的编写调试

### 编码思维

#### 程序架构，模块化，内在联系

分别管理，提高效率和便于管理。更多的是经验的总结，多练多写。

例如：不同模块的全局变量，数组定义到对应的.c文件

#### 库的调用，栈的思想，使用git，分工





# GIT  markdown

工具类型：GIT,SVN,CVS,VSS,TFS,Visual Studio Online....

## 分类

本地版本控制：补丁和版本，适合个人

集中版本控制：所有版本数据保存到服务器上，协同开发者从服务器上同步更新或者上传自己的修改。适用于公司，缺点很大，用户需要时常更新和同步数据，服务器故障损失大。因此需要定期备份。代表产品：SVN,CVS,VSS.

分布式版本控制:每个人都与版本信息库同步，存储空间占用大。安全隐患是个人可能泄露机密。不会因为网络和服务器故障而损失。代表产品：GIT

 GIT与SVN区别：

SVN是集中式版本控制系统，版本库是集中放在中央服务器的，而干活的时候，用的都是自己的电脑，所以首先要从中央服务器哪里得到最新的版本，然后干活，干完后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是必须联网才能工作，如果在局域网还可以，带宽够大，速度够快，如果在互联网下，如果网速慢的话，就纳闷了。

Git是分布式版本控制系统，那么它就没有中央服务器的，每个人的电脑就是一个完整的版本库，这样，工作的时候就不需要联网了，因为版本都是在自己的电脑上。既然每个人的电脑都有一个完整的版本库，那多个人如何协作呢？比如说自己在电脑上改了文件A，其他人也在电脑上改了文件A，这时，只需把各自的修改推送给对方，就可以互相看到对方的修改了。

GIT是目前世界上最先进的分布式版本控制系统。



## 历史

linux与BitKeeper终止合作，Linux之父Linus benedict torvaid两周时间开发了GIT系统（免费而且开源）

## 官网进行下载和安装

GIT Bash:Unix和Linux风格的命令行，使用和推荐最多

GIT CMD：windows风格的命令行

GIT GUI：图形界面的Git，不建议初学者使用，尽量先熟悉常用命令。

## 命令学习

cd /                 //切换到根目录
  cd /bin              //切换到根目录下的bin目录
  cd ../               //切换到上一级目录 或者使用命令：cd ..
  cd ~                 //切换到home目录
  cd -                 //切换到上次访问的目录
  cd xx(文件夹名)       //切换到本目录下的名为xx的文件目录，如果目录不存在报错
  cd /xxx/xx/x         //可以输入完整的路径，直接切换到目标目录，输入过程中可以使用tab键快速补全

pwd                 //显示当前目录路径

clear               //清屏命令

ls                   //查看当前目录下的所有目录和文件
  ls -a                //查看当前目录下的所有目录和文件（包括隐藏的文件）
  ls -l                //列表查看当前目录下的所有目录和文件（列表查看，显示更多信息），与命令"ll"效果一样
  ls /bin              //查看指定目录下的所有目录和文件 

touch（加类型）				//在当前目录下新建文件

rm						//移除一个文件

mkdir					//新建文件夹

rm-f					//清理文件夹

mv					//移动目标对象到文件夹中

reset					//重新初始化终端

history						//查看命令历史

help								//帮助

git config--（）--list					//查看配置 

## Git配置文件

#### 所有的配置文件都保存在本地

​     系统配置在GIT的安装目录下

​      个人配置在用户目录内。gitconfig文件中

git config --（） --list					//查看当前用户（）配置 

git config --system--list					//查看系统config的配置 

git config --global  user.name "名字名字" 		//写入config的个人配置

git config --global  user.email "邮箱邮箱" 			//写入个人配置邮箱

##### ”注意空格“





## GIT基本理论

### 四个工作区域

工作目录，暂存区，资源库，远程的git仓库

*Workspacce:工作区，就是你平时存放项目代码的地方

*Inder/Stage：暂存区，位于.git目录下的index文件，暂存区会记录 git add 添加文件的相关信息（文件名、大小），不保存文件实体，通过 id 指向每个文件的实体。

使用 git status 可以查看暂存区的状态，暂存区标记了当前工作区中那些内容是被 git 管理的，当完成某个需求或者功能后需要提交代码，第一步就是通过 git add 先提交到暂存区。

*Repository：仓库区，安全存放数据的位置，这里有提交的到所有版本的数据。HEAD指向最新放入仓库的版本。

*Remote：远程仓库区，托管代码的服务器，位于托管代码的服务器，远程仓库的内容能够被分布在多个地点的处于协作关系的本地仓库修改。比起本地仓库，远程仓库通常旧一些，因此本地仓库修改完之后需要同步到远程仓库。例如：GitHub，gitee

注意：git是隐藏文件夹需要在Windows中打开权限才能查看。

## Git 的工作流程

- 在工作区添加、修改文件；

- 将修改后的文件放入暂存区域；

  git add.

- 将暂存区域的文件提交到本地仓库；

  git commit.

- 将本地仓库的修改推送到远程仓库。

  则git管理的文件有三种状态：已修改（modified）已暂存（staged）已提交（committed）

### GIT项目的搭建

add到commit到push

clone到checkout和pull

一.创建本地仓库：1.创建全新的仓库；2.创建克隆远程的仓库

1.git init

2.git clone  (加网站地址可以去gitee找）

二.实现文件的版本控制

四种状态：

1.Untracked(未跟踪) ：通过git add.

2.Unmodify(已入库未修改):通过修改变成已修改，不然用git rm移出版本库回到上一级

3.Modified(已修改)：通过git add变成暂存，通过git checkout回到上一级，从库中取出文件覆盖当前文件

4

.Staged（暂存状态）：执行git commit同步修改到库中，变为已入库未修改的状态，执行git reset HEAD filename 则取消暂存，文件状态为已修改



git status[文件名字]			//查看指定文件状态

git status							//查看所有文件状态

git add .								//添加所有文件到暂存区

git commit-m“注释消息信息‘   					//提交暂存区中的内容到达本地仓库，-m提交信息



###### 忽略文件

主目录下建立”.gitignore“文件然后用语言进行设置



##### 使用码云

gitee的注册和使用，找寻开源

ssh-keygen -t rsa

添加公钥

用码云管理

开源许可证：限制商业化或者控制能否转载

GPL3.0

## 实践时出现的问题

##### The current branch master has no upstream branch.    指没有将本地的分支与远程仓库的分支进行关联



git log命令可以查看版本库中各个版本信息。

git branch 可以看见当前本地分支

通过`git branch -a`查看远程分支，有`master`和`remotes/origin/master`两个

git push --set-upstream origin master 使程序直接上传远程仓库

使用`git push -u origin master`命令上传本地仓库



##### Hi 张洁滨! You've successfully authenticated, but GITEE.COM does not provide shell access. 指git 向仓库推送代码失败。

ssh -T git@gitee.com 查看是否链接成功



#####  ! [rejected]        master -> master (non-fast-forward)    指码云中有的代码会被覆盖，可以强行推上先fetch到本地再merge和push

$ git fetch

$ git merge

3、在使用的时候，`git merge`，又出现了以下的问题

```vbnet
xu:QProj xiaokai$ git merge
fatal: refusing to merge unrelated histories
```

然后继续`git merge`,依然有问题

xu:QProj xiaokai$ git merge
fatal: refusing to merge unrelated histories

对于这个问题。使用`git pull origin master --allow-unrelated-histories`

后继续`git merge`

 `git add .`,`git commit -am "提交信息"`

然后再来一次`git merge`

然后输入`git pull`,显示如下

xu:QProj xiaokai$ git push origin master



#### 验证代码：

cd ~/.ssh

git remote -v 查看远程库的信息

cat ~/.ssh/id_rsa.pub      # 控制台上输出内容

```
ssh -T git@gitee.com
```

首次使用需要确认并添加主机到本机SSH可信列表。

$ pwd     回车之后进行查看当前文件夹位置

`$ ls`     查看当前文件夹都有什么文件

`$ cd ..`     点和cd之间有空格回退到上一级文件夹

`$ mkdir +文件夹名字` 只能新建文件夹

`touch +文件名` 只能新建文件

`$ rm 文件名.文件类型` 删除文件

`$ rm -r 文件夹`删除文件夹 ，注意这个要回到上一级文件夹才可以删。比如我要删除front-end文件夹，front-end在code里边，我就要在code目录下删除。

#### 在管理Git项目上，有两种克隆到本地的方法。

- 直接使用https url克隆到本地
- 使用SSH url克隆到本地

```
~/.ssh` 或者用`~/.ssh ls      观察电脑是否有.ssh文件夹
```

- 如果电脑上**有**，就会显示**bash: /c/Users/…/.ssh: Is a directory**
- 如果电脑上**没有**，那就显示**bash: /c/Users/…/.ssh: No such file or directory**

$ ssh -T git@gitee.com  测试链接

如果看到 **access denied**，者表示拒绝访问，那么你就需要使用 https 去访问。
注意，你是仓库的主人你才能使用SSH连接，如果你不是仓库主人，只是某个项目的成员，那你只能使用HTTPS连接。

$ git remote add + 名字 + 连接地址

添加之后没有任何提示，如果你想确定是否成功了，你可以再输一遍，这时候他会提示你刚才已经设置过了。

名字：你在往远程仓库推送的时候，你会说我要推给谁，总得给它起个名字。（你把孩子送去托儿所，你总得告诉司机是哪个托儿所吧）并且你以后可能会一个**本地仓库连接多个远程仓库**（这是后话），所以必须起名字加以区分。

- $ git remote -v 

- git remote remove + 名字    与某个仓库不链接

- **`git add -A`**，提交**所有变化**

- $ git commit -m "修改注释"

- $ git push -u 仓库名称 分支第一次要-u

- 分支：你现在只有主分支，所以分支直接写master。以后合作项目的时候，成员之间建了不同的分支，你就可以往你自己的分支上推。

- $ git push 名称 分支

- $ git push origin master -f     强制推送，因为报错90%是因为你本地仓库和远程仓库数据发生冲突，使用这个会直接用本地数据覆盖掉远程数据，可能损失数据哦。、

- $ git log 提交记录

- $ git commit --amend -m "修改的内容"

- $ git pull 仓库名称

- git fetch 加名字 加分支 同步本地和远程

- `git branch`命令的`-r`选项，可以用来查看远程分支，`-a`选项查看所有分支

- 可以使用`git merge`命令或者`git rebase`命令，在本地分支上合并远程分支。

- ```
  
  $ git fetch` + `$ git merge
  ```

**commit message格式**

```text
<type>(<scope>): <subject>
```

**type(必须)**

用于说明git commit的类别，只允许使用下面的标识。

feat：新功能（feature）。

fix/to：修复bug，可以是QA发现的BUG，也可以是研发自己发现的BUG。

- fix：产生diff并自动修复此问题。适合于一次提交直接修复问题
- to：只产生diff不自动修复此问题。适合于多次提交。最终修复问题提交时使用fix

docs：文档（documentation）。

style：格式（不影响代码运行的变动）。

refactor：重构（即不是新增功能，也不是修改bug的代码变动）。

perf：优化相关，比如提升性能、体验。

test：增加测试。

chore：构建过程或辅助工具的变动。

revert：回滚到上一个版本。

merge：代码合并。

sync：同步主线或分支的Bug。





git log后不能退出按q即可
