---
layout: default
title: Git
# parent: Linux
---

# Git

git is a version control system for tracking changes in source code during software development processes.

## Getting Started

### Create a Repository

Create a new local repository 

```shell
$ git init [project name]
```

Clone a repository 
``` shell
$ git clone git_url
```

Clone a repository into a specified directory 

```shell
$ git clone git_url my_directory
```

### Make a change
Show modified files in working directory, staged for your next commit
``` shell
$ git status
```

Stages the file, ready for commit 

```shell
$ git add [file]
```

Stage all changed files, ready for commit
``` shell
$ git add .
```

Commit all staged files to versioned history 

```shell
$ git commit -m "commit message"
```

Commit all your tracked files to versioned history
``` shell
$ git commit -am "commit message"
```

Unstages file, keeping the file changes 

```shell
$ git reset [file]
```

Revert everything to the last commit
``` shell
$ git reset --hard
```

Diff of what is changed but not staged 

```shell
$ git diff
```

Diff of what is staged but not yet commited
``` shell
$ git diff --staged
```

Apply any commits of current branch ahead of specified one 

```shell
$ git rebase [branch]
```

### Configuration

Set the name that will be attached to your commits and tags
``` shell
$ git config --global user.name "name"
```

Set an email address that will be attached to your commits and tags 

```shell
$ git config --global user.email "email"
```

Enable some colorization of Git output
``` shell
$ git config --global color.ui auto
```

Edit the global configuration file in a text editor 

```shell
$ git config --global --edit
```

### Working with Branches

List all local branches
``` shell
$ git branch
```

List all branches, local and remote 

```shell
$ git branch -av
```

Switch to a branch, my_branch, and update working directory
``` shell
$ git checkout my_branch
```

Create a new branch called new_branch 

```shell
$ git branch new_branch
```

Delete the branch called my_branch
``` shell
$ git branch -d my_branch
```

Merge branchA into branchB 

```shell
$ git checkout branchB 
$ git merge branchA
```

Tag the current commit
``` shell
$ git tag my_tag
```

### Observe your Repository

Show the commit history for the currently active branch 

```shell
$ git log
```

Show the commits on branchA that are not on branchB
``` shell
$ git log branchB..branchA
```

Show the commits that changed file, even across renames 

```shell
$ git log --follow [file]
```

Show the diff of what is in branchA that is not in branchB
``` shell
$ git diff branchB...branchA
```

Show any object in Git in human-readable format 

```shell
$ git show [SHA]
```

### Synchronize

Fetch down all the branches from that Git remote
``` shell
$ git fetch [alias]
```

Merge a remote branch into your current branch to bring it up to date 

```shell
$ git merge [alias]/[branch]
```

Transmit local branch commits to the remote repository branch
``` shell
$ git push [alias] [branch]
```

Fetch and merge any commits from the tracking remote branch 

```shell
$ git pull
```

Merge just one specific commit from another branch to your current branch
``` shell
$ git cherry-pick [commit_id]
```

### Remote

Add a git URL as an alias 

```shell
$ git remote add [alias] [url]
```

Show the names of the remote repositories you've set up
``` shell
$ git remote
```

Show the names and URLs of the remote repositories 

```shell
$ git remote -v
```

Remove a remote repository
``` shell
$ git remote rm [remote repo name]
```

Change the URL of the git repo 

```shell
$ git remote set-url origin [git_url]
```

### Temporary Commits

Save modified and staged changes
``` shell
$ git stash
```

List stack-order of stashed file changes 

```shell
$ git stash list
```

Write working from top of stash stack
``` shell
$ git stash pop
```

Discard the changes from top of stash stack 

```shell
$ git stash drop
```

### Tracking path Changes
Delete the file from project and stage the removal for commit
``` shell
$ git rm [file]
```

Change an existing file path and stage the move 

```shell
$ git mv [existing-path] [new-path]
```

Show all commit logs with indication of any paths that moved
``` shell
$ git log --stat -M
```

### Ignoring Files

```
/logs/*

!logs/.gitkeep

# Ignore Mac system files
.DS_store

# Ignore node_modules folder
node_modules

# Ignore SASS config files
.sass-cache
```

A `.gitignore` file specifies intentionally untracked files that Git should ignore

## Tricks

### Rename branch

* **Renamed to `new_name`**

```shell
$ git branch -m
```

* **Push and reset**

```shell
$ git push origin -u
```

