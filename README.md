文档制作工具 · Doc Builder
一个零依赖、零构建、纯前端的可视化文档编辑器。拖拽式搭积木排版，一键导出网页 / ZIP / PDF / Markdown。

打开一个 HTML 文件就能用——不用装 Node，不用跑 npm，不用后端。适合写报告、做笔记、整理学习计划、搭建个人导航页等场景。

✨ 特性一览
🎨 可视化编辑
拖拽式排版：从左侧组件库拖入画布，像搭积木一样组织内容

块级操作：每个块可拖拽移动、上移下移、复制、删除

嵌套容器：提示框、行内布局、表格单元格、树节点都能继续塞块

所见即所得：contenteditable 直接编辑文字，右侧属性面板实时调整样式

🧩 21 种内容组件
分类	组件
文字	标题（H1–H4）、正文段落、列表、引用、分割线、竖分割线
提示框	12 种主题（笔记 / 提示 / 警告 / 危险 / 成功 / 示例…），可折叠、可自定义主色与边框
代码	代码高亮（highlight.js）、一键复制、HTML/XML 代码可直接运行预览
数学	KaTeX 公式，编辑框下方实时预览
Markdown	marked 渲染，编辑框下方实时渲染为富文本，支持 GFM 全语法
媒体	图片 / 视频 / 音频，支持点击上传、拖入替换、外链引用
布局	行内布局（横向 flex，可加竖分割线）、列布局
导航	页面链接（内部跳转）、外部链接、页面嵌入、自动目录
交互	触发器（动作序列引擎）、可折叠树结构
📄 多页面文档
页面树：支持父子层级，预览 / 导出时导航自动折叠展开

主页设置：指定一个页面作为主页，导出 ZIP 时生成 index.html

页面排序：拖拽页面列表重新排列

📤 六种导出格式
格式	说明
完整网页	单文件 HTML，内置导航脚本，双击就能看
ZIP 包	多页面拆分文件 + 图片资源打包 + README
PDF	通过浏览器打印，A4 排版，支持页眉页脚与分页控制
Markdown	结构化转换，表格 / 提示框 / 树都有对应语法
JSON	完整数据快照，可再导入继续编辑
HTML 片段	只导出当前页的正文部分，方便嵌入其他网页
🛠 编辑体验
撤销 / 重做：60 步快照栈，输入防抖

自动保存：900ms 防抖写入 localStorage，刷新后提示恢复

行内格式：加粗 / 斜体 / 下划线 / 删除线 / 行内代码 / 超链接 / 字号 / 颜色 / 对齐

行内代码 toggle：再点一次取消，不会无限嵌套

富文本粘贴：白名单净化，剔除脚本与内联样式

入场 / 悬停动画：13 种动画，基于 IntersectionObserver 触发

侧栏可调宽：拖动分界线调节宽度，双击恢复默认，宽度记忆到 localStorage

🚀 启动加载
顶部全屏加载层，逐项显示 CDN 依赖状态与进度

单项 20 秒超时、整体 25 秒兜底

加载失败会列出具体库名，仍可继续进入使用

图标用内联 SVG，无网络也能正常显示

🚀 快速开始
方式一：直接使用
下载 index.html（或任意你命名的 HTML 文件）

双击用浏览器打开

选择模板或点「以空白开始」，开始创作

首次打开需要联网加载 Font Awesome / highlight.js / KaTeX / marked / JSZip。加载完成后大部分功能离线也能用（KaTeX 与 marked 已缓存）。

方式二：本地服务器（推荐）
部分浏览器对 file:// 协议下的剪贴板、跨 iframe 通信有限制，用本地服务器更稳：

bash
# Python 3
python3 -m http.server 8000

# 或 Node.js
npx serve .
然后访问 http://localhost:8000/。

方式三：GitHub Pages 部署
Fork 本仓库

进入 Settings → Pages，Source 选择 main 分支的根目录

等待一分钟，访问 https://<用户名>.github.io/<仓库名>/

⌨️ 快捷键
快捷键	功能
Ctrl + Z	撤销
Ctrl + Y / Ctrl + Shift + Z	重做
Ctrl + S	手动保存
Ctrl + P	打开预览
Ctrl + D	复制选中的块
Ctrl + K	在可编辑文本中插入超链接
Ctrl + ↑ / ↓	上移 / 下移选中的块
Delete	删除选中的块
Esc	取消选中 / 关闭弹窗
?	打开帮助
📖 使用示例
搭建一份工作报告
文件 → 新建文档 → 选择「工作报告」模板

