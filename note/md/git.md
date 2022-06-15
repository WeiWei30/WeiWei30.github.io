[toc]

# 安装

Mac通过Homebrew安装：

```bash
xcode-select --install
brew install git
```

# 初始化

设置用户名和邮箱

```
git config --global user.name "user name"
git config --global user.email xxx@xxx.com
```

初始化仓库

```
cd repository_path
git init
```

# 逻辑

追踪文件：该文件的所有修改被纳入git管理范围

修改文件：所有修改的版本(modified)被纳入暂存区(staged)

提交新版：将暂存区的文件发布(commit)为新版文件，所有文件变为未修改状态

1. `git status`

[三大分区介绍](https://blog.csdn.net/qq_32452623/article/details/78417609)

![img](../img/2.png)

采用`git status`查询文件当前状态：

*changes to be committed*：与上一版commit相比被修改的文件，将会在下次commit中发布

- *new file*：新添加的文件
- *modified*：已存在但被修改的文件

*changes not staged for commit*：未被追踪的文件，但被修改了，如果不纳入追踪，就不会在下次被commit

2. `git add`

使用`git add`追踪文件的更改，将其纳入暂存区。没有被加入暂存区的文件即使被修改，也不会发不到新版本中。add的意义在于，你可以选择哪些修改是需要在这次commit中提交的，而哪些修改可以留给之后提交。

- `git add .`：提交被修改和新建的文件，但不包括被删除的文件
- `git add -u --update`：提交所有更改的文件
- `git add -A --all`：提交已被修改和已被删除的文件，但不包括新文件

3. `git commit`

提交暂存区的修改到新版本。git会保存每个版本的所有文件

# 撤销

1. 二次提交

```
git commit -m 'initial commit'
git add forgotten_file
git commit --amend
```

只有一个版本，第二次提交的会完全代替第一次提交的。更好的控制仓库历史。

2. 将文件从暂存区返回工作区

```
git rest HEAD <file name>
```

等待下次提交

3. 撤销修改

```
git checkout -- <file name>
```

将其还原至上次提交时的样子(或者刚克隆完的样子，或者刚把它放入工作目录时的样子)，是在本地工作区还原。