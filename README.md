<p align="center">
  <img src="media/poster.png" width="300" />
  <br />
  <b>Git常用命令参考手册</b>
  <p align="center">基本涵盖了在开发中用到的git命令，能满足日常需求</p>
  <p align="center">通俗易懂的例子，30分钟快速入门</p>
  <p align="center">
    <a href="https://github.com/xjh22222228/git-manual/stargazers"><img src="https://img.shields.io/github/stars/xjh22222228/git-manual" alt="Stars Badge"/></a>
    <img src="https://img.shields.io/github/license/xjh22222228/git-manual" />
    <a href="https://hits.dwyl.com/xjh22222228/git-manual">
      <img src="https://hits.dwyl.com/xjh22222228/git-manual.svg" />
    </a>
  </p>
</p>

注：2020 年 10 月 GitHub 已将默认分支 `master` 更名为 `main` 分支。

---

# 目录

- [配置](#配置)
- [初始化仓库](#初始化仓库)
- [克隆仓库](#克隆仓库)
- [管理仓库](#管理仓库)
- [暂存文件](#暂存文件)
- [提交文件](#提交文件)
- [推送远端](#推送远端)
- [查看分支](#查看分支)
- [切换分支](#切换分支)
- [创建分支](#创建分支)
- [删除分支](#删除分支)
- [重命名分支](#重命名分支)
- [转移提交](#转移提交)
- [临时保存](#临时保存)
- [文件状态](#文件状态)
- [日志](#日志)
- [责怪](#责怪)
- [合并](#合并)
- [删除文件](#删除文件)
- [还原](#还原)
- [拉取](#拉取)
- [移动-重命名](#移动-重命名)
- [比较文件内容差异](#比较文件内容差异)
- [查看历史提交信息](#查看历史提交信息)
- [回滚版本](#回滚版本)
- [撤销](#撤销)
- [标签](#标签)
- [变基](#变基)
- [工作流](#工作流)
- [子模块](#子模块)
- [子树](#子树)
- [二分查找](#二分查找)
- [归档](#归档)
- [格式化日志](#格式化日志)
- [清空 commit 历史](#清空-commit-历史)
- [帮助](#帮助)
- [提交规范](#提交规范)
- [解决冲突](#解决冲突)
- [仓库迁移](#仓库迁移)
- [奇技淫巧](#奇技淫巧)
- [GUI 客户端](#GUI-客户端)
- [生成 SSH_Key](#生成SSH_Key)
- [其他](#其他)
- [记住密码](#记住密码)
- [清除账号](#清除账号)
- [加速](#加速)
- [思维导图](#思维导图)

## 配置

```bash
# 查看全局配置列表
git config --global -l
# 查看局部配置列表
git config --local -l

# 查看所有的配置以及它们所在的文件
git config --list --show-origin

# 查看已设置的全局用户名/邮箱
git config --global --get user.name
git config --global --get user.email

# 设置全局用户名/邮箱
git config --global user.name "xiejiahe"
git config --global user.email "example@example.com"

# 设置本地当前工作区仓库用户名/邮箱
git config --local user.name "xiejiahe"
git config --local user.email "example@example.com"

# 删除配置
git config --unset --global user.name
git config --unset --global user.email

# 修改默认文本编辑器，比如 nano
# 常用编辑器：emacs / nano / vim / vi
git config --global core.editor nano

# 将默认差异化分析工具设置为 vimdiff
git config --global merge.tool vimdiff

# 编辑当前仓库配置文件
git config -e  # 等价 vi .git/config

# 文件权限的变动也会视为改动, 可通过以下配置忽略文件权限变动
git config core.fileMode false

# 文件大小写设为敏感, git默认是忽略大小写
git config --global core.ignorecase false

# 配置 git pull 时默认拉取所有子模块内容
git config submodule.recurse true

# 记住提交账号密码, 下次操作可免账号密码
git config --global credential.helper store # 永久
git config --global credential.helper cache # 临时，默认15分钟

# 设置代理，http或者https
git config --global http.proxy "http://127.0.0.1:8080"
git config --global https.proxy "http://127.0.0.1:8080"

# 取消设置代理，http或者https
git config --global --unset http.proxy
git config --global --unset https.proxy
```

#### 命令别名配置

git 可以使用别名来简化一些复杂命令，类似 [alias](https://github.com/xjh22222228/linux-manual#alias) 命令。

```bash
# git st 等价于 git status
git config --global alias.st status

# 如果之前添加过，需要添加 --replace-all 进行覆盖
git config --global --replace-all alias.st status

# 执行外部命令, 只要在前面加 ! 即可
git config --global alias.st '!echo hello';
# 加 "!" 可以执行外部命令执行一段复杂的合并代码过程，例如：
git config --global alias.mg '!git checkout develop && git pull && git merge main && git checkout -';

# 删除 st 别名
git config --global --unset alias.st
```

#### 配置代理

```bash
# 设置
git config --global https.proxy  http://127.0.0.1:1087
git config --global http.proxy  http://127.0.0.1:1087

# 查看
git config --global --get http.proxy
git config --global --get https.proxy

# 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy
```

## 初始化仓库

`git init` 创建一个空的 Git 仓库或重新初始化一个现有的仓库

实际上 `git init` 命令用得不多，通常在 GUI 上进行操作。

```bash
# 会在当前目录生成.git
git init

# 以安静模式创建，只会打印错误或警告信息
git init -q

# 在当前目录下创建一个裸仓库，里面只有 .git 下的所有文件
git init --bare
```

## 克隆仓库

```bash
# https 协议克隆
git clone https://github.com/xjh22222228/git-manual.git

# SSH 协议克隆
git clone git@github.com:xjh22222228/git-manual.git

# 克隆指定分支， -b 指定分支名字，实际上是克隆所有分支并切换到 develop 分支上
git clone -b develop https://github.com/xjh22222228/git-manual.git

# --single-branch 完全只克隆指定分支
git clone -b develop --single-branch https://github.com/xjh22222228/git-manual.git

# 指定克隆后的文件夹名称
git clone https://github.com/xjh22222228/git-manual.git git-study # 如果后面是 . 在当前目录创建

# 递归克隆，如果项目包含子模块就非常有用
git clone --recursive https://github.com/xjh22222228/git-manual.git

# 浅克隆, 克隆深度为1, 只克隆指定分支且历史记录只保留最后一条, 通常用于减少克隆时间和项目大小
git clone --depth=1 https://github.com/xjh22222228/git-manual.git
git clone --depth=1 --no-single-branch https://github.com/xjh22222228/git-manual.git # --no-single-branch 同时克隆其他所有分支


# 裸克隆, 没有工作区内容，不能进行提交修改，一般用于复制仓库
git clone --bare https://github.com/xjh22222228/git-manual.git

# 镜像克隆, 也是裸克隆, 区别于包含上游版本库注册
git clone --mirror https://github.com/xjh22222228/git-manual.git
```

#### 克隆指定文件夹

有些仓库会包含 客户端、服务端、等多个端的代码, 但又不想完整克隆整个项目, 只想克隆某个文件夹，这个时候就需要用到 `稀疏检出`。

开启稀疏检出必须满足 2 个条件：

- `core.sparsecheckout` 设置为 true
- `.git/info/sparse-checkout` 文件列出要检出的目录列表

本仓库有个 `media` 文件夹，用它来演示吧。

```bash
# 1、创建一个目录并进入
mkdir hello-git && cd hello-git

# 2、初始化仓库
git init

# 3、设置仓库地址
git remote add origin https://github.com/xjh22222228/git-manual.git

# 4、开启稀疏检出功能
git config core.sparsecheckout true

# 5、编辑 .git/info/sparse-checkout 文件, 默认是没有需要手动新建
# 也可以通过命令将需要检出的目录路径写入追加进去
echo "media" >> .git/info/sparse-checkout

# 6、拉取内容, 这里指定的是 mater 分支
git pull origin main
```

<details>
  <summary>演示克隆指定文件夹.gif</summary>
  
  <img src="media/gitclone-sparsecheckout.gif">
</details>

## 管理仓库

`git remote` 命令用来管理远程仓库。

通常一个项目对应多个仓库就需要用到 `git remote`, 比如要推送到 `github` / `gitee` / `gitlab`， 就可以用 `git remote` 来管理多个仓库地址。

```bash
# 查看远程仓库服务器, 一般打印 origin , 这是 Git 给你克隆的仓库服务器的默认名字
# 一般只会显示 origin , 除非你有多个远程仓库地址
git remote

# 指定-v, 查看当前远程仓库地址
git remote -v

# 添加远程仓库地址 example 是自定义名字
# 添加完后可以通过 git remote 就能看到 example
git remote add example https://github.com/xjh22222228/git-manual.git

# 查看指定远程仓库信息
git remote show example

# 重命名远程仓库
git remote rename oldName newName # git remote rename example simple

# 移除远程仓库
git remote remove example

# 修改远程仓库地址，从HTTPS更改为SSH
git remote set-url origin git@github.com:xjh22222228/git-manual.git

# 后续的推送可以指定仓库名字
git push example
```

## 暂存文件

```bash
# 暂存所有
git add -A

# 暂存某个文件
git add ./README.md

# 暂存当前目录所有改动文件
git add .

# 暂存一系列文件
git add 1.txt 2.txt ...
```

## 提交文件

```bash
# -m 提交的描述信息
git commit -m "changes log"

# 只提交某个文件
git commit README.md -m "message"

# 提交并显示diff变化
git commit -v

# 允许提交空消息，通常必须指定 -m 参数
git commit --allow-empty-message

# 重写上一次提交信息，确保当前工作区没有改动
git commit --amend -m "新的提交信息"

# 跳过验证, 如果使用了类似 husky 工具。
git commit --no-verify -m "Example"
```

#### 修改提交日期

执行 `git commit` 时 `git` 会采用当前默认时间，但有时候想修改提交日期可以使用 `--date` 参数。

格式：`git commit --date="月 日 时间 年 +0800" -m "init"`

例子：`git commit --date="Mar 7 21:05:20 2021 +0800" -m "init"`

**月份简写如下：**

| 月份简写 | 描述   |
| -------- | ------ |
| Jan      | 一月   |
| Feb      | 二月   |
| Mar      | 三月   |
| Apr      | 四月   |
| May      | 五月   |
| Jun      | 六月   |
| Jul      | 七月   |
| Aug      | 八月   |
| Sep      | 九月   |
| Oct      | 十月   |
| Nov      | 十一月 |
| Dec      | 十二月 |

## 推送远端

```bash
# 默认推送当前分支
# 等价于 git push origin, 实际上推送到一个叫 origin 默认仓库名字
git push

# 推送到主分支
git push -u origin main

# 本地分支推送到远程分支， 本地分支:远程分支
git push origin <branchName>:<branchName>

# 强制推送, --force 缩写
git push -f
```

## 查看分支

```bash
# 查看所有分支
git branch -a

# 查看本地分支
git branch

# 查看远端分支
git branch -r

# 查看本地分支所关联的远程分支
git branch -vv

# 查看本地 main 分支创建时间
git reflog show --date=iso main

# 搜索分支, 借助 grep 命令來搜索, 包含关键字 dev
git branch -a | grep dev
```

#### 给分支添加备注

有时候分支过多很难通过分支名去判断这个分支做了什么。

```bash
# 命令
$ git config branch.{branch_name}.description 备注内容

# 给 hotfix/tip 分支添加备注信息
$ git config branch.hotfix/tip.description 修复细节
```

## 切换分支

```bash
# 切换到main分支
git checkout main

# 切换上一个分支
git checkout -

# 强制切换, 但是要小心，如果文件未保存修改会直接覆盖掉
git checkout -f main

# -t, 切换远端分支, 如果用了 git remote 添加一个新仓库就需要用 -t 进行切换
git checkout -t upstream/main
```

在克隆时使用 `--depth=1` 切换其他分支，比如切换 dev 分支：

```bash
git clone --depth=1 https://github.com/xjh22222228/git-manual.git

# 切换 dev 分支
git remote set-branches origin 'dev'
git fetch --depth=1 origin dev
git checkout dev
```

除了使用 `git checkout` 还有另一种方式切换那就是 `git switch`, 在 Git 版本 `2.23` 引入, 主要用于切换和创建分支。

```bash
# 切换到 develop 分支
git switch develop

# 切换到上一个分支
git switch -

# 强制切换到 develop 分支，并抛弃本地所有修改
git switch -f develop

# 创建分支并切换
git switch -c newBranch

# 强制创建分支
git switch -C newBranch

# 从前3次提交进行创建新的分支
git switch -c newBranch HEAD〜3

# -t, 切换远端分支, 如果用了 git remote 添加一个新仓库就需要用 -t 进行切换
git switch -t upstream/main
```

## 创建分支

```bash
# 创建一个名为 develop 本地分支
git branch develop

# 强制创建分支, 不输出任何警告或信息
git branch -f develop

# 创建本地 develop 分支并切换
git checkout -b develop

# 创建远程分支, 实际上创建本地分支然后推送到远端
git checkout -b develop
git push origin develop

# 创建一个空的分支, 不继承父分支，历史记录是空的，一般至少需要执行4步
git checkout --orphan develop
git rm -rf .  # 这一步可选，如果你真的想创建一个没有任何文件的分支
git add -A && git commit -m "提交" # 添加并提交，否则分支是隐藏的 （执行这一步之前需要注意当前工作区必须保留一个文件，否则无法提交）
git push --set-upstream origin develop # 推送到远程
```

## 删除分支

注意：删除分支不能删除当前分支，先切换到其他分支再删除。

```bash
# 删除本地分支
$ git branch -d <branchName>

# 大写 D 强制删除未完全合并的分支
# 等价 git branch --delete --force <branchName>
$ git branch -D <branchName>

# 删除远程分支
$ git push origin :<branchName>
$ git push origin --delete <branch-name>  # >= 1.7.0
```

## 重命名分支

```bash
# 重命名当前分支, 通常情况下需要执行3步
# 1、修改分支名称
# 2、删除远程旧分支
# 3、将重命名分支推送到远程
git branch -m <branchName>
git push origin :old_branch
git push -u origin new_branch


# 重命名指定分支
git branch -m old_branch new_branch
```

## 转移提交

`git cherry-pick` 可以用来将一个分支的某次提交转移到当前分支中。

假设有 `dev` 和 `main` 2 个分支, `dev` 分支中有 10 次提交记录, `main` 分支想把 `dev` 的第 5 次提交记录合并到当前分支中, 这正是此命令的使用场景。

还可以理解为将以前的某次提交再重新提交一次。

```bash
# 可以是一个 commit_id 或者是分支名
# 如果是分支名则是最后一次提交
git cherry-pick <commit_id>|branch_name

# 支持转移多个提交, 会产生多个提交记录
git cherry-pick <commit_id1> <commit_id2>

# 保留原有作者信息进行提交
git cherry-pick -x <commit_id>

# 重新编辑提交信息, 否则会应用之前的commit消息
git cherry-pick -e <commit_id>

# 断开当前操作回到初始状态
git cherry-pick --abort

# 当发生冲突时解决冲突后使用 git add 加入到暂存区然后执行下面命令继续执行
git cherry-pick --continue
```

<details>
  <summary>演示转移提交.gif: 把 `dev` 分支的第三次提交转移到当前 `main` 分支。</summary>
  
  <img src="media/cherry.gif">
</details>

## 临时保存

应用场景：假设当前分支某些功能做到一半了, 突然需要切换到其他分支修改 Bug, 但是又不想提交（因为切换分支必须清理当前工作区，否则无法切换），这个时候 `git stash` 应用场景就来了。

```bash
# 保存当前修改工作区内容
git stash

# 保存时添加注释, 推荐使用此命令
git stash save "修改了#28 Bug"

# 保存包含没有被git追踪的文件
git stash -u

# 查看当前保存列表
git stash list

# 恢复修改工作区内容, 会从 git stash list 移除掉
git stash pop # 恢复最近一次保存内容到工作区, 默认会把暂存区的改动恢复到工作区
git stash pop stash@{1} # 恢复指定 id， 通过 git stash list 可查到
git stash pop --index # 恢复最近一次保存内容到工作区, 但如果是暂存区的内容同样恢复到暂存区

# 与 pop 命令一致, 唯一不同的是不会移除保存列表
git stash apply

# 清空所有保存
git stash clear

# 清空指定 stash id, 如果 drop 后面不指定id清除最近的一次
git stash drop stash@{0}
git stash drop  # 清除最近一次

# 查看已保存的修改文件内容
git stash show -p stash@{0}
```

## 文件状态

```bash
# 完整查看文件状态
git status

# 以短格式给出输出
git status -s

# 忽略子模块
git status --ignore-submodules

# 显示已忽略的文件
git status --ignored
```

## 日志

查看历史日志可以通过 `git log` / `git shortlog` / `git reflog`。

`git log` 命令是 3 个最强大的命令

```bash
# 查看完整历史提交记录
git log

# 查看前N次提交记录 commit message
git log -2

# 查看前N次提交记录，包括diff
git log -p -2

# 从 commit 进行搜索, 可以指定 -i 忽略大小写
git log -i --grep="fix: #28"

# 从工作目录搜索包含 alert(1) 这段代码何时引入
git log -S "alert(1)"

# 查看指定作者历史记录
git log --author=xjh22222228

# 查看某个文件的历史提交记录
git log README.md

# 只显示合并日志
git log --merges

# 以图形查看日志记录, --oneline 可选
git log --graph --oneline

# 以倒序查看历史记录
git log --reverse
```

`git shortlog` 以简短的形式输出日志, 通常用于统计贡献者代码量。

```bash
# 默认以贡献者分组进行输出
git shortlog

# 列出提交者代码贡献数量, 打印作者和贡献数量
git shortlog -sn

# 以提交贡献数量排序并打印出message
git shortlog -n

# 采用邮箱格式化的方式进行查看贡献度
git shortlog -e
```

`git reflog` 通常被引用为 `安全网`，当 `git log` 没有想要的信息时可以尝试用 `git reflog`。

当回滚某个版本时记录是不保存在 `git log` 中, 想要找到这条回滚版本信息时 `git reflog` 就用上了。

```bash
git reflog # 等价于 git log -g --abbrev-commit --pretty=oneline
```

## 责怪

`git blame` 意思是责怪，你懂的。

`git blame` 用于查看某个文件的修改历史记录是哪个作者进行了改动。

```bash
# 查看 README.md 文件的修改历史记录，包括时间、作者以及内容
git blame README.md

# 查看谁改动了 README.md 文件的 11行-12行
git blame -L 11,12 README.md
git blame -L 11 README.md   # 查看第11行以后

# 显示完整的 hash 值
git blame -l README.md

# 显示修改的行数
git blame -n README.md

# 显示作者邮箱
git blame -e README.md

# 对参数进行一个组合查询
git blame -enl -L 11 README.md
```

---

## 合并

feature/v1.0.0 分支代码合并到 develop

```bash
git checkout develop
git merge feature/v1.0.0
```

将上一个分支代码合并到当前分支

```bash
git merge -
```

以安静模式合并, 把 develop 分支合并到当前分支并不输出任何信息

```bash
git merge develop -q
```

合并不编辑信息, 跳过交互

```bash
git merge develop --no-edit
```

合并分支后不进行提交

```bash
git merge develop --no-commit
```

退出合并，恢复到合并之前的状态

```bash
git merge --abort
```

合并某个分支指定文件或目录, 需要注意的是这会直接覆盖现有文件，而不是本质上的合并。

```bash
# 将dev分支的 src/utils/http.js src/utils/load.js 2个文件合并到当前分支下
git checkout dev src/utils/http.js src/utils/load.js
```

允许合并不相关的历史记录，如果在克隆使用了 `--depth` 参数会导致合并的时候会发生较大冲突，`allow-unrelated-histories` 参数可以有效的解决这个问题

```bash
git merge develop --allow-unrelated-histories
```

## 删除文件

此命令使用相对较少，通常用于清除文件缓存，比如加入 `.gitignore` 文件不生效问题

```bash
# 删除 1.txt 文件
git rm 1.txt

# 删除当前所有文件, 与rm -rf 命令不同的是不会删除 .git 目录
git rm -rf .

# 清除当前工作区缓存，但不会删除文件，通常用于修改文件名不生效问题
git rm -r --cached .
```

## 还原

还原操作通过 `git restore` 命令。

`git restore` 是在 `2.23` 引入的, 是为了分离 `git checkout` / `git reset` 职责。

```bash
# 撤销工作区文件修改, 不包括新建文件
git restore README.md # 一个文件
git restore README.md README2.md # 多个文件
git restore . # 当前全部文件

# 从暂存区回到工作区
git restore --staged README.md
```

## 拉取

`git pull` 拉取最新内容并合并。

#### 拉取远程分支最新内容

默认情况下拉取当前分支

```bash
# 如果出现冲突会自动合并
git pull
```

#### 拉取指定分支

```bash
# 远程分支名:本地分支名
git pull origin main:main
# 如果某个远程分支拉取并合并到当前分支后面可以省略
git pull origin main
```

#### 拉取指定工作目录

```bash
# 默认情况下拉取会在当前工作目录中，但如果想拉取指定工作目录，可以指定 `-C`
git -C /opt/work pull
```

#### 同步 Fork 仓库

当 Fork 别人仓库后，原仓库发生变化，可以通过以下操作合并到 Fork 仓库

```bash
# 1、添加原远程仓库：git remote add 自定义名字 远程仓库地址
git remote add upstream https://github.com/xjh22222228/git-manual.git

# 2、拉取远程最新分支内容
git fetch --depth=1 upstream main

# 3、远程最新内容合并到当前分支(允许合并不相关历史记录)
git merge upstream/main --allow-unrelated-histories

# 4、推送到远程
git push
```

## 移动-重命名

`git mv` 命令用来重命名文件或移动文件, 大部分开发者会选择手动进行移动文件, 手动和用 `git mv` 是有区别的。

手动和命令两者的区别（假设`README.md`重命名为`README2.md`）：

- 手动：先删除 `README.md`, 然后创建 `README2.md`, 历史记录无法正常追踪
- `git mv`: 实际上是更新索引，把文件进行重命名, 可以通过历史记录方便检索

`git mv` 和 uninx `mv` 命令很像，如果你熟悉的话。

注意：新创建的文件不支持 `git mv` , 必须先提交。

```bash
# 将 1.txt 重命名为 2.txt
git mv 1.txt 2.txt

# 强制将 1.txt 重命名为 2.txt, 不管2.txt文件存不存在
git mv -f 1.txt 2.txt

# 移动目录也一样
git mv temp temp2
```

## 比较文件内容差异

`git diff` 命令用于查看`工作区文件`内容与暂存区或远端之间的差异。

#### git diff

```bash
# 查看所有文件工作区与暂存区的差异
git diff

# 查看指定文件工作区与暂存区差异
git diff README.md

# 查看指定 commit 内容差异
git diff dce06bd

# 对比2个commit之间的差异
git diff e3848eb dce06bd

# 比较2个分支最新提交内容差异, develop分支与main分支, 如果没有差异返回空
git diff develop main

# 比较2个分支指定文件内容差异, develop 和 main READNE.md 文件差异
git diff develop main README.md README.md

# 查看工作区冲突文件差异
git diff --name-only --diff-filter=U

# 查看上一次修改了哪些文件
git diff --name-only HEAD~
git diff --name-only HEAD~~ # 前2次...
```

## 查看历史提交信息

可以通过 `git show` 命令查看历史提交信息。

```bash
# 不指定参数默认查看最新一条信息
git show

# 指定 commit_id 查看
git show d68a1ef

# 也可以指定 commit_id 查看指定文件提交信息
git show d68a1ef README.md

# 只指定文件名查看最后一次提交包含此文件的提交信息
git show README.md

# 指定分支名查看最后一次提交信息
git show feature/dev
```

## 回滚版本

回滚版本有 2 种方法：

- `git reset` - 回滚版本后之前的历史记录将不保存, 不保留痕迹, 基本上不存在冲突情况。
- `git revert` - 回滚版本后之前的历史记录还存在并多增加了一条 `Revert` 记录，很容易出现冲突。

`git reset` 命令用法：

```bash
# 回滚上一个版本
git reset --hard HEAD^

# 回滚上两个版本
git reset --hard HEAD^^

# 或者回滚到前X次
git reset HEAD~1

# 回滚到指定 commit_id ， 通过 git log 查看
git reset --hard 'commit id'

# 回滚并保留之前的修改
git reset --soft HEAD^
```

`git revert` 命令用法：

```bash
# 回滚上一次提交版本
git revert HEAD^

# 回滚指定commit
git revert 8efef3d37

# --no-edit 回滚并跳过编辑消息
git revert HEAD^ --no-edit

# 断开当前操作，还原初始状态
git revert --abort

# 推送到远程，假设当前是 main 分支
git push -u origin main
```

回滚到指定分支或 Commit_id 指定文件, 命令：

`git checkout [branch|commit_id] file file...`

```bash
$ git checkout main 1.txt 2.txt
$ git checkout 8efef3d37 1.txt 2.txt
```

## 撤销

```bash
# 撤销当前工作区所有文件的改动
git checkout -- .

# 撤销工作区指定文件改动
git checkout -- README.md

# 暂存区回到工作区
git reset HEAD^ # 上一次
git reset HEAD ./README.md # 指定 ./README.md 文件从暂存区回到工作区

# 指定commit回到工作区（前提是未推送到远程仓库）, 需要还原的上一个commit_id
git reset <commit_id>

# 把某个commit_id还原初始状态 （前提是未推送到远程仓库）, 需要还原的上一个commit_id
git reset --hard <commit_id>
```

## 标签

```bash
# 列出本地所有标签
git tag

# 列出远程所有标签
git ls-remote --tags origin

# 按照特定模式查找标签, `*` 模板搜索
git tag -l "v1.0.0*"

# 创建带有附注标签
git tag -a v1.1.0 -m "标签描述"

# 创建轻量标签, 不需要带任何参数
git tag v1.1.0

# 后期打标签, 假设之前忘记打标签了，可以通过git log查看commit id
git log
git tag -a v1.1.0 <commit_id>

# 推送到远程，默认只是本地创建
git push origin v1.1.0

# 一次性推送所有标签到远程
git push origin --tags

# 删除标签, 你需要再次运行 git push origin v1.1.0 才能删除远程标签
git tag -d v1.1.0

# 删除远程标签
git push origin --delete v1.1.0

# 检出标签
git checkout v1.1.0

# 查看本地某个标签详细信息
git show v1.1.0
```

## 变基

`git rebase` 命令有 2 个比较实用的功能：

- 将多个 commit 记录合并为一条
- 代替 `git mrege` 合并代码

### 1、将多个 commit 记录合并为一条

要注意保证当前工作区没内容再操作。

1、指定需要操作的记录，这时候会进入交互式命令

```bash
# start起点必填， end 可选，默认当前分支 HEAD 所指向的 commit
git rebase -i <start> <end>

git rebase -i HEAD~5 # 操作最近前5条提交记录
git rebase -i e88835de # 或者以 commit_id 进行操作
```

| 参数      | 描述                                                            |
| --------- | --------------------------------------------------------------- |
| p, pick   | 保留当前 commit，默认                                           |
| r, reword | 保留当前 commit，但编辑提交消息                                 |
| e, edit   | 保留当前 commit，但停止修改                                     |
| s, squash | 保留当前 commit，但融入上一次提交                               |
| b, break  | 在这里停止（稍后使用 `git rebase --continue` 继续重新设置基准） |
| d, drop   | 删除当前 commit                                                 |

这里是倒序排列，最新的记录在最后

<img src="media/gitrebase-3.png" width="700" />

2、除了第一条后面全部改成 `s` 或 `squash`:

<img src="media/gitrebase-4.png" width="700" />

3、按 `:wq` 退出交互式，接着进入另一个交互式来编辑 commit 消息, 如果不需要修改之前的 commit 消息则直接退出：

<img src="media/gitrebase-5.png" width="700" />

4、强制推送到远端

```bash
# 推送到 main 分支
git push -u -f origin main
```

### 2、合并分支代码

都说用 `git rebase` 代替 `git merge` 进行合并，这 2 个区别在于 `git rebase` 可以使历史记录更清晰, 下面 2 张图对比一下：

第一张图是 `git rebase`，第二张图是 `git merge`。

可以看出 `git rebase` 是一条直线的，`git merge` 则是各种交叉，很难理解。

<img src="media/gitrebase-1.png" width="700" />
<img src="media/gitrebase-2.png" width="700" />

假设有 2 个分支，main 和 dev，下面使用 `git rebase` 将 dev 分支代码合并到 main 分支上。

```bash
# 1、先切换到 main 分支
git switch main

# 2、dev 分支合并到当前 main 分支
git rebase dev

# 没有冲突情况, 直接推送
git push

# 发生冲突情况，先解决完冲突 => 暂存 => 继续 => 强推
git add -A
git rebase --continue # 继续
git push -f # 强制推送
```

中断 `git rebase` 操作, 如果操作一半不想继续使用 `rebase` 命令则可以中断此次操作。

```bash
$ git rebase --abort
```

## 工作流

Git Flow 是一套基于 git 的工作流程，这个工作流程围绕着 project 的发布(release)定义了一个严格的如何建立分支的模型。

`git flow` 只是简化了操作命令，不用 `git flow` 也可以，只要遵循 `git flow` 流程操作即可，手动一条一条命令执行也一样的。

`git flow` 不是内置命令，需要单独安装。

#### 初始化

每个仓库都必须初始化一次才能使用，这是针对当前用户而言的。

```bash
# 通常直接回车以完成默认设置
git flow init
```

#### 开始开发一个功能

假设我们要开始开发一个新的功能比如登录注册，这个时候就要打一个 `feature` 分支进行独立开发。

```bash
# 步骤一：开启新的功能, 起一个分支名叫 v1.1.0, 建立后分支名为 feature/v1.1.0
git flow feature start v1.1.0

# 步骤二：将分支推送到远程, 在团队协作中这一步少不了
git flow feature publish v1.1.0

# 最后：完成功能, 会将当前分支合并到 develop 分支然后删除 feature/v1.1.0 分支，回到 develop
git flow feature finish v1.1.0
```

#### 打补丁

什么情况下需要打补丁？ 假设已经上线的功能有 BUG 需要修复就需要打补丁了。

hotfix 是针对 `main` 分支进行打补丁的。

```bash
# 步骤一：开启一个补丁分支叫 fix_doc 用于修改文档错误，建立后分支名为 hotfix/fix_doc
git flow hotfix start fix_doc

# 步骤二：推送到远程，也可以不推，如果多人同时改BUG就需要推送共享分支
git flow hotfix publish fix_doc

# 最后：完成补丁, 将当前分支合并到 main 和 develop，然后删除分支，回到 develop
git flow hotfix finish fix_doc
```

#### 发布

假设产品给了个新需求并完成，这个时候可以选择发布。不发布也行，但是发布后会有版本区分，以后想找到某个版本的代码就很方便。

```bash
# 步骤一：建立一个发布版本 v1.1.0 建立后分支名为 release/v1.1.0
git flow release start v1.1.0

# 步骤二：推送到远程, 可选
git flow release publish v1.1.0

# 最后：将当前分支合并到 main 和 develop，打上一个标签，接着删除当前分支并回到 develop 分支上
git flow release finish v1.1.0
```

参考：

- [https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
- [https://www.git-tower.com/learn/git/ebook/cn/command-line/advanced-topics/git-flow](https://www.git-tower.com/learn/git/ebook/cn/command-line/advanced-topics/git-flow)

#### Git flow schema

![](media/git-flow.png)

---

## 子模块

`git submodule` 子模块的作用类似于包管理，类似 `npm`, 主要是复用仓库, 但比包管理使用起来更方便。

子模块可以不建立版本分支管理代码, 因为它是依赖主应用，所以建立版本分支可以从主应用去操作，那么一旦建立新的版本分支当前的所有内容都会被锁定在这个分支上，不管子模块仓库怎么修改。

#### 添加子模块

添加完子模块后会发现根目录下多了个 `.gitmodules` 元数据文件，主要是用于管理子模块。

```bash
git submodule add https://github.com/xjh22222228/git-manual.git # 默认添加到当前目录下
git submodule add https://github.com/xjh22222228/git-manual.git submodules/git-manual  # 添加到指定目录

# -b 指定需要添加仓库的某个分支
git submodule add -b develop https://github.com/xjh22222228/git-manual.git
```

#### 删除子模块

```bash
# 1、直接删除子模块目录
rm -rf submodule

# 2、编辑目录下的 .gitmodules 文件把需要删除的子模块删除掉

# 最后直接推送
git add -A
git commit -m "删除子模块"
git push
```

#### 克隆一个包含子模块的仓库

```bash
# --recursive 用于递归克隆，否则子模块目录是空的
git clone --recursive https://github.com/xjh22222228/git-manual.git

# 如果已经克隆了一个包含子模块的项目，但忘记了 --recursive， 可以使用此命令 初始化、抓取并检出任何嵌套的子模块
git submodule update --init --recursive
```

#### 修复子模块分支

当把一个包含子模块的仓库克隆下来后会发现子模块分支不对，可以使用下面命令纠正：

```bash
git submodule foreach -q --recursive 'git checkout $(git config -f $toplevel/.gitmodules submodule.$name.branch || echo main)'
```

#### 更新子模块代码

方法一：通常我们需要更新代码只需要执行 `git pull`, 这是比较笨的办法。

```bash
# 递归抓取子模块的所有更改，但不会更新子模块内容
git pull

# 这个时候需要进入子模块目录进行更新, 这样就完成了一个子模块更新，但是如果有很多子模块就比较麻烦了
cd git-manual && git pull
```

方法二：使用 `git submodule update` 更新子模块

```bash
# git 会尝试更新所有子模块, 如果只需要更新某个子模块只要在 --remote 后指定子模块名称
git submodule update --remote

# --recursive 会递归所有子模块, 包括子模块里的子模块
git submodule update --init --recursive
```

方法三：使用 `git pull` 更新, 这是一种新的更新模式，需要 >= 2.14

```bash
git pull --recurse-submodules
```

如果嫌麻烦每次 git pull 都需要手动添加 `--recurse-submodules`，可以配置 git pull 的默认行为， 如何配置请参考 [配置](#配置)

具体使用还可以看这里 [git submodule 子模块使用教程](https://www.xiejiahe.com/blog/detail/5dbceefc0bb52b1c88c30853)

## 子树

如果你知道 `git submodule` 那就大概知道 `git subtree` 干嘛用了， 基本上是做同一件事，复用仓库或复用代码。

官方建议使用 `git subtree` 代替 `git submodule`。

`git subtree` 优势：

- 不会像子模块需要 `.gitmodules` 元数据文件管理
- 子仓库会当做普通目录, 其实是没有仓库概念的
- 支持较旧的 Git 版本（甚至比 v1.5.2 还要旧）。
- 简单工作流程的管理很容易。

`git subtree` 劣势：

- 命令过于复杂, 推送拉取都很麻烦
- 虽然用于替代子模块, 但使用率并没有子模块广泛
- 子仓库和主仓库混合在一起, 历史记录相当于有 2 个仓库的记录

`git subtree` 命令用法:

```bash
git subtree add   --prefix=<prefix> <commit>
git subtree add   --prefix=<prefix> <repository> <ref>
git subtree pull  --prefix=<prefix> <repository> <ref>
git subtree push  --prefix=<prefix> <repository> <ref>
git subtree merge --prefix=<prefix> <commit>
git subtree split --prefix=<prefix> [OPTIONS] [<commit>]
```

在操作 `git subtree` 时当前工作区必须清空，否则无法执行。

## 添加子仓库

- `--prefix` 指定将子仓库存储位置
- `main` 是分支名称
- `--squash` 通常做法是不将子仓库整个历史记录存储在主仓库中，如果需要的话可以忽略整个参数

添加子仓库后, 会跟普通文件一样看待，可以进入 sub/common 目录执行 `git remote -v` 会发现没有仓库。

```bash
git subtree add --prefix=sub/common https://github.com/xjh22222228/git-manual.git main --squash
```

## 更新子仓库

当远程子仓库有内容变更时，可以通过下面命令进行更新：

```bash
git subtree pull --prefix=sub/common https://github.com/xjh22222228/git-manual.git main --squash
```

## 推送到子仓库

假如修改了子仓库里的内容，可以将修改这部分的内容推送到子仓库中

```bash
# 需要先在主仓库把子仓库的代码暂存
git add sub/common
git commit -m "子仓库修改"
# 然后推送
git subtree push --prefix=sub/common https://github.com/xjh22222228/git-manual.git main --squash
```

## 切割

随着项目的迭代, 主仓库会提交过多, 会发现每次 `push` 时会非常慢，尤其在 `windows` 平台较为明显。

每次 `push` 到子仓库里头时会花费大量的时间来重新计算子仓库的提交。并且因为每次 `push` 都是重新计算的，所以本地仓库和远端仓库的提交总是不一样的，这会导致 git 无法解决可能的冲突。

当使用 `git split` 命令后，使用 `git subtree push`，git 只会计算 split 后的新提交。

```bash
git subtree split --prefix=sub/common --branch=main
```

## 简化命令

通过以上实操，不难发现，`git subtree` 太长了，每次操作都要敲这么长的命令，谁能忍得住。

将子仓库添加为远程仓库：

```bash
# common 是仓库名字，可以随意定义
git remote add -f common https://github.com/xjh22222228/git-manual.git
```

要做其他 `git subtree` 命令时就不需要敲仓库地址了：

```bash
git subtree push --prefix=sub/common common main --squash
```

虽然省去了仓库地址，命令还是太长。

还有另一种解决方案，就是使用别名，例如在 `mac` 或 `linux` 中使用 [`alias`](https://github.com/xjh22222228/linux-manual#alias) 命令:

```bash
alias push="git subtree push --prefix=sub/common https://github.com/xjh22222228/git-manual.git main --squash"
```

也可以使用 git 自带的别名命令 => [命令别名配置](#命令别名配置)

如果你写前端，可以在 `package.json` 文件中加入：

```json
{
  "scripts": {
    "push": "git subtree push --prefix=sub/common https://github.com/xjh22222228/git-manual.git main --squash"
  }
}
```

下次需要推送时执行:

```bash
npm run push 或者 yarn push
```

## 二分查找

`git bisect` 基于二分查找算法, 用于定位引入 Bug 的 commit，主要 4 个命令。

此命令非常实用, 如果你的 Bug 不知道是哪个 commit 引起的，可以尝试此方法。

```bash
# 开始
git bisect start [终点] [起点] # 通过 git log 确定起点和终点
git bisect start HEAD 4d83cf

# 记录这次的commit是好的
git bisect good

# 记录这次的commit是坏的
git bisect bad

# 退出
git bisect reset
```

参考 [https://github.com/bradleyboy/bisectercise](https://github.com/bradleyboy/bisectercise)

## 归档

创建一个归档文件，可以理解为将当前项目压缩为一个文件。会忽略掉 `.git` 目录。

但与 `zip` / `tar` 等压缩不同，`git archive` 支持将某个分支或 commit 进行归档。

**参数**

| 参数     | 描述                                                                                |
| -------- | ----------------------------------------------------------------------------------- |
| --format | 可选，指定格式，默认 tar, 支持 tar 和 zip，如果不填会根据 --output 后缀格式进行推断 |
| --output | 输出到指定目录                                                                      |

```bash
# 归档 main 分支 并打包在当前目录下 output.tar.gz
git archive --output "./output.tar.gz" main

# 归档指定commit
git archive --output "./output.tar.gz" d485a8ba9d2bcb5

# 归档为 zip, 无需指定 --format， 因为会根据文件后缀进行推断
git archive --output "./output.zip" main

# 归档一个或多个目录, 而不是归档整个项目
git archive --output "./output.zip" main src tests
```

## 格式化日志

在使用 `git log` 命令时可以携带 `--pretty=format` 用来格式化日志。

**常用格式如下：**

| 参数 | 描述                                                                   |
| ---- | ---------------------------------------------------------------------- |
| %H   | 完整 commit hash                                                       |
| %h   | 简写 commit hash 一般是前 7 位                                         |
| %T   | 完整 hash 树                                                           |
| %t   | 简写 hash 树                                                           |
| %an  | 作者名称                                                               |
| %ae  | 作者邮箱                                                               |
| %ad  | 作者日期, RFC2822 风格：`Thu Jul 2 20:42:20 2020 +0800`                |
| %ar  | 作者日期, 相对时间：`2 days ago`                                       |
| %ai  | 作者日期, ISO 8601-like 风格： `2020-07-02 20:42:20 +0800`             |
| %aI  | 作者日期, ISO 8601 风格： `2020-07-02T20:42:20+08:00`                  |
| %cn  | 提交者名称                                                             |
| %ce  | 提交者邮箱                                                             |
| %cd  | 提交者日期，RFC2822 风格：`Thu Jul 2 20:42:20 2020 +0800`              |
| %cr  | 提交者日期，相对时间：`2 days ago`                                     |
| %ci  | 提交者日期，ISO 8601-like 风格： `2020-07-02 20:42:20 +0800`           |
| %cI  | 提交者日期，ISO 8601 风格： `2020-07-02T20:42:20+08:00`                |
| %d   | 引用名称： (HEAD -> main, origin/main, origin/HEAD)                    |
| %D   | 引用名称，不带 `()` 和 换行符： HEAD -> main, origin/main, origin/HEAD |
| %e   | 编码方式                                                               |
| %B   | 原始提交内容                                                           |
| %C   | 自定义颜色                                                             |

例子：

```bash
git log -n 1 --pretty=format:"%an" # xjh22222228

git log -n 1 --pretty=format:"%ae" # xjh22222228@gmail.com

git log -n 1 --pretty=format:"%d" #  (HEAD -> main, origin/main, origin/HEAD)

# 自定义输出颜色, %C后面跟着颜色名
git log --pretty=format:"%Cgreen 作者：%an"
```

## 清空 commit 历史

清空 `commit` 有 2 种方法。

1、第一种方法原理是通过新建新的分支，假设要清空 commit 分支是 `develop`

```bash
# 1、新建一个新分支
git checkout --orphan new_branch
# 2、暂存所有文件并提交
git add -A && git commit -m "First commit"
# 3、删除本地 develop 分支
git branch -D develop
# 4、再将 new_branch 分支重命名为 develop
git branch -m develop
# 5、强制将 develop 分支推送到远程
git push -f origin develop
```

2、第二种方法通过更新 `引用`, 假设要重设 `main` 分支

```bash
# 通过 git log 找到第一个 commit_id
git update-ref refs/heads/main 9c3a31e68aa63641c7377f549edc01095a44c079

# 接着可以提交
git add .
git commit -m "第一个提交"
git push -f # 注意一定要强制推送
```

这 2 种方法都是用于清空 commit 历史， 不会造成当前文件的丢失，所以放心。

笔者推荐使用第二种方法，更安全可靠。

## 帮助

```bash
# 详细打印所有git命令
git help

# 打印所有git命令, 此命令不会有详细信息，更清晰一些
git help -a

# 列出所有可配置的变量
git help -c
```

## 提交规范

| 标志     | 描述                     |
| -------- | ------------------------ |
| feat     | 该提交含有新的特性       |
| style    | 通常是代码格式的修改     |
| chore    | 构建过程或辅助工具的变动 |
| fix      | 修复 Bug                 |
| docs     | 文档修改                 |
| test     | 单元测试改动             |
| refactor | 代码重构                 |
| perf     | 性能优化、体验           |
| revert   | 回滚版本                 |
| merge    | 代码合并                 |
| typo     | 错字, 比如单词拼错       |

**例子：**

```bash
# 含有新特性
git commit -m "feat: 新增xx功能"

# 代码格式化
git commit -m "style: 规范Eslint"

# 修改Jenkins构建流程
git commit -m "chore: Update Jenkins"

# 修复Bug, 建议描述清晰, 日后方便查找, #688 是修复某个id的编号
git commit -m "fix(登录闪烁): #688"

# 修改文档
git commit -m "docs: git pull"

# 单元测试改动
git commit -m "test: 测试登录"

# 项目代码重构
git commit -m "refactor: 流程模块重构"
```

## 解决冲突

**代码合并/更新代码** 经常会遇到冲突的情况。

#### 解决冲突的流程如下：

1. 执行 `git pull` 把代码拉下来，git 会自动尝试合并
2. 编辑冲突文件, 根据实际情况保留本地代码还是远端代码
3. 暂存文件并推送到远端

<details>
  <summary>点击查看解决冲突.gif</summary>
  
  <img src="media/git-merge-conflict.gif">
</details>

面向 GUI 的用户，推荐 3 个工具专门处理 git 冲突：

- [meld](http://meld.sourceforge.net/install.html)
- [kdiff3](http://kdiff3.sourceforge.net/)
- 在冲突时执行 `git mergetool` 命令会启动一个默认 GUI

[这篇文章专门介绍这 2 个工具如何使用](https://gitguys.com/topics/merging-with-a-gui/)

## 仓库迁移

仓库迁移也可以叫复制仓库。

有时候需要从一个旧仓库迁移到新仓库，如果手动只能把文件进行迁移，但是如果需要把分支、标签、历史记录一起迁移就需要复制仓库。

旧仓库 A: https://github.com/xjh22222228/A.git
新仓库 B: https://github.com/xjh22222228/B.git

1、克隆旧裸仓库

```bash
# 克隆裸仓库，里面没有工作区内容
git clone --bare https://github.com/xjh22222228/A.git
```

2、镜像推送至新仓库

```bash
cd A
git push --mirror https://github.com/xjh22222228/B.git
```

3、删除刚刚克隆的旧仓库

```bash
rm -rf A
```

4、拉取新仓库

```bash
git clone https://github.com/xjh22222228/B.git
```

除了通过命令迁移之外，可以通过网页导入仓库的方式也可以。

## 奇技淫巧

**美化 `git log`, 直逼 GUI**

```bash
# 1、全局配置
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
# 2、输入下面命令, 日志变得非常直观化
git lg

# 这里另外提供几种模式, 可以选择喜欢的一种进行别名配置
git config --global alias.lg "log --graph --pretty=format:'%Cred%h - %Cgreen[%an]%Creset -%C(yellow)%d%Creset %s %C(yellow)<%cr>%Creset' --abbrev-commit --date=relative"

git config --global alias.his "log --graph --decorate --oneline --pretty=format:'%Creset %s %C(magenta)in %Cred%h %C(magenta)commited by %Cgreen%cn %C(magenta)on %C(yellow) %cd %C(magenta)from %Creset %C(yellow)%d' --abbrev-commit --date=format:'%Y-%m-%d %H:%M:%S'"

git config --global alias.hist "log --graph --decorate --oneline --pretty=format:'%Cred%h - %C(bold white) %s %Creset %C(yellow)%d  %C(cyan) <%cd> %Creset %Cgreen(%cn)' --abbrev-commit --date=format:'%Y-%m-%d %H:%M:%S'"
```

<details>
  <summary>效果图.png</summary>
  
  <img src="media/git-log.png">
</details>

## GUI 客户端

推荐几款比较好用的 git 图形界面工具, 不分先后。

- 免费 - [Github Desktop](https://desktop.github.com/)
- 免费 - [Sourcetree](https://www.sourcetreeapp.com/)
- 免费 - [tortoiseGit](https://tortoisegit.org/)
- 免费 - [gitkraken](https://www.gitkraken.com/)
- 免费 - [gitup](https://gitup.co/)
- 免费 - [magit](https://github.com/magit/magit)
- 收费 - [smartgit](https://www.syntevo.com/smartgit/)
- 收费 - [git-fork](https://git-fork.com/)
- 收费 - [tower](https://www.git-tower.com/)
- 收费 - [lazygit](https://github.com/jesseduffield/lazygit)

## 生成 SSH_Key

以下适用于 `Mac` / `Linux`。

1、进入到 ssh

```bash
cd ~/.ssh
```

2、替换为您的 GitHub 电子邮件地址

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

3、当提示“输入要在其中保存密钥的文件”时，按 Enter。接受默认文件位置。 (建议修改名字，防止以后被覆盖)

```
> Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
```

4、在提示符下，键入一个安全密码, 默认回车即可

```bash
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

5、生成的 SSH Key 添加到 `ssh config` 中

```bash
vim ~/.ssh/config

# 粘贴
Host *
  IgnoreUnknown AddKeysToAgent,UseKeychain
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

最后将公钥添加到 [https://github.com/settings/keys](https://github.com/settings/keys) 中

```
cat ~/.ssh/id_rsa.pub
```

<details>
  <summary>演示生成SSH Key.gif</summary>
  
  <img src="media/ssh-key.gif">
</details>

## 其他

```bash
# 查看git版本
git --version

# 清除本地git缓存
git rm -r --cached .

# 列出没有被 .gitignore 忽略的文件列表
git ls-files
```

## 记住密码

使用 https 方式会要求每次都需要输入账号和密码，如果想下次不弹出账号密码可以按以下方式：

```bash
# 临时记住密码，默认15分钟
git config --global credential.helper cache

# 自定义记住密码时间，单位秒
git config credential.helper 'cache --timeout=3600'

# 长期记住密码
git config --global credential.helper store
```

## 清除账号

清除 git 已保存的用户名和密码

```bash
# windows
git credential-manager uninstall

# mac / linux (以下任意一条命令都可)
git config --global credential.helper ""
git config --global --unset credential.helper
```

## 加速

在国内克隆或下载版本会很慢，可以借助下面镜像站点进行加速。
克隆：

```bash
# 公有仓库
git clone https://ghproxy.com/https://github.com/xjh22222228/git-manual.git

# 私有仓库, 需要配合Token使用 => https://github.com/settings/tokens
git clone https://user:your_token@ghproxy.com/https://github.com/your_name/your_private_repo
```

资源加速：

```bash
https://raw.githubusercontent.com/xjh22222228/git-manual/main/media/poster.png
# ↓ 替换为
https://cdn.jsdelivr.net/gh/xjh22222228/git-manual@main/media/poster.png

# 备用域名，只需要替换域名
# testingcf.jsdelivr.net
# img.jsdmirror.com
# gcore.jsdelivr.net
```

###### Github 文件/GIST/RAW 加速：

使用方法打开 [https://www.7ed.net/](https://www.7ed.net/)

## 思维导图

![](media/map.jpg)

[⬆ 回顶部](#)
