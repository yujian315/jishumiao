# jishumiao.com

技术喵 — 在线工具集合站，风格参考 neal.fun

## 技术栈

- **框架**: Astro 4 (纯静态 SSG)
- **部署**: GitHub → Cloudflare Pages (自动构建)
- **域名**: jishumiao.com
- **CF 账号**: inkwp@qq.com

## 项目结构

```
src/
├── layouts/
│   ├── BaseLayout.astro      # 首页布局
│   └── ToolLayout.astro      # 工具页布局（带顶部导航栏）
└── pages/
    ├── index.astro            # 首页：分类展示工具卡片
    └── {category}/            # 按分类组织工具
        └── {tool-name}.astro  # 具体工具页面
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

## 新增工具流程

1. 在 `src/pages/{category}/` 下创建 `{tool-name}.astro`
2. 使用 `ToolLayout` 作为布局
3. 在 `src/pages/index.astro` 的 `categories` 数组中添加工具条目
4. 动态内容的样式必须用 `<style is:global>` 并加唯一前缀避免冲突
5. 推送到 GitHub 后 Cloudflare Pages 自动构建部署

## 部署流程

```bash
git add . && git commit -m "描述" && git push
```

推送后 Cloudflare Pages 自动触发构建，无需手动操作。

## 安全规则

- **绝对禁止** 在任何代码、配置文件、提交记录中包含 API 密钥或密码
- 凭据统一存放在 `/Users/keen/Documents/开发代码/claudeCode/mySites/configAPi/`，仅本地读取使用
- `.gitignore` 中已排除敏感文件

## 构建命令

- `npm run dev` — 本地开发 (localhost:4321)
- `npm run build` — 构建静态文件到 `dist/`
- `npm run preview` — 预览构建结果
