# RainDream · 雨梦 🌸

> 在代码与文字之间寻找真实的自己。

🔗 [raindream.top](https://raindream.top)

## 项目结构

```
├── index.html      # 主页
├── blog.html       # 博客页
├── styles.css      # 共享样式（两页共用）
├── common.js       # 共享交互逻辑（两页共用）
├── posts.js        # 文章数据
├── sw.js           # 离线缓存 Service Worker
├── avatar.webp     # 页面内头像
└── avatar.jpg      # 社交分享图（og:image）
```

## 写博客

打开 `posts.js`，在数组末尾加一篇（`id` 必须唯一，不能和已有文章重复）：

```js
{
  id: 6,
  date: '2026-08-06',
  tags: ['生活'],
  title: '标题',
  excerpt: '摘要',
  body: `正文，Markdown 格式，支持 [链接](url)`
}
```

## 修改代码

- **共享样式** → 打开 `styles.css`（导航、主题、配色变量、页脚等两页共用的部分）
- **共享交互** → 打开 `common.js`（主题切换、移动端导航、回到顶部、滚动高亮等）
- **主页内容** → 打开 `index.html`，搜索对应中文就能定位到要改的位置
- **联系方式** → 打开 `index.html`，搜索 `contact-grid`，改里面几个 `<a href="...">` 的链接和文字
- **关于我** → 打开 `index.html`，搜索 `关于我` 或 `about-text`，直接改段落文字
- **配色** → 打开 `styles.css`，搜索 `:root`，蓝粉颜色在 CSS 变量 `--blue` 和 `--pink` 里
- **头像** → 替换 `avatar.webp`（页面内头像）；`avatar.jpg` 用作社交分享图（og:image），保持同名即可

页面专属的样式仍留在各自的 `<style>` 里，交互逻辑留在各自的 `<script>` 里。

## 部署

### Cloudflare Pages（推荐）

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com) → Workers & Pages
2. 点 **Create** → **Pages** → **Connect to Git**
3. 选择 GitHub 仓库 `raindream-personal-website`
4. Build settings 留空，直接点 **Save and Deploy**
5. 部署完成后会分配一个 `*.pages.dev` 域名，可绑定自定义域名

### Vercel

1. 打开 [vercel.com](https://vercel.com) → **New Project**
2. 导入 GitHub 仓库
3. Framework 选 **Other**，Build 和 Output 留空
4. 点 Deploy

### GitHub Pages

1. 仓库 Settings → Pages
2. Source 选 **Deploy from a branch**，分支选 `main`
3. 文件夹选 `/ (root)`
4. Save，等几分钟即可

## 本地运行

直接双击 `index.html` 在浏览器打开，或：

```bash
python -m http.server 8080
```

## 离线说明

主页完全不依赖外部网络。博客页的 Markdown 渲染依赖 `marked.js` CDN，断网时会降级显示纯文本。

Service Worker 缓存策略（`sw.js`）：

- `index.html`、`blog.html`、`posts.js` 走**网络优先**——发布新文章后，老访客刷新页面即可看到，无需手动清缓存；
- `avatar.webp` 等静态资源走**缓存优先**——若替换了这类文件，把 `sw.js` 顶部的 `CACHE_VERSION` 从 `v2` 改成 `v3`（每次 +1），老访客才会拉到新版本。
