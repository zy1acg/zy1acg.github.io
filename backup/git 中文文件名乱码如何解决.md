## git 中文文件名乱码如何解决

中文乱码只是"显示"被转义了。

一行救命配置：git config --global core.quotepath false，再 git status，中文就正常显示了。

- 为什么默认会这样？那串 \NNN 是字节的八进制写法。
- git 默认（core.quotepath=true）把文件名里非 ASCII 的字节，每个都转义成 \八进制 打印，图的是在各种老终端"安全显示"。
- 而文件名本身存的就是合法 UTF-8 字节——用 xxd 看 "项目说明.txt"，项=e9a1b9、目=e79bae……一个中文 3 字节。
- 验证那串数字：\344\270\255 换成十六进制 = E4 B8 AD，正是 UTF-8 的"中"。

> [!warning]
> 说清边界：core.quotepath=false 改的是显示、不是修文件（文件本来就没坏）；前提是终端为 UTF-8（现在基本都是），老 GBK 终端是另一码事。
