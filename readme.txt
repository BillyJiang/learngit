廖雪峰老师的Git教程
    http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

笔记    
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
            Git必须知道当前版本是哪个版本？在Git中，用HEAD表示当前版本。上一个版本就是HEAD^,上上一个版本
        就是HEAD^^,往上100个版本写成HEAD~100。
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
        新建文件test.txt,并add到暂存区，再commit到master分支
            git add test.txt
            git commit -m "add test.txt"
        此时你在工作区删除了test文件，或用命令删除了文件 rm test.txt
            假如是你删错了，可以使用git checkout -- test.txt恢复到最新版本。
            若不是删错了，你仅仅删除了工作区的test文件，为了和分支保持一致，
        需要从版本库中删除该文件，使用 git rm删掉，并且git commit。
            git rm test.txt
            git commit -m "remove test.txt"
        这样文件就从版本库中被删除了。
4.远程仓库
    只要注册一个GitHub账号，可以免费获得Git远程仓库。
    由于本地Git仓库和GitHub仓库之间的传输是通过SSH加密的。所以，需要一点设置：
        第一步:创建SSH Key
            在"用户主目录"下，看看有没有.ssh目录，如果有，再看看这个目录有无id_rsa和id_rsa.pub两个文件
        如果已经有，可直接调到下一步。如果没有，打开Git Bash，创建SSH Key:
            ssh-keygen -t rsa -C "youremail@example.com"
        一路回车，使用默认值即可。
        完成之后，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH key的密钥对
            id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
        第二步: 注册一个GitHub账号并登陆，打开setting->SSH and GPG keys->New SSH key ->
            填上任意title，在Key文本框里粘贴id_rsa.pub文件的内容。->add SSH key ->就能看到已经添加的Key
            当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把
        每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。
    4.1 添加远程库
        现已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步。
        登陆GitHub，右上角 New Repository 创建一个新的仓库 ->Repository name 填入learngit，其它默认
        设置->Create repository 成功创建了一个新的Git仓库
        目前，在GitHub上的这个learngit仓库还是空的，GitHub告诉我们可以从这个仓库克隆出新的仓库，也可以
        把一个已有的本地仓库与之关联，然后把本地仓库的内容推送到GitHub仓库。
            根据GitHub的提示，在本地的learngit仓库下运行命令：
                git remote add origin https://github.com/BillyJiang/learngit.git
            远程库的名字就是origin(Git默认的叫法，可以更改但origin这个名字一看就知道是远程库)
        下一步就可以把本地库的所有内容推送到远程库上
                git push -u origin master
            把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
            由于远程库是空的，我们第一次推送master分支时，加上了-u参数,Git不但会把本地的master分支内容推送
            的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时
            就可以简化命令。
            推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一样了。
            只要本地作了提交，可通过命令 git push origin master 把本地master分支的最新修改推送到GitHub。
    
    4.2从远程库克隆
        4.1讲了先有本地库，后有远程库的时候，如何关联远程库。
        假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。
            第一步：登陆GitHub，创建一个新的仓库，名字叫 gitskills
                我们勾选Initialize this repository with a README，这样GitHub会自动为我们创建一个README.md文件。
            创建完毕后，可以看到README.md文件
            现在，远程库已经准备好了。
            第二步：用命令git clone克隆一个本地库
                git clone git@github.com:billyjiang/gitskills.git
                注意把Git库的地址换成你自己的，然后进入gitskills目录看看，已经有README.md文件了。
            也许你还注意到，GitHub给出的地址不止一个，还可以用https://github.com/billyjiang/gitskills.git 。
            实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议。
                使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的
            公司内部就无法使用ssh协议而只能用https。
5.分支管理    
    5.1 创建与合并分支
        在版本回退里，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。
    master叫主分支。HEAD指向master(指向当前分支)，master指向commit(提交)。
        创建分支(dev)
            git branch dev
        切换分支
            git checkout dev
            创建并切换到dev分支(git checkout 命令加上-b参数 表示创建并切换)
                git checkout -b dev
        查看分支
            git branch
            git branch命令会列出所有分支，当前分支前面会标一个*号。
            我们就可以在dev分支上正常提交，比如对readme.txt做个修改.
                creating a new branch is quick.
        提交
            git add readme.txt
            git commit -m "branch test"
        dev分支的工作完成，我们就可以切换回master分支.
            git checkout master
            切换回master分支后，再查看一个readme.txt文件，刚才添加的内容不见了！
        因为那个提交是在dev分支上，而master分支此刻的提交点并没有变。
        
        合并？
            将dev分支的工作成果合并到master分支上
                git merge dev
                git merge 命令用于合并指定分支到当前分支。合并后，就可以看到和dev最新提交是一样的。
            合并完了，就可以删除dev分支了。
                git branch -d dev
            查看branch
                git branch
                只剩下master分支了。
    5.2解决冲突
        当master分支和新的分支(feature1)各自都分别有了新的提交。
        这时，Git无法执行"快速合并"，只能试图把各自的修改合并起来，但这种合并就可能会有冲突。
        文件存在冲突，必须手动解决冲突后再提交。git status 查看冲突的文件。
        打开冲突的文件：
            Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容。
            修改成一个版本。并提交。
        用带参数的git log命令可以看到分支的合并情况(分支合并图)：
            git log --graph --pretty=oneline --abbrev-commit
            --graph 显示ASCII图形表示的分支合并历史
            --pretty=oneline 用oneline 将每个提交放在一行显示
            --abbrev-commit 仅显示SHA-1的前几个字符
        最后删除feautre1分支
            git branch -d feature1
    5.3分支管理策略
        一般情况下，合并分支时，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
        如何从分支历史上看出分支信息？
            强制禁用Fast forward模式，Git就会在merge时生成一个新的commit。
        使用 --no-ff方式的git merge
            创建并切换dev分支
                git checkout -b dev
            修改readme.txt文件，并提交一个新的commit
                git add readme.txt
                git commit -m "add merge"
            切换到master
                git checkout master
            准备合并dev分支，使用 --no-ff参数，表示禁用Fast forward
                git merge --no-ff -m "merge with no-ff" dev
                由于本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。
            合并后，用git log 查看分支历史。
                git log --graph --pretty-oneline --abbrev-commit
        分支策略
            
    
    
    
    
    
    
    
    
    
    
    
    
    
    
