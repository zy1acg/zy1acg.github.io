## .gitignore 只是 Git 忽略文件的5种方式之一。

1. 最容易栽的坑——.gitignore 对已跟踪文件无效，要 git rm --cached；
2. git/info/exclude 本地私有忽略；
3. git update-index --skip-worktree 隐藏本地改动；
4. 子目录 .gitignore 与全局 core.excludesFile；
5. git check-ignore -v 一键排错。每条都能照着敲。

> [!note]
> 被跟踪的文件 .gitignore 管不住 → git rm --cached <文件> 再提交
> 私人临时文件 → 写进 .git/info/exclude（不提交、不影响同事）
> 本地配置改了不想提交 → git update-index --skip-worktree <文件>（git ls-files -v 看到大写 S 即生效）
> 全局垃圾如 .DS_Store → git config --global core.excludesFile ~/.gitignore_global
> 搞不懂谁忽略了某文件 → git check-ignore -v <文件>，输出"来源文件:行号:规则 路径"