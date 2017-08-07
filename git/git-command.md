# Git 常用命令

>记录了Git 在日常使用中用到的命令 



###路劲跳转 
cd E: 

cd E:/hiGit  

###返回上级目录
cd ../  

###列出文件
ls

###列出目录
ls -a


###打开Git Bash查看电脑上是否已经存在SSH密钥
cd ~/.ssh

###创建新的ssh key
ssh-keygen -t rsa -C "your_email@youremail.com"
>执行这条命令会如上图提示文件保存路径，可以直接按Enter，然后提示输入 passphrase（密码），输入两次（可以不输直接两次Enter）

###复制ssh key到github

###测试 ssh 链接 github
ssh -T git@github.com
>出现Successfully就OK

###用户配置文件
git config --global user.name "John Doe"

git config --global user.email johndoe@ example.com

###查看配置信息
git config --list

###直接查阅某个环境变量的设定，只要把特定的名字跟在后面即可 
git config user.name [name]

###获取帮助
git help

###获取制定帮助
git help [name]  
>例如：git help config 或者 git help add 等

###查看版本
git --version  




###新建仓库
git init  [文件夹]  

###clone仓库
git clone [远程仓库项目名]  

###clone仓库到指定目录
git clone [远程仓库项目名]  '目录名称'




###添加项目到缓存   
git add [文件名]
>可以同时添加多个文件或单个文件

>当然如果你可以add多个文件后再一次性commit，不过如果我们改动的文件很多的话，我们可以git add .一次添加全部，但有一些是几百年都不变一次的又或者自动生成的，比如lib，gen，bin文件夹等等，我们可以在代码仓库的根目录下创建一个名为.gitignore的文件，然后编辑里面的内容，把不需提交的文件忽略掉！

###添加目录中的所有文件
git add .    
>与 git add * 效果一致   不过那只是因为我们这还木有子目录，不需要递归地添加新文件。

###列出添加缓存之前变更部分
git add -p 
>请查看《Pro Git》中 git add 的 “-p” 参数，以了解更多关于提交文件的灵活性的例子。





###查看文件在工作目录与缓存的状态
git status 

###以获得简短的结果输出 
git status -s
> 输出结果前缀 
？  还未添加到缓存   
A   已添加到缓存   
M   文件添加到缓存后有修改    
D   表示工作区已删除文件     


  

###尚未缓存的改动
git diff 

###查看已缓存的改动
git diff –-cached 

###查看已缓存的与未缓存的所有改动 
git diff HEAD --file  

###显示摘要而非整个 diff
git diff –-stat 

###比较两个不同的分支 
git diff branchA ^branchB/branchB  



###提交到本地仓库 
git commit 

###-m 为当前提交添加注释
git commit -m '注释内容'   

###自动将在提交前将已记录、修改的文件放入缓存区
git commit -a 

###自动添加到缓存，并以注释方式提交
git commit -am  '注释内容'




###取消缓存已缓存的内容
git reset HEAD --file 

###将文件从缓存区移除
git rm 
>默认情况下，git rm file 会将文件从缓存区和你的硬盘中（工作目录）删除。 如果要在工作目录中留着该文件，可以使用 git rm --cached




###列出本地仓库分支
git branch 

###列出本地仓库分支(包括最近提交的 “hash值” 和  “文字注释”)
git branch -v 

###列出远程仓库分支
git branch -r 

###创建分支 
git branch (branchname) 

###命令切换到该分支
git checkout (branchname)

###创建新分支，并立即切换到它
git checkout -b (branchname) 

###删除分支
git branch -d (branchname) 




#git tag 给历史记录中的某个重要的一点打上标签

###新建标签
git tag v1.0

###新建一个带注解的标签
git tag -a    
>-a 选项意为“创建一个带注解的标签从而使你为标签添加注解。绝大部分时候都会这么做的。 不用 -a 选项也可以执行的，但它不会记录这标签是啥时候打的，谁打的，也不会让你添加个标签的注解。 我推荐一直创建带注解的标签。
现在，注意当我们执行 git log --decorate 时，我们可以看到我们的标签了：
果我们忘了给某个提交打标签，又将它发布了，我们可以给它追加标签。在相同的命令末尾加上提交的 SHA，执行，就可以了 


###给commit id 为25656e2的历史版本打标签
git tag v1.0  25656e2
git tag -a v0.9 558151a
>带注解

###查看标签
git tag  

###用git show tagname查看标签信息
git show v1.0   





###将分支合并到你的当前分支
git merge (branchname) 

###合并仓库或分支
git merge github/master 

