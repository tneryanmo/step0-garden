# 花園寫作規範（GARDEN-GUIDE）

> 這份是給寫作者（Ryan＋AI）看的，不會發佈到網站。
> 網站只吃 `content/`，repo 根目錄的檔案不會上站。

## Vault 在哪

Obsidian 開這個資料夾當 vault：

```
step0-garden/content/
```

`.obsidian/` 設定會落在裡面，Quartz 已設定忽略它，不會發佈、不用管。

## 新增一篇

1. 檔名用英文 slug，如 `psychology/shame.md`（決定網址，不事後改）。
2. 放進對應資料夾：`psychology/` 心理、`philosophy/` 哲學、`experiments/` 實驗。
3. Frontmatter 從這個範本抄：

```md
---
title: 中文標題
tags:
  - 心理
date: 2026-10-12
---
```

## 生長狀態（重要）

內文**第一行**標狀態，格式抄現有筆記：

- 🌱 種子 seedling：潦草、可能錯 → 第一行 `🌱 種子｜潦草，可能錯。`，frontmatter 加 `unlisted: true`
- 🌿 萌芽 budding：有結構、連了 2 篇以上 → 第一行 `🌿 萌芽｜這篇還在長，最後更新 YYYY-MM-DD。`，**拿掉** `unlisted`
- 🌳 長青 evergreen：穩定、可引用 → 第一行 `🌳 長青。`，無 `unlisted`

`unlisted: true` 的效果：不進 sitemap（不推給 Google），但站內 graph 照樣看得到。
seedling 想升級：內容長好＋連好 2 篇 → 換首行＋刪 `unlisted` → 改 `date` 為當天。

## 連結習慣

- 一篇只講一個想法，看到關連就用 `[[slug|顯示文字]]` 連，如 `[[psychology/fear|恐懼]]`。
- 同資料夾可短寫 `[[fear|恐懼]]`，跨資料夾寫全路徑。
- 每篇至少連 1–2 篇，不要寫孤島。斷掉的 `[[ ]]` 會顯示斷鏈樣式＋build warning，不破版。
- 連回主站用完整 URL，如 `[網誌定稿](https://step0.club/blog/stability-trap)`。

## 發佈（2026-10-12 更新：push 不會自動部署）

Cloudflare 這顆 Worker 沒有接 Git 自動 build（push 到 v5 不會觸發），
要用 wrangler 從本機直推。第一次先登入（會開瀏覽器）：

```bash
npx wrangler login
```

之後每次發佈（內容或樣式）：

```bash
npx quartz build && npx wrangler deploy
```

等 dashboard 顯示 Ready → 到 `https://step0.club/garden/` 看成品。
想省部署次數就攢多篇一次推（一次 deploy＝一次版本）。

## 不要動的東西

- `quartz.config.yaml` 的 `baseUrl: step0.club/garden`、`locale: zh-TW`（動了全站掛掉，先問再改）。
- `content/index.md` 是花園首頁，大改前先討論。
- 圖片：能少用就少用；要用就放 `content/attachments/`，內文用 `![[...]]` 引用。
