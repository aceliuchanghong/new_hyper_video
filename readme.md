### 使用

```bash
# 技能安装
npx hyperframes skills
# 为 claude code 执行
npx skills add heygen-com/hyperframes

cd 00_测试系列
# 在当前现有文件夹内进行初始化
npx hyperframes init .
# 重新唤醒预览服务
npx hyperframes preview
# 渲染成 MP4
npx hyperframes render --output output.mp4
```

```
/hyperframes 做一个`什么是agent?`的教学视频 @什么是agent.md
```

### 渲染报错：`An executablePath or channel must be specified for puppeteer-core`

**根因**：hyperframes 渲染依赖一个独立的 `chrome-headless-shell`，需从 Google CDN 下载到 `C:\Users\<user>\.cache\hyperframes\chrome\`。国内网络通常下载失败（只留下空文件夹、可执行文件缺失），puppeteer 启动时找不到浏览器就报这个错。

**解决**：设环境变量 `HYPERFRAMES_BROWSER_PATH` 复用本机已装的 Chrome，绕过下载。这是 `findBrowser()` 的第一优先级，命中即用。

```bash
# 临时（当前终端）
export HYPERFRAMES_BROWSER_PATH="C:/Program Files/Google/Chrome/Application/chrome.exe"
npx hyperframes render

# 永久（用户级，PowerShell 执行一次，新终端自动生效）
powershell -Command "[Environment]::SetEnvironmentVariable('HYPERFRAMES_BROWSER_PATH','C:\Program Files\Google\Chrome\Application\chrome.exe','User')"
```

Edge 也可以：`C:/Program Files (x86)/Microsoft/Edge/Application/msedge.exe`

> 注意：永久变量在新开的终端才生效；当前已开着的会话需重启。另外可删掉坏掉的空缓存目录避免干扰：`rm -rf ~/.cache/hyperframes/chrome/chrome-headless-shell/win64-*`
