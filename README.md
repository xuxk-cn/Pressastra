# Pressastra —— WordPress 博客发布与管理工具箱

**Pressastra** 是一款面向 WordPress 站长的桌面应用工具集，用于 **Markdown 博文一键发布、图片批量压缩上传、首页/置顶/菜单布局管理、数据库备份与全站数据迁移、浏览器授权登录** 等日常运维场景。

> 项目名 **Pressastra**。

---

## 一、功能概览

| 分类 | 工具 | 主要功能 |
|:---|:---|:---|
| 📤 发布 | **Markdown 单篇上传** | 单篇 Markdown 转 HTML 发布，可选分类、特色图片、草稿/发布状态 |
| | **Markdown 批量上传** | 项目目录批量发布，支持预演模式（不实际发布） |
| 💾 备份 | **全站导出 WXR+媒体+JSON 清单** | 一键导出 WordPress 全站文章、页面、媒体库，生成 WXR 标准 XML 与内容清单 |
| | **数据库 SQL 全库导出** | 通过 WordPress 管理后台接口导出全部数据表（含用户、设置、文章等） |
| | **数据库导入/恢复** | 将 SQL 备份合并或覆盖写入目标站点 |
| | **全站导入 WXR+媒体+JSON 清单** | 将 WXR 全站 XML + 媒体库文件 + 内容清单 回导入到目标站点，支持特色图回填、重复 URL 跳过 |
| 🛠 管理 | **页眉/页脚/版权编辑** | 可视化编辑站点页眉、页脚、版权信息，支持多语言 |
| | **文章卡片编辑 标题/摘要** | 文章列表分页浏览（每页 10 篇，支持上下页），在线编辑标题与摘要，支持更换特色图片（中文文件名支持） |
| | **菜单编辑器 页眉导航/页脚栏目/页脚资源** | 可视化编辑 WordPress 菜单结构与链接 |
| | **媒体库重复图片检测/清理** | 按内容 MD5 检测重复图片，支持勾选删除，删除后自动刷新列表 |
| 📐 布局 | **首页布局设置（每页篇数/列数/检查）** | 自定义首页每页显示文章数、网格列数，自动检查首页是否符合设置 |
| 📌 置顶 | **置顶博文设置（多条有序置顶）** | 为首页或分类设置多条置顶文章，支持置顶顺序调整（最新置顶排最前） |
| 📥 导入 | **文件夹批量导入媒体库** | 将本地文件夹内的图片批量上传到 WordPress 媒体库 |
| 🧰 其他 | **站点连接向导（浏览器授权）** | 弹出系统浏览器在 WordPress 后台完成应用密码授权，全程不接触主密码 |
| | **图片压缩裁切（尺寸可自定义）** | 批量压缩图片，支持自定义宽高、质量、格式 |
| | **GitHub 仓库同步** | 同步 GitHub 项目信息 |
| | **修改网站后台密码** | 修改 WordPress 管理员密码 |

---

## 二、快速开始

### 1. 下载与安装

