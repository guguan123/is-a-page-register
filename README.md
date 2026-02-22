# is-a.page

为你的个人主页、开源项目、Notion 笔记或任何有趣的网页，提供一个免费且纯粹的定制域名。

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
[![Powered by Cloudflare](https://img.shields.io/badge/Powered%20by-Cloudflare-F38020.svg?style=flat-square)](#)

is-a.page 是一个面向所有创作者的免费子域名分发项目。与 `is-a.dev` 强烈的开发者身份属性不同，`is-a.page` 更加开放和宽泛——只要它是一个网页（Page），无论是设计作品集、在线简历、播客导航，还是一个单纯的无聊按钮，你都可以为它申请一个体面的短链接。

## 核心特性

- **URL 边缘重定向**：支持 HTTP 302 重定向。非常适合给 Notion、Obsidian Publish、Carrd 等长链接绑定简短的入口。
- **完整的 DNS 支持**：支持 `CNAME`, `A`, `AAAA`, `TXT`, `MX` 记录。无缝接入 Vercel, Netlify, GitHub Pages 等托管平台。
- **开箱即用的 HTTPS**：由 Cloudflare 提供底层网络支持，默认开启代理与免费 SSL 证书。

## 申请规则

为了维持域名的长期可用性与良好声誉，请在提交 PR 前确认你的申请符合以下底线要求：

1. **基本格式**：前缀长度必须 **`>= 4`** 个字符。仅允许小写英文字母、数字和短横线（不能以短横线开头或结尾）。
2. **禁止囤积**：申请的域名必须指向一个**已上线且有实际内容**的页面。拒绝“先占位后开发”或指向失效链接。
3. **内容安全**：严禁任何涉政、色情、赌博、黑产、钓鱼网站及违反所在地区法律法规的内容。违规者将被永久封禁域名及 GitHub ID。
4. **合理使用**：目前对单人申请数量没有严格的硬性限制，但请按需申请，避免滥用公共资源。

## 申请指南

只需要基本的 GitHub 操作即可完成申请。

### 1. 准备文件

Fork 本仓库。在 `domains/` 目录下创建一个新的 JSON 文件。
**文件命名即为你想要的子域名**。例如，你想申请 `my-project.is-a.page`，则创建文件 `domains/my-project.json`。

### 2. 编写配置

根据你的需求，选择对应的配置模板填入。

**场景一：URL 重定向（推荐）**  
适用于 Notion、各类云文档、社交媒体主页等无法直接绑定域名的场景。

```json
{
  "description": "我的开源项目说明文档",
  "type": "REDIRECT",
  "url": "https://your-workspace.notion.site/your-long-page-id",
  "owner": {
    "username": "你的 GitHub 用户名",
    "email": "你的邮箱"
  }
}
```

**场景二：CNAME 解析**  
适用于 Vercel、GitHub Pages、Hashnode 等支持自定义域名的托管服务。

```json
{
  "description": "基于 Vercel 部署的个人博客",
  "type": "CNAME",
  "cname": "cname.vercel-dns.com",
  "proxied": true,
  "owner": {
    "username": "你的 GitHub 用户名",
    "email": "你的邮箱"
  }
}
```
*注：`proxied: true` 会开启 Cloudflare 代理。如果你的托管服务商要求直连验证或自行签发证书，请显式设置为 `false`。*

*(如需配置 A、AAAA、MX、TXT 等记录，请参考仓库内的完整示例说明。)*

### 3. 提交 PR

将修改 Commit 并提交 Pull Request。
系统会自动运行 CI 校验脚本（检查长度、敏感词、格式等）。如果 CI 亮起红灯 ❌，请点击 Details 查看具体报错并修改；如果亮起绿灯 ✅，请等待管理员人工 Review。

合并后，DNS 和重定向规则将自动推送到 Cloudflare。

## 修改与注销

你的域名由你存放在本仓库的 JSON 文件声明。
- **修改**：提交 PR 修改你原有的 JSON 文件（例如更换 `url` 或 `cname`），合并后自动覆盖线上配置。
- **注销**：提交 PR 删除你的 JSON 文件。合并后系统会自动清理对应的 DNS 和重定向规则（自动 GC 机制）。

## 社区展示 (Showcase)

如果你用 `is-a.page` 构建了有趣、有设计感或有价值的网页，欢迎在 PR 中说明。我们会不定期将优秀站点收录至下方展示墙。

- *(等待你的加入...)*
- *(等待你的加入...)*

## 鸣谢

- 概念与运作模式致敬 [is-a.dev](https://github.com/is-a-dev/register) 社区。
- 基础设施由 [Cloudflare](https://www.cloudflare.com/) 提供支持。
