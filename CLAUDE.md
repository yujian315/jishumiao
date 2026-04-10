# jishumiao.com

技术喵 — 在线工具集合站，风格参考 neal.fun

## 技术栈

- **框架**: Astro 4.16 (纯静态 SSG)
- **部署**: GitHub → Cloudflare Pages (自动构建)
- **GitHub**: https://github.com/yujian315/jishumiao
- **域名**: jishumiao.com
- **CF 账号**: inkwp@qq.com
- **监控**: Plausible (pv4.zeezan.com)

## 项目结构

```
src/
├── layouts/
│   ├── BaseLayout.astro      # 首页布局（含 SEO、OG 标签、监控 JS）
│   └── ToolLayout.astro      # 工具页布局（带顶部导航栏、SEO）
└── pages/
    ├── index.astro            # 首页：分类展示工具卡片
    └── {category}/            # 按分类组织工具
        └── {tool-name}.astro  # 具体工具页面
public/
├── favicon.svg
├── og-default.svg             # 社交分享默认图片
├── robots.txt
└── sitemap.xml                # 手动维护，新增工具需更新
```

## URL 分类规则

工具按类别放在对应目录下：

| 分类 | URL 前缀 | 说明 |
|------|----------|------|
| AI 工具 | `/ai/` | Token 计算器、提示词工具等 |
| 开发工具 | `/dev/` | JSON 格式化、正则测试等 |
| 文本工具 | `/text/` | 字数统计、编码转换等 |
| 数学工具 | `/math/` | 进制转换、计算器等 |
| 设计工具 | `/design/` | 颜色选择器、渐变生成等 |
| 趣味工具 | `/fun/` | 人格测试、小游戏等娱乐向工具 |

## 已上线工具

- `/ai/token-counter` — Token 计算器（估算 GPT-4o、Claude、DeepSeek 等模型的 Token 数量与费用）
- `/fun/sbti` — SBTI 人格测试（30 题鉴定 27 种人格，含隐藏触发，原作者：B 站 @蛆肉儿串儿，交互版：sx349/sbti-interactive）

## 新增工具流程

1. 在 `src/pages/{category}/` 下创建 `{tool-name}.astro`
2. 使用 `ToolLayout` 作为布局
3. 在 `src/pages/index.astro` 的 `categories` 数组中添加工具条目
4. 动态内容的样式必须用 `<style is:global>` 并加唯一前缀（如 `.tc-`）避免冲突
5. 在 `public/sitemap.xml` 中添加新 URL
6. 推送到 GitHub 后 Cloudflare Pages 自动构建部署

## 部署流程

```bash
git add . && git commit -m "描述" && git push
```

推送后 Cloudflare Pages 自动触发构建，无需手动操作。

- **构建命令**: `npm run build`
- **部署命令**: `npx wrangler deploy`
- **输出目录**: `dist`
- wrangler.jsonc 已配置好静态资产部署

## SEO 已配置

- Canonical URL（自动生成）
- Open Graph + Twitter Card 标签
- sitemap.xml + robots.txt
- 页面结构化 H1/H2/H3

## 安全规则

- **绝对禁止** 在任何代码、配置文件、提交记录中包含 API 密钥或密码
- 凭据统一存放在 `/Users/keen/Documents/开发代码/claudeCode/mySites/configAPi/`，仅本地读取使用
- `.gitignore` 中已排除敏感文件
- GitHub Token 通过环境变量 `GH_TOKEN` 传入 git push

## 构建命令

- `npm run dev` — 本地开发 (localhost:4321)
- `npm run build` — 构建静态文件到 `dist/`
- `npm run preview` — 预览构建结果
