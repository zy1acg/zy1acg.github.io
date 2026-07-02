## 版本控制方案

### 游戏存档式的快照

### 分支思想，并行开发

### Remote - 方便协作 减少中心化缺点影响，多地存有版本
#### 冲突解决
#### 断网
#### 数据安全性，完整性

## git配置和初始化

### 配置
```bash
git config --global user.name "yourname"
git config --global user.email "youremail" # email不用""括起来
git config --global core.editor vscode 
```
+ name 显示在commit元数据中，让别人认识你，协作情况下使用。
+ email 个人联系信息，与github无关。
+ editor 古法时代用，git提交的时候默认打开的编辑器。

### 查看配置
```bash
git config --list # 显示全局配置
git config --list -local # 显示具体git文件夹配置
```

### git配置文件层级
| 层级 | 作用范围 | 优先级 |
| --- | --- | --- |
| system | 整台电脑的所有用户 | 低 |
| global | 当前用户| 中 |
| local | 当前仓库 | 高 |
> 覆盖规则: local > global > system

+ windows
  + git system config path
    + C:\Program Files\Git\etc\gitconfig
  + git global config path
    + C:\Users\\<用户名>\\.gitconfig
  + git local config path
    + <项目地址>\\.git\config

## git的使用
+ 准备一个git仓库文件夹
```bash
git init # 仓库初始化

git add . # 将需要提交的文件移动到暂存区，准备提交
git status -sb # 查看仓库文件状态
git commit -m "first commit" # 提交版本，生成’快照’
git log # 查看提交信息
git log --oneline --graph # 每个版本提交信息只显示在一行 基于文本的分支图展示
```
+ git的配置文件层级

| 层级 | 作用范围 | 优先级 |
| --- | --- | --- |
| system(系统级) | 当前电脑的所有用户 | 低 |
| global(用户级) | 当前用户 | 中 |
| local(项目级)  | 当前项目 | 高 |
> 配置文件覆盖规则: local > global > system

+ 文件状态
  + untracked
  + unmodified
  + modified
  + staged

## branch

+ 理解版本提交，HEAD指针，HEAD指针移动概念

### 创建branch，切换分支
```bash

git branch [branchName] # 创建branchName分支

git checkout -b [branchName] # 创建branchName，并将HEAD指向新分支

git checkout [branchName] # 切换到branchName分支，HEAD指向branchName分支
```

### merge 合并
```bash
git checkout [合并目标分支] # 指针移动
git merge [拉取的分支（被合并）] # 注意是拉取的分支
```

> 合并的概念： 目标分支拉取被合并的分支

### 合并冲突

+ 建议避免进行fast forward merge

```bash
git merge --no-off [branchName]

git config --global merge.ff false

git reset --hard HEAD~1 # 回退HEAD指针，撤销回退
``` 

### git 常用命令
- 查看分支 git branch 
- 新建分支 git branch dev
- 切换分支 git checkout dev
- 新建并切换分支 git checkout -b testing
- 合并分支-提交测试 git merge dev
- 基于主分支创建新分支 git checkout feature/login
  - 主分支代码更新版本 
  - 合并feature/login 分支到主分支，发生冲突 git merge feature/login
  - 终止合并 git merge --abort
  - 在开发分支手动处理冲突
  - 再次合并到主分支完成上线
- 轻量标签 git tag v1.0.0
- 带备注正式标签（推荐）git tag -a v1.0.0 -m "正式版 v1.0.0 上线"
- 查看所有标签 git tag
- 查看标签详情 git show v1.0.0
- 推送单个标签到远程 git push origin v1.0.0
- 推送全部标签 git push origin --tags
- 查看远程标签 git ls-remote --tag origin
- 基于标签版本修复bug流程 git checkout -b hotfix/v1.0-fix v1.0.0
- 在开发过程中，需要紧急修复bug的处理过程
  - git stash
  - git stash list
  - git stash pop
- git alias 别名的使用 
  - 系统级别名设置 alias 命令
  - 快速查看状态 git config --global alias.s "status"
  - 简洁树形日志 git config --global alias.lg "log --oneline --graph --all"
  - 快速提交 git config --global alias.c "commit -m"
  - 查看已设置别名 git config --get-regexp alias
- 系统级别名设置 alias 命令
```bash 
vim ~/.bashrc

alias gitadd="git add"
alias gitstatus="git status"
alias gitcommit="git commit -m "
alias gitbranch="git branch"

source ~/.bashrc

alias | grep git
```
- 其他
   type gitadd