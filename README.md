# Creator90 Publisher

Creator90 Publisher is a Codex plugin for one workflow:

- Publish the supplied talking-head video to Douyin and WeChat Channels.
- Publish image-text notes to Xiaohongshu.

The plugin contains instructions and a repo marketplace. It does not include the uploader runtime, media files, or account cookies. Publishing runs through the `sau` CLI from a compatible `social-auto-upload` checkout on the user's computer.

## Install the uploader runtime

Install a compatible copy of [`social-auto-upload`](https://github.com/dreammis/social-auto-upload) on each computer, then follow that project's `docs/install.md`. On macOS/Linux:

```bash
git clone https://github.com/dreammis/social-auto-upload.git
cd social-auto-upload
uv venv
source .venv/bin/activate
uv pip install -e .
patchright install chromium
```

Windows PowerShell:

```powershell
git clone https://github.com/dreammis/social-auto-upload.git
cd social-auto-upload
uv venv
.venv\Scripts\activate
uv pip install -e .
patchright install chromium
```

## Install the Codex plugin

Add this GitHub repository as a plugin marketplace, then install `creator90-publisher` from the Codex Plugins Directory:

```bash
codex plugin marketplace add tianqiyun3090-bot/creator90-publisher
codex plugin add creator90-publisher@creator90
```

Alternatively, clone this repository and add the local marketplace from its root:

```bash
git clone https://github.com/tianqiyun3090-bot/creator90-publisher.git
cd creator90-publisher
codex plugin marketplace add .
```

In Codex, open the Plugins Directory, choose the `Creator90` marketplace, and install **Creator90 内容发布**. Restart Codex if the marketplace does not appear.

## Sign in on each computer

The default CLI account alias is `creator`. Each computer must log in locally to the authorized account for every platform it will use:

```bash
.venv/bin/sau douyin login --account creator --headed
.venv/bin/sau tencent login --account creator --headed
.venv/bin/sau xiaohongshu login --account creator --headed
```

On Windows, use `.venv\Scripts\sau.exe`. The account holder must scan the login QR code. Cookies stay in the local runtime's `cookies/` directory; never send or commit them.

## Use it

Ask Codex to prepare or publish content, name the media paths and target platforms, and say whether to publish now or schedule a time. The plugin only targets Douyin video, WeChat Channels video, and Xiaohongshu image-text notes. It checks each account separately before publishing.
