## 第一部分 Git入门
### 一、安装git
#### 1.1 不同平台
* Linux: yum -y install git
* Windows：先从http://www.git-scm.com/download/下载Windows版的git，然后安装，推荐Git for Windows Portable

#### 1.2 设置
在命令行输入：

    git config --global user.name "Your Name"
    git config --global user.email "email@example.com"
    git config的--global参数，表示这台机器所有的Git仓库都使用这个配置。
 
 
### 二、创建第一个项目
#### 2.1 版本库
版本库又叫仓库(repository)，可简单理解成一个目录，此目录的所有内容都可以被git管理，
每个文件的创建、修改、删除都能跟踪，并能追踪历史。
* 第一步，创建一个新目录并进入这个目录中，命令：

      $ mkdir myweb
      $ cd myweb
* 第二步，使用命令把这个目录变成Git可以管理的仓库，命令：

      $ git init
创建完成后，这个Git版本库就可用来记录和跟踪该项目的代码了。
> 注意：`git init` 命令会生成一个.git目录，它是Git用于管理版本库的，不可修改！
  
#### 2.2 添加文件到版本库
> 注意，只能跟踪文本文件的改动，二进制文件也可管理，但不能跟踪变化。

* 首先，创建一个index.html文件，内容如下：
  `<h1>hello world</h1>`
* 第一步，使用命令添加文件到版本库的暂存区。命令：

      $ git add readme.txt

> git add <file> 可反复多次使用，添加多个文件；

* 第二步，用命令提交到仓库。命令：
  $ git commit -m "Added home page."
> commit可以一次提交多个文件，提交一次创建一个。

这时，使用`git log`后输出的第一行显示Git自动产生的SHA-1码，它能保证是独一无二的；第二行是提交者的信息；第三行是提交日期；最后是提交留言。

#### 2.3 在项目中工作
第一个项目的版本库已经生成。
* 修改文件
index.html文件中没有<html>主元素。现在添加。

      <html>
          <h1>hello world</h1>
      </html>

修改完后，使用`git status`会显示工作区的状态。

    $ git status
此命令将修改过的文件在Changes not staged for commit:下列出来，这时需要将修改的文件添加到暂存区。
> Git有三个地方可以存放代码。
> 1. 工作区；编辑文件时可以直接在这里操作。
> 2. 暂存区；存放的是准备提交到版本库中的修改，它是工作区和版本库之间的缓冲区。
> 3. 版本库；

添加文件到暂存区：

    $ git add index.html
查看状态

    $ git status
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

            modified:   index.html

注意：modified:   index.html由红色变为绿色。
提交修改

    $ git commit -m "add <html> to index.html"
查看日志

    $ git log -1
    commit 5e83c82bd76480c14575b26bcef5b820f1f50606
    Author: Daniel <danielwang1228@sina.com>
    Date:   Mon Sep 14 22:26:26 2015 +0800

        add <html> to index.html

> `git log` 命令的 `-1`参数用于限命输出的提交条目的个数; 使用参数--pretty=oneline可以每一个记录显示在一行中。重要信息包括：commit id，时间，操作人等。

#### 2.4 使用分支
　　项目代码完成后，还需要进行多次测试，最终达到预期的功能和质量。与此同时，借助分支，可以开始下一个版本的新功能开发。
　　分支能够为代码保留一份拷贝。当创建了自己的分支，可以在自己的分支上修改、提交等操作，到修改完毕后一次性合并到原来的分支上，既安全又不影响别人工作。创建分支的命令语法：
    `git branch <new branch> <old branch>`

    $ git branch RB_1.0 master

上面的命令从主分支(master)上创建一个名为RB_1.0的分支，RB代表发布分支(release branch)。Git默认会有一个master分支，即主分支。
修改代码:

    <html>
        <body>
            <h1>hello world</h1>
        </body>
    </html>

添加到暂存区：`$ git add index.html`; 提交到版本库：`$ git commit -m "Added <body>"`。
主分支代码已经被修改并提交。这时切换到RB_1.0分支，切换分支使用命令`git checkout`

    $ git checkout RB_1.0
这时会发现，在主分支上做的修改与提交都消失了。
在发布前做最后的修改：加入<head>和<title>标签。

    <html>
        <head>
            <title>Home Page</title>
        </head>
        <body>
            <h1>hello world</h1>
        </body>
    </html>
添加暂存区：`$ git add index.html`; 提交到版本库：`$ git commit -m "release branch"`。
现在可以发布了，为此，要给这个版本打个标签。 

#### 2.5 处理发布
　　给Git中的文件打标签，意味着在版本库的历史中标记出特定的点，这样将来就比较容易找到相应版本的代码。现在打一个名为1.0的标签：

    $ git tag 1.0 RB_1.0