从 [GitHub Releases](https://github.com/xuxk-cn/Pressastra/releases) 下载最新版 `Pressastra.exe`（或 `Pressastra-Runner.exe` 运行器），双击运行即可，无需安装 Python 环境。

> 打包版为**零源码分发**（目录内不含 `.py` 源码），可直接交付给客户使用。

### 2. 首次登录

1. 填写 **网站地址**（如 `https://你的域名`，可不带 `http://`，程序自动补全）
2. 填写 **用户名** 与 **密码**（或 WordPress 应用密码）
3. 点击 **🔗 登录**
   - 密码为空：弹出系统浏览器，在 WordPress 后台完成“应用密码”授权，**全程不接触主密码**
   - 密码非空：直接表单登录
4. 登录成功后，凭据自动加密存入 **Windows 凭据管理器**（DPAPI 按用户加密），下次启动自动继承

> **商用标准**：登录凭据不写死在代码里，也不上传到任何第三方服务器；应用与站点直连，数据不经过本项目服务器。

---

## 三、授权系统（商业分发）

Pressastra 采用 **License Server** 架构，支持离线验签与设备绑定，适合商业分发。

### 授权服务器地址

客户端启动时向授权服务器校验：

```
http://eduomni.dpdns.org:8088/api/verify.php
```

### 套餐

| 套餐 | 名称 | 价格 | 设备数 | 有效期 |
|:---|:---|:---|:---|:---|
| TRIAL | 试用版 | 免费 | 1 台 | 14 天 |
| BASIC | 基础版 | ¥49 | 1 台 | 永久 |
| PRO | 专业版 | ¥99 | 3 台 | 永久 |
| TEAM | 团队版 | ¥199 | 10 台 | 永久 |

### 首次使用流程

1. 启动程序，**免费试用 14 天**（无需授权码，自动计时）
2. 试用期内全部功能可用
3. 到期后，需在 [授权服务器后台](http://eduomni.dpdns.org:8088/mgr/) 购买或获取授权码，在应用激活框输入即可继续使用
4. 授权码支持**设备绑定**，一台机器一台授权；如需换机，可在后台自助解绑（30 天冷却）

### 服务端部署

授权服务器部署在 Oracle 云主机（PHP + MySQL），完整部署文档见：

- [server/部署独立授权站.sh](server/部署独立授权站.sh) —— 一键独立部署脚本（独立目录 `/var/www/wpb-license/`、独立 nginx 站点 8088 端口、独立库 `wpb_license`）
- [server/README.md](server/README.md) —— 授权服务器完整部署与 API 接口文档
- [server/操作说明.md](server/操作说明.md) —— 授权服务器详细操作手册（建表、支付回调、后台发码、故障排查）

---

## 三、核心功能使用指南

### 1. 发布博客（Markdown → WordPress）

#### 单篇发布（Markdown 一键上传）

1. 登录后进入「发布 → Markdown 一键上传」
2. 选择本地 `.md` 博文文件
3. 可选：选择特色图片（封面）
4. 点击「发布到网站」
5. 标题、正文、分类自动同步；发布成功后可在 WordPress 后台查看

#### 批量发布（适合多项目）

1. 进入「发布 → 批量上传+封面压缩+GitHub链接」
2. 选择本地项目根目录（程序自动扫描博文文件）
3. 勾选要发布的项目，可启用「预演模式」先预览不实际发布
4. 点击「批量发布」

> 支持在文章末尾自动添加 GitHub 项目链接按钮（需在 `github_projects.json` 中配置项目与仓库对应关系）。

---

### 2. 备份与迁移

#### 全站备份（推荐）

1. 进入「备份 → 全站导出 WXR+媒体+JSON 清单」
2. 点击「开始导出」，程序会：
   - 从服务器下载 WXR 全站 XML（文章、页面、分类、标签、附件元数据）
   - 批量下载媒体库图片到本地 `media/` 目录
   - 生成 `内容清单.json`（用于后续导入时恢复特色图）
3. 导出目录可直接作为“备份包”保存或拷贝到新站点

#### 数据库 SQL 全库导出

适合需要完整数据库表结构与数据的场景（包含用户、设置、插件配置等 WordPress 原生表）。

#### 全站导入（搬家）

将导出的目录（WXR + media/ + 内容清单.json）导入到另一站点：

1. 进入「备份 → 全站导入 WXR+媒体+JSON 清单」
2. 填写目标站点地址、用户名、密码
3. 选择备份目录
4. 点击「开始导入」
   - 媒体库按文件名自动去重，已存在的不重复上传
   - 文章/页面默认导入为**草稿**，避免误发布到线上
   - 特色图根据内容清单自动回填
   - 导入完成后自动对账，报告缺失项

---

### 3. 置顶管理（首页/分类置顶）

1. 进入「置顶 → 置顶博文设置」
2. 选择“首页”或某个分类板块
3. 点击文章左侧「📌」将其设为置顶
4. 支持多条置顶，最新置顶排最前，其余自动后移
5. 每个位置最多保留 5 条，超出自动挤掉最旧的

---

### 4. 图片压缩裁切

进入「🧰 其他 → 图片压缩裁切」：

1. 选择图片文件或文件夹
2. 设置目标宽度、高度、质量、输出格式
3. 点击「开始压缩」，进度实时显示
4. 支持中文文件名（自动处理编码，免受主机 WAF 拦截）

---

## 三、客户端配置文件（settings.json）

打包版发布时会生成空白 `settings.json`，首次登录后自动写入：

```json
{
  "language": "zh",
  "theme": "dark",
  "url": "https://edunm.dpdns.org",
  "username": "xuxk3581@gmail.com",
  "password": "",
  "auto_copy": false,
  "password_store": "windows-credential-manager",
  "license_server": "http://eduomni.dpdns.org:8088"
}
```

- **密码**：不以明文保存在 settings.json，而是存入 Windows 凭据管理器（DPAPI 按用户加密）
- **license_server**：授权服务器地址，发布前必须填写（留空则跳过授权校验，进入试用模式）

---

## 四、打包与分发（零源码）

### 构建环境

- Python 3.8+
- PyInstaller
- 依赖：tkinter、customtkinter、markdown、PIL、PIL._tkinter_finder、coffee、qr_resource 等

### 打包命令

```bash
# 在 WordPress工具集 目录下
打包.bat
```

打包特点：

- **onedir 模式**：生成 `publish/` 目录，`WP-Blog-Tools.exe` 即主程序
- **零源码**：publish 根目录不含任何 `.py` 源码，所有工具模块已编译进 exe
- **WP-Tools-Runner.exe**：工具运行器，支持 `--check`（全部 25/26 模块可导入自检）与 `--check-gui`（10/10 嵌入界面自检）
- **重打包前**：务必先 `taskkill /IM WP-Blog-Tools.exe /F` 退出正在运行的 exe，否则 PyInstaller 会嵌套目录

### 代码签名（商业发布建议）

当前暂未代码签名，客户首次运行可能遇到 Windows SmartScreen。建议：

1. 发布走 **GitHub Releases**，公布 SHA256 校验值
2. 客户文档注明：SmartScreen 弹窗选「仍要运行」
3. 有首批付费客户后，购买 Windows OV 代码签名证书，在 `打包.bat` 最后一步加入 `signtool` 签名

---

## 五、授权服务器部署（服务端）

如需自行部署授权服务器（或替换为自己的授权站点），请参考：

- **[server/部署独立授权站.sh](server/部署独立授权站.sh)** —— 一键部署脚本（Oracle 云主机）
- **[server/README.md](server/README.md)** —— 授权服务器完整架构与 API 接口文档
- **[server/操作说明.md](server/操作说明.md)** —— 授权服务器部署与日常运维手册
- **[server/部署助手.sh](server/部署助手.sh)** —— 通用部署助手（适配已有网站根目录）

### 部署摘要

| 项目 | 说明 |
|:---|:---|
| 程序目录 | `/var/www/wpb-license/`（独立目录，与现有项目并列）|
| Nginx 站点 | 独立端口 `8088`，不影响现有站点 |
| 数据库 | `wpb_license` / 用户 `wpb_user`（仅授权这一个库）|
| 签名密钥 | `WPB_LICENSE_SECRET`（客户端与服务器必须一致）|
| 后台令牌 | `WPB_ADMIN_TOKEN`（mgr/ 后台登录用）|
| 管理后台 | `http://你的域名:8088/mgr/` |
| 购买页 | `http://你的域名:8088/static/buy.html`|

部署后必做：

1. **Oracle 云控制台** → 安全列表 → 入站规则放行 TCP **8088**
2. 上传 `private.pem` 到 `/var/www/wpb-license/_lib/keys/private.pem`（启用 RSA v2 非对称验签；不传则回退 HMAC，新版客户端会拒绝）
3. 客户端发布前把 `LICENSE_SERVER_BASE` 填成授权服务器地址

---

## 五、开发与二次开发

### 模块结构

```
WordPress工具集/
├─ wp_tools_hub.py      主窗口（登录卡、工具分发）
├─ wp_login_common.py   SmartHTTP 客户端（应用密码优先 + 表单兜底）
├─ wp_credential_store.py  Windows 凭据管理器（DPAPI）
├─ wp_license.py         License v2 RSA-2048 离线验签
├─ wp_connect_wizard.py  浏览器授权向导
├─ wp_exporter.py        全站 WXR 导出
├─ sticky_posts_gui.py   置顶管理（兼 WPClient 登录客户端）
├─ cli_tools_gui.py      多入口工具（批量上传/布局/导出等）
├─ import_media_gui.py   媒体批量导入
├─ compress_images_gui.py 图片压缩裁切
├─ header_footer_editor.py 页眉页脚编辑
├─ post_card_editor.py   文章卡片编辑
├─ menu_editor_gui.py    菜单编辑器
├─ db_export.py / db_import.py 数据库导出/导入
├─ homepage_layout_gui.py 首页布局
├─ import_media_gui.py   媒体导入
├─ upload_all.py         批量上传
├─ change_site_password.py 修改后台密码
├─ coffee / locales / qr_resource / md2wp 等辅助模块
└─ 打包.bat              打包为 exe
```

### 隐私与安全

- **应用密码不经过 wp-login.php**，表单验证码 / Turnstile / 2FA / 主机登录防护一律不触发
- 登录凭据加密存在 **Windows 凭据管理器**，`settings.json` 中仅留空密码标记
- 诊断包导出时自动剔除凭据与 Cookie
- 不上传站点 URL、文章内容到任何第三方服务器
- 客户端与站点直连，授权服务器仅校验 license key 与设备指纹哈希

---

## 六、版本历史

| 版本 | 日期 | 主要更新 |
|:---|:---|:---|
| 1.0 | 2026-09 | 初始版本，Markdown 发布、数据库导出、图片压缩 |
| 1.1 | 2026-10 | 授权闸门、License v2 RSA 验签、凭据管理器、诚实 UA、主机防护指引 |
| 1.1.1 | 2026-11 | 浏览器授权登录、全站导入 WXR、登录卡浏览器授权、零源码打包 |
| 2.0 | 2026-11 | 重命名为 **Pressastra**，免码试用 14 天、三处存储防篡改试用、零源码打包、客户端端到端加密验签 |

---

## 七、联系与反馈

- 作者：xuxk-cn
- GitHub：https://github.com/xuxk-cn
- 测试站点：https://edunm.dpdns.org（演示用，数据仅供测试）
- 授权服务器：http://eduomni.dpdns.org:8088

---

> **商用说明**：本应用为商业软件，发布前请填写 `LICENSE_SERVER_BASE` 并完成代码签名。免费试用 14 天，到期后需购买授权码。如需代码签名证书或定制开发，请联系作者。