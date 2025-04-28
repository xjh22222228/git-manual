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

- [git config 配置](#git-config-配置)
- [git init 初始化仓库](#git-init-初始化仓库)
- [git clone 克隆仓库](#git-clone-克隆仓库)
- [git remote 管理仓库](#git-remote-管理仓库)
- [git add 暂存文件](#git-add-暂存文件)
- [git commit 提交文件](#git-commit-提交文件)
- [git push 推送远端](#git-push-推送远端)
- [git branch 创建查看删除重命名分支](#git-branch-创建查看删除重命名分支)
- [git checkout 切换创建分支恢复文件](#git-checkout-切换创建分支恢复文件)
- [git switch 切换创建分支](#git-switch-切换创建分支)
- [git cherry-pick 转移提交](#git-cherry-pick-转移提交)
- [git stash 临时保存](#git-stash-临时保存)
- [git status 文件状态](#git-status-文件状态)
- [git log 日志](#git-log-日志)
- [git shortlog 日志](#git-shortlog-日志)
- [git reflog 日志](#git-reflog-日志)
- [git blame 最后修改信息](#git-blame-最后修改信息)
- [git merge 合并](#git-merge-合并)
- [git rm 删除文件](#git-rm-删除文件)
- [git restore 还原](#git-restore-还原)
- [git pull 拉取](#git-pull-拉取)
- [git mv 移动/重命名文件](#git-mv-移动/重命名文件)
- [git diff 比较文件内容差异](#git-diff-比较文件内容差异)
- [git show 查看历史提交信息](#git-show-查看历史提交信息)
- [git reset 回滚版本](#git-reset-回滚版本)
- [git tag 标签](#git-tag-标签)
- [git rebase 变基](#git-rebase-变基)
- [git flow 工作流](#git-flow-工作流)
- [git submodule 子模块](#git-submodule-子模块)
- [git subtree 子树](#git-subtree-子树)
- [git bisect 二分查找](#git-bisect-二分查找)
- [git archive 归档](#git-archive-归档)
- [清空 commit 历史](#清空-commit-历史)
- [帮助](#帮助)
- [提交规范](#提交规范)
- [解决冲突](#解决冲突)
- [仓库迁移](#仓库迁移)
- [奇技淫巧](#奇技淫巧)
- [GUI 客户端](#GUI-客户端)
- [使用 SSH 克隆仓库](#使用-SSH-克隆仓库)
- [其他](#其他)
- [记住密码](#记住密码)
- [清除账号](#清除账号)
- [加速](#加速)
- [思维导图](#思维导图)

## git config 配置

git config 是 Git 中用于配置各种参数的命令，它允许你对 Git 的行为和环境进行个性化设置。这些设置可以分为三个不同的级别：系统级、全局级和仓库级，不同级别设置的优先级不同，仓库级设置会覆盖全局级设置，而全局级设置又会覆盖系统级设置。

#### 基本语法

```bash
git config [--system | --global | --local] <name> <value>
```

- `--system`：指定系统级配置，对所有用户的所有仓库生效。配置文件通常位于 `/etc/gitconfig`（Linux 或 macOS）。
- `--global`：指定全局级配置，对当前用户的所有仓库生效。配置文件通常位于 `~/.gitconfig` 或 `~/.config/git/config`（Linux 或 macOS）。
- `--local`：指定仓库级配置，仅对当前仓库生效。配置文件位于当前仓库的 `.git/config` 目录下。
- 如果不指定以上任何选项，默认使用 `--local`。
- `<name>`：要配置的参数名称。
- `<value>`：要为参数设置的值。

```bash
# 查看全局配置列表
git config --global -l

# 查看当前仓库配置列表
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

## git init 初始化仓库

`git init [--bare] [directory]` 用于在指定目录下创建一个新的 Git 仓库

`--bare`：可选参数，用于创建一个裸仓库。裸仓库通常用于作为远程仓库，不包含工作目录，主要用于多人协作时共享代码。

`directory`：可选参数，指定要初始化 Git 仓库的目录。若不指定，将在当前目录下初始化仓库。

#### 使用场景

- `新项目初始化`：当你开始一个新的项目时，可使用 `git init` 命令将项目目录转换为 Git 仓库，从而方便对项目进行版本控制。
- `已有项目纳入版本控制`：如果你有一个已经存在的项目，但尚未使用版本控制，也可以使用 `git init` 命令将其纳入 Git 的管理之下。

```bash
# 会在当前目录生成.git
git init

# 以安静模式创建，只会打印错误或警告信息
git init -q

# 在当前目录下创建一个裸仓库，里面只有 .git 下的所有文件
git init --bare
```

## git clone 克隆仓库

#### 基本语法

```bash
git clone [options] <repository> [<directory>]
```

- `options`：可选参数，用于指定克隆操作的一些额外设置。
- `<repository>`：必选参数，指定要克隆的远程仓库的地址。这个地址可以是基于 HTTP/HTTPS 协议的，也可以是基于 SSH 协议的。
- `<directory>`：可选参数，指定克隆到本地的目标目录名称。如果不指定，Git 会使用远程仓库的名称作为本地目录名。

#### 常用选项

- `--depth <depth>`：进行浅克隆，只克隆指定深度的提交历史，而不是完整的历史记录。这可以显著减少克隆所需的时间和磁盘空间。例如，`git clone --depth 1 <repository>` 只克隆最新的一次提交。
- `--branch <branch>` 或 `-b <branch>`：指定要克隆的分支。默认情况下，Git 会克隆远程仓库的默认分支（通常是 `main` 或 `master`）。例如，`git clone -b develop <repository>` 会克隆远程仓库的 `develop` 分支。
- `--single-branch`：只克隆指定分支的内容，不克隆其他分支的历史记录。结合 `--branch` 选项使用，例如 `git clone --single-branch --branch feature <repository>` 只会克隆 `feature` 分支。

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

## git remote 管理仓库

`git remote` 是 Git 里用于管理远程仓库的命令，借助它可以对远程仓库进行查看、添加、删除、重命名等操作。

#### 基本语法

```bash
git remote [options] [command] [args]
```

- `options`：可选参数，用于指定命令的一些额外设置。
- `command`：指定要执行的操作命令。
- `args`：执行命令所需的参数。

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

# 更新远程仓库的信息
git remote update
```

## git add 暂存文件

`git add` 是 Git 中一个基础且关键的命令，主要用于将工作目录中修改或新增的文件添加到暂存区。

#### 基本语法

```bash
git add [options] <file>...
```

- `options`：可选参数，用于指定不同的添加行为。
- `<file>`：要添加到暂存区的文件或目录，可以指定多个文件，用空格分隔。

```bash
# 暂存所有
git add -A

# 暂存某个文件
git add ./README.md

# 暂存当前目录所有改动文件
git add .

# 暂存一系列文件
git add 1.txt 2.txt ...

# 暂存所有修改文件或删除文件，创建新的文件不会被暂存
git add -u
```

#### 注意事项

- `.gitignore 文件`：git add 命令会忽略 `.gitignore` 文件中指定的文件和目录，即使使用 `git add .` 或 `git add -A` 也不会添加这些被忽略的文件。
- `重复添加`：如果多次对同一个文件执行 `git add` 命令，只有最后一次添加的更改会被包含在提交中。

## git commit 提交文件

`git commit` 是 Git 中用于将暂存区的内容永久保存到本地仓库历史记录中的关键命令。通过提交，你可以记录项目在某个特定时间点的状态，同时添加描述性的信息，方便后续查看和理解每次更改的目的。

#### 基本语法

```bash
git commit [options] [-m <message>]
```

- `options`：可选参数，用于指定不同的提交行为。
- `-m <message>`：用于提供本次提交的简短描述信息，`<message>` 是具体的描述内容。

```bash
# -m 提交的描述信息
git commit -m "changes log"

# 当提交信息较为复杂，需要多行描述可以不适用 -m 参数，Git会默认打开文本编辑器让你输入提交信息
git commit

# 只提交某个文件
git commit README.md -m "message"

# 提交并显示diff变化
git commit -v

# 允许提交空消息，通常必须指定 -m 参数
git commit --allow-empty-message

# 重写上一次提交信息，确保当前工作区没有改动
git commit --amend -m "新的提交信息"

# 跳过验证, 如果使用了类似 husky 工具。
git commit --no-verify -m "message"
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

## git push 推送远端

`git push` 是 Git 中用于将本地仓库的提交推送到远程仓库的命令。当你在本地完成了一系列的代码修改、添加和提交操作后，就可以使用 `git push` 把这些更改同步到远程仓库。

#### 基本语法

```bash
git push [options] [<repository> [<refspec>...]]
```

- `options`：可选参数，用于指定推送操作的一些额外设置。
- `<repository>`：可选参数，指定要推送的远程仓库的名称，默认是 origin。
- `<refspec>`：可选参数，用于指定本地分支和远程分支的映射关系，格式为 `[+]<src>:<dst>`。

```bash
# 默认推送当前分支
# 等价于 git push origin, 实际上推送到一个叫 origin 默认仓库名字
git push

# 设置上游分支并推送
#  使用 -u 或 --set-upstream 选项，在推送的同时将本地分支与远程分支关联起来。之后，再进行该分支的推送或拉取操作时，就可以直接使用 git push 或 git pull，无需再指定远程仓库和分支名称
git push -u origin main

# 本地分支推送到远程分支， 本地分支:远程分支
git push origin <branchName>:<branchName>

# 强制推送, --force 缩写
git push -f

# 删除远程分支
git push origin :old-feature
git push origin --delete old-feature # 或者
```

## git branch 创建查看删除重命名分支

`git branch` 是 Git 中用于管理分支的核心命令

#### 基本语法

```bash
git branch [options] [branch-name] [start-point]
```

#### 查看分支

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

# 查看哪些分支已经合并到当前分支
# 该命令会列出已经将其更改合并到当前分支的所有分支。通常，这些分支可以安全地删除。
git branch --merged

# 查看哪些分支还未合并到当前分支
git branch --no-merged
```

#### 创建分支

```bash
# 创建分支
git branch new-feature

# 从指定 commit 创建分支
git branch new-feature commit-hash

# 强制创建分支
git branch -f main

# 创建孤立分支，没有历史记录
git checkout --orphan new-feature
```

#### 删除分支

```bash
# 删除本地已合并的main分支
git branch -d main

# 强制删除本地分支
git branch -D branch-to-delete
```

#### 重命名分支

```bash
# 重命名分支
git branch -m old-branch-name new-branch-name
```

#### 给分支添加备注

有时候分支过多很难通过分支名去判断这个分支做了什么。

```bash
# 命令
$ git config branch.{branch_name}.description 备注内容

# 给 hotfix/tip 分支添加备注信息
$ git config branch.hotfix/tip.description 修复细节
```

## git checkout 切换创建分支恢复文件

`git checkout` 是 Git 里一个极为常用的命令，它主要用于在不同分支间切换、恢复文件以及创建新分支并切换到该分支。

#### 基本语法

```bash
git checkout [options] <branch>
git checkout [options] -- <file>
```

- `options`：可选参数，用来指定不同的操作行为。
- `<branch>`：要切换到的分支名称。
- `<file>`：要恢复的文件名称。

#### 切换分支

```bash
# 切换分支
git checkout <branch>

# 切换上一个分支
git checkout -
```

在克隆时使用 `--depth=1` 切换其他分支，比如切换 dev 分支：

```bash
git clone --depth=1 https://github.com/xjh22222228/git-manual.git

# 切换 dev 分支
git remote set-branches origin 'dev'
git fetch --depth=1 origin dev
git checkout dev
```

#### 创建分支

```bash
# 创建本地 develop 分支并切换
git checkout -b develop

# 根据 commit hash 创建新的分支
git checkout -b new-branch commit-hash

# 创建远程分支, 实际上创建本地分支然后推送到远端
git checkout -b develop
git push origin develop

# 创建一个空的分支, 不继承父分支，历史记录是空的，一般至少需要执行4步
git checkout --orphan develop
git rm -rf .  # 这一步可选，如果你真的想创建一个没有任何文件的分支
git add -A && git commit -m "提交" # 添加并提交，否则分支是隐藏的 （执行这一步之前需要注意当前工作区必须保留一个文件，否则无法提交）
git push --set-upstream origin develop # 推送到远程
```

#### 恢复文件到上一次提交的状态

```bash
# -- 后跟着文件名称， 表示恢复该文件到上一次提交的状态
git checkout -- file.txt
```

## git switch 切换创建分支

`git switch` 是 Git 2.23 版本引入的新命令，旨在简化分支切换操作，它是 `git checkout` 部分功能的替代，主要用于在不同分支之间进行切换，让操作更加清晰和安全。

#### 基本语法

```bash
git switch [options] <branch>
git switch [options] -c <new-branch> [start-point]
```

- `options`：可选参数，用于指定不同的操作行为。
- `<branch>`：要切换到的目标分支名称。
- `-c`：创建新分支并切换到该分支。
- `<new-branch>`：要创建的新分支名称。
- `start-point`：可选参数，指定新分支的起始提交点，默认是当前分支的最新提交。

#### 切换分支

```bash
# 切换到 develop 分支
git switch develop

# 切换到上一个分支
git switch -

# 强制切换到 develop 分支，并抛弃本地所有修改
git switch -f develop

# -t, 切换远端分支, 如果用了 git remote 添加一个新仓库就需要用 -t 进行切换
git switch -t upstream/main
```

#### 创建分支

```bash
# 创建分支并切换
git switch -c newBranch

# 强制创建分支
git switch -C newBranch

# 从前3次提交进行创建新的分支
git switch -c newBranch HEAD〜3

# 也可以从某个 commit hash 创建分支
git switch -c new-branch commit-hash

# --track 创建 dev 分支并与远程 code/dev 分支关联
git switch --track code/dev
```

## git cherry-pick 转移提交

`git cherry-pick` 是 Git 里一个非常实用的命令，其作用是把指定的提交应用到当前分支。

#### 使用场景

- `同步部分提交`：当你仅需把某个分支里的部分提交同步到另一个分支时，`git cherry-pick` 就派上用场了，而无需合并整个分支。
- `修复特定问题`：要是在某个分支发现了问题，并且已经在另一个分支修复，那么可以使用 `git cherry-pick` 把修复提交应用到有问题的分支。

#### 基本用法

- `--edit|-e`：在应用提交之前，允许你编辑提交信息。
- `--no-commit`：应用提交但不自动创建新的提交，这样你可以在之后手动提交。
- `--signoff`：在提交信息中添加你的签名，表示你对提交负责。

```bash
# 单个提交
git cherry-pick <commit-hash>

# 多个连续提交
#  <start-commit-hash> 是起始提交的哈希值，<end-commit-hash> 是结束提交的哈希值。注意，起始提交不会被包含在内，只会应用从起始提交之后到结束提交的所有提交。
git cherry-pick <start-commit-hash>..<end-commit-hash>

# 多个不连续提交
git cherry-pick <commit-hash-1> <commit-hash-2> <commit-hash-3>
```

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

## git stash 临时保存

`git stash`是 Git 里一个实用的命令，它可以把当前工作目录里还没提交的修改（包含暂存区和非暂存区的修改）保存起来，让工作目录回到上一次提交时的干净状态。

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

## git status 文件状态

`git status`是 Git 中一个非常基础且常用的命令，它用于显示工作目录和暂存区的状态。通过该命令，你可以了解到哪些文件被修改、哪些文件被添加到暂存区、哪些文件被删除等信息。

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

## git log 日志

执行 `git log` 命令，会显示当前分支从最近到最早的所有提交记录，每条记录包含提交哈希、作者、日期以及提交说明。

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

# 将每条提交记录显示为一行，仅包含提交哈希的前几位和提交说明，便于快速查看
git log --oneline

# 以图形查看日志记录
git log --graph --oneline

# 以倒序查看历史记录
git log --reverse

# --since 和 --until：显示指定时间范围内的提交记录
git log --since="2025-03-01" --until="2025-03-25"
```

#### 格式化日志

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

## git shortlog 日志

`git shortlog` 命令，它会按照作者对提交进行分组，并统计每个作者的提交数量，同时显示每个作者的最新提交信息。

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

## git reflog 日志

`git reflog` 命令，它会展示本地仓库引用的更新历史，每条记录包含引用的哈希值、操作名称、提交信息以及时间等内容。

- 显示 HEAD（或指定引用）在过去一段时间内的所有移动记录。
- 包括提交、分支切换、重置、变基等操作，即使这些提交不再属于任何分支。
- 面向引用变更，记录操作历史，适合救急和调试。

如果你执行 `git reset --hard` 或删除分支，某些提交会变得 `“不可达”`，`git log` 不会显示。

```bash
# 每条提交记录以一行的形式输出日志
git reflog

# 恢复丢失提交，通过 git reflog 找回 commit_id
git reflog
git reset --hard commit_id

# 指定显示的记录数量。例如，显示最近的 5 条记录
git reflog -n 5

# 以相对时间（如 “2 days ago”）显示记录的日期
git reflog --relative-date

# 按照不同的日期格式显示记录。例如，以 iso 格式显示日期
git reflog --date=iso
```

#### 注意事项

- 记录的是本地仓库的操作历史，不会随着代码一起推送到远程仓库。
- 记录默认会保留 90 天（对于可达对象）或 30 天（对于不可达对象），但这个时间可以通过配置项 `gc.reflogExpire` 和 `gc.reflogExpireUnreachable` 进行调整。

## git blame 最后修改信息

`git blame` 是 Git 里一个极为实用的命令，其主要功能是逐行查看文件内容的最后修改信息，包括最后修改该内容的提交哈希、作者、日期以及提交信息。

#### 基本语法

```bash
git blame <文件名>
```

```bash
# 查看 README.md 文件的修改信息，他会以每行修改信息展示
git blame README.md

# 查看文件的指定的行数修改信息
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

# -w 忽略空格更改
git blame -w README.md

# 以更易读的格式显示时间戳
git blame -c README.md
```

## git merge 合并

`git merge`是 Git 里用于将分支的修改合并到当前分支的命令。

`feature/v1.0.0` 分支代码合并到 `develop`

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

合并提交指定自定义的提交信息

```bash
git merge develop -m "Merge develop branch into main"
```

## git rm 删除文件

`git rm <file>`：此命令用于把文件从工作目录和索引中移除，并且会把这次移除操作记录到下一次提交里。

```bash
# 删除 1.txt 文件
git rm 1.txt

# 删除当前所有文件, 与rm -rf 命令不同的是不会删除 .git 目录
git rm -rf .

# 清除当前工作区缓存，但不会删除文件，通常用于修改文件名不生效问题
git rm -r --cached .

# 把文件从索引中移除，工作目录里的文件会被保留。这在你想让 Git 不再追踪某个文件
git rm --cached <file>
```

## git restore 还原

`git restore`是 Git 2.23 版本引入的一个命令，主要用于恢复工作区文件和暂存区的状态。

是为了分离 `git checkout` / `git reset` 职责。

```bash
# 撤销工作区文件修改, 不包括新建文件
git restore README.md # 一个文件
git restore README.md README2.md # 多个文件
git restore . # 当前全部文件

# 从暂存区回到工作区
git restore --staged README.md
```

## git pull 拉取

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

## git mv 移动-重命名文件

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

## git diff 比较文件内容差异

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

## git show 查看历史提交信息

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

## git reset 回滚版本

回滚版本有 2 种方法：

- `git reset` - 会改变提交历史。当使用 git reset 移动 HEAD 指针后，被跳过的提交在没有其他引用的情况下，最终可能会被 Git 的垃圾回收机制清理掉，从而从提交历史中消失。
- `git revert` - 不会删除任何原有的提交，而是在提交历史中新增一个反向操作的提交。提交历史的连续性得以保留，所有原有的提交仍然存在于历史记录中。

`git reset` 命令用法：

```bash
# --hard 丢弃工作区和暂存区，回到当前提交
git reset --hard

# 回滚上一个版本
git reset --hard HEAD^

# 回滚上两个版本
git reset --hard HEAD^^

# 回滚到指定 commit_id ， 通过 git log 查看
git reset --hard 'commit id'

# 回滚到前一次修改，默认--mixed，重置暂存区，工作区不变
git reset HEAD~1

# --soft 保留之前的暂存区和工作区
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

```

## git tag 标签

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

## git rebase 变基

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

## git flow 工作流

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

## git submodule 子模块

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

## git subtree 子树

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

#### 添加子仓库

- `--prefix` 指定将子仓库存储位置
- `main` 是分支名称
- `--squash` 通常做法是不将子仓库整个历史记录存储在主仓库中，如果需要的话可以忽略整个参数

添加子仓库后, 会跟普通文件一样看待，可以进入 sub/common 目录执行 `git remote -v` 会发现没有仓库。

```bash
git subtree add --prefix=sub/common https://github.com/xjh22222228/git-manual.git main --squash
```

#### 更新子仓库

当远程子仓库有内容变更时，可以通过下面命令进行更新：

```bash
git subtree pull --prefix=sub/common https://github.com/xjh22222228/git-manual.git main --squash
```

#### 推送到子仓库

假如修改了子仓库里的内容，可以将修改这部分的内容推送到子仓库中

```bash
# 需要先在主仓库把子仓库的代码暂存
git add sub/common
git commit -m "子仓库修改"
# 然后推送
git subtree push --prefix=sub/common https://github.com/xjh22222228/git-manual.git main --squash
```

#### 切割

随着项目的迭代, 主仓库会提交过多, 会发现每次 `push` 时会非常慢，尤其在 `windows` 平台较为明显。

每次 `push` 到子仓库里头时会花费大量的时间来重新计算子仓库的提交。并且因为每次 `push` 都是重新计算的，所以本地仓库和远端仓库的提交总是不一样的，这会导致 git 无法解决可能的冲突。

当使用 `git split` 命令后，使用 `git subtree push`，git 只会计算 split 后的新提交。

```bash
git subtree split --prefix=sub/common --branch=main
```

#### 简化命令

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

## git bisect 二分查找

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

## git archive 归档

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

## 使用 SSH 克隆仓库

使用 SSH 克隆仓库需要先在电脑生成 SSH 公钥和密钥，以下是生成步骤：

1. 进入到 ssh

```bash
cd ~/.ssh
```

2. 替换为您的 GitHub 电子邮件地址

```bash
# -t ed25519: 使用 Ed25519 算法（更现代且安全）。
# -C: 添加注释，通常是你的邮箱，与GitHub邮箱没有关系
ssh-keygen -t ed25519 -C "your_email@example.com"

# 按提示操作，可以直接回车，默认会生成 ~/.ssh/id_ed25519，你可以修改名称作为管理
```

3. 查看公钥并添加到 GitHub 账号

[https://github.com/settings/keys](https://github.com/settings/keys)

```bash
# 输出类似于 ssh-ed25519 AAAAC3Nza... your_email@example.com，复制整个内容。
cat ~/.ssh/id_ed25519.pub
```

4. 添加 SSH 密钥

```bash
ssh-add ~/.ssh/id_ed25519
```

5. 测试连接

```bash
# 输出以下信息说明 ssh 连接成功
# Hi xxxxx! You've successfully authenticated, but GitHub does not provide shell access.
ssh -T git@github.com
```

#### 管理多个 GitHub 账号

如果你有多个 GitHub 账号，需要额外的配置 `ssh config`

修改 `~/.ssh/config`

```bash
vim ~/.ssh/config
```

```bash
# Host 是自定义名称，通常用 GitHub 账号命名
# 账号1
Host user1
  HostName github.com
  User git
  # 修改你的密钥文件路径
  IdentityFile ~/.ssh/id_ed25519

# 账号2
Host user2
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_2
```

使用自定义名称测试连接

```bash
ssh -T git@user1
```

克隆仓库

```bash
#             Host:用户/仓库
git clone git@user1:admin/demo.git
```

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
