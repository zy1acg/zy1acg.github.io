## git 敏感信息不小心提交了，如何抹除

commit 过的密钥已经永久写进历史，任何人 clone 后 git show 旧提交就能翻出来。
把含密钥的 .env 提交进 Git 了，很多人第一反应是 git rm 删掉再提交——没用。

- 第一步，复现误提交：把含密钥的 .env 提交，再正常写两次功能；
- 第二步，演示错误删法：git rm + commit 后，工作区干净了，但 git show 旧提交密钥原样还在；
- 第三步，git filter-branch 重写每个提交、把 .env 从所有历史抹除，再清备份引用+reflog+gc；验证全历史搜不到 .env、代码没丢。
- 工具说明：官方现在推荐 git filter-repo（需 pip 安装），本机演示用内置的 git filter-branch（开箱即用、官方标记有坑但抹单文件够用）。

> [!warning]
> 边界讲清：只要 push 过，远端和别人的 clone 里都还有——一定先去吊销/轮换密钥，再清历史；清历史是善后，不是挽回泄露。