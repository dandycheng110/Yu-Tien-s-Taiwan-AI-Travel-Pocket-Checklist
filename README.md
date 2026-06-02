# 🧳 沉浸式旅遊行程展示網站 · Immersive Travel Itinerary Showcase

> 一個**單檔、零建置**的沉浸式旅遊行程網站範本。首頁是一格格的行程卡，點任一張就走進那趟旅程 —— 全螢幕 Hero、隨滾動展開的動態時間軸、毛玻璃站點卡與「一鍵帶走行程」。把行程與照片換成你自己的，幾分鐘就能上線。

<p>
  <img alt="HTML" src="https://img.shields.io/badge/HTML-single--file-E34F26?logo=html5&logoColor=white">
  <img alt="GSAP" src="https://img.shields.io/badge/GSAP-ScrollTrigger-88CE02?logo=greensock&logoColor=white">
  <img alt="No Framework" src="https://img.shields.io/badge/framework-none-555">
  <img alt="No Build" src="https://img.shields.io/badge/build-none-44cc88">
  <img alt="Deploy" src="https://img.shields.io/badge/deploy-Vercel-black?logo=vercel">
</p>

---

## ✨ 特色

- **行程卡首頁** — 響應式卡片網格（手機 2 / 平板 3 / 桌機 4 欄）；每張卡有專屬封面、地區標籤與站點數，hover 浮起、封面緩緩放大。
- **沉浸式行程頁** — 點卡進入：全螢幕 Hero（標題分行揭開 + 背景視差）、動態時間軸（進度條隨滾動填滿、節點左右交錯淡入）、底部行動呼籲。
- **資料驅動** — 所有內容集中在一個 `trips` 陣列，卡片與內頁全部自動生成；新增一趟旅程只要加一個物件，版面完全不用動。
- **一鍵帶走** — 「匯入行程」把該趟行程複製到剪貼簿；「在地圖上開啟」連到 Google Maps 路線。
- **單檔・零依賴** — 一支 `index.html` 就能跑，動畫由 CDN 載入的 GSAP 處理，沒有打包步驟、不需 Node。
- **無障礙友善** — 尊重系統「減少動態效果」設定，會自動關閉動畫。

> 📦 本範本內建一份**示範清單（8 趟台灣行程 + 暫用照片）**，可直接當起點，逐步替換成你自己的內容。

## 🛠️ 技術

| 類別 | 使用 |
|------|------|
| 核心 | 原生 HTML / CSS / JavaScript（無框架、無建置） |
| 動畫 | [GSAP](https://gsap.com) + ScrollTrigger（cdnjs CDN） |
| 字型 | Google Fonts — Noto Sans TC / Noto Serif TC / Bebas Neue |
| 地圖 | Google Maps 導航連結 |
| 圖片 | 預設為 Wikimedia Commons 暫用圖（可換成自有照片） |

## 📁 專案結構

```text
your-repo/
├── index.html        # 主程式（單檔:HTML + CSS + JS + 資料）
├── images/           # 你的照片放這裡（可選）
│   ├── hsinchu-cover.jpg
│   └── ...
└── README.md
```

## 🚀 本機預覽

最簡單：直接用瀏覽器開 `index.html`。
若想用本機伺服器（避免少數相對路徑問題）：

```bash
python3 -m http.server 8000   # 或 npx serve
# 打開 http://localhost:8000
```

## ✏️ 自訂你的版本

### 1. 改品牌名稱
打開 `index.html`，把這四處的文字換成你的站名（預設為示範用標題）：

| 位置 | 說明 |
|------|------|
| `<title>…</title>` | 瀏覽器分頁／分享標題 |
| `<h1 class="lib__title">…</h1>` | 首頁大標 |
| `<footer class="lib__foot">…</footer>` | 頁尾 |
| JS 內 `const text = \`…\`` | 「匯入行程」複製出的文字 |

### 2. 新增 / 編輯行程
所有內容都在 `index.html` 上方的 `trips` 陣列。每趟是一個物件，每個站點是 `plan` 裡的一筆：

```js
const trips = [
  {
    region: '新竹',                              // 卡片角落的地區標籤
    theme: '放空 · 海線',                         // 卡片副標小字
    hours: '6 小時',                              // 預估時長
    titleLines: ['新竹海線', '放空之旅'],          // Hero 大標（分兩行）
    sub: '把腦袋交給海風,沿著海岸線慢慢放空的一天。', // Hero 副標
    q: '新竹南寮漁港',                             // 「地圖」鈕的 Google Maps 搜尋字
    dir: 'https://www.google.com/maps/dir/?api=1&origin=…', // 選填:完整路線(不填則用 q 搜尋)
    cover: 'images/hsinchu-cover.jpg',            // 卡片封面 + Hero 大圖
    hero:  'images/hsinchu-hero.jpg',             // 選填:Hero 想用不同圖才填(沒填用 cover)
    c1:'#0f2d44', c2:'#c07a3e', c3:'#eab35a',     // 漸層三色(沒放圖時的底色)
    glow:'rgba(255,235,180,.55)', accent:'#f0b54e', // 光暈色、強調色
    plan: [                                       // ── 時間軸站點 ──
      {
        t:'14:00',                                // 時間
        d:'60 min',                               // 停留時間
        title:'十八尖山',                          // 站名
        hook:'先讓腦袋降溫',                        // 一句亮點
        tag:'森林',                                // 標籤
        img:'images/hsinchu-1.jpg',               // 該站照片(選填)
        desc:'平緩的城市森林步道,沿途有水站與樹蔭。' // 說明
      },
      // …更多站點
    ]
  },
  // …更多行程
];
```

### 3. 換照片
`cover`、`hero`、`plan[].img` 三個欄位皆可不填（不填就用漸層底色）。把照片放進 `images/` 後，將欄位改成 `images/你的檔名.jpg` 即可。
建議尺寸：封面／Hero 約 **1600×1000**、站點圖約 **1200×900**，壓到 **300KB** 內（[squoosh.app](https://squoosh.app)），用 `.jpg` 或 `.webp`。載入失敗會自動退回漸層，不會壞版。

### 4. 調整卡片欄數
在 CSS 的 `.grid` 把 `grid-template-columns: repeat(4, 1fr)` 的數字改掉即可（含各斷點）。

### 5. 調整配色
每趟的 `c1 / c2 / c3 / glow / accent` 控制該趟的漸層與主色，改色碼就能換整頁氛圍。

## ☁️ 部署到 GitHub + Vercel

1. 確認主檔名為 `index.html`。
2. 在 [GitHub](https://github.com) 建立 repository → **Add file → Upload files**，把 `index.html` 與 `images/` 一起上傳並 Commit。
3. 到 [Vercel](https://vercel.com) 用 GitHub 登入 → **Add New… → Project** → 匯入該 repo → **Deploy**（純靜態，無需設定）。
4. 取得 `your-name.vercel.app`；之後每次 push，Vercel 會自動重新部署。

> 也可用 GitHub Pages：Settings → Pages → 選 `main` 分支根目錄即可。

## 🙏 圖片來源與授權

範本預設的照片為**暫用示意圖**，取自 [Wikimedia Commons](https://commons.wikimedia.org)，多為 CC 授權（部分需標示作者，詳見各圖檔頁面）。**正式公開前，建議全部替換為自有或自行授權的照片**，即可免除標示問題。

## 📄 授權

- 程式碼：MIT License（可自由使用、修改、再散布）
- 圖片：依各自來源授權（見上）

---

<sub>Made with ☕ + GSAP · a single-file, no-build immersive travel itinerary template</sub>