上面的命令作用是在RB_1.0分支上打上一个标签，名为1.0。这时可以使用不带参数的`git tag`命令查看标签:

    $ git tag
　　在给代码打过标签以，需要做一些整理工作。现在两条分支(master和RB_1.0)有不同的提交。创建RB_1.0以后，主分支用于版本2.0上新功能开发，现在要把RB_1.0分支上所做的修改合并到主分支上来。
　　使用变基命令`git rebase`可以实现这项工作。变基是把一条分支上的修改在另一条分支的末梢重现。
　　首先使用`git checkout`命令切回到主分支：

    $ git checkout master
　　使用命令`git rebase`，后面跟一个参数：希望变基到那条分支末梢的分支名称。

    $ git rebase RB_1.0
最后，使用`git branch -d`命令删除发布分支RB_1.0(由于在RB_1.0分支末梢打过标签，只要标签在，提交记录就都在）。

    $ git branch -d RB_1.0


## 第二部分 Git日常用法
### 三、添加与提交
#### 3.1 添加文件到暂存区

> 暂存的变更就是工作区中那些打算提交到版本库的变更。暂存操作将会更新Git的内部索引，该索引称为暂存区。
> 通过暂存区，可以设置哪些变更要提交到版本库，哪些暂时不提交。

命令：`git add`
功能：添加新文件和修改版本库中已有的文件到暂存区。
用法：`git add <file1> <file2> ...`
参数： 
* `-i` 启动交互命令提示符，这种方式可以交互暂存新文件，暂存对已有文件的修改，甚至只部分修改。
它会有几个选项可以选择。
>  1: status       2: update       3: revert       4: add untracked
>  5: patch        6: diff         7: quit         8: help
>  2 是添加文件到暂存区；3 是取消已暂存的修改；5 可以选择单个或多个文件，选择后会显示这些文件的当前内容与版本库中的差异。
* `-p` 直接进入补丁(patch)模式。

#### 3.2 提交到版本库
　　提交将变更添加到版本库的历史记录中，并为它们分配一个提交名称。
命令：`git commit`
功能：将暂存区的修改提交到版本库中。
参数：
* `-m` 本次提交的说明文字。可以传递多个`-m`。如果不带-m参数，Git会启动编辑器来编辑说明文件，用此方式时可以添加`-v`将要提交的内容与版本库中的比较结果添加到编辑器中。
* `-a` 把工作区中当前所有的修改直接提交到版本库中。注意：只会把已纳入版本库的文件提交到版本库，不会添加尚未被跟踪的文件。

#### 3.3 查看修改的内容
　　使用`git status` 和 `git diff`，查看工作区中做的修改。
1. 看到状态
命令：`git status`
功能：查看工作区的变动。
参数：
* `-s` 简短显示
* `-b` 查看分支信息

2. 查看文件改动
命令：`git diff`
功能：显示工作区、暂存区及版本库之间的差异。
参数：如果不带参数，将显示工作区与暂存区之间的区别。
* `--cached` 显示暂存区与版本库中的区别。
* `HEAD` 显示工作区、暂存区的与版本的差别。 `$ git diff HEAD`

#### 3.4 管理文件
##### 3.4.1 文件重命名与移动
命令：`git mv <原文件名称> <新文件名称>`
功能：使用原文件的内容来创建新文件，新文件保留原文件的历史修改记录，并删除原文件。
> 如果不使用git mv命也可以监测到文件移动 ，但会增加操作步骤：首先移动文件，然后`git add`添加新文件，最后`git rm`删除旧文件。

##### 3.4.2 忽略文件
　　将要忽略的文件名添加到`.gitignore`文件中。 支持通配符，如*.swp。这样，`git status`就不会显示文件名`.swp`结尾的文件了，取而代之的是一个新的`.gitignore`文件。

### 四、分支
#### 4.1 什么叫分支
　　实际工作中，要为许多任务设定优先级。如添加新功能、重构代码或修正Bug等，如果只使用一条版本来跟踪无法满足要求，因此需要创建和使用多条分支，多条分支可用来记录不同的版本记录。
　　Git中，任何修改和都是在分支上完成的，默认有一个主分支(master)。可以将主分支重命名。

    $ git branch -m master newmaster

#### 5.2 创建新分支
* 创建分支
命令：`git branch <分支名>`
功能：创建指定名称的分支。

* 查看分支
命令:`git branch`
功能：以列表形式查看所有的分支。当前所在分支用`*`指示。

* 切换分支
命令：`git checkout <分支名>`
功能：切换分支。

* 创建并切换到新分支
命令：`git checkout -b <分支名>`
功能：创建并切换到新分支



