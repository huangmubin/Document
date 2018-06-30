# Git

* Working Directory
* Repository
    * stage
    * master

![git](_images/git_1.jpg)

# Install

Install git.

```
$ sudo apt-get install git
```

To check if git has a successful installation.

```
$ git

usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]
```

# Create repository: init

```
$ git init

Initialized empty Git repository in /Users/myron/Developer/Temp/GitTemp/.git/
```

# File operation: add rm

Add file contents to the index.

```
git add [--verbose | -v] [--dry-run | -n] [--force | -f]
        [--interactive | -i] [--patch | -p] [--edit | -e]
        [--[no-]all | --[no-]ignore-removal | [--update | -u]]
        [--intent-to-add | -N] [--refresh] [--ignore-errors]
        [--ignore-missing] [--] [<pathspec>...]
```

```
$ git add *
$ git add <#file#>
```

Remove files from the working tree and from the index.

```
git rm [-f | --force] [-n] [-r] [--cached]
        [--ignore-unmatch] [--quiet] [--] <file>...
```

```
$ git rm <#file#>
```

# Record changes: commit

Record changes to the repository

```
git commit [-a | --interactive | --patch] [-s] [-v] [-u<mode>]
        [--amend] [--dry-run]
        [(-c | -C | --fixup | --squash) <commit>]
        [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
        [--allow-empty-message] [--no-verify] [-e]
        [--author=<author>] [--date=<date>] [--cleanup=<mode>]
        [--[no-]status] [-i | -o] [-S[<keyid>]] [--] [<file>...]
```

```
$ git commit -m <#commit_content#>

[master (root-commit) 3ed09f4] update
 4 files changed, 14 insertions(+)
 create mode 100644 ToolBoxTestPlayground.playground/Contents.swift
 create mode 100644 ToolBoxTestPlayground.playground/contents.xcplayground
 create mode 100644 ToolBoxTestPlayground.playground/playground.xcworkspace/contents.xcworkspacedata
```

# Restore: checkout reset

## checkout

Switch branches or restore working tree files.

```
git checkout [-q] [-f] [-m] [<branch>]
git checkout [-q] [-f] [-m] --detach [<branch>]
git checkout [-q] [-f] [-m] [--detach] <commit>
git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new_branch>] [<start_point>]
git checkout [-f|--ours|--theirs|-m|--conflict=<style>] [<tree-ish>] [--] <paths>...
git checkout [-p|--patch] [<tree-ish>] [--] [<paths>...]
```

Restore working tree files

```
$ git checkout *
$ git checkout <#file#>
```

## Reset

Reset current HEAD to the specified state

```
git reset [-q] [<tree-ish>] [--] <paths>...
git reset (--patch | -p) [<tree-ish>] [--] [<paths>...]
git reset [--soft | --mixed [-N] | --hard | --merge | --keep] [-q] [<commit>]
```

Reset the stage changes to last commit

```
$ git reset 
$ git reset HEAD <#file#>

Unstaged changes after reset:
M	AppDelegate.swift
```

Move the current HEAD to specified state

```
// revoke the stage
$ git reset HEAD
// revoke the last modification commit
$ git reset HEAD^
// revoke the next to last modification commit
$ git reset HEAD^^
// revoke the next 100 to last modification commit
$ git reset HEAD~100
// revoke to the commit with number
$ git reset --hard afff9fa39bdb5fbbdbc553965319919a858a21a7
```

# Log status: status diff log reflog

## status

Show the working tree status.

```
git status [<options>...] [--] [<pathspec>...]
```

```
$ git status

On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   AppDelegate.swift
	new file:   AppDelegate2.swift
```

## diff

Show changes between commits, commit and working tree, etc

```
git diff [options] [<commit>] [--] [<path>...]
git diff [options] --cached [<commit>] [--] [<path>...]
git diff [options] <commit> <commit> [--] [<path>...]
git diff [options] <blob> <blob>
git diff [options] [--no-index] [--] <path> <path>
```

Different with stage.

```
$ git diff 
$ git diff <#file#>

diff --git a/AppDelegate.swift b/AppDelegate.swift
index ba522c3..807d807 100644
--- a/AppDelegate.swift
+++ b/AppDelegate.swift
@@ -2,3 +2,4 @@
 1234567
 12345678
 123
+dafad
```

A commit different with other commit

```
$ git diff 1ab0b34e03f65c6 53aee5fae7d07a3

diff --git a/AppDelegate.swift b/AppDelegate.swift
index ba522c3..11c02b0 100644
--- a/AppDelegate.swift
+++ b/AppDelegate.swift
@@ -1,4 +1,2 @@
 123456
 1234567
-12345678
-123
diff --git a/AppDelegate2.swift b/AppDelegate2.swift
deleted file mode 100644
index 190a180..0000000
--- a/AppDelegate2.swift
+++ /dev/null
@@ -1 +0,0 @@
-123
```

## log

Show commit logs

```
git log [<options>] [<revision range>] [[--] <path>...]
```

All log

```
$ git log

commit 1ab0b34e03f65c6d37876b02dd28c037eae28f7a
Author: Myron <hmb87381041@163.com>
Date:   Thu Mar 23 11:05:02 2017 +0800

    update5

commit 53aee5fae7d07a387e3a375a92cd466ed34da649
Author: Myron <hmb87381041@163.com>
Date:   Thu Mar 23 10:48:58 2017 +0800

    update2
```

