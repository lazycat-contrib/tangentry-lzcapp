# tangentry-lzcapp

[Tangentry](https://github.com/mu-zi-lee/Tangentry) 的 LazyCat LPK 打包 —— 本地优先的多平台内容聚合、阅读与笔记工具（Go 单容器）。

## 形态

- 单容器镜像：`muzileee/tangentry`，端口 7380，数据在 `/data`
- 镜像交付：**lazycat 模式**（官方商店要求镜像来自懒猫镜像源，由 Action 转存并改写 manifest）

## 发布目标：双商店

官方商店 + 喵喵商店。版本发现用 Docker Hub 严格三段式 SemVer tag，排除 latest 与两段式别名。

## 官方商店强制要求（已满足）

| 要求 | 处理 |
|------|------|
| 密码类应用必须提供凭据 | 部署参数 login_password 自动生成 20 位密码，TANGENTRY_PASSWORD 注入 + /login 免密填充 |
| 上传/下载必须接文件选择器拦截 | 注入 lzc-file-chooser-inject.js（on: browser, when: /*） |
| 图标不超过 200 KB | 512x512 PNG，约 18 KB |
| 截图（PC 2-8 张） | 5 张上游官方截图，2000x1250 |
| 仅 PC 平台 | package.yml 声明 unsupported_platforms: ios, android, tvos |

## 结构

- `package.yml` — LPK v2 包元数据 + 平台限制
- `lzc-manifest.yml` — 单服务、免密登录注入、文件选择器注入
- `lzc-deploy-params.yml` — 登录密码部署参数
- `content/lazycat-injects/` — 文件选择器拦截脚本
- `.github/screenshots/` — 官方商店截图
- `.github/lazycat-action.yml` — 双商店配置
- `.github/workflows/lazycat.yml` — 每日自动跟版 + 双商店发布
