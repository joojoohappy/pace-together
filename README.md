# Pace Together 一起跑

> **當我們一起跑。** 在不同地方上班的朋友,約一個時間、一個目的,一起練。

<img src="docs/story.png" width="260" align="right" alt="Pace Together">

我跟朋友在不同的地方上班,下班時間也不一樣,但我們想一起訓練。每次揪團都要煩惱:在哪集合?哪條路車少?跑完要去哪吃?

Pace Together 讓你說「這次想練什麼」,它會依目的去評估條件,給你幾條路線,匯出到手錶或 Google 地圖就能跑。

- **⚡ 間歇跑**:找附近的標準跑道或公園環線,依你想跑的距離排課表(例如 4 × 800 m)
- **🎨 跑圖案**:愛心、貓咪、狗狗、星星、閃電,**輸入任何文字或 emoji 就畫出來**(2026、GO、TPE…),也可以**自己用手指畫**或**上傳一張圖**。照著路網排,算出形狀還原度,並**避開大馬路**
- **☕ 跑完喝咖啡 / 🍜 跑完吃東西**:看那個時間**終點附近有哪些店還開著**,把終點放在店最多的地方
- **🌿 輕鬆聊天跑 / 🏁 長距離**:經過公園或河濱,繞一圈回來
- **🤝 配速不同模式**:
  - **同一圈各跑各的**:繞同一個 1–2 km 的圈,一起開始、一起結束,列出每個人在時間內跑幾圈(快的人多跑、慢的人少跑)
  - **全程一起跑**:用最慢的人的配速(加上今天狀態)一起跑,每 2 km 一個等人點,可以選跑完去咖啡廳或吃東西

- **📣 跑步當天一鍵傳訊息**:「已抵達集合點」「我會晚 10 分鐘到」「請跑慢一點」「我需要補給」「請在終點等我」「我迷路了 / 我受傷了(附上目前位置)」……按一下就寫好,傳到 LINE / Messenger / WhatsApp 群組,鎖屏也收得到通知。還有計時,跑完自動算配速。

- **長度剛好**:每條路線都會自動縮放、重新排,直到跟你要的公里數差 0.5 km 以內(最多 1 km),差太多的不會出現

每條路線都會告訴你**為什麼選它**,並用「符合你的需求嗎?」列出:長度差多少、圖案還原度、車多程度、終點那時有沒有開的店,還有大家到集合點的距離。

> 「在 Google 地圖看整條路線」會把起點、終點和沿路約 8 個點交給 Google,用步行模式顯示幾乎一樣的路線(Google 偶爾會選不同的小路)。要一模一樣,請用 GPX:手錶可以直接帶路,或匯入 Google My Maps。「導航到集合點」只帶你到起點。

**👉 直接用:https://joojoohappy.github.io/pace-together/**

概念影片:[`docs/when-we-run.mp4`](docs/when-we-run.mp4)

## 免費、不用登入、不花 token

- **不用帳號**:打開網頁就能用。揪人只要丟一個分享連結,路線都存在連結裡,朋友點開就看得到。
- **路線規劃不靠 AI**:用的是開放地圖資料與免費服務,完全不花 token:
  - 地名 → [Nominatim](https://nominatim.org)(OpenStreetMap)
  - 公園、跑道、店家營業時間、大馬路 → [Overpass API](https://overpass-api.de)
  - 步行路線 → [FOSSGIS OSRM](https://routing.openstreetmap.de)(步行 profile)
  - 地圖 → [Leaflet](https://leafletjs.com) + CARTO 底圖
- **AI 是選配**:右上角「AI 設定」可以接任何 OpenAI 相容的 API(Google Gemini、Groq、OpenRouter 免費模型,或自己電腦上的 Ollama)。只用在兩件事:把一句話轉成設定(約 150 token)、幫推薦路線寫兩句介紹(約 300 token)。Key 只存在使用者自己的瀏覽器。沒設定時,「用一句話說」會用關鍵字解析,一樣能用。

## 部署(5 分鐘)

整個 App 就是一個 `index.html`,沒有後端。

**GitHub Pages**
1. 把這個資料夾推到 GitHub
2. Settings → Pages → Source 選「Deploy from a branch」,Branch 選 `main`、資料夾 `/ (root)`
3. 幾分鐘後就有 `https://<你的帳號>.github.io/<repo>/` 可以用

**其他**:Netlify Drop、Cloudflare Pages、Vercel 都可以直接丟資料夾。

要改用的服務,改 `index.html` 最上面的 `CONFIG`。

## 使用量與公共服務的規範

這個專案用的是社群提供的免費公共服務,請遵守它們的使用規範:

- Nominatim:每秒最多 1 次(程式已經自動排隊,並把查過的地名快取在瀏覽器)
- Overpass、FOSSGIS OSRM:適量使用。一次規劃大約 1 次 Overpass、3–6 次路線查詢
- 如果你的站流量很大,請自架 [OSRM](https://github.com/Project-OSRM/osrm-backend) / [Overpass](https://github.com/drolbr/Overpass-API) / [Nominatim](https://github.com/osm-search/Nominatim),或改用有免費額度的商用服務,然後改 `CONFIG`

## 隱私

- 沒有後端、沒有資料庫。輸入的內容只存在你自己的瀏覽器(localStorage)
- 分享連結裡**只留路線**;大家的出發地只保留到約 1 公里的精度
- 地名查詢會送到 Nominatim,路線查詢會送到 OSRM(都是 OpenStreetMap 社群的服務)

## 兩個版本

| | `index.html`(這個) | `claude-artifact/` |
|---|---|---|
| 需要帳號 | 不用 | 每個人都要 Claude 帳號 |
| 費用 | 免費 | 免費(AI 用各自的 Claude 額度) |
| 依目的規劃多條路線 | ✅ | AI 規劃一條 |
| 匯出 GPX / Google 地圖 | ✅ | ✅ |
| 一鍵狀態訊息 | ✅ 傳到 LINE 等群組 | ✅ 頁面內即時同步 |
| 計時 | ✅ | ✅ |
| 排行榜、紀念分享圖、照片牆 | — | ✅ |

## Roadmap

- [ ] 免費的即時同步(例如 Firebase 免費方案),讓網頁版也能「已抵達 / 請跑慢一點」
- [ ] 河濱自行車道優先的路線
- [ ] 天氣與日落時間

路線是自動產生的建議,出發前請確認路況與安全。歡迎開 issue 或 PR,改動請維持「單一 HTML、零營運成本」的原則。

## 維護

這是個人 side project,有空才更新,issue 和 PR 不保證回覆。想要的功能歡迎 fork 自己做。

## License

[MIT](LICENSE)。地圖資料 © OpenStreetMap 貢獻者(ODbL)。
