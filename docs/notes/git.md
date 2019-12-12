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
