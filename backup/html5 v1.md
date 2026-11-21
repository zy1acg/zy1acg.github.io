# HTML/HTML5 常用标签：最佳实践与使用注意点。

> **来源**：[HTML/HTML5 常用标签和属性 最佳实践 · arry 老师的博客（艾编程）](https://www.arryblog.com/guide/html5/html-html5-course.html)
> **整理日期**：2026-11-14
> **覆盖范围**：原页 10 个章节 —— 标题、段落、div、HTML5 特性、列表、多媒体、语义化、表单、冷门实用标签、表格
> **体例说明**：本文是要点提炼，按「标签 → 最佳实践 → 注意点 → 示例」重新组织；最后一节为前端工程实践补充，已单独标注，**非原文内容**。

---

## 一、全局原则：贯穿全文的 6 条主线

| # | 原则 | 具体落地 | 主要涉及标签 |
|---|---|---|---|
| 1 | **语义优先** | 有语义标签就别用 `div`；`div` 只在「纯容器、无合适语义」时使用 | `div` / `header` / `nav` / `main` / `article` / `section` / `aside` / `footer` |
| 2 | **结构不跳级** | 每页 1 个 `h1`，有 `h3` 必有 `h1`、`h2`；列表必须是父子组合 | `h1~h6` / `ul·ol·li` / `dl·dt·dd` |
| 3 | **表现交给 CSS** | HTML5 已废弃的表现属性一律改用 CSS | `ul[type]`、`table[width/cellpadding/cellspacing]`、`iframe[frameborder/scrolling]`、`b/i/u` |
| 4 | **无障碍是必填项** | `alt`、`label`、`title`、降级文本、屏幕阅读器描述都要写 | `img` / `label` / `a` / `iframe` / `audio` / `video` |
| 5 | **安全写进默认值** | 新窗口必配 `rel`；第三方嵌入必配 `sandbox` 与 HTTPS | `a[target=_blank]` / `iframe` |
| 6 | **性能与稳定性** | 明确尺寸防布局抖动、懒加载、避免深层嵌套 | `img` / `iframe` / `div` |

---

## 二、逐标签详解

### 2.1 标题标签 `h1` ~ `h6`

| 标签 | 语义 | 要点 |
|---|---|---|
| `h1` | 一级标题 | 相当于文章主题，对搜索引擎最重要；**一个页面只能有 1 个**，多了会被视为作弊 |
| `h2` | 二级标题 | 标注分类 / 列表名称，可适当放长尾关键词 |
| `h3` | 三级标题 | 标注内容页标题链接 / 相关文章；层级不可跳级 |
| `h4`~`h6` | 四~六级标题 | 数量不限，按层级递进 |

**SEO 分页面类型设置（原文推荐）**

| 页面类型 | `h1` | `h2` | `h3` |
|---|---|---|---|
| 首页 | 网站 logo（强调 `alt`，`alt` 含首页标题与核心关键词） | 分类页面 | 内容页标题链接 |
| 列表页 / 栏目页 | 分类名称 | 子分类名称 | 内容页标题链接 |
| 内容页 / 详情页 | 文章标题 | 列表名称 | 相关文章 |

- `h1` 中**必须包含核心关键词**；`h2`、`h3` 可适当含长尾关键词。
- 参考标杆：百度百科、京东首页（logo 用 `h1`）、小米首页栏目（用 `h2`）。

```html
<h1>前端开发</h1>
<h2>核心技术</h2>
<h3>HTML 语义化</h3>
```

---

### 2.2 段落标签 `p` / `br`

| 项 | 说明 |
|---|---|
| 语义 | `p` = `Paragraph`，任何段落都应放进 `p` 中 |
| 为什么必须用 | HTML 源码里换行，页面**不会**跟着换行；只有 `p` 才会形成段落 |
| 可嵌套 | 行内元素（`a`、`span`、`strong`、`em`、`img` 等） |
| 禁止嵌套 | `h` 系列、其他 `p`、以及任何块级元素（浏览器会自动闭合 `p`，导致 DOM 结构与预期不符） |

**最佳实践（原文）**：不要用 `<br>` 模拟段落间距；避免在 `<p>` 中嵌套块级元素。

```html
<!-- 正确 -->
<p>这是第一段，包含 <a href="#">链接</a> 与 <strong>重点</strong>。</p>
<p>这是第二段。</p>

<!-- 错误：p 内嵌块级元素 -->
<p>说明文字<div>块内容</div></p>
```

---

### 2.3 容器标签 `div`

`div` = `division`（分隔），无语义、什么都能装，俗称「盒子」，是 `DIV + CSS` 布局的基础。

**8 类典型场景**

| 场景 | 说明 |
|---|---|
| 布局容器 | 页眉 / 主体 / 侧边栏 / 页脚划分；配合 Flex、Grid 做响应式 |
| 样式与视觉 | 加背景、边框、内边距；把相关元素分组统一样式 |
| JavaScript 操作 | 作为 DOM 查询目标、动态内容渲染（AJAX 结果）的挂载点 |
| 表单分组 | `.form-group` 包裹 `label + input` |
| 多媒体包装 | 包裹 `video`、地图等需额外样式/脚本的内容 |
| 组件化开发 | React / Vue 组件的根元素 |
| 条件渲染 / 隐藏 | 用 CSS 或 JS 控制 `display` |
| 模板与占位符 | 加载前的骨架 / loading 占位 |

**最佳实践（原文 3 条）**

1. **避免过度使用** —— 优先 `section`、`article` 等语义化标签，仅在必要时用 `div`。
2. **合理命名** —— 用有意义的 `class` / `id`，便于维护与样式控制。
3. **性能优化** —— 避免嵌套过深，减少 DOM 操作开销。

---

### 2.4 HTML5 基础特性

**① 空白折叠现象（写 HTML 时最容易误解的规则）**

- 文字之间的多个空格、换行会被**折叠成一个空格**。
- 标签「内壁」与文字之间的空格会被忽略。
- 需要真实空格用 `&nbsp;`（半角）、`&emsp;`（全角，1 个中文字宽）；需要保留原始换行与空格用 `<pre>`。

**② 常用转义符**

| 显示 | 描述 | 实体名称 | 实体编号 |
|---|---|---|---|
| 空格 | 不换行空格 | `&nbsp;` | `&#160;` |
| 全角空格 | 1 个中文字宽 | `&emsp;` | — |
| `<` | 小于号 | `&lt;` | `&#60;` |
| `>` | 大于号 | `&gt;` | `&#62;` |
| `&` | 和号 | `&amp;` | `&#38;` |
| `"` | 双引号 | `&quot;` | `&#34;` |
| `'` | 撇号 | `&apos;` | `&#39;` |
| `¥` / `€` | 人民币 / 欧元 | `&yen;` / `&euro;` | `&#165;` / `&#8364;` |
| `©` / `®` / `™` | 版权 / 注册商标 / 商标符号 | `&copy;` / `&reg;` / `&trade;` | `&#169;` / `&#174;` / `&#8482;` |

> 原文提示：`™` **无强制法律要求**，任何企业或个人均可使用，表示「正在作为商标使用」，但未完成法律注册流程。

**③ 注释**

```html
<!-- 注释内容 -->
```

- 作用：提高可读性与可维护性；网页中不显示，仅源码可见。
- VS Code 快捷键：`Ctrl + /`。

---

### 2.5 列表标签 `ul` / `ol` / `dl`

| 标签 | 语义 | 全称 |
|---|---|---|
| `ul` + `li` | 无序列表（顺序不重要） | unordered list / list item |
| `ol` + `li` | 有序列表（顺序重要） | ordered list |
| `dl` + `dt` + `dd` | 定义列表 | definition list / data term / data definition |

**硬性规则（原文反复强调）**

- `ul`/`ol` 与 `li` 是**父子组合标签，不能单独出现**；`ul`/`ol` 的**子元素只能是 `li`**。
- `li` 内可以放**任意标签**（包括嵌套新列表），书写时 `li` 需缩进一个 Tab。
- 避免列表嵌套过深。
- 开发高频场景：导航栏、各种 list 列表页。

**属性对照**

| 标签 | 属性 | 取值 / 规则 | 状态 |
|---|---|---|---|
| `ul` | `type` | `disc` 实心圆（默认）/ `square` 实心方块 / `circle` 空心圆 | **HTML5 已废弃**，改用 CSS `list-style-type` |
| `ol` | `type` | `1`（默认）/ `A` / `a` / `I` / `i` | 可用 |
| `ol` | `start` | 必须整数、且为阿拉伯数字（即使 `type` 是字母也写数字） | 可用 |
| `ol` | `reversed` | HTML5 新增**布尔属性**，无需值，写单词即可 | 可用 |

```html
<!-- 用 CSS 代替废弃的 ul[type] -->
<ul style="list-style-type: square">
  <li>小炒肉</li>
</ul>

<ol type="A" start="3" reversed>
  <li>JavaScript</li>
  <li>Python</li>
</ol>
```

**定义列表注意点**

- `dd` 是对 `dt` 的解释说明；内容交替出现，**一个 `dt` 可对应多个 `dd`**。
- 也允许 `dt`/`dd` 不交替，而是拆到**多个 `dl`** 中，更方便 CSS 控制样式（小米官网首页底部即此类结构）。
- `dl` 用于「术语 + 定义」，**避免用于简单键值对**。

**最佳实践汇总表（原文）**

| 标签 | 适用场景 | 最佳实践 | 注意事项 |
|---|---|---|---|
| `ul` | 顺序不重要 | 菜单、导航链接 | 避免嵌套过深 |
| `ol` | 顺序重要 | 步骤说明、排名 | 合理使用编号类型 |
| `li` | `ul`/`ol` 的子元素 | 购物车商品、步骤项 | 不能单独使用 |
| `dl` | 术语和定义 | 术语解释、产品规格 | 避免用于简单键值对 |
| `dt` | 定义术语 | 技术术语、名称 | 内容应简洁 |
| `dd` | 定义描述 | 术语解释、详细说明 | 一个 `dt` 可对应多个 `dd` |

---

### 2.6 多媒体与链接

#### 2.6.1 `img`

| 属性 | 说明 |
|---|---|
| `src` | `source`，图片存储目录 + 完整文件名；图片**必须放在项目文件夹内**（如 `images/`） |
| `alt` | `alternate`，图像文本描述（不强制，但强烈建议） |
| `width` / `height` | 单位 px，可不写；**省略其中一个则按原始比例缩放** |

**图片标签规范（原文硬性要求）**

- **PC 端**：必须填写 `src`、`width`、`height`、`alt`，合称「**图片四要素**」。
- **移动端**：必须填写 `alt`。
- `alt` **不能是无意义字符**，要能表达图片含义（如道具图就写道具名称）。

**`alt` 的三个作用**：① 图片加载失败时显示备用文本；② 供网页朗读器朗读，服务视障用户；③ 告诉搜索引擎图片含义，利于爬虫抓取与 SEO。

> 原文强调：图片只是被「引入」网页，本质上并没有被插入到页面中。

**网页支持的图片格式**

| 格式 | 描述 |
|---|---|
| `.bmp` | Windows 画图默认格式，位图 |
| `.jpeg/.jpg` | 有损压缩，通常用于照片 |
| `.png` | 便携式网络图像，用于 logo、背景图形，支持透明/半透明 |
| `.gif` | 动画，如表情包 |
| `.svg` | 矢量图 |
| `.webp` | 最新压缩算法，非常优秀的图片格式 |

**路径**

| 类型 | 写法 | 说明 |
|---|---|---|
| 相对路径 | `images/logo.png`、`../images/logo.png`、`../../images/logo.png` | 从当前网页出发找图片；`../` 回退上一级，`./` 当前目录 |
| 绝对路径 | `D:\web\...\logo.png`、`https://example.com/xxx.png` | 文件或文件夹的完整精准地址 |

#### 2.6.2 `a`

`a` = `anchor`（锚）；`href` = `hypertext reference`（超文本引用）。

| 属性 / 用法 | 说明 |
|---|---|
| `href` | 支持相对路径与绝对路径 |
| `title` | 鼠标悬停提示文本 |
| `target="_blank"` | 新窗口打开；`_self` 为默认（当前页跳转） |
| 页面锚点 | 给目标标签加 `id`，链接写 `href="#id"`，地址栏出现 `#id` 并自动滚动；跨页面带 `#` 也能定位 |
| 回到顶部 | HTML5 直接写 `href="#top"`，**无需定义 `id="top"`** |
| 包裹块级元素 | HTML5 允许 `<a>` 包裹 `div`/`h2`/`p` 等，实现「整块可点击」 |

**特殊链接**

| 类型 | 写法 | 注意点 |
|---|---|---|
| 普通下载 | `<a href="doc/1.zip">` | 指向 exe/zip/rar/word/excel 等自动成为下载链接 |
| 强制下载 | `<a href="./a.pdf" download="笔记.pdf">` | PDF、图片默认会在标签页预览；`download` 改为下载，**可自定义文件名且需带扩展名**，部分浏览器出于安全策略可能忽略自定义名 |
| 邮件 | `<a href="mailto:xxx@example.com">` | 自动打开系统邮件客户端 |
| 电话 | `<a href="tel:18966666666">` | 自动打开手机拨号键盘 |

**`rel` 属性取值（原文表）**

| 值 | 用途 |
|---|---|
| `nofollow` | 不跟踪、不传递权重，常用于用户生成内容或广告链接 |
| `noopener` | 阻止新页面通过 `window.opener` 访问原页面 `window`，防钓鱼/篡改 |
| `noreferrer` | 类似 `noopener`，额外阻止发送 `Referer` 头，保护隐私 |
| `external` | 非标准但广泛使用，仅标记外链，无技术效果 |
| `ugc` | 标记用户生成内容（评论、论坛帖），建议降低权重传递 |
| `sponsored` | 标记赞助 / 付费链接，帮助搜索引擎识别广告 |

> `rel` 值大小写不敏感；`ugc`、`sponsored` 较新，主流搜索引擎（如 Google）已支持，部分小工具可能未完全支持。

**`a` 标签最佳实践（原文）**

1. **安全性**：使用 `target="_blank"` 时**务必加 `rel="noopener noreferrer"`**，防止 `window.opener` 攻击。
2. **SEO**：合理使用 `nofollow`、`ugc`、`sponsored`，避免把权重传给不希望优化的链接。
3. **实践参考**：可右键检查大厂网站（搜索 `rel`）、Vue 官网。

```html
<a href="https://example.com" target="_blank" rel="noopener noreferrer">安全外链</a>
<a href="./report.pdf" download="年度报告.pdf">下载 PDF</a>
<a href="#top">回到顶部</a>
```

#### 2.6.3 `audio` / `video` / `source`

- HTML5 已取代早年插入音视频所需的 Flash 技术。
- 常用属性：`controls`（显示播放控件）、`src`、`autoplay`（不等待下载完成即播）、`loop`（循环）。
- **标签对内的文字是降级内容**：浏览器不支持该标签时显示。
- `<source>` 允许定义**多个格式**，浏览器选择自己支持的播放；**都支持时默认取第一个**，因此要把最优格式放前面。

| 媒体 | 格式 | MIME-type |
|---|---|---|
| 音频 | MP3 / Ogg / Wav | `audio/mpeg` / `audio/ogg` / `audio/wav` |
| 视频 | mp4 / webm / avi / ogv | `video/mp4` / `video/webm` / `video/avi` / `video/ogv` |

```html
<video controls width="500">
  <source src="video/1.mp4" type="video/mp4" />
  <source src="video/1.webm" type="video/webm" />
  您的浏览器不支持 video 标签，请升级浏览器。
</video>
```

#### 2.6.4 `iframe`

在当前页嵌入另一个 HTML 文档（第三方内容、广告、视频、地图），主流浏览器都支持，但**不当使用会带来性能、安全与体验问题**。

| 属性 | 说明 | 状态 |
|---|---|---|
| `src` | 嵌入页面 URL，相对/绝对均可 | 必填 |
| `width` / `height` | 像素或百分比 | 建议显式设置 |
| `title` | 为屏幕阅读器提供描述性文本 | **无障碍必填** |
| `sandbox` | 额外限制（如 `allow-same-origin`、`allow-scripts`） | 安全关键 |
| `allow` | 控制内嵌页功能（`camera`、`microphone`） | 安全关键 |
| `loading` | `lazy` 延迟加载（默认立即） | 性能关键 |
| `name` | 框架名称，供 JS 定位 | 可用 |
| `referrerpolicy` | 控制请求时 `Referer` 头 | 隐私 |
| `frameborder` | 是否显示边框 | **HTML5 不推荐 → 用 CSS** |
| `scrolling` | 是否显示滚动条 | **HTML5 不推荐 → 用 CSS** |

- `referrerpolicy="no-referrer-when-downgrade"`：HTTPS→HTTP 降级时不发 `Referer`，其余情况发送；多数场景是浏览器默认行为，通常无需显式指定。
- 嵌入广告 / 第三方内容：**严格限制 `sandbox` 权限**，并**避免 `allow-popups`** 防弹窗广告。

**iframe 最佳实践（原文表）**

| 维度 | 做法 | 原因 |
|---|---|---|
| 安全 | 设置 `sandbox`、指定 `allow` | 防止恶意代码攻击 |
| 安全 | 避免混合内容，`src` 用 `https://` | 防止被拦截 / 中间人风险 |
| 性能 | `loading="lazy"` | 减少首屏加载时间 |
| 性能 | 明确 `width` / `height` | 避免布局抖动（CLS） |
| 性能 | 减少嵌套层级 | 防止性能下降 |
| 可访问性 | 添加 `title` | 屏幕阅读器可读 |
| 可访问性 | 避免关键内容依赖 iframe | 重要内容应直接放主页面 |
| 体验 | 提供备用内容 / 链接 | iframe 加载失败时有兜底 |
| 体验 | 避免自动播放（尤其音频） | 减少干扰 |
| SEO | 避免滥用 iframe | 搜索引擎通常无法索引 iframe 内内容 |

```html
<iframe src="https://example.com/embed" width="800" height="600"
        title="视频播放器" loading="lazy"
        sandbox="allow-scripts allow-same-origin"
        referrerpolicy="no-referrer-when-downgrade"></iframe>
```

---

### 2.7 语义化标签

**为什么要语义化（原文 6 条）**：① 无 CSS 时也有良好内容结构；② 提升用户体验（`title`、`alt`、`label`）；③ 利于 SEO，爬虫靠标签判断上下文与关键词权重；④ 可访问性，帮助屏幕阅读器；⑤ 国际化，遵循 W3C 通用标准便于各国开发者理解；⑥ 可维护性，减少页面间差异。

**文本格式化标签**

| 标签 | 功能 | 语义 / 用途 | 状态 |
|---|---|---|---|
| `span` | 行内区块，无默认样式 | 需特殊标记的文本，配合 CSS 定位样式 | 推荐 |
| `strong` | 加重语气（粗体） | 重要、紧迫的内容 | 推荐 |
| `em` | 强调（斜体） | 语气/情感强调 | 推荐 |
| `mark` | 高亮 | 需用户特别注意的文本 | 推荐 |
| `del` / `ins` | 删除线 / 下划线 | 已删除、不再准确的内容 / 新增或修改的内容 | 推荐（如原价 / 现价） |
| `small` | 小号字 | 版权、免责声明等次要文本 | 可用 |
| `sup` / `sub` | 上标 / 下标 | 公式、脚注、化学式 | 可用 |
| `pre` | 预格式化文本 | **保留空格和换行**、等宽字体，常用于展示源代码 | 可用 |
| `code` / `kbd` / `samp` / `var` | 代码片段 / 键盘输入 / 程序输出 / 变量 | 技术文档语义 | 可用 |
| `abbr` | 缩写词 | 用 `title` 提供全称 | 可用 |
| `q` / `blockquote` / `cite` / `dfn` | 短引用 / 长引用 / 作品标题 / 术语定义 | 引用与定义语义 | 可用 |
| `figure` / `figcaption` | 独立流内容 / 其标题 | 图像、图表、照片、代码块的独立单元 | 推荐 |
| `time` | 日期时间 | 用 `datetime` 提供机器可读格式 | 推荐 |
| `b` / `i` | 纯视觉加粗 / 斜体，**无语义** | — | **已被 CSS 替代** |
| `u` | 下划线（非强调用途） | — | **已被 CSS 替代，不推荐用于强调** |

**HTML5 区块标签**

| 标签 | 描述 | 应用场景 | 注意点 / 最佳实践 |
|---|---|---|---|
| `header` | 页头 | 页眉或区块头部 | 页面顶部导航栏、文章标题区 |
| `nav` | 导航条 | 导航链接集合 | 主导航、面包屑、页脚快速链接 |
| `main` | 网页核心部分 | 文档主要内容 | **每个页面只能有一个**，且不应包含侧边栏、页眉页脚等重复内容 |
| `article` | 独立、可分发的完整内容 | 博客文章、新闻、帖子、评论 | 会被搜索引擎主要抓取 |
| `section` | 文档区域，语义比 `div` 大 | 主题分区 | 内容需要单独标题时使用，通常内含 `h1`~`h6` |
| `aside` | 非必要但相关内容 | 侧边栏、引文、广告 | 应与主要内容相关且可独立 |
| `footer` | 页脚 | 页脚或区块底部 | 版权、作者、联系信息 |

---

### 2.8 表单元素

**基础**：所有表单都由 `<form>` 包裹；`action` 指定提交地址，`method` 指定 HTTP 方法。

```html
<form action="/user/login" method="post"> ... </form>
```

| 控件 | 关键写法 | 注意点 |
|---|---|---|
| 单行文本框 | `<input type="text">` | `value` 是真实值；`placeholder` 只是浅灰提示文本、**不是值**；`disabled` 禁用交互 |
| 密码框 | `type="password"` | 内容隐藏显示 |
| 单选按钮 | `type="radio"` | **同组 `name` 必须相同才互斥**；`value` 是提交值；`checked` 默认选中 |
| 复选框 | `type="checkbox"` | 同组 `name` 设相同值；`checked` 默认选中 |
| 下拉菜单 | `<select>` + `<option>` | `option` 的 `value` 是提交值 |
| 分组下拉 | `<optgroup label="...">` | **第一项通常是提示项，设为 `disabled selected`**；用 `optgroup` 分组 |
| 多行文本框 | `<textarea rows cols>` | `rows` / `cols` 定义行列数 |
| 按钮 | `type="button"` / `submit` / `reset` | 普通按钮也可简写为 `<button></button>` |
| 表单分组 | `<fieldset>` + `<legend>` | `legend` 提供分组标题 |

**`label` 两种绑定方式（重要）**

```html
<!-- HTML5 推荐：直接包裹，点文字即选中 -->
<label><input type="radio" name="sex" checked /> 保密</label>

<!-- HTML4 写法：for 对应 input 的 id -->
<input type="radio" name="city" id="beijing" />
<label for="beijing">北京市</label>
```

> 原文的坑：只写 `<input type="radio">男` 时，**点击文字无法选中按钮**，必须用 `label` 绑定。

**下拉分组最佳实践示例（原文）**

```html
<label for="country">国家：</label>
<select id="country" name="country" required>
  <option value="" disabled selected>请选择国家</option>
  <optgroup label="亚洲">
    <option value="CN">中国</option>
  </optgroup>
</select>
```

**HTML5 新增 `input[type]`**

| type | 控件 | type | 控件 |
|---|---|---|---|
| `color` | 颜色选择 | `number` | 数字输入 |
| `date` / `time` | 日期 / 时间 | `range` | 拖拽条 |
| `email` | 电子邮件 | `search` | 搜索框 |
| `file` | 文件选择 | `url` | 网址 |

> 原文表述：兼容到 IE9、手机端完全兼容（属教程写作时的兼容性结论，实际项目请以当前目标浏览器为准）。

**`datalist`**：为输入框提供备选项，用户输入内容与选项匹配时显示智能提示；用 `input[list]` 关联 `datalist[id]`。

```html
<input type="text" list="language-list" />
<datalist id="language-list">
  <option value="JavaScript">JavaScript</option>
  <option value="Python">Python</option>
</datalist>
```

---

### 2.9 冷门但实用的 HTML5 标签

| 标签 | 作用 | 注意点 |
|---|---|---|
| `details` + `summary` | 无需 JS 创建可折叠内容区块 | 常用于 FAQ；`open` 属性可默认展开 |
| `progress` | **未知总量**的进度（如下载） | 用 `value` / `max`；标签内文字作降级 |
| `meter` | **已知总量**的度量（如磁盘使用） | 与 `progress` 的语义区别是关键 |
| `output` | 显示计算或用户操作结果 | 常与表单 `oninput` 结合 |
| `ruby` / `rt` / `rp` / `rb` | 东亚字符注音 | `ruby` 包裹、`rt` 注音、`rp` 为不支持浏览器提供括号备用、`rb` 明确包裹基础文本（可选，提升可读性） |

```html
<details open>
  <summary>点击查看详情</summary>
  <p>这里是折叠的内容。</p>
</details>

<progress id="file" value="70" max="100">70%</progress>
<meter id="disk" value="0.6">60%</meter>

<ruby>汉<rp>(</rp><rt>Hàn</rt><rp>)</rp>字<rp>(</rp><rt>zì</rt><rp>)</rp></ruby>
```

> 支持 `ruby` 的浏览器显示「汉 Hàn 字 zì」；不支持时靠 `rp` 显示「汉(Hàn)字(zì)」。

---

### 2.10 表格标签

| 标签 | 描述 |
|---|---|
| `table` | 定义表格 |
| `caption` | 表格标题，**必须作为 `table` 的第一个子元素** |
| `thead` / `tbody` / `tfoot` | 页眉 / 主体 / 页脚 |
| `tr` | 表格行 |
| `th` | 表头单元格 |
| `td` | 普通单元格 |

**属性状态（原文明确标注）**

| 属性 | 状态 |
|---|---|
| `width`、`cellpadding`、`cellspacing` | **HTML5 不支持 → 用 CSS** |
| `border` | 大部分表现属性在 HTML5 已废弃，统一交 CSS |
| `td` 的其他表现属性 | HTML5 已不支持，直接用 CSS |
| `colspan`（跨列）、`rowspan`（跨行） | **仍可用**，值为数字 |

> 原文结论：HTML5 中 `table` 标签的大部分属性已经废弃，全部用 CSS 代替。

```html
<table>
  <caption>同学通讯录</caption>
  <thead>
    <tr><th>姓名</th><th colspan="2">联系方式</th></tr>
  </thead>
  <tbody>
    <tr><td>张三</td><td>电话</td><td>邮箱</td></tr>
  </tbody>
</table>
```

---

## 三、「已废弃 / 不推荐」写法速查

| 写法 | 判定 | 正确替代 |
|---|---|---|
| `<ul type="square">` | HTML5 废弃 | `style="list-style-type: square"` / CSS |
| `table` 的 `width` `cellpadding` `cellspacing` `border` | HTML5 废弃 | CSS |
| `td` 的表现属性 | HTML5 不支持 | CSS（仅保留 `colspan`/`rowspan`） |
| `iframe` 的 `frameborder` `scrolling` | HTML5 不推荐 | CSS `border`、`overflow` |
| `<b>` `<i>` 表达「重要 / 强调」 | 无语义 | `<strong>` `<em>`；纯视觉用 CSS |
| `<u>` 用于强调 | 不推荐 | CSS 或语义标签 |
| `<br>` 模拟段落间距 | 反模式 | 多个 `<p>` + CSS `margin` |
| `<p>` 内嵌块级元素 / 嵌套 `<p>` | 非法结构 | 拆成同级块元素 |
| 一个页面多个 `h1` | SEO 视为作弊 | 只保留 1 个 `h1` |
| 标题层级跳级（无 `h1`/`h2` 直接 `h3`） | 结构不规范 | 逐级递进 |
| `<a target="_blank">` 无 `rel` | 安全漏洞 | `rel="noopener noreferrer"` |
| 裸写 `iframe` 无 `sandbox`/`title` | 安全 + 无障碍缺陷 | 补 `sandbox`、`title`、HTTPS |
| 深层嵌套 `div` | 性能 / 可维护性差 | 语义标签 + 扁平结构 |
| `dl` 用于简单键值对 | 语义不匹配 | 用普通列表 / 表格 |
| `li` 单独使用、`ul` 直接放非 `li` 子元素 | 非法结构 | 严格遵守父子组合 |

---

## 四、可直接套用的语义化骨架

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>页面标题</title>
</head>
<body>
  <header>
    <h1>站点 / 文章主标题</h1>
    <nav aria-label="主导航">
      <ul>
        <li><a href="./index.html">首页</a></li>
        <li><a href="./about.html">关于</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h2>文章标题</h2>
      <section>
        <h3>小节标题</h3>
        <p>段落内容，包含 <strong>重点</strong> 与 <a href="#ref">锚点链接</a>。</p>
        <figure>
          <img src="images/demo.webp" alt="智能家居门锁示意图"
               width="600" height="400" />
          <figcaption>图 1：产品示意</figcaption>
        </figure>
      </section>
    </article>

    <aside>
      <h2>相关内容</h2>
      <p>侧边栏 / 引文 / 广告</p>
    </aside>
  </main>

  <footer>
    <p><small>版权声明</small></p>
    <a href="#top">回到顶部</a>
  </footer>

  <a href="https://external.example.com" target="_blank"
     rel="noopener noreferrer">安全外链</a>
</body>
</html>
```

---

## 五、高频踩坑 Checklist

| # | 检查项 | 一句话原因 |
|---|---|---|
| 1 | 全页只有 1 个 `h1`，层级不跳级 | SEO 与文档大纲 |
| 2 | 每个段落都用 `p`，`p` 内无块级元素 | 避免浏览器自动闭合导致 DOM 错乱 |
| 3 | `img` 写全 `src`/`width`/`height`/`alt`，`alt` 有意义 | 图片规范四要素 + 无障碍 + SEO |
| 4 | `ul`/`ol` 子元素只有 `li`，`li` 不单独出现 | 父子组合标签 |
| 5 | `ul` 不用 `type`，改 CSS `list-style-type` | HTML5 已废弃 |
| 6 | `ol` 的 `start` 用阿拉伯数字；`reversed` 不写值 | 布尔属性规则 |
| 7 | 单选/复选同组 `name` 一致，文字用 `label` 包裹 | 互斥 + 点击文字可选中 |
| 8 | 下拉第一项提示用 `disabled selected`，多分组用 `optgroup` | 用户体验 |
| 9 | `target="_blank"` 必带 `rel="noopener noreferrer"` | 防 `window.opener` 攻击 |
| 10 | 下载 PDF / 图片加 `download`，自定义名带扩展名 | 否则浏览器直接预览 |
| 11 | `audio`/`video` 提供多个 `source` + 降级文字；最优格式放最前 | 浏览器默认取第一个支持的 |
| 12 | `iframe` 有 `title`、`sandbox`、`loading="lazy"`、固定尺寸、`https` | 安全 / 性能 / 可访问性 / CLS |
| 13 | `main` 每页仅一个，且不含页眉页脚侧边栏 | 语义规范 |
| 14 | `caption` 是 `table` 第一个子元素；跨行列只用 `colspan`/`rowspan` | 其余表现属性已废弃 |
| 15 | `b`/`i`/`u` 不用于语义强调 | 已被 CSS 与语义标签替代 |
| 16 | 注释写清结构，但不写敏感信息 | 注释随源码下发 |

---

## 六、专家补充（⚠️ 非原文内容，为前端工程实践增补）

以下内容**原页面未展开**，用于把教程结论落到生产环境：

| 补充点 | 建议 |
|---|---|
| 图片与 CLS | `width`/`height`（或 CSS `aspect-ratio`）能预留空间避免布局抖动；首屏外图片加 `loading="lazy"`、`decoding="async"`；**纯装饰图写 `alt=""`**，避免朗读器读出无意义内容 |
| `target` 写法 | 规范值是 `_blank`；原文提到的 `blank` 实际是「命名窗口」而非标准关键字，建议统一用 `target="_blank"`。现代浏览器对 `_blank` 已隐式 `noopener`，但显式写 `rel` 更稳妥、兼容旧环境 |
| `button` 默认值 | `<button>` 在 `<form>` 内默认 `type="submit"`，非提交按钮务必显式写 `type="button"`，否则会误触发提交 |
| 非导航的点击 | 不要用 `<a href="#">` 承载 JS 动作（会跳到页首），应使用 `<button type="button">` |
| 表格语义 | `table` 只用于**表格数据**，不要用于页面布局；`th` 加 `scope="col"` 或 `scope="row"`，配 `caption` 提升可访问性 |
| `pre` + `code` | 展示源码时建议 `<pre><code>...</code></pre>`，且内部 `<`、`&` 必须转义为 `&lt;`、`&amp;` |
| `h1` 数量 | HTML5 规范本身允许多 `h1`（分段大纲模型），但 SEO 与屏幕阅读器实践仍强烈建议**每页一个**（与原文结论一致） |
| 表单提交 | 控件必须有 `name` 才会随表单提交；可补 `required`、`pattern`、`min`/`max`、`autocomplete` 做原生校验与体验优化 |
| 自动播放 | `audio`/`video` 的 `autoplay` 常被浏览器静音策略拦截，需配合 `muted` 或用户手势 |
| 注释安全 | HTML 注释会随源码下发到客户端，禁止写密钥、内部路径、敏感业务信息 |

---

**整理说明**：本文按「原页结论 → 结构化表格 → 可复用代码 → 工程补充」重排，若与原文表述有出入，以[原页面](https://www.arryblog.com/guide/html5/html-html5-course.html)为准。
