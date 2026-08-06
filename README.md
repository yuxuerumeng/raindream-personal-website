# RainDream · 雨梦 🌸

> 在代码与文字之间寻找真实的自己。

🔗 [i.raindream.top](https://i.raindream.top)

## 项目结构

```
├── index.html      # 主页
├── blog.html       # 博客页
├── posts.js        # 文章数据
└── avatar.jpg      # 头像
```

## 写博客

打开 `posts.js`，在数组末尾加一篇：

```js
{
  id: 5,
  date: '2026-08-06',
  tags: ['生活'],
  title: '标题',
  excerpt: '摘要',
  body: `正文，Markdown 格式，支持 [链接](url)`
}
```

## 修改代码

所有代码都在 HTML 文件中，用文本编辑器打开即可：

- **主页内容** → 打开 `index.html`，搜索对应中文就能定位到要改的位置
- **联系方式** → 搜索 `contact-grid`，找到四个 `<a href="...">` 标签改链接
- **关于我** → 搜索 `关于我` 或 `about-text`，直接改段落文字
- **配色** → 搜索 `:root`，蓝粉颜色在 CSS 变量 `--blue` 和 `--pink` 里
- **头像** → 替换 `avatar.jpg` 文件，保持同名即可

HTML 里的 `<style>` 标签负责样式，`<script>` 标签负责交互逻辑。

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
