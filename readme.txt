Git is a distributed version control system.
Git is free software distributed under the GPL.

Git:
    
安装git软件
    https://git-for-windows.github.io
    安装完成后 开始->Git->Git Bash 
    再设置
        git config --global user.name "Your Name"
        git config --global user.name "email@example.com"
    git config 命令的--global参数 用了这个参数表示这台机器上所有的Git仓库都会使用这个配置。        
创建版本库
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
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
