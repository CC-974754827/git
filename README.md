# git

### 获取帮助
```
$ git help <verb>
$ git <verb> --help
$ man git-<verb>
```

## 获取 Git 仓库
### 在现有目录中初始化仓库
```
$ git init
该命令将创建一个名为 .git 的子目录，这个子目录含有初始化的 Git 仓库中所有的必须文件，这些文件是 Git 仓库的骨干。 
但在这个时候，仅仅是做了一个初始化的操作，项目里的文件还没有被跟踪。
```
### git add 实现对指定文件的跟踪; git commit 提交
```
$ git add .
$ git add *.c
$ git add LICENSE
$ git commit -m 'initial project version'
```
### 克隆现有的仓库
```
$ git clone https://
```

## 记录每次更新到仓库
```
工作目录下的每一个文件都不外乎这两种状态：已跟踪或未跟踪。 
已跟踪的文件是指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后，它们的状态可能处于未修改，已修改或已放入暂存区。 
工作目录中除已跟踪文件以外的所有其它文件都属于未跟踪文件，它们既不存在于上次快照的记录中，也没有放入暂存区。 
初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪文件，并处于未修改状态。
```
### 检查当前文件状态
```
$ git status
查看所有已跟踪文件在上次提交后是否被更改过

状态简览  将得到一种更为紧凑的格式输出
git status -s 或 git status --short   
新添加的未跟踪文件前面有 ?? 标记
新添加到暂存区中的文件前面有 A 标记
修改过的文件前面有 M 标记
```
### 忽略文件
```
$ cat .gitignore
$ *.[oa] //忽略所有以 .o 或 .a 结尾的文件
$ *~ //忽略所有以波浪符（~）结尾的文件
```
```
文件 .gitignore 的格式规范如下：
所有空行或者以 ＃ 开头的行都会被 Git 忽略。
可以使用标准的 glob 模式匹配。
匹配模式可以以（/）开头防止递归。
匹配模式可以以（/）结尾指定目录。
要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。
```
### 查看已暂存和未暂存的修改
```
查看尚未暂存的文件更新了哪些部分
$ git diff
查看已暂存的将要添加到下次提交里的内容
$ git diff --cached
$ git diff --staged //高版本
```
### 移除文件
```
$ git rm 文件
$ git rm \*~ //该命令为删除以 ~ 结尾的所有文件。
```
### 移动文件(重命名)
```
$ git mv 文件
```
## 查看提交历史
```
默认不用任何参数的话，git log 会按提交时间列出所有的更新，最近的更新排在最上面。
$ git log 
$ git log -p -2 // -p，用来显示每次提交的内容差异。 -2 来仅显示最近两次提交
$ git log --stat//每次提交的简略的统计信息
$ git log --since=2.weeks //列出所有最近两周内的提交
```
## 撤消操作
```
$ git commit --amend
```
eg

```
最终只会有一个提交, 第二次提交将代替第一次提交的结果
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```
### 取消暂存的文件
```
$ git reset HEAD 文件
```
### 撤消对文件的修改
```
$ git checkout -- 文件
```
## 远程仓库的使用
### 查看远程仓库
```
$ git remote
$ git remote -v //显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL
$ git remote show [remote-name]
```
### 添加远程仓库
```
$ git remote add <shortname> <url>  //添加一个新的远程 Git 仓库，同时指定一个你可以轻松引用的简写
$ git fetch pb //想拉取 Paul 的仓库中有但你没有的信息
```
### 从远程仓库中抓取与拉取
```
$ git fetch [remote-name] //抓取
$ git pull origin master //拉取
```
### 推送到远程仓库
```
$ git push origin master
```
### 远程仓库的移除与重命名
```
$ git remote rename pb paul //重命名
$ git remote rm paul //移除
```
## 打标签
### 列出标签
```
$ git tag
```
### 创建标签 附注标签
```
两种主要类型的标签：轻量标签（lightweight）与附注标签（annotated）
$ git tag -a v1.4 -m 'my version 1.4' // -a 创建标签  -m 指定了一条将会存储在标签中的信息
```
### 轻量标签
```
$ git tag v1.4-lw
```
### 共享标签
```
$ git push origin v1.5
$ git push origin --tags //会把所有不在远程仓库服务器上的标签全部传送到那里
```
### 删除标签
```
$ git tag -d v1.4-lw
```
### 检出标签
```
$ git checkout 2.0.0
```
## Git 别名
```
$ git config --global alias.ci commit // 意味着，当要输入 git commit 时，只需要输入 git ci
```
```
$ git last //看到最后一次提交
```
## 分支
### 分支创建
```
$ git branch testing //创建一个 testing 分支
```
### 分支切换
```
$ git checkout testing
```
新建分支并同时切换到该分支上
```
$ git checkout -b iss53
```
删除分支
```
$ git branch -d hotfix
```
### 合并merge
```
$ git merge hotfix
```
## 分支管理
```
$ git branch -v  //查看每一个分支的最后一次提交
$ git branch --merged //查看哪些分支已经合并到当前分支
$ git branch --no-merged //查看所有包含未合并工作的分支
```
