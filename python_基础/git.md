一、从远程库克隆

先创建远程库，然后，从远程库克隆。

首先，登陆GitHub，创建一个新的仓库

![github-init-repo](https://liaoxuefeng.com/books/git/remote/clone/create-repo.png)

我们勾选`Initialize this repository with a README`，这样GitHub会自动为我们创建一个`README.md`文件。创建完毕后，可以看到`README.md`文件：

![github-init-repo-2](https://liaoxuefeng.com/books/git/remote/clone/repo-content.png)

现在，远程库已经准备好了，下一步是用命令`git clone`克隆一个本地库：

```plain
$ git clone git@github.com:michaelliao/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
Receiving objects: 100% (3/3), done.
```

注意把Git库的地址换成你自己的，然后进入`gitskills`目录看看，已经有`README.md`文件了：

```plain
$ cd gitskills
$ ls
README.md
```

二、连接远程仓库

git remote add origin  git@github.com:zhangjiaqi1126/study.git



三、第二步，进入克隆的目录，用命令`git add`告诉Git，把文件添加到仓库：

```
$ git add readme.txt
```

四、第三步，用命令`git commit`告诉Git，把文件提交到仓库：

```
$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```



五、第四步，把本地库的所有内容推送到远程库上：

```
$ git push -u origin master
```





要查看当前所在的Git分支，可以使用以下命令：

```bash
git branch
```

使用 `git checkout` 命令来切换到另一个分支。

例如，如果你想切换到名为 `dev` 的分支，可以使用以下命令：

```bash
git checkout dev
```