>合并pull两个不同的项目，出现的问题如何去解决fatal: refusing to merge unrelated histories
我在Github新建一个仓库，写了License，然后把本地一个写了很久仓库上传。
先pull，因为两个仓库不同，发现refusing to merge unrelated histories，无法pull
因为他们是两个不同的项目，要把两个不同的项目合并，git需要添加一句代码，在git pull，这句代码是在git 2.9.2版本发生的，最新的版本需要添加--allow-unrelated-histories




###查看commit记录 
git log 
>显示一个分支中提交的更改记录 

###查看commit最后一次提交记录
git log -n 1 

###查看commit最后一次提交记录所对应的文件 
git log -n 1 --stat 

###查看commit最后一次提交记录所更改的细节
git log -n 1 -p 

###只寻找某个特定作者的提交
git log –author 

###根据日期过滤提交记录
git log –since –before

###根据提交注释过滤提交记录
git log –grep 

###依据所引入的差值过滤
git log -S 

###显示每个提交引入的补丁(更改的细节)
git log -p 

###显示每个提交引入的改动的差值统计
git log –-stat 

###查看历史记录的紧凑简洁的版本。
git log --oneline 

###查看历史中什么时候出现了分支、合并。
git log --graph  

###分布视图
git log --oneline --decorate --graph

###对比记录
git log [] ^[]   
>^表示非

###直接按键盘q键
退出git log   




###显示文件内容
cat [文件名]  

###当前分支的文件
git ls-files  




###列出远端别名
git remote   
###列出远端别名（详情） 
git remote -v

###添加一个新的远端仓库别名
git remote add  
>此命令将 [url] 以 [alias] 的别名添加为本地的远端仓库。

###删除现存的某个别名
git remote rm  
>如果你需要删除一个远端 —— 不再需要它了、项目已经没了，等等 —— 你可以使用 git remote rm [alias] 把它删掉。




###上传到远处仓库
git push origin master  




###从远端仓库下载新分支与数据  
git fetch [alias]
###同步所有仓库
git fetch --all 

在fatch时，你可以看到 Git 做的映射。远端仓库的主分支成为了本地的一个叫做“github/master”的分支。 这样我就可以执行 git merge github/master 将远端的主分支和并入我的本地主分支。 或者，我可以 git log github/master ^master 看看该分支上的新提交。 如果你的远端仓库叫做“origin”，那远端主分支就会叫做 origin/master。几乎所有能在本地分支上执行的命令都可以在远端分支上用。
如果你有多个远端仓库，你可以执行 git fetch [alias] 提取特定的远端仓库， 或者执行 git fetch --all 告诉 Git 同步所有的远端仓库。




###从远端仓库提取数据并尝试合并到当前分支
git pull [alias] 

###删除文件夹下的所有 .git 文件
find . -name ".git" | xargs rm -Rf




###vim 命令-小结1
1. 光標在屏幕文本中的移動既可以用箭頭鍵，也可以使用 hjkl 字母鍵。
h (左移)	j (下行)       k (上行)	   l (右移)
  2. 欲進入vim編輯器(從命令行提示符)，請輸入︰vim 文件名 <回車>
  3. 欲退出vim編輯器，請輸入以下命令放棄所有修改︰
<ESC>   :q!	<回車>
     或者輸入以下命令保存所有修改︰
<ESC>   :wq	<回車>
  4. 在正常模式下刪除光標所在位置的字符，請按︰ x
  5. 在正常模式下要在光標所在位置開始插入文本，請按︰
i     輸入必要文本	<ESC>


###参考网站
http://www.ihref.com/read-16369.html(比较详细-适合初学者)
http://www.cnblogs.com/newpanderking/p/4005698.html（总结比较好）  


###丢弃最后一次的提交
git reset --hard HEAD^

###回滚到指定commit 版本(版本号-7位即可)
git reset --hard [commit_id]

###如果想切换到新的 branch 里并回归到上一次提交的状态
git checkout -b new-topic HEAD^

BTW:HEAD^等于HEAD~1，HEAD^^等于HEAD~2

### 回退后，你突然后悔了，想回退回新的那个版本，可是遗憾的是，你键入git log却发现没有了最新的那个版本号，这怎么办呢... 没事，Git中给你提供了这颗"后悔药"，Git记录着你输入的每一条指令呢！键入：

git reflog
>可以查看所有分支的所有操作记录（包括（包括commit和reset的操作），包括已经被删除的commit记录，git log则不能察看已经删除了的commit记录


>git本地操作参考:http://blog.csdn.net/hebbely/article/details/51858938
