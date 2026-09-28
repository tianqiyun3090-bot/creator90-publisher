---
name: creator90-publisher
description: 为 creator90 主账号整理并发布抖音、视频号口播视频和小红书图文笔记。使用仓库的 sau CLI；当用户要准备、检查或发布这三个平台的内容时调用。
---

# creator90 内容发布

使用 `social-auto-upload` 项目当前的 `sau` CLI 完成 creator90 的平台发布工作流。默认 CLI 账号别名为 `creator`。账号文件只保存登录态；不要读取、复制、输出或提交其中的 Cookie 和凭证。

## 运行环境

- 先在当前工作区查找项目根目录（以 `docs/CLI.md` 和 `pyproject.toml` 为标记），并从该目录使用 CLI。
- macOS/Linux 使用 `.venv/bin/sau`；Windows 使用 `.venv/Scripts/sau.exe`。只有项目环境不可用时，才检查系统 `sau` 是否指向兼容版本。
- 如果没有项目副本或可用 CLI，先说明依赖并请用户提供/克隆项目路径。按 `docs/install.md` 安装依赖；不要在发布任务中擅自安装全局依赖。
- 插件不包含 CLI 运行时或账号登录态。每台电脑都需要各自安装运行环境，并由用户在本机完成账号登录。

## 平台范围

- 抖音：只发布用户提供的口播视频，使用 `sau douyin upload-video`。
- 视频号：只发布用户提供的口播视频，使用 `sau tencent upload-video`。
- 小红书：只发布图文笔记，使用 `sau xiaohongshu upload-note`。
- 不选择、检查或发布到其他平台。

## 发布流程

1. 从仓库根目录工作，先看 `docs/CLI.md` 中的当前命令契约，并按操作系统选择项目虚拟环境中的 `sau`。
2. 确认用户给出的素材、文案、标题和平台范围。用户未指定平台子集时，默认准备三个平台；抖音与视频号可复用同一口播视频，分别整理标题、简介和话题，不添加原稿没有的事实。
3. 小红书只做图文：默认调用 `$xhs-visual-director`，把口播稿改写成适合小红书阅读和吸引点击的笔记正文，并由 Codex 按内容生成约 4 张 3:4 图文页。用户不会提供小红书配图；不要复用为视频发布准备的封面。每张图都必须对应口播里的观点、例子或方法，不为凑数加入低相关内容。保留事实和核心观点，不编造案例或承诺。用户明确提供了成套小红书图片或要求纯文字发布时，按该明确要求执行。
4. 发布前只检查目标平台的账号 `creator`、素材路径和最终文案。每个平台分别检查登录态；不要因一个平台的账号有效就推定另外两个平台也有效。
5. 如果登录态失效，运行该平台的 `login --account creator --headed`，把二维码图片直接展示给用户，让用户扫码。登录成功后重新运行 `check`，再继续任务。不要代替用户处理验证码或要求其发送凭证。
6. 只有用户明确要求发布/现在发布时才立即发布；用户提供时间时按 `docs/CLI.md` 的格式传 `--schedule`。仅要求准备或检查时不发布。时间或平台不清楚时，先准备内容并询问。
7. 抖音和视频号发布默认保留“含 AI 生成内容”标注；小红书有对应标注入口时也开启。
8. 逐个平台读取 CLI 最终结果，明确区分发布成功、失败、扫码登录和验证码状态。只有 CLI 明确报告成功，才告知用户已发布。

## 命令模板

```bash
.venv/bin/sau douyin check --account creator
.venv/bin/sau douyin upload-video --account creator --file <video> --title "<标题>" --desc "<简介>" --tags "标签1,标签2"

.venv/bin/sau tencent check --account creator
.venv/bin/sau tencent upload-video --account creator --file <video> --title "<标题>" --desc "<简介>" --tags "标签1,标签2"

.venv/bin/sau xiaohongshu check --account creator
.venv/bin/sau xiaohongshu upload-note --account creator --images <图片1> <图片2> --title "<标题>" --note "<正文>" --tags "标签1,标签2"
```

定时发布时，在对应上传命令中加入 `--schedule "YYYY-MM-DD HH:MM"`。不传 `--schedule` 会立即发布。
