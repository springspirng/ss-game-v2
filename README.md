# M0 · 翻轉偵測探針

> Life need some BUG 專案的技術探針。**不是遊戲**，只驗證一件事：
> 「相對翻轉偵測」在真機上，正拿 / 反拿當基準都準不準。

## 這頁在測什麼

1. **iOS 感測器授權流程**：點 ▼ START 觸發 `requestPermission()`。
2. **即時感測器讀值**：orientation(β/γ/α)、gravity(x/y/z)、screen.orientation。
3. **相對翻轉判定（核心）**：先校準基準 `gRef`，再算「目前重力向量與基準的夾角」，接近 180° 判定為翻轉。
4. **5 秒倒數模擬**：重現遊戲的啟動窗口——倒數開始擷取基準，窗口內翻轉 → 顯示「啟動成功」。
5. **門檻 / 去抖可調**：現場拉 slider 找出最佳參數。
6. **桌機備援**：按空白鍵或「模擬翻轉」按鈕，無感測器也能測流程。

## 怎麼測（手機）

1. 開啟 GitHub Pages 網址（見下）。
2. 點 **▼ START**，允許感測器。
3. **正拿手機**點「校準並開始 5 秒倒數」→ 倒數內把手機上下翻過來 → 應顯示 `FLIP 已偵測 ✓` 與「啟動成功」。
4. **反拿手機**（一開始就倒著拿）重複步驟 3 → 一樣要能偵測到翻轉。這是本探針最關鍵的驗證點。
5. 把下方「紀錄」用「複製紀錄」貼回來，就能一起校準門檻與去抖時間。

## 部署到 GitHub Pages

把 `index.html` 放進 repo 根目錄後：

```bash
# 在你 clone 好的 s-g-demo1 資料夾裡
git add index.html README.md
git commit -m "add M0 flip-detection spike"
git push origin main
```

然後到 GitHub repo → **Settings → Pages** →
Source 選 `Deploy from a branch` → Branch 選 `main` / `/ (root)` → Save。

約一分鐘後網址會是：

```
https://springspirng.github.io/s-g-demo1/
```

> ⚠️ 感測器 API 一定要 HTTPS，`github.io` 天生是 HTTPS，所以手機開這個網址就能測。
> 本機直接開 `index.html`（file://）**收不到 iOS 感測器**，請務必用 Pages 網址或 `localhost`。

## 判讀重點

- 正拿、反拿兩種基準，翻轉時夾角都應衝到 ~180° 並穩定觸發。
- 若某機種 `devicemotion` 沒有重力值，頁面會自動改用 orientation 推導（事件狀態列會標示），比較兩者穩定度。
- 記下每支機的：能不能觸發、延遲感、最佳門檻/去抖 → 回填到 `../Life need some BUG/02_技術可行性文件.md` 的實驗清單。
