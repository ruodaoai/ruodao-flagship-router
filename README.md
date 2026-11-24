# FlagshipRouter 免费模型网关（若道桌面端插件）

> 英文文档：[README.en.md](./README.en.md)

把 [FlagshipRouter](https://github.com/theRizwan/FlagshipRouter)（基于 9router 的本地 OpenAI 兼容网关/控制台）做成若道桌面端功能插件：市场下载安装后，一键装好本地网关，自动启动、自动生成 API Key，并把里面的免费模型**一键接入若道 Agent**，在对话里直接选用。

## 特性

- **一键安装**：后台下载上游源码 → 安装依赖 → 构建网关（支持本地 ZIP/源码目录离线安装、GitHub 镜像加速），关闭界面不中断，进度可查。
- **自动启动**：网关以独立进程运行（默认 `127.0.0.1:20128`，端口被占用自动换空闲端口），数据目录与若道桌面端隔离。
- **自动 API Key**：设置 `REQUIRE_API_KEY` 后自动登录控制台创建「Ruodao Agent」Key 并校验，无需手动操作。
- **一键接入 Agent**：在工作台勾选模型后，通过桌面端 `saveCustomModel` 把网关注册为模型提供方（`wire_api = "responses"`，网关原生支持 `/v1/responses`），配置持久化到 `config.toml`，重启后仍可用。
- **自检与排障**：doctor 逐项检查 Node 版本 / 安装 / 连通性 / Key / 模型数；log 返回安装与运行日志。

## 使用流程

1. 在若道桌面端「插件」页导入本插件（或从市场安装）。
2. 打开侧边栏「免费模型网关」工作台，点击 **一键安装**（首次约 2–8 分钟，可用「查询安装进度」轮询）。
3. 安装完成后点击 **启动网关**，然后 **拉取模型**，勾选需要的模型。
4. 点击 **接入 Agent**——模型即刻出现在若道 Agent 的模型列表中。
5. 控制台（可选）：浏览器打开 `http://127.0.0.1:20128`，密码在状态卡片中展示，可自行添加上游账号与模型。

## 配置项

| Key | 说明 |
| --- | --- |
| `RUODAO_FLAGSHIP_PORT` | 网关端口，默认 20128 |
| `RUODAO_FLAGSHIP_MIRROR` | GitHub 加速镜像前缀，如 `https://gh-proxy.com` |
| `RUODAO_FLAGSHIP_SOURCE_ZIP` | 离线安装：源码 ZIP 本地路径 |
| `RUODAO_FLAGSHIP_SOURCE_DIR` | 离线安装：本地源码目录 |
| `RUODAO_FLAGSHIP_API_KEY` | 手动指定网关 API Key（留空自动生成） |

数据目录：`~/.ruodao-flagship-router`（可用环境变量 `RUODAO_FLAGSHIP_HOME` 覆盖）。密钥只落盘在数据目录，不进仓库。

## 环境要求

- Node.js >= 20.9（推荐 22 LTS），带 npm（无 npm 时插件会自动下载 npm 运行时）。
- 首次构建需要网络下载源码与依赖（约 60–150 MB）。
- 安装会自动补齐上游的 optionalDependencies（`better-sqlite3` / `@aws-sdk/credential-providers`）：这两个模块在 `next build` 期间会被静态解析，缺一个就必然构建失败；插件装包时跳过原生编译，运行期由 Node 内置 `node:sqlite` / `sql.js` 兜底，**不需要** Visual Studio C++ 工具链。
- 构建失败重试会复用已装好的依赖，不必再等一遍 `npm install`。

## 命令清单

`install` / `install-status` / `status` / `start` / `stop` / `models` / `doctor` / `uninstall`（`{ purge: true }` 连数据一起删）/ `log`，全部通过 stdin/stdout 传 JSON。

## 测试

```bash
node --test test/
```

仅供学习研究，请遵守上游项目（MIT）与各模型提供方的服务条款。