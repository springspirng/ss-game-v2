# 01-game-demo — Life need some BUG（可玩版）

推上 GitHub Pages 用手機玩的遊戲本體。

## 檔案

| 檔案 | 說明 |
|------|------|
| `index.html` | **遊戲本體**（Pages 首頁）。下樓玩法 + 翻轉通關。 |
| `spike.html` | M0 翻轉偵測診斷探針（備查用，數值/門檻校準）。 |

## 怎麼玩

1. 手機開 Pages 網址（見下），點 **▼ START**，允許感測器。
2. 進入 **5 秒倒數**——此時把手機**上下翻轉過來**，就會啟動隱藏的通關模式。
3. 倒數結束開始下樓：**點螢幕左 / 右半邊**控制左右移動，踩穩每一階平台。
   - 平台由 `t/u/r/n` 字母排成 → 拼出 **TURN**（提示你「轉」）。
   - 尖刺（天花板 `v` / 平台 `^`）會扣 life。
4. 若倒數時**沒翻轉** → 無盡下樓，樓層 `B1、B2…` 一直往下，永遠玩不完。
5. 若倒數時**翻轉了** → 畫面倒轉成上樓，樓層 `1F→…→69F`，**爬到 69F 通關**。

> 桌機測試：方向鍵移動；倒數時按 `F` 模擬翻轉。

## 翻轉判定（已依真機實測調校）

實測手拿翻轉夾角最多約 140°（達不到 180°），所以採**雙保險**：
主判定看「裝置 Y 軸重力符號相對基準是否反轉」（近乎二元、最可靠），
備援看「與基準夾角 > 120°」。詳見 `../Life need some BUG/02_技術可行性文件.md` §8。

## 部署 / 更新（GitHub Pages）

repo 已 `git init`。每次改完：

```bash
cd "/Users/spring/Documents/MDCG/Co_AI/26/01_swag_新竹工程師/preproduction/game-demo/01-game-demo"
git add -A && git commit -m "update game" && git push
```

首頁：`https://springspirng.github.io/s-g-demo1/`
（repo 需為 public 才能開免費 Pages；Settings → Pages → Source 選 main / root。）