id + commit

```
git log --pretty=oneline

1ab0b34e03f65c6d37876b02dd28c037eae28f7a update5
53aee5fae7d07a387e3a375a92cd466ed34da649 update2
```

graph

```
$ git log --graph --pretty=oneline --abbrev-commit

*   55f1da8 merge with no-ff
|\  
| * 4264eb0 add
|/  
*   0257385 Merge branch 'name'
|\  
| * e6a5fe2 name
* | cb9c8c4 mast
* | 07b9c74 test
|/  
* 196ccf1 remove
* 441b100 YES
```

## reflog

Manage reflog information

```
git reflog <subcommand> <options>
```

```
$ git reflog

1ab0b34 HEAD@{0}: commit: update5
53aee5f HEAD@{1}: reset: moving to HEAD^^
3e11d09 HEAD@{2}: commit: update4
475935c HEAD@{3}: commit: update3
53aee5f HEAD@{4}: reset: moving to HEAD
53aee5f HEAD@{5}: reset: moving to HEAD
53aee5f HEAD@{6}: reset: moving to HEAD
53aee5f HEAD@{7}: reset: moving to HEAD
53aee5f HEAD@{8}: reset: moving to HEAD
53aee5f HEAD@{9}: commit: update2
afff9fa HEAD@{10}: commit: upda
3ed09f4 HEAD@{11}: commit (initial): update
```

# Branch Merge

List, create, or delete branches

```
git branch [--color[=<when>] | --no-color] [-r | -a]
     [--list] [-v [--abbrev=<length> | --no-abbrev]]
     [--column[=<options>] | --no-column]
     [(--merged | --no-merged | --contains) [<commit>]] [--sort=<key>]
     [--points-at <object>] [<pattern>...]
git branch [--set-upstream | --track | --no-track] [-l] [-f] <branchname> [<start-point>]
git branch (--set-upstream-to=<upstream> | -u <upstream>) [<branchname>]
git branch --unset-upstream [<branchname>]
git branch (-m | -M) [<oldbranch>] <newbranch>
git branch (-d | -D) [-r] <branchname>...
git branch --edit-description [<branchname>]
```

## List branch

```
$ git branch

* dev
  master
```

## Create branch

```
$ git branch <#new_branch_name#>
```

## Switch branch

```
$ git checkout <#branch_name#>

Switched to branch 'dev'
```

## Merge branch

```
$ git merge <#some_branch_want_merge_to_this_branch#>

Already up-to-date.
```

## Delete branch

```
$ git branch -d <#delete_branch#>
```

Delete branch whatever

```
$ git branch -D <#delete_branch#>
```



# Bug 分支

* `git stash`

把当前工作区的所有东西都临时存储起来并返回原始状态。

```
$ git stash

Saved working directory and index state WIP on master: 55f1da8 merge with no-ff
HEAD is now at 55f1da8 merge with no-ff
```

* `git stash list`

查看被储存起来的列表

```
$ git stash list

stash@{0}: WIP on master: 55f1da8 merge with no-ff
```

* `git stash apply stash@{0}`

恢复某一个保存点，并且不删除它。

* `git stash drop stash@{0}`

删除一个保存点

* `git stach pop stash@{0}`

恢复并删除某个保存点

# 标签

* `git tag` 查看所有标签
* `git tag <tag name>` 新增标签
* `git tag <tag name> <commit id>` 给某个一提交打上标签
* `git show <tag name>` 显示标签信息
* `git tag -a <tag name> -m <tagCommit> <commit id>` 创建带文字说明的标签
* `git tag -d <tag name>` 删除标签


# 远程提交

## SSH Key 秘钥

1. 创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

2. 到远程仓库中设置 id_rsa.pub 文件里的内容。作为 SSH Key

## 关联远程仓库

```
$ git remote add origin git@github.com:michaelliao/learngit.git
```

## 推送 master 分支的所有内容

/// 第一次
```
git push -u origin master
```

/// 之后
```
git push origin master
```

michaelliao 是仓库名称

## 克隆一个仓库

```
$ git clone git@github.com:michaelliao/gitskills.git
```


# 参考资料

[廖雪峰: 史上最浅显易懂的 Git 教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000) (当真是业界良心……)

---
<!--  


  -->

# 2016-10-16 新增: 让 Git 忽略某一种文件

* 步骤
    * 添加 .gitignore_global 文件，通常添加在: ~/.gitignore_global
    * 在 ~/.gitconfig 中添加 .gitignore_global

> .gitignore_global 内容如下，可自行选择，只保留不需要 git 添加的文件类型。

```
# .gitignore_global
####################################
######## OS generated files ########
####################################
.DS_Store
.DS_Store?
*.swp
._*
.Spotlight-V100
.Trashes
Icon?
ehthumbs.db
Thumbs.db
####################################
############# Packages #############
####################################
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip
```

> .gitconfig 内容，[core] 以及后面的内容是自行添加的。

```
[filter "lfs"]
        clean = git-lfs clean %f
        smudge = git-lfs smudge %f
        required = true
[user]
        name = huangmubin
        email = hmb87381041@163.com
[core]
        excludesfile = /Users/Myron/.gitignore_global
```

