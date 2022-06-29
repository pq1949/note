### git 提交规范

```
feat: (new feature for the user, not a new feature for build script)

fix: (bug fix for the user, not a fix to a build script)

docs: (changes to the documentation)

style: (formatting, missing semi colons, etc; no production code change)

refactor: (refactoring production code, eg. renaming a variable)

test: (adding missing tests, refactoring tests; no production code change)

chore: (updating grunt tasks etc; no production code change)

```

https://gist.github.com/joshbuchea/6f47e86d2510bce28f8e7f42ae84c716s


https://github.com/conventional-changelog/conventional-changelog/blob/9c359faacea93b566f19c4c7214a6bca58edf99f/conventions/angular.md

https://www.conventionalcommits.org/zh/v1.0.0-beta.2/


### git配置

- 查看`git`的配置文件的位置
```bash
 git config --list --show-origin
```
- 打开配置文件
```bash
git config -e [--local] [--global] (默认是`global`)
git config --global user.name "xxx"  也可以直接设置，不用打开编辑器
```

### 提交
```bash
git add . （做了修改（包括文件的添加、删除和修改））
git commit -m "message"

git commit -am “message” (只做了修改，没有删除和添加）

git commit --amend  修改上次的提交

```
### 同步Github fork 出来的分支

1、配置remote，指向原始仓库
```
git remote add upstream https://github.com/InterviewMap/InterviewMap.git
```
2、上游仓库获取到分支，及相关的提交信息，它们将被保存在本地的 upstream/master 分支
```
git fetch upstream
# remote: Counting objects: 75, done.
# remote: Compressing objects: 100% (53/53), done.
# remote: Total 62 (delta 27), reused 44 (delta 9)
# Unpacking objects: 100% (62/62), done.
# From https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY
# * [new branch] master -> upstream/master
```
3、切换到本地的 master 分支

```
git checkout master
# Switched to branch 'master'
```
4、把 upstream/master 分支合并到本地的 master 分支，本地的 master 分支便跟上游仓库保持同步了，并且没有丢失本地的修改。
```
git merge upstream/master
# Updating a422352..5fdff0f
# Fast-forward
# README | 9 -------
# README.md | 7 ++++++
# 2 files changed, 7 insertions(+), 9 deletions(-)
# delete mode 100644 README
# create mode 100644 README.md
```
5、上传到自己的远程仓库中
`git push `

### centos 利用yum更新git


```
#安装源
yum install http://opensource.wandisco.com/centos/7/git/x86_64/wandisco-git-release-7-2.noarch.rpm
#安装git
yum install git
#更新git
yum update git
```
https://my.oschina.net/tonystark/blog/1920556


### 查看 git 配置是哪个文件生效的
```
$ git config --get-all --show-origin core.autocrlf
file:"C:\\ProgramData/Git/config"       true
file:C:/Users/Administrator/.gitconfig  false
```

### git撤销merge,彻底学会git revert的用法

revert 可以取消指定的某次提交内容。

当讨论 revert 时，需要分两种情况，因为 commit 分为两种：一种是常规的 commit，也就是使用 git commit 提交的 commit；另一种是 merge commit，在使用 git merge 合并两个分支之后，你将会得到一个新的 merge commit。

merge commit 和普通 commit 的不同之处在于 merge commit 包含两个 parent commit，代表该 merge commit 是从哪两个 commit 合并过来的

```
git show bd86846
commit bd868465569400a6b9408050643e5949e8f2b8f5
Merge: ba25a9d 1c7036f
```
revert 常规 commit
使用 git revert <commit id> 即可，git 会生成一个新的 commit，将指定的 commit 内容从当前分支上撤除。

revert merge commit
revert merge commit 有一些不同，这时需要添加 -m 选项以代表这次 revert 的是一个 merge commit

但如果直接使用 git revert ，git 也不知道到底要撤除哪一条分支上的内容，这时需要指定一个 parent number 标识出"主线"，主线的内容将会保留，而另一条分支的内容将被 revert。

如上面的例子中，从 git show 命令的结果中可以看到，merge commit 的 parent 分别为 ba25a9d 和 1c7036f，其中 ba25a9d 代表 master 分支（从图中可以看出），1c7036f 代表 will-be-revert 分支。需要注意的是 -m 选项接收的参数是一个数字，数字取值为 1 和 2，也就是 Merge 行里面列出来的第一个还是第二个。

我们要 revert will-be-revert 分支上的内容，即 保留主分支，应该设置主分支为主线，操作如下：

```
git revert -m 1 bd86846
```

https://www.cnblogs.com/bescheiden/articles/10563651.html


### git 操作场景

https://ohshitgit.com/
