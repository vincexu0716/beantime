# beantime.app

豆时 BEANTIME 的对外站点，GitHub Pages 托管（CNAME → beantime.app）。

- `/` 产品首页（`index.html`）：按九张上架截图对应的功能分区
- `/privacy.html` 隐私政策
- `/support.html` 支持与帮助

后两个页面同时用作 App Store Connect 的「支持 URL」与「隐私政策 URL」。

## 图片

`img/` 里的界面图都来自模拟器实拍，统一按 1320×2868 的原始截图缩到高 1320（宽 607）后存 JPG：

| 文件 | 来源 |
|---|---|
| `home.jpg` / `detail.jpg` / `brew.jpg` / `score.jpg` / `stats.jpg` / `brand.jpg` / `wish.jpg` | `../上架截图-2026-11/raw/f1–f7` |
| `intake.jpg` / `scan.jpg` | 录入表单、豆卡识别结果页实拍（`CM_OPEN_INTAKE` / `CM_SCAN_DEMO=zh`） |
| `share-*.jpg` / `yearcard.jpg` | `../screenshots/cards/*.png`（App 内 `ShareCardGenerator` 渲染） |
| `og.jpg` | `../推广素材-2026-11/04_官网头图-1920x1080/02_og-1200x630.png` |

改界面后重出官网图的顺序：先在模拟器截图 → 覆盖 `../上架截图-2026-11/raw/` 对应文件 → 按下表重导 → 本地起服务看一眼。

```bash
# 单张：高 1320、JPG q84
sips -s format jpeg -s formatOptions 84 -Z 1320 ../上架截图-2026-11/raw/f1_home.jpg --out img/home.jpg

# 整页预览（Chrome 无头，桌面 1440 宽 / 移动 500 宽）
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new \
  --hide-scrollbars --window-size=1440,9600 --screenshot=/tmp/site.png "file://$PWD/index.html"
```

注意：无头 Chrome 的窗口宽度有 500px 下限，量手机版请用 500 宽渲染，不要用 390（会被裁切，看着像页面溢出）。
