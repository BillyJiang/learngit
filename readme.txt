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
            
        
        
        
        
        
        
        
        
        
        
        
       
    
    
    
    
    
    
    
    
    
    
    
    
    
    