双击标题改字，正文段落直接编辑

拖一个「表格」到画布，设置行列数

在右侧属性面板调整边框粗细、颜色、表头

文件 → 导出 PDF → 打印对话框选择「另存为 PDF」

编写学习计划
文件 → 新建文档 → 选择「学习计划」模板

修改总目标、阶段规划的表格

点左侧「新建子页面」，创建「每周复盘」

在页面属性面板把「每周复盘」的父页面设为「学习计划」

文件 → 导出 ZIP → 得到带树形导航的多页面网站

做一个网址导航页
选择「网页导航」模板

拖动「行内布局」到画布，往里面塞多个「外部链接」

在属性面板填入 URL 和按钮文字

勾选「在子元素之间显示竖线」让布局更好看

🏗 技术实现
整体架构
text
┌─────────────── app (CSS Grid) ───────────────┐
│  header：文件菜单 / 撤销重做 / 复制 / 帮助 / 预览  │
├────────┬───────────────────────┬─────────────┤
│ 左侧栏  │      画布 canvas       │   右侧属性栏  │
│ 页面树  │  （当前页面的块集合）    │  （当前选中块）│
│ 组件库  │                       │             │
└────────┴───────────────────────┴─────────────┘
              status-bar（字数 / 块数 / 保存状态）
核心设计：DOM 即数据源
数据层：state.pages[]，每项带 id / name / slug / bg / isHome / parentId 和活的 DOM 元素引用 el

视图层：页面内容真实存在于 DOM 中，编辑直接改 DOM，不做虚拟 DOM

序列化层：serializeContainer() 把 DOM 转成干净、可独立打开的 HTML

关键机制
机制	实现方式
拖拽	自定义 drag 事件 + document.elementsFromPoint() 精确定位落点
撤销	快照式，防抖 400ms，栈上限 60
自动保存	localStorage + 900ms 防抖
代码高亮	聚焦时还原纯文本（可编辑），失焦时重新 hljs.highlightElement
触发器	data-actions JSON 存动作列表，导出后用 Promise 链顺序执行
动画	CSS @keyframes + IntersectionObserver 触发入场
页面嵌入	递归序列化，深度 ≥ 1 时只显示提示避免循环
剪贴板净化	白名单标签，剔除 style / class / id / on* 与 javascript:
依赖（全部走 CDN）
库	用途
Font Awesome 6	图标
highlight.js 11	代码语法高亮
KaTeX 0.16	数学公式渲染
marked 14	Markdown 渲染
JSZip 3	ZIP 打包
🌐 浏览器兼容性
浏览器	版本要求
Chrome / Edge	≥ 105
Firefox	≥ 110
Safari	≥ 15.4
主要用到的新特性：

CSS color-mix() — 提示框主题色混色

contenteditable="plaintext-only" 降级方案

IntersectionObserver

srcdoc 属性（用于运行代码块）

📂 项目结构
只有一个文件：

text
doc-builder/
├── index.html      # 全部代码（HTML + CSS + JS 内联）
├── README.md       # 本文档
└── LICENSE         # MIT
🔒 数据与隐私
所有内容只存在你的浏览器里，不上传任何服务器

自动保存到 localStorage，键名 docbuilder_v17

侧栏宽度记忆键名 docbuilder_panel_w

想彻底清空，使用 文件 → 清除本地存储

导出的 ZIP / HTML 里，图片会转成 base64 或打包到 pages/images/，不会泄漏到外部

🤝 贡献
欢迎提交 Issue 和 PR。特别欢迎以下方向：

新增组件（甘特图、时间线、思维导图等）

更多导出格式（Word、Epub）

更完善的 Markdown 扩展语法

主题系统（暗色模式等）

i18n 多语言支持

开发指引
因为没有任何构建工具，改完直接刷新浏览器即可。建议开启 DevTools 的 Disable cache。

新增一个组件需要改 5 处：

左侧 #palette-main 加 .palette-item

buildContent() 的 switch 加分支 + 写 buildXxx()

renderProps() 加属性面板分支，以及 propsEl 的 click / change / input 处理

serializeBlock() 加导出分支（否则导出丢内容）

可选：blockToMd() 加 Markdown 映射

📜 许可
MIT License

🙏 致谢
组件设计参考了 Material for MkDocs 与 Notion

提示框配色取自 Material Design

感谢所有开源依赖的作者

<div align="center">
如果这个工具对你有帮助，欢迎点个 ⭐ Star 支持一下！

⬆ 回到顶部

</div>