* **Delete remote branch**

```shell
$ git push origin --delete
```

### Log

Search change by content 
```shell
$ git log -S''
```

Show changes over time for specific file
```shell
$ git log -p <file_name>
```

Print out a cool visualization of your log 
```shell
$ git log --pretty=oneline --graph --decorate --all
```

### Branch
List all branches and their upstreams 
```shell
$ git branch -vv
```

Quickly switch to the previous branch 
```shell
$ git checkout -
```

Get only remote branches
```shell
$ git branch -r
```

Checkout a single file from another branch 
```shell
$ git checkout --
```

### Commit
Rewrite last commit message
```shell
$ git commit -v --amend
```

### Git Aliases

```shell
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```

See also: [More Aliases](https://gist.github.com/johnpolacek/69604a1f6861129ef088)


## Set up the server

添加 git 用户

```shell
sudo adduser git
```

配置 SSH-Key 登录

```shell
scp ~/.ssh/id_rsa.pub git@lsong.org:~/lsong-key.pub

ssh git@lsong.org
...
mkdir /home/git/.ssh
cat lsong-key.pub >> .ssh/authorized_keys
sudo chown -R git:git /home/git/.ssh
sudo chmod 700 !$
sudo chmod 600 /home/git/.ssh/*
```

现在应该可以在本地通过 `git` 用户登录服务器了

```shell
ssh git@lsong.org
```

### 开始一个项目

在服务器上启动一个项目

```shell
cd ~git/
mkdir project.git
cd project.git
git --bare init
```

在本地开始这个项目

```shell
cd myproject
git init
git add .
git commit -m 'initial commit'
git remote add origin git@lsong.org:project.git
git push origin master
```

你也可以 `clone` 这个项目

```shell
git clone git@lsong.org:project.git
```

### 权限控制

#### 读写权限

让需要 `git` 服务写权限的用户将 SSH 公钥发给你

```shell
cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCB007n/ww+ouN4gSLKssMxXnBOvf9LGt4L
ojG6rs6hPB09j9R/T17/x4lhJA0F3FR1rP6kYBRsWj2aThGw6HXLm9/5zytK6Ztg3RPKK+4k
Yjh6541NYsnEAZuXz0jTTyAUfrtU3Z5E003C4oxOj6H0rfIF1kKI9MAQLMdpGW1GYEIgS9Ez
Sdfd8AcCIicTDWbqLAcU4UpkaX8KyGlLwsNuuGztobF8m72ALC/nLF6JLtPofwFBlgc+myiv
O7TCUSBdLQlgMVOFq1I2uPWQOkOWQAHukEOmfjy2jctxSDBQ220ymjaNsHT4kgtZg2AYYgPq
dAv8JggJICUvax2T9va5 gsg-keypair
```

然后你需要

```shell
cat /tmp/id_rsa.john.pub >> ~/.ssh/authorized_keys
```

这个用户就可以提交了

#### 只读权限

```shell
cd ~git/public_html
ln -s ../project.git project.git
```

要开启需要

```shell
cd project.git
mv hooks/post-update.sample ./hooks/post-update
chmod a+x ./hooks/post-update
./hooks/post-update
```

任何人都可以通过

```shell
git clone https://lsong.org/~git/project.git
```

来 `clone` 项目

### 安全性

你可以用 Git 自带的 `git-shell` 工具限制 `git` 用户的活动范围。只要把它设为 `git` 用户登入的 shell，那么该用户就无法使用普通的 bash 或者 csh 什么的 shell 程序。编辑 `/etc/passwd` 文件：

```shell
sudo vim /etc/passwd
```

在文件末尾，你应该能找到类似这样的行：

```shell
git:x:1000:1000::/home/git:/bin/sh
```

把 bin/sh 改为 /usr/bin/git-shell （或者用 `which git-shell` 查看它的实际安装路径）。该行修改后的样子如下：

```shell
git:x:1000:1000::/home/git:/usr/bin/git-shell
```

现在 `git` 用户只能用 SSH 连接来推送和获取 Git 仓库，而不能直接使用主机 shell。尝试普通 SSH 登录的话，会看到下面这样的拒绝信息：

```shell
$ ssh git@gitserver
fatal: What do you think I am? A shell?
Connection to gitserver closed.
```

### Git Server Alternatives

+ [GitLab](https://gitlab.com)
+ [Gogs](https://gogs.io)
+ [Gitea](https://gitea.io)