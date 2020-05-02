
对Git命令进行了整理，会陆陆续续的增加，当做一个参考手册


## 配置
```
# 查看配置列表
git config -l

# 查看已设置的用户名
git config --global --get user.name

# 设置用户名
git config --global user.name "xiejiahe"

# 查看已设置的邮箱
git config --global --get user.email

# 设置邮箱
git config --global user.email "mb06@qq.com"
```

## 查看文件状态
```
git status
```

## 查看日志
```
# 查看完整历史提交记录
git log

# 查看前N次提交记录 commit message
git log -2

# 查看前N次提交记录，包括diff
git log -p -2

# 搜索关键词
git log -S 你好
```

## 初始化本地仓库
```
# 会在当前目录生成.git
git init
```

----

## 克隆
```
# https 协议
git clone https://github.com/xjh22222228/public.git

# SSH协议
git clone xjh22222228@github.com/xjh22222228/public.git

# 克隆某个分支， -b 后面分支名字
git clone -b v2.8.0 https://github.com/xjh22222228/public.git

# 递归克隆，如果项目包含子模块就非常有用
git clone --recursive xjh22222228@github.com/xjh22222228/public.git

# 克隆深度为1, 不会把历史的记录也克隆，这样可以节省克隆时间
git clone --depth=1 https://github.com/xjh22222228/public.git
```



----


## 查看分支
```
# 查询所有分支
git branch --all

# 查看本地分支
git branch

# 查看远端分支
git branch -r
```

## 切换分支
```
# 2种方法，切换到master分支
git checkout master
git switch master

# 切换上一个分支
git checkout -
```

## 创建分支
```
# 创建develop分支
git branch develop

# 创建develop分支并切换
git checkout -b develop

# 切换远端分支
git checkout -t origin/dev
```


## 删除分支
```
# 删除本地分支
git branch -d <branchName>

# 删除远程分支
git branch -d -r origin/<branchName>
git push origin :<branchName>
```

## 重命名分支
```
# 重命名当前分支
git branch -m <branchName>
```


----


## 代码合并
```
# 两步法, 将 feature/v1.0.0 分支代码合并到 develop
git checkout develop
git merge feature/v1.0.0

# 或者一步法
git merge feature/v1.0.0 develop
```



## 暂存
```
# 暂存所有
git add -A

# 暂存某个文件
git add ./README.md

# 添加当前目录所有改动文件
git add .

# 暂存一系列文件
git add 1.txt 2.txt ...
```

## 删除
git add 的反向操作
```
# 删除1.txt 文件
git rm 1.txt
```

## 提交
```
# -m 提交的信息
git commit -m "changes log"

# 提交显示diff变化
git commit -v
```

## 推送
```
# 推送内容到主分支
git push -u origin master

# 本地分支推送到远程， 本地分支:远程分支
git push origin <branchName>:<branchName>

# 简写，默认推送当前分支
git push

# 强制推送, -f 是 --force 缩写
git push -f
```

----


## 拉取最新内容
```
# 推荐使用这个，因为不会做自动合并
git fetch origin master

# 相当于git fetch 然后 git merge
git pull

# 后面的意思是： 远程分支名:本地分支名
git pull origin master:master

# 如果是要与本地当前分支合并，则冒号后面的<本地分支名>可以不写
git pull origin master
```




----

## 查看文件的改动
```
# 查看所有文件改动
git diff

# 查看具体文件的改动
git diff README.md

# 查看某个版本的改动, 后面那一窜是commitId， git log后就能看到
git diff d68a1ef2407283516e8e4cb675b434505e39dc54

# 查看某个文件的历史修改记录
git log README.md
git show d68a1ef2407283516e8e4cb675b434505e39dc54 README.md
```


----

## 回滚版本
```
# 回滚上一个版本
git reset --hard HEAD^

# 回滚上两个版本
git reset --hard HEAD^^

# 回退到指定版本，git log 就能看到commit id了
git reset --hard 'commit id'

# 回滚版本是不保存在 git log，如果想查看使用
git reflog
```

----

## 撤销修改，比如修改了文件但是没有提交，又想撤回原来的状态
```
# 撤销当前目录下所有文件的改动
git checkout -- .

# 撤销指定文件修改
git checkout -- README.md
```


## 暂存区回到工作区
```
# 指定 ./README.md 文件从暂存区回到工作区
git reset HEAD ./README.md
```


## 其他
```
# 查看远程仓库地址
git remote -v
```


## 记住提交账号密码
```
# 会要求输入账号和密码， 下次提交就免账号密码
git config --global credential.helper store
```

## 清除git已保存的用户名和密码
```
# windows
git credential-manager uninstall
# mac linux
git config --global credential.helper store
```

## 清除本地git缓存
```
git rm -r --cached .
```

## 奇技淫巧
```
# 列表提交者贡献数量
git shortlog -sn
```
