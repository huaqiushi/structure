版本控制
===========

.. contents:: 目录

基本流程
-----------
a. 创建远程仓库
b. checkout 创建本地仓库（git为clone）
c. add 从工作区添加代码 **（svn添加至本地仓库；git添加至暂存区）**
d. commit 提交代码 **（svn提交至远程仓库；git提交至本地仓库（之后push提交至远程仓库））**

注：git与svn的区别在于：git的本地仓库是远程仓库的克隆，而svn的本地仓库可以只有远程仓库的部分代码

Git命令
----------

#. git add    有两个用途： 一是将文件添加到工作区（执行命令前文件状态为untracked，执行后变为tracked）；二是将工作区中已修改的文件添加到暂存区（执行命令前文件状态为modified，执行后变为staged）
#. git commit    将暂存区文件提交到本地仓库（注：pycharm中的git插件对git add做了封装，commit前可以不add）
#. git push    将本地仓库文件提交到远程仓库
#. git status    查看工作区和暂存区状态
#. git fetch
#. git merge
#. git update
#. git checkout
#. git reset    版本回退
#. git rebase
#. git stash

使项目中的某些文件不被Git追踪
-------------------------------
1. 在本地仓库添加.gitignore文件可以匹配之后添加的文件，使其不被追踪
2. 对于已经被追踪的文件，使用下面的命令使其不被追踪

.. code-block:: shell

    $ git rm --cached README

Git中的文件的三种状态
----------------------
- 已修改（modified）：位于工作区。
- 已暂存（staged）：位于暂存区。对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中
- 已提交（committed）：位于本地仓库。

    - 注：工作区、暂存区和本地仓库都是逻辑意义上的划分，其在物理上通过对文件标记实现
    - 注：每次提交更新或保存项目状态时，git会对当前的全部文件制作一个 **快照** 并保存这个快照的 **索引**

.. image:: ../.img/git.JPG

Git分支
---------
在git中，分支与其文件之间的关系就是指针与object之间的关系。

    - 注1：创建分支实质上是创建一个指向当前object的指针（指针永远指向当时的object）
    - 注2：合并分支实质上是创建一个合并后的object并使两个指针均指向它

object
''''''''''
每一次commit或者merge后都会对当时的全部文件制作一个快照，这些快照即object

HEAD
''''''''
保存了用户当前所在的分支

FAQ
--------

Git版本回滚
''''''''''''''
1. 回滚整个提交: git checkout version-number
2. 回滚特定文件: git checkout version-number filename（提交代码时会给当前所有修改过的文件的修改行都打上同一个版本号）
