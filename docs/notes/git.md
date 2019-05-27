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
