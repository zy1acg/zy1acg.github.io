## git reset 手滑了怎么办

"git reset --hard HEAD~2"——手一滑，辛苦写的两次提交从 git log 里消失，工作区文件也回退了。别急着重写，commit 过的东西几乎不会真丢。

- 第一步，连提交 A/B/C 三次，再 reset --hard HEAD~2 复现这次手滑，git log 里只剩 A；
- 第二步，reset 删掉的只是分支指针、提交对象还躺在仓库里，用 git reflog 列出 HEAD 走过的每一步，找到丢失前那条 C 的哈希；
- 第三步，git reset --hard 对着那串哈希，A/B/C 和文件就逐字全部回来了。

> [!warning]
> 边界也说清：从没 commit 过、还在工作区的改动，被 reset --hard 冲掉就真没了——不夸大成"什么都能救"。