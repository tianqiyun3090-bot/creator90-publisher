# Creator90 内容发布插件

这个 Codex 插件打包了 `creator90-publisher` Skill。它通过 `social-auto-upload` 项目的 `sau` CLI 执行发布：抖音和视频号发布口播视频，小红书发布图文。

## 每台电脑需要准备

插件不包含上传器运行时，也不包含账号 Cookie。每台电脑都需要：

1. 安装 Codex，并克隆本项目。
2. 在项目根目录按 [`social-auto-upload` 安装文档](https://github.com/dreammis/social-auto-upload/blob/main/docs/install.md) 安装 Python 依赖和 Patchright Chromium。macOS/Linux：

   ```bash
   uv venv
   source .venv/bin/activate
   uv pip install -e .
   patchright install chromium
   ```

   Windows PowerShell：

   ```powershell
   uv venv
   .venv\Scripts\activate
   uv pip install -e .
   patchright install chromium
   ```

3. 将本项目根目录添加为 Codex 插件 marketplace，再安装插件：

   ```bash
   codex plugin marketplace add <本机项目根目录>
   codex plugin add creator90-publisher@creator90
   ```

4. 在本机分别登录要使用的平台。账号别名默认是 `creator`：

   ```bash
   .venv/bin/sau douyin login --account creator --headed
   .venv/bin/sau tencent login --account creator --headed
   .venv/bin/sau xiaohongshu login --account creator --headed
   ```

   Windows 使用 `.venv/Scripts/sau.exe`。扫码由账号持有人在本机完成。每个平台的登录态都保存在本机项目的 `cookies/` 目录，不要把 Cookie 文件复制到插件或提交到 Git。

用户提供的素材路径仍需在运行该任务的电脑上可访问。没有该项目副本、依赖或登录态时，插件会先提示补齐环境，不会假定其他电脑已配置好。
