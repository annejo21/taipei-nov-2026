# 台北 10 天 9 夜 · 旅行手册

单一 HTML 页面，零外部依赖，手机打开快、断网也能看。部署在 Cloudflare Workers（免费方案），
连接 GitHub 后 **push 就自动上线**。

```
public/index.html   整本手册（单一文件，无第三方库、无外部字体、无 CDN）
public/sw.js        Service Worker，让页面断网时也能打开
wrangler.jsonc      Cloudflare Workers 静态资源设定
package.json        只用来让 Cloudflare 装 wrangler
```

---

## 一次性设置（💻 必须在电脑上做）

1. **注册 / 登入 Cloudflare** — <https://dash.cloudflare.com>。免费方案就够，不用绑卡。
2. 左侧选 **Compute (Workers)** → **Create** → 切到 **Import a repository** 分页。
3. 点 **Connect GitHub**，会跳到 GitHub 安装 Cloudflare 的 App。
   授权范围选 **Only select repositories**，只勾 `annejo21/taipei-nov-2026`。
4. 回到 Cloudflare，选这个 repo，然后设定：

   | 栏位 | 填什么 |
   |---|---|
   | Project name | `taipei-nov-2026` |
   | **Branch to deploy** | `claude/taipei-travel-handbook-uqb7xs` |
   | Build command | 留空（或 `npm install`） |
   | Deploy command | `npx wrangler deploy` |
   | Root directory | 留空 |

   > **Branch 一定要选 `claude/taipei-travel-handbook-uqb7xs`**，这样每次更新都会自动上线，
   > 不需要再手动去 GitHub 点 Merge。

5. 点 **Create and deploy**，等 1–2 分钟。
6. 拿到公开网址，长得像 `https://taipei-nov-2026.<你的帐号>.workers.dev`
   —— 任何人点开就能看，不用登入、不用装 App。

之后每次内容更新，push 上去 30 秒内自动重新发布，**你不用再做任何事**。

## 可选（💻 电脑上）

- **自订网域**：Workers 专案 → Settings → Domains & Routes → Add Custom Domain。需要你自己有网域。

## 到台湾前（📱 手机上）

- 在**有网路时**先打开一次网址，让离线快取建立起来。
- Safari：分享 → 加入主画面 ／ Chrome：⋮ → 加到主屏幕。之后点图示就是全屏，跟 App 一样。

---

## 本机预览（可选）

```bash
npm install
npx wrangler dev      # http://localhost:8787
```

或直接用浏览器打开 `public/index.html`（Service Worker 在 `file://` 下不会启用，其余功能正常）。
