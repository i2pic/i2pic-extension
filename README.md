# i2pic — Local Image Converter

> 17 种图片格式转换器，全部在浏览器本地完成，**不上传、不注册、不追踪**。

[Homepage](https://www.i2pic.com) · [Chrome Web Store](#) · [Report Issue](https://github.com/haskx/i2pic-extension/issues) · [Privacy Policy](./PRIVACY.md)

![i2pic](./public/icons/icon-128.png)

---

## 这是什么

i2pic 是一个浏览器扩展，把 17 个常用图片格式转换器装进一个 toolbar 弹窗。所有转换都在你的设备上通过 WebAssembly、Canvas 和浏览器内置解码器完成——你的图片字节从未离开过本机。

## 核心特性

- **17 个转换器**：HEIC / TIFF / JFIF / ICO / EPS / WebP / SVG / DNG / HTML / MP4 全覆盖
- **三个入口**：
  1. 工具栏图标 → 弹出 popup，拖拽文件转换
  2. 右键网页图片 → 上下文菜单**自动按原格式筛选**，只显示能用的工具
  3. 鼠标悬停任意图片 → 浮动按钮，弹出针对该格式的快捷 picker
- **真·本地**：无网络请求、无账号、无分析、无第三方脚本
- **专业能力**：
  - 多尺寸 ICO favicon（16/32/48/64/128/256 一键生成）
  - 多页 TIFF → PNG（每页一张）
  - WebP 透明通道保留
  - WebP → SVG 矢量追踪
  - 多帧输出 ZIP 打包下载

## 转换器清单

| Slug | From → To | 输入扩展名 |
|---|---|---|
| `heif-to-jpg` | HEIF → JPG | .heic .heif |
| `webp-to-jpg` | WebP → JPG | .webp |
| `webp-to-png` | WebP → PNG | .webp |
| `webp-to-ico` | WebP → ICO | .webp |
| `webp-to-pdf` | WebP → PDF | .webp |
| `webp-to-svg` | WebP → SVG | .webp |
| `tiff-to-png` | TIFF → PNG | .tif .tiff |
| `jfif-to-png` | JFIF → PNG | .jfif .jpg .jpeg |
| `ico-to-png` | ICO → PNG | .ico |
| `html-to-png` | HTML → PNG | .html .htm |
| `eps-to-png` | EPS → PNG | .eps .ps |
| `svg-to-jpg` | SVG → JPG | .svg .svgz |
| `dng-to-jpg` | DNG → JPG | .dng |
| `mp4-to-webp` | MP4 → WebP | .mp4 .m4v .webm .mov |
| `webp-compress` | WebP 压缩 | .webp |
| `jpg-compress` | JPG 压缩 | .jpg .jpeg |
| `heic-viewer` | HEIC 预览 | .heic .heif |

## 安装

### 方式一：从 Chrome Web Store 安装（推荐普通用户）

发布后从商店一键安装（链接见顶部）。

### 方式二：加载已解压的扩展程序（开发者 / 内测）

1. 克隆仓库并构建：
   ```bash
   git clone https://github.com/haskx/i2pic-extension.git
   cd i2pic-extension
   pnpm install
   pnpm build
   ```
2. 打开 Chrome → 地址栏输入 `chrome://extensions`
3. 右上角打开 **开发者模式**
4. 点 **加载已解压的扩展程序** → 选择仓库下的 `dist/` 目录
5. 工具栏出现 i2pic 图标，完成

详细步骤见 [LOAD-EXTENSION.md](./LOAD-EXTENSION.md)。

## 使用

### 工具栏弹窗

点工具栏的 i2pic 图标 → 弹出 popup：
- 顶部下拉选择转换器（17 种）
- 拖拽文件到中央虚线区，或点 **Pick files** 选择
- 自动转换 → 点单个 **Download** 或顶部 **Download all as ZIP**

### 右键网页图片

在任意网页的图片上右键 → 上下文菜单出现：
- `Convert with i2pic · WebP → JPG`（仅显示与该图片格式匹配的工具）
- `Convert with i2pic · WebP → PNG`
- ...
- `Open i2pic Converter`（兜底，打开完整 popup）

> 菜单按图片 URL 扩展名自动筛选，无扩展名 / data URL 时只显示兜底项。

### 悬停浮动按钮

鼠标悬停任意 `<img>` → 左上角出现 `⬇ i2pic · Convert` 徽章 → 点击弹出 picker：
- 头部显示检测到的原格式：`Convert with i2pic · .webp`
- 列出该格式可用的所有转换器
- 底部 `更多工具` 行兜底打开完整 popup

## 开发

### 环境要求

- Node.js ≥ 20
- pnpm ≥ 10（`corepack enable` 自动启用）
- Chrome ≥ 116（MV3 + offscreen API 要求）

### 常用命令

```bash
pnpm install        # 安装依赖
pnpm build         # 类型检查 + 生产构建到 dist/
pnpm dev           # watch 模式构建，改完代码自动重建
pnpm typecheck     # 只跑 tsc 类型检查
pnpm lint          # eslint 检查
```

### 开发循环

```bash
pnpm dev           # 终端 1：watch 构建
# 终端 2 不需要，去 chrome://extensions 点扩展卡片右下角 ↻ 刷新即可应用新代码
```

### 项目结构

```
i2pic-extension/
├── public/                  # 静态资源（构建时拷贝到 dist）
│   ├── manifest.json        # MV3 清单
│   ├── popup.html           # popup 入口 HTML
│   ├── offscreen.html       # offscreen document 入口
│   └── icons/               # 16/32/48/128 应用图标
├── src/
│   ├── background/          # Service worker（右键菜单、消息桥）
│   │   └── index.ts
│   ├── content/             # Content script（悬停徽章 + picker）
│   │   └── index.ts
│   ├── popup/               # React popup UI
│   │   ├── App.tsx
│   │   ├── main.tsx
│   │   ├── index.html
│   │   └── styles.css
│   ├── offscreen/           # Offscreen document（重型解码预留）
│   │   ├── index.html
│   │   └── index.ts
│   ├── core/
│   │   ├── catalog.ts       # 17 个工具的元数据
│   │   └── engines.ts       # 转换器实现
│   ├── lib/
│   │   └── utils.ts         # cn / formatBytes 等
│   └── global.d.ts          # 全局类型声明
├── assets/store/            # Chrome Web Store 提交素材
│   ├── promo-small.jpg      # 440×280
│   ├── promo-large.jpg      # 920×680
│   ├── promo-marquee.jpg    # 1400×560
│   └── screenshot-{1,2,3}.jpg  # 1280×800
├── PRIVACY.md               # 隐私政策
├── LOAD-EXTENSION.md        # 加载步骤
└── package.json
```

### 添加新转换器

1. 在 `src/core/catalog.ts` 的 `TOOLS` 数组里加一项：
   ```ts
   {
     slug: 'foo-to-bar',
     from: 'FOO',
     to: 'BAR',
     keyword: 'foo to bar',
     category: 'Your / Category',
     tagline: 'Convert FOO to BAR.',
     engine: 'browser',
     acceptExt: '.foo',
   }
   ```
2. 在 `src/core/engines.ts` 实现 `fooToBar(file: File)` 并注册到 `CONVERTERS`：
   ```ts
   export async function fooToBar(file: File): Promise<ConvertResult[]> {
     // ... 解码 + 编码逻辑
     return [{ blob, name, width, height }]
   }

   export const CONVERTERS: Record<string, Converter> = {
     // ...
     'foo-to-bar': (file) => fooToBar(file),
   }
   ```
3. `pnpm build` → `chrome://extensions` 点 ↻ 刷新扩展即可生效。

右键菜单和悬停 picker 会自动按 `acceptExt` 把新工具加进去，无需改 background / content。

## 隐私

i2pic 不收集、不传输、不存储任何用户数据。所有图片处理都在浏览器内完成。详见 [PRIVACY.md](./PRIVACY.md)。

## 第三方库（全部打包，全部本地运行）

- [heic2any](https://github.com/alexcorvi/heic2any) — HEIC/HEIF 解码
- [UTIF.js](https://github.com/photopea/UTIF.js) — TIFF 解码
- [imagetracerjs](https://github.com/jankovicsandras/imagetracerjs) — 位图 → SVG 矢量追踪
- [modern-screenshot](https://github.com/qq15725/modern-screenshot) — HTML → PNG 渲染
- [fflate](https://github.com/101arrowz/fflate) — ZIP 打包
- [lucide-react](https://lucide.dev)、[sonner](https://sonner.emilkowalski.dev/)、[clsx](https://github.com/lukeed/clsx)、[tailwind-merge](https://github.com/dcastil/tailwind-merge) — UI 辅助

## 浏览器支持

| 浏览器 | 最低版本 | 备注 |
|---|---|---|
| Chrome | 116+ | MV3 + offscreen API 要求 |
| Edge | 116+ | 同上 |
| Arc | 基于 Chromium 116+ | 同上 |
| Brave / Opera / Vivaldi | 同 Chromium 116+ | 同上 |

> Firefox / Safari 暂不支持（manifest 用了 MV3 + Chrome 专有 API 如 offscreen）。

## 联系

- **主页**：[www.i2pic.com](https://www.i2pic.com)
- **Issues**：[github.com/haskx/i2pic-extension/issues](https://github.com/haskx/i2pic-extension/issues)
- **邮箱**：support@i2pic.com

## License

MIT License © 2026 [i2pic](https://www.i2pic.com). See [LICENSE](./LICENSE) for details.

> License 文件需自行创建。如需采用其他协议（Apache-2.0 / GPL-3.0 等），替换此段并新增对应 LICENSE 文件即可。
