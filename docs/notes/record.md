

### AI

* [leon 一个开源的个人助手](https://github.com/leon-ai/leon)
  可以部署在服务器, 可以离线使用

### 文本编辑器
  * [smeditor 基于 Vue.js 2.0+ 石墨文档样式的富文本编辑器组件](https://github.com/GeekPark/smeditor)
  * [wangEditor 基于javascript和css开发的 Web富文本编辑器， 轻量、简洁、易用、开源免费](http://www.wangeditor.com/)
  * [Simditor An Easy and Fast WYSIWYG Editor](https://simditor.tower.im/)
  * [vditor 一款浏览器端的 Markdown 编辑器，使用 TypeScript 实现](https://github.com/b3log/vditor)
  * [CodeMirror 基于Javascript，短小精悍，实时在线代码高亮显示，他不是某个富文本编辑器的附属产品，他是许多大名鼎鼎的在线代码编辑器的基础库。](https://github.com/codemirror/CodeMirror)
    [demo](http://www.ibloger.net/assets/apps/tryit/index.html)
  * [Boostnote A markdown editor for developers on Mac, Windows and Linux](https://github.com/BoostIO/Boostnote)

### 图片素材网站
  * [Unsplash 高品质免费高清图片](https://unsplash.com/)
  * [知乎推荐的图片网址](https://www.zhihu.com/question/19619335)

### 团队协同工具
  * [leangoo](https://www.leangoo.com)
  * [trello](https://trello.com/)


### 服务资源
  * [chinese-xinhua 中华新华字典数据库。包括歇后语，成语，词语，汉字](https://github.com/pwxcoo/chinese-xinhua)
  * [知乎无限 live 数据库，仅供学术用途](https://github.com/calpa/zhihu-unlimited-live/blob/master/db.json)
  * [网易云音乐 Node.js API service](https://github.com/Binaryify/NeteaseCloudMusicApi)


### logo制作
  * [logomakr](https://logomakr.com/)
  * [logoaa](https://www.logoaa.com/)
  * [logoaplus](http://www.logoaplus.com)
  * [logaster](https://www.logaster.cn/)
  * [logosc](https://www.logosc.cn/)

### 文档工具
  * [docz](https://github.com/pedronauck/docz)
  * [docsify ](https://github.com/docsifyjs/docsify)
  * [docpress](https://github.com/docpress/docpress)
  * [vuepress](https://github.com/vuejs/vuepress)
  * [react-styleguidist](https://github.com/styleguidist/react-styleguidist)
  * [storybook](https://github.com/storybooks/storybook)
  * [docsify-demo-box-react](https://github.com/njleonzhang/docsify-demo-box-react)
  * [jsdoc-to-markdown](https://github.com/jsdoc2md/jsdoc-to-markdown)
  * [esdoc](https://github.com/esdoc/esdoc)
  * [apidoc](https://github.com/apidoc/apidoc)

### 表情
  * [emoji markup](https://gist.github.com/pq1949/540172a2d4e5db33980f99a9d2c8c5cc)

### 印记中文出品，唯一与官方文档同步的中文文档
  * https://www.docschina.org/


### 排序动画演示
  * https://visualgo.net/en/sorting  ⭐️⭐️⭐️⭐️⭐️


### 在线制作PPT
A framework for easily creating beautiful presentations using HTML

  * https://github.com/hakimel/reveal.js?utm_source=gold_browser_extension#full-setup
  * [Online Editor](https://slides.com/?ref=github)


### 搭建ssh服务器
  * https://github.com/Austin9999/new-pac/wiki/%E8%87%AA%E5%BB%BAss%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%95%99%E7%A8%8B

ssr安装脚本

```bash
wget -N --no-check-certificate https://softs.fun/Bash/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```

ssr备用脚本
```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
```

谷歌BBR加速脚本
```bash
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && bash bbr.sh
```

### 运行流畅的客服系统 ⭐️⭐️⭐️⭐️⭐️
动画
  * https://www.intercom.com/
  * https://small.chat/

### 国内客服

1. 美洽
2. 网易七鱼 https://qiyukf.com/

### Code Review 工具

  `phacility`  https://phacility.com  [预览](https://secure.phabricator.com/D20083)
  `gerrit` https://www.gerritcodereview.com/

### terminal for Windows⭐️⭐️⭐️⭐️⭐️

[MobaXterm](https://mobaxterm.mobatek.net/)



### yarn network error

```
info There appears to be trouble with your network connection. Retrying...
```
```bash
yarn config set proxy http://127.0.0.1:1080
yarn config set https-proxy http://127.0.0.1:1080
```

https://github.com/yarnpkg/yarn/issues/4890


### create-react-app 使用docz报错

`package.json`文件中加入

```json
"resolutions": {
  "ansi-styles": "^3.2.0"
}
```
删除lock文件重新install
```
rm yarn.lock && yarn
```

关于 `resolutions` 可以看[这里](https://yarnpkg.com/lang/zh-hans/docs/selective-version-resolutions/)，yarn专门用来解决指定安装特定版本包的字段

npm中没有对应的字段，不过可以用 `npm-force-resolutions`这个来解决 略显麻烦 所以还是用yarn吧

https://github.com/pedronauck/docz/issues/536

https://stackoverflow.com/questions/52416312/npm-equivalent-of-yarn-resolutions


### nginx 配置自签名证书

创建私钥
```
openssl genrsa -out server.key 1024
```
创建证书签名请求 (Common Name要填成对应网站的IP或者域名,其他的可忽略)
```
openssl req -new -key server.key -out server.csr
```

创建自签名证书 (可以添加  `-days 3650` 指定10年有效期 )
```
openssl x509 -req -in server.csr -signkey server.key -out server.crt
```
配置nginx

```
 server {
    listen 8082 ssl;
    ssl_certificate /home/leo/nginx/conf/server.crt;
    ssl_certificate_key /home/leo/nginx/conf/server.key;
    location / {
       alias /home/leo/webim/;
     }
   }

```

https://ningyu1.github.io/site/post/51-ssl-cert/

http://blog.harrisonxi.com/2017/02/%E7%BB%99nginx%E5%88%9B%E5%BB%BA%E4%B8%AA%E8%87%AA%E7%AD%BE%E5%90%8DSSL%E8%AF%81%E4%B9%A6.html


### CentOS 7 更新nginx

切换到root用户，新建如下文件
```
vi /etc/yum.repos.d/nginx.repo
```

贴入如下内容
```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
```

开始更新
```
yum update nginx
```

之前有启动过nginx，需要先停止在更新
```
sudo service nginx stop
```

```
sudo service nginx start
```

https://codybonney.com/install-the-latest-version-of-nginx-on-centos-6-and-centos-7-using-yum/


### nginx 403 Forbidden
可能是文件访问权限的问题
nginx version: nginx/1.14.2
默认配置文件中是用nginx这个用户启动的，所以会没有权限
```
root     21877     1  0 17:42 ?        00:00:00 nginx: master process nginx
nginx    25148 21877  0 17:54 ?        00:00:00 nginx: worker process

```
把配置文件的用户改成静态资源所属的用户即可

https://www.jianshu.com/p/e0dadb871894


### git alias 配置

```
git config --list | grep alias
alias.lg=log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
alias.st=status
alias.ci=commit
alias.co=checkout
alias.br=branch


git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
git config --global alias.st status


or edit  .gitconfig

[credential]
        helper = manager
[difftool "sourcetree"]
        cmd = 'd:/Program Files/Beyond Compare 4/BComp.exe' \"$LOCAL\" \"$REMOTE\"
[mergetool "sourcetree"]
        cmd = 'd:/Program Files/Beyond Compare 4/BComp.exe' \"$LOCAL\" \"$REMOTE\" \"$BASE\" \"$MERGED\"
        trustExitCode = true
[core]
        autocrlf = false
        safecrlf = true
[alias]
        lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
        st = status
        ci = commit
        co = checkout
        br = branch
```


### 找技术库的网站 ⭐️⭐️⭐️

www.awesomes.cn/


### webpac在线配置 ⭐️⭐️⭐️

https://createapp.dev/


### css裁剪路径 ⭐️⭐️⭐️

https://bennettfeely.com/clippy/
### Package Diff

https://diff.intrinsic.com/?pkg=&min=&max=


### 获取本机ip地址

```js
function getIPAdress(){
    var interfaces = require('os').networkInterfaces();
    for(var devName in interfaces){
          var iface = interfaces[devName];
          for(var i=0;i<iface.length;i++){
               var alias = iface[i];
               if(alias.family === 'IPv4' && alias.address !== '127.0.0.1' && !alias.internal){
                     return alias.address;
               }
          }
    }
}
```


### git教程

https://learngitbranching.js.org/


### 不错的nodejs教程

https://nodeschool.io/zh-cn/


### git bash 新增命令别名

打开`gitbash` 直接`cd`进入个人根目录
```bash
cd
notepad .bashrc
```
输入下面内容到 `.bashrc` 文件
notepad++的安装目录中如果有特殊字符，可以用 `\` 进行转义
```
alias o="/d/Program\" \"Files\" \"\(x86\)/Notepad++/notepad++.exe"
```


### windows Terminal 安装

1. `git clone git@github.com:microsoft/Terminal.git`
2. `git submodule update --init --recursive`
3. `.\nuget restore OpenConsole.sln` ( `nuget` 可以在`\dep\nuget`中找到)
4. 安装 `visual studio 2017`  https://docs.microsoft.com/en-us/visualstudio/releasenotes/vs2017-relnotes 2019也安装过，错误比较多就换了
5. 用`visual studio 2017` 打开 `OpenConsole.sln` 生产解决方案，不出意外，会有些错误，按照提示去网上搜解决办法，
    其中一个改了比较久的是pch内存不够，这个需要改一下windows的默认的虚拟内存，同时 visual studio 中对应设置成\zm200 获取其他可以
6. 需要设置成 release 和 x64 进行构建
7. 最后好不容易编译好了，又会提示windows版本不够要升级，那就升级一下吧，注册账号，更新到windows预览版
   ![](../imgs/Snipaste_2019-05-08_15-10-52.png)
8. 然后在部署就可以成功了
   ![](../imgs/Snipaste_2019-05-08_16-25-37.png)

装完后可以在win10商店中安装一下wsl玩玩

ubuntu或者debian，安装之前需要 进入应用，选择程序和功能，点击启用或关闭Windows功能，勾选适用于Linux的Windows子系统
![](../imgs/Snipaste_2019-05-08_16-34-55.png)

`ubuntu`和`debian`的目录在`windows`中下面对应的目录里

```
C:\Users\Administrator\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs

C:\Users\Administrator\AppData\Local\Packages\TheDebianProject.DebianGNULinux_76v4gfsz19hv4\LocalState\rootfs\home\leo
```

有意思的是在windows中直接复制或者新建文件在wsl中是看不到这个文件的，但是wsl新建同名文件保存又会提示失败。

通过在wsl的shell中 输入 `explore.exe .` 打开对应的网络位置后，可以进行两个系统的文件共享

`\\wsl$` 这个就是安装的系统共享的目录

WSL 使用指南
https://github.com/microsoft/Terminal/issues/489#issue-441161390


wsl 中还可以配置一下 hosts文件 登录的时候会更加方便，wsl中设置启动默认的用户是 `debian config --default-user root` 切换到 `root`用户后可以用 `passwd`更改密码

https://zhuanlan.zhihu.com/p/36482795

### windows 批量重命名

`ren *.txt *.sql`
https://blog.csdn.net/zhouzihan520xj/article/details/40301087


### 除了追番，你还可以在 B 站爱上学习
https://sspai.com/post/54624


### dva与umi笔记
https://yewills.github.io/2019/05/19/dva_umi/

### 网页模板
http://www.ym4j.com/


### js 调用栈演示
http://latentflip.com/loupe/


### 评论
- [Valine ](https://valine.js.org/)
- [GITALK](https://gitalk.github.io/)


### Canvas + WebSocket + Redis 实现一个视频弹幕
https://segmentfault.com/a/1190000016654011


### 简述 OAuth 2.0 的运作流程
https://www.barretlee.com/blog/2016/01/10/oauth2-introduce/


### node 爬虫全栈
https://github.com/yhlben/cdfang-spider

### Kiwi-国际化全流程解决方案
https://github.com/alibaba/kiwi


### 一个基于 React 的可缩放图片控件
https://github.com/Caldis/react-zmage

###  下载视频
https://www.urlgot.com/

https://www.clipconverter.cc/

https://mac.eltima.com/cn/youtube-downloader-mac.html


1. 下载视频
https://www.urlgot.com/

2. 自动识别字幕
https://www.8bage.com/

3. 字幕格式转换(ass->srt)
http://www.nicetool.net/app/subtitle_convert.html


### centOS 安装 Gitlab Runner

https://mirror.tuna.tsinghua.edu.cn/help/gitlab-runner/

1. 新建 `/etc/yum.repos.d/gitlab-runner.repo`

```
[gitlab-runner]
name=gitlab-runner
baseurl=https://mirrors.tuna.tsinghua.edu.cn/gitlab-runner/yum/el7
repo_gpgcheck=0
gpgcheck=0
enabled=1
gpgkey=https://packages.gitlab.com/gpg.key
```
2. 执行
```
sudo yum makecache
sudo yum install gitlab-runner
```
3. 启动
```
sudo gitlab-runner start
```

### 徽章地址 Badges

https://shields.io/
https://badgen.net/
https://forthebadge.com/
https://badge.fury.io/
https://github.com/boennemann/badges

### 使用Astah Community建UML类图之总结
https://www.cnblogs.com/wuhuisheng/archive/2012/09/12/2682263.html
### restful-api-design-references
https://github.com/aisuhua/restful-api-design-references

### 正则表达式
1. [learn-regex](https://github.com/ziishaned/learn-regex/blob/master/translations/README-cn.md)


### chrome 插件开发

1. [Chrome 插件开发官方文档 What are extensions?](https://developer.chrome.com/extensions)
2. [Chrome扩展及应用开发（首发版）](http://www.ituring.com.cn/book/miniarticle/110853)
3. [360极速浏览器翻译的官方文档](http://open.chrome.360.cn/extension_dev/overview.html)

### 静态页面

1. http://8.101.com/  动画流畅


### 在线 ppt
1. https://slides.com/
2. https://ppt.baomitu.com/

### UI

[创建华丽 UI 的 7条规则](https://juejin.im/post/5ce6407cf265da1bb13f0a2a)

### Homebrew 镜像使用帮助
1. 替换现有上游
```bash
git -C "$(brew --repo)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
//git -C "$(brew --repo)" remote set-url origin https://mirrors.ustc.edu.cn/brew.git/

git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
//git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git/

brew update
```
2. 复原
```bash
git -C "$(brew --repo)" remote set-url origin https://github.com/Homebrew/brew.git

git -C "$(brew --repo homebrew/core)" remote set-url origin https://github.com/Homebrew/homebrew-core

brew update
```

### iterm2 自动登录

![](../imgs/iterm2-profiles.png)
```bash
set user xxx
set host xxx
set password xxxxx

set timeout 30
spawn ssh $user@$host
expect {
        "(yes/no)?"
        {send "yes\r";exp_continue}
        "password:"
        {send "$password\r"}
}
interact
```
https://blog.csdn.net/shaobo8910/article/details/75514849
https://codingstyle.cn/topics/31

### Mac优化之Finder自定义全局快捷键
https://juejin.im/post/5b9486fcf265da0acc7943d3

### install  zsh

1. check
```bash
cat /etc/shells
// or
chsh -l
```
2. install zsh
```bash
yum install zsh -y
chsh -s /bin/zsh
```

3. install oh-my-zsh
https://github.com/robbyrussell/oh-my-zsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
//or
sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
//or
curl -Lo install.sh https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh
sh install.sh
```
1. Themes

查看已安装主题 `ls ~/.oh-my-zsh/themes`

**主题**
主题预览： https://github.com/robbyrussell/oh-my-zsh/wiki/Themes
修改主题， 直接修改 `.zshrc` 中 `ZSH_THEME="agnoster"` 为对应名称即可

`agnoster` 主题乱码时,把 Powerline  字体安上 `sudo apt-get install fonts-powerline`

https://github.com/powerline/fonts


**插件**
- 自动补全: `git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
`

修改 `.zshrc` 中 `plugins=(git zsh-autosuggestions)`
https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md

- 高亮
 `git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting`

 修改 `.zshrc` 中 `plugins=(git zsh-autosuggestions zsh-syntax-highlighting)`
https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md

#### 代理
```bash
# proxy list
alias proxy='export all_proxy=socks5://127.0.0.1:1080'
alias unproxy='unset all_proxy'
proxy
```

```bash
alias proxy='export all_proxy=socks5://127.0.0.1:1080 \
	export http_proxy=http://127.0.0.1:1080 \
	export https_proxy=http://127.0.0.1:1080 \
	export HTTP_PROXY=http://127.0.0.1:1080 \
	export HTTPS_PROXY=http://127.0.0.1:1080'

alias unproxy='unset all_proxy \
	unset http_proxy
	unset https_proxy
	unset HTTP_PROXY
	unset HTTPS_PROXY'
```

### 提示精简
`.zshrc`  中加入 `DEFAULT_USER="leo"`

`vi ~/.oh-my-zsh/themes/agnoster.zsh-theme`
显示判断在这里
```
# Context: user@hostname (who am I and where am I)
prompt_context() {
  if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
    prompt_segment black default "%(!.%{%F{yellow}%}.)%n@%m"
  fi
}
```

#### win10

[How to setup a nice looking terminal with WSL in Windows 10 Creators Update](https://medium.com/@Andreas_cmj/how-to-setup-a-nice-looking-terminal-with-wsl-in-windows-10-creators-update-2b468ed7c326)

[如何给 Windows Terminal 增加一个新的终端（以 Bash 为例）](https://blog.walterlv.com/post/add-a-new-profile-for-windows-terminal.html)


#### 参考
https://github.com/robbyrussell/oh-my-zsh


### monorepo 新浪潮 | introduce lern
https://github.com/pigcan/blog/issues/3

### 构建自己的React UI组件库: 从v0.0.0到 v0.0.1
https://juejin.im/post/5c28bbdff265da616501a8b3

https://github.com/cuke-ui/cuke-ui

### markdown-here
https://github.com/adam-p/markdown-here?utm_source=gold_browser_extension


### 私有npm源instlal方式

公司搭建的私有`npm`镜像可能会存在一些包的同步问题，虽然能够通过 `npm show` 看到某个版本的包，但是就是`install`失败，去私有仓库上去掉同步按钮依然没有作用

可以在`package.json`文件同层目录下，新增一个 `.npmrc` 文件，内容如下

```rc
registry=https://registry.npm.taobao.org
@sdp.nd:registry=http://registry.npm.sdp.nd/
```
让公司的私有包都走公司的镜像，其他的包都走`taobao`的镜像即可

其他一些可能会用到的文件的地址

```
chromedriver_cdnurl=https://npm.taobao.org/mirrors/chromedriver
phantomjs_cdnurl=https://npm.taobao.org/mirrors/phantomjs
sass_binary_site=https://npm.taobao.org/mirrors/node-sass
```
### 远程调试

[whistle](http://wproxy.org/whistle/install.html)
[zan-proxy](https://youzan.github.io/zan-proxy/)

### ruby gem 镜像

https://gems.ruby-china.com

### 安装 cocoapods

`sudo gem install cocopods` 命令有可能会报没权限的错误，把安装位置调整一下就可以了

`sudo gem install cocoapods -n /usr/local/bin`

https://www.jianshu.com/p/b8406ff1e2f1

https://stackoverflow.com/questions/2893889/how-do-i-fix-the-you-dont-have-write-permissions-into-the-usr-bin-directory

### charles系列破解激活办法
Registered Name: https://zhile.io
License Key: 48891cf209c6d32bf4

https://zhile.io/2017/07/07/charles-proxy-usage-and-license.html

### ES 语法支持列表
https://github.com/williamkapke/node-compat-table

### node  utf-8 BOM 头的问题
`fs.writeFileSync(filePath, '\ufeff' + JSON.stringify(data, null, 2))`

### any-rule 常用正则大全, 支持vscode扩展插件
vscode 插件dmeo
https://github.com/any86/any-rule


### linux 免密登录
除了在目标机器的 `~/.ssh/authorized_key` 文件中添加本机的公钥，还可以通过`ssh-copy-id -i ~/.ssh/id_rsa.pub 用户名@ip`  的方式自动添加，此命令会自动添加，判断是否重复添加已经修改权限更方便

wsl 中还可以配置一下 hosts文件 登录的时候会更加方便，wsl中设置启动默认的用户是 `debian config --default-user root` 切换到 `root`用户后可以用 `passwd`更改密码

https://blog.csdn.net/m0_37590135/article/details/74275859
https://blog.csdn.net/qxoqx/article/details/52779710
https://blog.csdn.net/hao45e/article/details/79992803

### linux ssh config

```
Host example                       # 关键词
    HostName example.com           # 主机地址
    User root                      # 用户名
    # IdentityFile ~/.ssh/id_ecdsa # 认证文件
    # Port 22                      # 指定端口
```

管理多组密钥对

```
Host github
    HostName %h.com
    IdentityFile ~/.ssh/id_ecdsa_github
    User git
Host coding
    HostName git.coding.net
    IdentityFile ~/.ssh/id_rsa_coding
    User git
```

```
# 原来
$ git clone git@git.coding.net:deepzz/test.git

# 现在
$ git clone coding:deepzz/test.git
```

[Bad owner or permissions on .ssh/config的解决](https://my.oschina.net/lovewinner/blog/1118876)
```
sudo chmod 600 config
```

[SSH Config 那些你所知道和不知道的事](https://deepzz.com/post/how-to-setup-ssh-config.html)



### 让终端命令也走代理的方式
不同系统内置的命令使用的环境变量可能不同，这里直接全部都设置一下
.zshrc 里面加入下面的命令，然后执行一下 . ./zshrc 生效后即可通过 `proxy`  `unproxy` 启用和关闭终端代理了
```
alias proxy='export all_proxy=socks5://127.0.0.1:1086 \
	export HTTP_PROXY=$all_proxy \
	export http_proxy=$all_proxy \
	export https_proxy=$all_proxy \
	export HTTP_PROXY=$all_proxy \
	export HTTPS_PROXY=$all_proxy'

alias unproxy='unset all_proxy \
	unset ALL_PROXY \
	unset http_proxy \
	unset https_proxy \
	unset HTTP_PROXY \
	unset HTTPS_PROXY'
```
https://github.com/mrdulin/blog/issues/18


### vi 中不能用鼠标复制了
试试 `vi ` 中设置  `set mouse=c`
http://vimdoc.sourceforge.net/htmldoc/options.html

`vi` 大小写 `guw` `gUw` 单词  `gul` `gUl` 当前字符  `guu`  `gUU` 当前行
`vi` 跳转到行 `gg` 首行   `G` 未行   `5G`第5行
`vi` 删除 `x` 单个字符  `dw` 单词  `dd` 当前行  `5dd` 删除5行

### mac 同步时间

sudo sntp -sS time.apple.com 命令来强制更新系统时间。

https://superuser.com/questions/155785/mac-os-x-date-time-synchronization/633837#633837


### linux 文件说明

```

d代表的是目录(directroy)
-代表的是文件(regular file)
s代表的是套字文件(socket)
p代表的管道文件(pipe)或命名管道文件(named pipe)
l代表的是符号链接文件(symbolic link)
b代表的是该文件是面向块的设备文件(block-oriented device file)
c代表的是该文件是面向字符的设备文件(charcter-oriented device file)
```

```
-rw------- (600)      只有拥有者有读写权限。
-rw-r--r-- (644)      只有拥有者有读写权限；而属组用户和其他用户只有读权限。
-rwx------ (700)     只有拥有者有读、写、执行权限。
-rwxr-xr-x (755)    拥有者有读、写、执行权限；而属组用户和其他用户只有读、执行权限。
-rwx--x--x (711)    拥有者有读、写、执行权限；而属组用户和其他用户只有执行权限。
-rw-rw-rw- (666)   所有用户都有文件读、写权限。
-rwxrwxrwx (777)  所有用户都有读、写、执行权限。
```

https://blog.csdn.net/u013197629/article/details/73608613

### 保持ssh不自动断开

如果是想让主机所有用户都生效，修改/etc/ssh/ssh_config
如果只想让本人生效，则修改 ~/.ssh/config

```
Host *
    ServerAliveInterval 30
    ServerAliveCountMax 3
```

如果此处还有一个配置项叫 SendEnv LANG LC_*，老高建议最好注释掉，否则如果本地是中文环境，而服务器没有对应的中文语言选项时系统可能会出现很多莫名其妙的BUG，所以保持原始英文语言环境为上。

https://blog.phpgao.com/keep_connect_ssh.html

http://bluebiu.com/blog/linux-ssh-session-alive.html


### centos install docker
卸载旧版本
  `sudo yum remove docker docker-common docker-selinux docker-engine`

1. 安装
   step by step
   ```
   sudo yum install -y yum-utils device-mapper-persistent-data lvm2 wget

   sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
   or
   wget -O /etc/yum.repos.d/docker-ce.repo https://download.docker.com/linux/centos/docker-ce.repo

  把软件仓库地址替换为 TUNA:
  sudo sed -i 's+download.docker.com+mirrors.tuna.tsinghua.edu.cn/docker-ce+' /etc/yum.repos.d/docker-ce.repo

   sudo yum install docker-ce docker-ce-cli containerd.io
   ```

  by script
  `curl -fsSL https://get.docker.com -o get-docker.sh`
  `sudo sh get-docker.sh`
2. 查看
   `sudo yum list installed | grep docker`
3. 启动
   `sudo systemctl start docker`  （开机自启 `sudo systemctl enable docker`）
   `ps -ef |grep docker`
   `sudo systemctl status docker`
4. 设置不用输入 sudo
    把当前用户添加到 docker 组中
    `sudo usermod -aG docker leo`
5. 卸载
   `sudo yum remove docker-ce-cli containerd.io docker-ce`

https://cloud.tencent.com/developer/labs/lab/10054
wget -O /etc/yum.repos.d/docker-ce.repo https://download.docker.com/linux/centos/docker-ce.repo


https://docs.docker.com/install/linux/docker-ce/centos/#install-docker-ce
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-centos-7


### debian install docker
```
sudo apt-get remove docker docker-engine docker.io

sudo apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/debian $(lsb_release -cs) stable"

【curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun】 或者这样使用官方提供的镜像地址

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io

apt list --installed |grep docker
apt list --installed |grep container

dpkg -l | grep docker
dpkg -l | grep container

sudo systemctl status docker
sudo systemctl start docker (wsl 中需要再win10中安装客户端)

sudo docker run hello-world
```

https://mirror.tuna.tsinghua.edu.cn/help/docker-ce/

https://docs.docker.com/install/linux/docker-ce/debian/


 /etc/docker/daemon.json 中配置镜像

 ```
 {
    "registry-mirrors": ["https://mirror.ccs.tencentyun.com"]
}
 ```

### win10 install docker

1 下载地址
https://download.docker.com/win/stable/Docker%20Desktop%20Installer.exe (使用迅雷或者360极速浏览器下载速度会变块)

https://hub.docker.com/?overlay=onboarding


2. docker setting 中 Expose daemon on tcp://localhost:2375 without TLS
   wsl 中的 profile 添加 `export DOCKER_HOST=127.0.0.1:2375`
   生效  `. ./.zshrc`
3. `docker run hello-world`

https://medium.com/%E4%B8%80%E5%80%8B%E5%B0%8F%E5%B0%8F%E5%B7%A5%E7%A8%8B%E5%B8%AB%E7%9A%84%E9%9A%A8%E6%89%8B%E7%AD%86%E8%A8%98/wsl-%E8%88%87-windows-%E7%9A%84%E5%AE%8C%E7%BE%8E%E9%9B%99%E7%B5%90%E5%90%88-%E5%9C%A8wsl-%E4%B8%AD%E5%AE%89%E8%A3%9D-docker-e722e87ffa3b
https://zhuanlan.zhihu.com/p/61542198


### docker 源 国内

```
/etc/docker/daemon.json  中添加如下配置，没有这个文件则新建一个

{
  "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn/"]
}
```
重新启动 docker

`sudo systemctl restart docker`

http://mirrors.ustc.edu.cn/help/dockerhub.html?highlight=docker
https://www.jianshu.com/p/df75f9b5fcf6
https://www.jianshu.com/p/405fe33b9032
https://yeasy.gitbooks.io/docker_practice/install/mirror.html

### docker 教程

https://docker-curriculum.com/#setting-up-your-computer

docker install
https://github.com/yeasy/docker_practice
https://yeasy.gitbooks.io/docker_practice/introduction/what.html

https://github.com/jaywcjlove/docker-tutorial

30 分钟快速入门 Docker 教程
https://juejin.im/post/5cacbfd7e51d456e8833390c

非常详细的Docker学习教程
https://blog.csdn.net/zmx729618/article/details/72930474


免费 `docker` 练习
https://labs.play-with-docker.com/

Docker-in-Docker
docker 里面安装docker 并且尝试通过`systemctl start docker` 启动 `docker deamon` 是错误的做法 ，正确的`docker in docker` 是利用`docker` 的`cs`架构，在容器里面的`docker` 链接宿主机的 `docker daemon`
`docker run -v /var/run/docker.sock:/var/run/docker.sock  -itd centos:centos`

或者这样，就不用再内部`docker`里面安装`docker-ce`了
`docker run -d -v /var/run/docker.sock:/var/run/docker.sock -v $(which docker)`
http://www.dockone.io/article/431
https://cloud.tencent.com/developer/article/1199395

https://www.jianshu.com/p/0ecedb072c69
https://blog.container-solutions.com/running-docker-in-jenkins-in-docker

http://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/
https://github.com/jpetazzo/dind


10张图带你深入理解Docker容器和镜像
http://dockone.io/article/783


### docker install  Jenkins

Docker Hub 上的官方 Jenkins 镜像

`docker pull jenkins/jenkins:lts`
https://jenkins.io/zh/blog/2018/12/10/the-official-Docker-image/

https://github.com/jenkinsci/docker/blob/master/README.md

Jenkins 插件安装失败
https://www.cnblogs.com/sxdcgaq8080/p/10489326.html


密码位置
`cat /var/jenkins_home/secrets/initialAdminPassword`


jenkins插件下载镜像加速
`https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json`
https://blog.csdn.net/you227/article/details/81076032

the status of Jenkins mirrors
http://mirrors.jenkins-ci.org/status.html

使用 Docker 部署 Jenkins
https://trafficmgr.net/2019/02/01/docker-jenkins/

### 解决df -h卡死问题
解决方式
首先就是使用strace去追踪到底在哪里卡住了

`strace df -h`

如果没有这个命令那么去安装一xia

`yum install strace`

之后就找到了卡住的地方

```
stat("/", {st_mode=S_IFDIR|0555, st_size=4096, ...}) = 0
stat("/sys/fs/selinux", {st_mode=S_IFDIR|0755, st_size=0, ...}) = 0
stat("/proc/sys/fs/binfmt_misc",
```

重启下面这个服务就好

`systemctl restart proc-sys-fs-binfmt_misc.automount`

https://www.jianshu.com/p/b50daaf322f2
https://blog.arstercz.com/centos7-%E7%B3%BB%E7%BB%9F-df-hang-%E9%97%AE%E9%A2%98%E5%A4%84%E7%90%86%E8%AF%B4%E6%98%8E/


### Mac VSCode 更新失败
权限问题

`ls -lrt ~/Library/Caches | grep vscode -i`
查看可知 `com.microsoft.VSCode.ShipIt` 的权限不对 ，修改成当前用户即可
`sudo chown $USER ~/Library/Caches/com.microsoft.VSCode.ShipIt/`


### nload - 实时监控Linux网络带宽使用情况

`yum install nload`

```
$ nload
Or
$ nload eth0
```
一次显示多个设备; 不显示流量图，使用-m选项
`nload -m`

https://www.howtoing.com/nload-monitor-linux-network-traffic-bandwidth-usage


### 获取当前操作系统版本号
`lsb_release -a | -cs`
默认没有安装的话 `centos`执行下面命令进行安装 `lsb_release`

`yum install -y redhat-lsb`


### 无服务 serlvess
https://docs.parseplatform.org/parse-server/guide/#using-parse-sdks-with-parse-server

https://jimmysong.io/posts/what-is-serverless/


### 开发一个高质量的前端组件，这些姿势一定要知道
https://mp.weixin.qq.com/s?__biz=MzUxMzcxMzE5Ng==&amp;mid=2247493007&amp;idx=1&amp;sn=caf4e39e99dc9731e46e7661fafe3fd4&amp;chksm=f95250ccce25d9da61e597fb1caeebfc61e265a0de85f92f1d9e7841212fd13c4f3748abebd7#rd


### Spring Boot 揭秘与实战 源代码
https://github.com/lianggzone/springboot-action

### Why You Should Use ESLint, Prettier and EditorConfig Together
https://blog.theodo.com/2019/08/why-you-should-use-eslint-prettier-and-editorconfig-together/

### Using ESLint and Prettier in a TypeScript Project
https://dev.to/robertcoopercode/using-eslint-and-prettier-in-a-typescript-project-53jb

### Empower Your Dev Environment with ESLint, Prettier and EditorConfig with No Conflicts
https://blog.theodo.com/2019/08/empower-your-dev-environment-with-eslint-prettier-and-editorconfig-with-no-conflicts/


### pc微信浏览器调试方法

pc微信浏览器无法打开开发者工具，可以用这个工具查看一下需要debug页面的控制台错误

https://github.com/Tencent/vConsole

### meta http-equiv="Cache-Control" Pragma Expires not work

```js
<meta http-equiv="Expires" content="0" />
  <meta http-equiv="Pragma" content="no-cache" />
  <meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate" />
```
https://stackoverflow.com/questions/49547/how-do-we-control-web-page-caching-across-all-browsers


### Beyond Compare 破解
```
cd Library/Application\ Support/Beyond\ Compare
rm -rf registry.dat


#or
rm -rf ~/Library/Application\ Support/Beyond\ Compare/registry.dat
```
https://blog.csdn.net/qq_27093465/article/details/85166780

### pnpm 解决了我的哪些痛点
https://juejin.cn/post/7036319707590295565


#### GitHub 上 9 个美观大气的后台管理系统
https://juejin.cn/post/7052195023311339527?utm_source=gold_browser_extension


### 移动端H5网页开发常见问题汇总
https://juejin.cn/post/7055599228478816270?utm_source=gold_browser_extension


### 动画方案
https://airbnb.design/lottie/
https://svga.io/
https://pag.io/


### node-pre-gyp 安装失败

node-pre-gyp ERR! Completion callback never invoked!
node-pre-gyp ERR! System Darwin 20.3.0
node-pre-gyp ERR! command "/Users/leo/.nvm/versions/node/v10.17.0/bin/node" "/Users/leo/IMGO/weixin_coupon_cashier/node_modules/fsevents/node_modules/node-pre-gyp/bin/node-pre-gyp" "install" "--fallback-to-build"
node-pre-gyp ERR! cwd /Users/leo/IMGO/weixin_coupon_cashier/node_modules/fsevents
node-pre-gyp ERR! node -v v10.17.0
node-pre-gyp ERR! node-pre-gyp -v v0.9.1
node-pre-gyp ERR! This is a bug in `node-pre-gyp`.
node-pre-gyp ERR! Try to update node-pre-gyp and file an issue if it does not help:
node-pre-gyp ERR!     <https://github.com/mapbox/node-pre-gyp/issues>


https://github.com/mapbox/node-pre-gyp/issues/367



### 国内低代码平台

https://github.com/taowen/awesome-lowcode


### monorepo

https://monorepo.tools/


### chrome 历史版本记录

https://en.wikipedia.org/wiki/Google_Chrome_version_history


### Autoplay policy in Chrome  chroem 音频 视频自动播放策略
https://developer.chrome.com/blog/autoplay/

https://blog.csdn.net/qq_35052138/article/details/120205490

![](https://vipcdn.mgtv.com/lego/20221110/lego/5fde3b4660e111eda3afecf4bbc30ba4.png)

webview 可以关掉这个配置

```js

// android

webview.getSettings.setMediaPlaybackRequiresUserGesture(false)

// ios
// WKWebView
WKWebViewConfiguration *config = [[WKWebViewConfiguration alloc] init];
    config.allowsInlineMediaPlayback = YES;
    config.mediaPlaybackRequiresUserAction = false;

    displayWebView=[[WKWebView alloc] initWithFrame:rect configuration:config];
    displayWebView.UIDelegate=self;
    displayWebView.navigationDelegate=self;

// UIWebView :
[self.webView setMediaPlaybackRequiresUserAction:NO];

```

### 动画框架

1. Anime.js  https://github.com/juliangarnier/anime

2. GSAP  https://github.com/greensock/GSAP

https://www.codeinwp.com/blog/best-javascript-animation-libraries/


### 苹果钱包动画
https://codepen.io/gokulramesh94/pen/RwrzJGr

### 贝塞尔曲线

1 https://www.xuanfengge.com/easeing/easeing/
2. https://xuanfengge.com/easeing/ceaser/
3. https://cubic-bezier.com/#.17,.67,.83,.67


### dom加水印

https://github.com/saucxs/watermark-dom/blob/master/watermark.js

https://www.npmjs.com/package/watermark-dom


### datagrip 激活

licenses sever http://lic-server.mephi.ru

http://blog.idejihuo.com/wp-content/uploads/2022/04/jetbrains-license-servers.txt


### 可视化表单

https://www.vform666.com/


### apple pay 文档

https://developer.apple.com/apple-pay/implementation/



### Babel 插件手册

https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/plugin-handbook.md#toc-stages-of-babel

### AST
https://astexplorer.net/

https://github.com/jamiebuilds/the-super-tiny-compiler/blob/master/the-super-tiny-compiler.js
