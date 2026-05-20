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
    + C:\Users\<用户名>\.gitconfig
  + git local config path
    + <项目地址>\.git\config

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
## git的配置文件层级

| 层级 | 作用范围 | 优先级 |
| --- | --- | --- |
| system(系统级) | 当前电脑的所有用户 | 低 |
| global(用户级) | 当前用户 | 中 |
| local(项目级)  | 当前项目 | 高 |
> 配置文件覆盖规则: local > global > system

## git文件状态
  + untracked
  + unmodified
  + modified
  + staged
