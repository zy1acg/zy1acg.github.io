## git stash 一存一弹就保住现场。现场保护者
正写着功能，工作区一堆没提交的改动，突然被叫去修紧急 bug——直接切分支 git 还拦着你。别把半成品乱塞一个提交，

- 第一步，git stash push -u 把改到一半的代码和没跟踪的新文件整包存起来，工作区瞬间干净；
- 第二步，安心修完紧急 bug 正常提交，现场没被半成品干扰；
- 第三步，git stash pop 把现场原样弹回，还和刚才的 hotfix 自动合并。
- 再加一段救命的：万一手滑 git stash drop 把 stash 删了，drop 会打印哈希、git fsck 也能把它列出来，git stash apply 那串哈希就原样救回。

> [!warning]
> 边界也说清：从没 stash、也没 commit、还在工作区的改动，被冲掉就真没了——不夸大成"什么都能救"。