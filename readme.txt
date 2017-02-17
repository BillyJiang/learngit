Git is a distributed version control system.
Git is free software distributed under the GPL.

Git:
    
1.安装git软件
    https://git-for-windows.github.io
    安装完成后 开始->Git->Git Bash 
    再设置
        git config --global user.name "Your Name"
        git config --global user.name "email@example.com"
    git config 命令的--global参数 用了这个参数表示这台机器上所有的Git仓库都会使用这个配置。        
2.创建版本库
    选择一个地方，创建一个空目录
        mkdir learngit
        cd learngit
        pwd
    pwd命令用于显示当前目录
        git init
    git init 命令把这个目录变成Git可以管理的仓库
    新建一个readme.txt,把一个文件放到Git仓库只需要两步
        用命令git add告诉Git，把文件添加到仓库
            git add readme.txt
        用命令git commit告诉Git，把文件提交到仓库
            git commit -m "wrote a readme file"
        git commit 命令，-m 后面输入的是本次提交的说明，输入有意义的内容，方便从历史记录里方便地找到改动记录
    为什么Git添加文件需要add,commit 一共两步呢？
        因为commit可以一次提交很多文件，所以可以多次add不同的文件
        git add file1.txt
        git add file2.txt file3.txt
        git commit -m "add 3 files"
3.时光机穿梭
    修改readme.txt文件，运行git status命令看看结果。
    git status 命令可以让我们时刻掌握仓库当前的状态，上面的命令是说 readme.txt被修改过了，但还没有准备提交的修改。
    如何查看具体修改哪些内容？使用git diff命令
        git diff readme.txt
    知道对readme.txt作了什么修改后，再把它提交到仓库就OK了。
    提交修改和提交新文件是一样的。
        git add readme.txt
    再执行git commit 之前，先运行git status看看当前仓库的状态
        git status 告诉我们，将要被提交的修改包括readme.txt
    提交后，再用git status 命令看看仓库的当前状态。
        git status 告诉我们当前没有需要提交的修改，而且，工作目录是干净的。
    
    3.1版本回退
        由于不断在git add 和 git commit已经忘记了每次都改了什么内容。
        在Git中，我们使用git log命令查看。
            git log
        git log命令显示从最近到最远到提交日志。如果嫌输出信息太多，可以试试加上 --pretty=oneline参数。
            git log --pretty=oneline
            需要注意的是，前面有一大串数字15ecde84babdb89338f89776edfd400ce58c20dd是commit id(版本号)
        现在知道所有的版本和版本号。要回退到上个版本或指定版本，怎么办？
            Git必须知道当前版本是哪个版本？在Git中，用HEAD表示当前版本。上一个版本就是HEAD^,上上一个版本就是HEAD^^
        往上100个版本写成HEAD~100。
            使用git reset 命令,回退到上一个版本。
                git reset --hard HEAD^
            再用git log 看看版本库的状态。发现刚才的版本已经不见了?
            这时需要找到刚才版本的版本号前几位(53b6d2c)。再次使用git reset命令
                git reset --hard 53b6d2c
            再git log 看下所有版本，发现已经回来了。哈哈。
        当你回退到某个版本，关掉了电脑。再开机想恢复新版本，发现找不到commit id 怎么办？
            使用git reflog用来记录你的每一次命令。
                git reflog
    3.2工作区和暂存区
        工作区(working directory)
            就是你在电脑里能看到的目录，比如我的learngit文件夹就是一个工作去。
        版本库(repository)
            工作区有个.git目录，这个不算工作区，而是Git的版本库。
            Git版本库里存了很多东西，其中最重要的是stage(或index)的暂存区，还有Git自动创建的第一个分支master,
        以及指向master的一个指针叫HEAD。
            工作区           版本库
              |          stage       master
              |            |            |       
              |            |            |         
              | ---add---> |-->commit-->|       
              |            |            |          
              |            |            |       
              |            |            |          
              |            |            |       
            前面将文件添加到Git版本库的时候，分两步执行的。
                第一步，用git add 把文件添加进去，实际上就是把文件修改添加到暂存区
                第二步，用git commit 提交更改，实际上就是把暂存区的所有内容提交到当前分支
            由于我们创建Git版本时，Git自动为我们创建了唯一一个master分支，所以，git commit 就是往master分支上提交更改。
            可以简单理解，需要提交的修改通通放到暂存区，然后，一次性提交暂存区的所有修改。
    3.3管理修改
        第一次修改->git add ->第二次修改->git add ->git commit 这样才能保证两次修改的内容都能commit中。
        Git是如何跟踪修改的，每次修改，如果不add到暂存区，就不会加入到commit中。
    3.4撤销修改
        第一种:如果在工作区修改了文件，还没有add到暂存区。想要撤销修改，使用git status查看一下。
            Git会告诉你，git checkout -- file 可以丢弃工作区的修改。
                git checkout -- readme.txt
              把readme.txt文件在工作区的修改全部撤销。
        第二种:如果在工作区修改了文件并add 到暂存区，还未commit到分支。使用git status 查看一下，
            修改只是添加到了暂存区，还没有提交。
            Git同样告诉我们，用命令git reset HEAD file 可以把暂存区的修改撤销掉(unstage),重新放回工作去。
                git reset命令既可以回退版本，也可以把暂存区的修改回到工作区。当我们用HEAD时，表示最新的版本。
            再用 git status 查看一下，现在暂存是干净的，工作区有修改。
    3.5删除文件
        
        
        
        
        
        
        
        
        
        
       
    
    
    
    
    
    
    
    
    
    
    
    
    
    
