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
