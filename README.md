[English](#english) | [简体中文](#简体中文)

---

## English

# Logflare

A serverless blog system running entirely on Cloudflare Workers + KV + D1 + R2, with built-in AI capabilities powered by Workers AI.

Zero server, zero cost (within free tiers), deploy in 4 steps.

### Deploy

1. **Create a Cloudflare account** (skip if you have one)
2. **Create resources** in Cloudflare Dashboard:
   - 1 KV Namespace
   - 1 D1 Database
   - 1 R2 Bucket
3. **Create a Worker**, paste the contents of [`index.js`](index.js) into the code editor, and deploy. Then bind the resources:
   - KV Namespace → variable name `LF_KV` (Free: 100K reads/day, 1K writes/day)
   - D1 Database → variable name `LF_DB` (Free: 5 GB storage, 5M reads/day, 100K writes/day)
   - R2 Bucket → variable name `LF_FS` (Free: 10 GB storage, 10M reads/month, 1M writes/month)
   - *(Recommended)* Workers AI → variable name `LF_AI` (Free: 10,000 neurons/day)

   Exceeding the free tier limits will cause the corresponding service to fail. It will become available again after the usage resets (daily or monthly depending on the resource). If you expect very high usage, consider upgrading to a Cloudflare paid plan (this project is completely free and has no affiliation with Cloudflare).

4. **Visit your Worker URL** — the setup wizard will guide you through initial configuration

Optionally, bind a custom domain to the Worker.

### Features

- WordPress-style setup wizard (first visit triggers install)
- Admin panel with dashboard, post/tag management, media library, settings
- Markdown editor with toolbar, live preview, media upload, image drag/drop & paste
- Rich content rendering with lazy-loaded CDN libraries:
  - **Math formulas** — KaTeX, auto-upgrades to MathJax when needed
  - **Diagrams** — Mermaid, Graphviz (DOT), Nomnoml, Flowchart.js, Cytoscape (network graphs)
  - **Charts** — ECharts, Vega-Lite, Plotly, Chart.js, ApexCharts
  - **Science** — SMILES (chemistry), 3Dmol.js (molecular 3D), function-plot (math), d3-celestial (star maps)
  - **Maps** — Leaflet (interactive maps), Globe.gl (3D globe)
  - **Music** — ABC notation (abcjs)
  - **Project** — Frappe Gantt, WaveDrom (timing), Markmap (mind maps)
  - **Utility** — QRCode, Barcode (JsBarcode)
  - Zero cost when unused — libraries load only when the corresponding syntax is detected
- Per-post license settings (CC BY/SA/NC/ND, CC0, All Rights Reserved) with CC badge icons
- Custom slug support for posts and tags with automatic ID-based fallback URLs
- Modern card-style responsive design with unified design system
- Multi-language support with 11 built-in languages, custom language generation, and RTL layout support:
  - **Built-in**: English, 简体中文, 繁體中文, 日本語, 한국어, Bahasa Melayu, Tiếng Việt, ไทย, தமிழ், עברית, العربية
  - **Custom**: Auto-generate translations via DeepL, Workers AI (M2M100), or MyMemory with progress bar
- Visitor statistics (PV/UV with geo location), writing time tracking, word count
- Footer with copyright, visitor stats, and powered-by credits
- RSS Feed and Sitemap
- SEO support (Open Graph meta tags, noindex option)
- Data import/export (JSON) with full metadata preservation
- Full reset and partial reset with selective preservation options
- Schema incompatibility detection with friendly maintenance page, admin login, and rollback/export/reset options
- Auto-initializing D1 schema and R2 assets (downloaded from jsDelivr on first run)
- Accessibility: focus-visible, prefers-reduced-motion, prefers-contrast, 44px touch targets

### AI Features (via Workers AI)

Bind Workers AI (`LF_AI`) to unlock these features — all marked with a star icon in the editor:

- **AI Title** — generate a concise, engaging title from your article
- **AI Excerpt** — auto-generate a summary (max 200 characters)
- **AI Tags** — suggest relevant, atomic tags (avoids overlapping or redundant tags)
- **AI Cover** — generate a blog cover image using Stable Diffusion XL
- **AI Review** — thorough review: typos, grammar, clarity, and improvement suggestions
- **AI Rewrite** — rewrite/improve your article with optional instructions (preserves original as "before" version)
- **AI Reference Creation** — write a new article based on reference material and your prompt

### External Services (Optional)

- **DeepL API** — high-quality admin language translation. Configure API key in Settings → External Services. [Get a free key](https://www.deepl.com/pro-api)

### How It Works

- `index.js` (~213 KB) is the entire Worker — paste it into Cloudflare
- `assets/` (CSS, JS, images, language packs) are automatically downloaded to the user's R2 bucket on first visit
- Posts are stored in KV (content) and D1 (metadata)
- Media files are stored in R2
- Site config and user info are stored in D1, but during reset recovery R2 is used as temporary storage when the user opts to preserve them

### License

MIT

---

## 简体中文

# Logflare

完全运行在 Cloudflare Workers + KV + D1 + R2 上的无服务器博客系统，内置基于 Workers AI 的智能创作功能。

零服务器、零成本（免费额度内），4 步完成部署。

### 部署

1. **注册 Cloudflare 帐号**（已有则跳过）
2. 在 Cloudflare 控制台**创建资源**：
   - 1 个 KV 命名空间
   - 1 个 D1 数据库
   - 1 个 R2 存储桶
3. **创建 Worker**，将 [`index.js`](index.js) 的内容粘贴到代码编辑器中并部署。然后绑定资源：
   - KV 命名空间 → 变量名 `LF_KV`（免费：每天 10 万次读取、1000 次写入）
   - D1 数据库 → 变量名 `LF_DB`（免费：5 GB 存储、每天 500 万次读取、10 万次写入）
   - R2 存储桶 → 变量名 `LF_FS`（免费：10 GB 存储、每月 1000 万次读取、100 万次写入）
   - *（推荐）* Workers AI → 变量名 `LF_AI`（免费：每天 10,000 able neurons）

   超出免费用量会导致对应的服务不能完成，需要经历用量重置的冷却期才能再次使用。如果您的预期用量非常高，可以选择升级到 Cloudflare 的付费计划（本服务完全免费，与 Cloudflare 无利益相关）。

4. **访问你的 Worker URL** — 安装向导会引导你完成初始配置

可选：为 Worker 绑定自定义域名。

### 功能

- WordPress 风格的安装向导（首次访问自动触发）
- 管理后台：仪表盘、文章/标签管理、媒体库、设置
- Markdown 编辑器，支持工具栏、实时预览、媒体上传、图片拖拽/粘贴上传
- 丰富的内容渲染，CDN 按需动态加载：
  - **数学公式** — KaTeX 渲染，需要时自动升级为 MathJax
  - **图表** — Mermaid、Graphviz (DOT)、Nomnoml、Flowchart.js、Cytoscape（网络图）
  - **数据可视化** — ECharts、Vega-Lite、Plotly、Chart.js、ApexCharts
  - **学科** — SMILES（化学结构式）、3Dmol（3D 分子）、function-plot（数学函数）、d3-celestial（星图）
  - **地图** — Leaflet（交互式地图）、Globe.gl（3D 地球）
  - **音乐** — ABC 记谱法 (abcjs)
  - **项目** — Frappe Gantt（甘特图）、WaveDrom（时序图）、Markmap（思维导图）
  - **工具** — QRCode（二维码）、Barcode（条形码）
  - 未使用时零开销 — 仅在检测到对应语法时才加载对应库
- 文章级版权设定（CC BY/SA/NC/ND、CC0、保留所有权利），CC 协议附带官方徽章图标
- 文章和标签支持自定义 slug，无 slug 时自动使用 ID 作为 URL
- 统一设计系统的现代卡片式响应式设计
- 多语言支持，11 种内置语言 + 自定义语言生成 + RTL 布局支持：
  - **内置**：English、简体中文、繁體中文、日本語、한국어、Bahasa Melayu、Tiếng Việt、ไทย、தமிழ்、עברית、العربية
  - **自定义**：通过 DeepL、Workers AI (M2M100) 或 MyMemory 自动生成翻译，带进度条
- 访客统计（PV/UV + 地理位置）、创作时长追踪、字数统计
- 页脚：版权信息、访客统计、技术署名
- RSS Feed 和 Sitemap
- SEO 支持（Open Graph 标签、noindex 选项）
- 数据导入/导出（JSON 格式），完整保留元数据
- 支持全面重置和部分重置，可选择性保留数据
- Schema 不兼容检测，友好维护页面 + 管理员登录 + 回退/导出/重置
- D1 表结构和 R2 资产自动初始化（首次运行时从 jsDelivr 下载）
- 无障碍：键盘焦点指示器、减少动画、高对比度、44px 触摸目标

### AI 功能（通过 Workers AI）

绑定 Workers AI（`LF_AI`）即可解锁以下功能 — 编辑器中所有 AI 操作均以星标图标标识：

- **智能标题** — 根据文章内容生成简洁有吸引力的标题
- **智能摘要** — 自动生成文章摘要（最多 200 字）
- **智能标签** — 推荐相关的原子化标签（避免重叠和冗余）
- **智能封面** — 使用 Stable Diffusion XL 生成博客封面图
- **智能审阅** — 全面审阅：错别字、语法、表达清晰度及改进建议
- **智能改稿** — 改写/润色文章，支持自定义改稿提示（原稿作为"改前稿"保留）
- **参考创作** — 基于参考资料和创作提示生成新文章

### 外部服务（可选）

- **DeepL API** — 高质量管理员语言翻译。在设置 → 外部服务中配置 API Key。[获取免费密钥](https://www.deepl.com/pro-api)（可能要求提供信用卡信息）

### 工作原理

- `index.js`（约 213 KB）是完整的 Worker 代码 — 粘贴到 Cloudflare 即可
- `assets/`（CSS、JS、图片、语言包）在首次访问时自动下载到用户的 R2 存储桶
- 文章存储在 KV（正文）和 D1（元数据）中
- 媒体文件存储在 R2 中
- 站点配置和用户信息存储在 D1 中，重置恢复阶段在用户选择保留对应数据时使用 R2 作为临时存储

### 许可证

MIT
