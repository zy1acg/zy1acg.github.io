## git rebase 听着高级，也是最容易把人坑哭的命令之一

用错一次，能让整个团队的历史乱套。想清楚再决定是否使用rebase。

- 造一个分支：feature 上有提交 A、B，与此同时 master 自己往前走了一个提交。
- 在 feature 上执行 git rebase master，Git 把 A、B 摘下来、重新接到 master 最新提交后面，历史变成一条直线。
> [!warning]
>但最容易踩坑的是：代码一个字没改，A、B 的提交号却全变了（d419ee5→1b9d04e）。为什么？
> 接上期对象模型——commit 对象里记着 parent，rebase 把 parent 从旧 base 换成了 master 的新提交，parent 变 → commit 内容变 → 按内容算出全新 SHA。
> 所以 rebase 不是"搬动"提交，是照新 parent 重新打造一串提交。

> [!important]
> 内容没丢，旧提交也还在 reflog 里、reset 能回去。
> 但记住头号铁律：千万别 rebase 已经推到公共分支、别人正在用的提交——你造的是全新 SHA，别人手里还是旧的，历史一对就分裂。
> 一句话：本地没推的提交用 rebase 整理成直线，公共历史老老实实用 merge。