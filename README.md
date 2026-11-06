# A2O 知識問答小助手

單頁 HTML 實作的知識問答機器人，基於 A2O（虛構）公司六份內部文件，以 **Groq API** 回答。

> ⚠️ 練習用專案：所有公司、人名、電話、Email、產品資料皆為程式產生的**虛構假資料**，與任何真實公司或個人無關（屬《智慧行政與行銷業務全方位AI應用實戰班》練習包）。

## 功能

- 🔒 使用前需輸入自己的 **Groq API Key**（[console.groq.com/keys](https://console.groq.com/keys) 免費申請）
  - Key 只存在你的瀏覽器（可選記住），由瀏覽器直接呼叫 Groq，不經過其他伺服器
- 📚 知識庫（6 份，內嵌於頁面）：
  - 新人須知 2026 版（現行）
  - 新人須知 2024 版（已停用——陷阱文件，測試時注意是否誤用）
  - 報價流程 / 退換貨辦法
  - 產品母稿（WH-12，對外說法標準）
  - 客服 Q&A 精選（40 筆客服紀錄整理）
- 🔎 內建關鍵字檢索（bigram + unigram 評分），只把相關段落餵給模型
- 📄 回答附「參考依據」文件標籤；知識庫沒有的會老實說不知道
- 🎛 可切換模型：`openai/gpt-oss-120b`（預設）、`gpt-oss-20b`、`qwen/qwen3.8-27b`
  - ⚠️ Llama 系列（llama-3.3-70b-versatile 等）自 2026-08 起為 Groq Enterprise 限定，免費帳號不可用

## 使用

1. 打開 `index.html`（或 GitHub Pages 網址）
2. 輸入 Groq API Key → 驗證 → 開始問答
3. 試問：
   - 「業務最多能打幾折？」（須回答牌價 95 折，不是 9 折）
   - 「TC-40 收貨 10 天能退嗎？」（須依 14 天規定，不是 7 天）
   - 「SC-800 有 E-Mark 嗎？」（只能說目前沒有，不可承諾時間）
   - 「今天台中天氣如何？」（應老實說查不到）

## 架構

純前端、零後端：

```
使用者輸入 → 頁內檢索（找出相關段落）→ 組成 system prompt
   → fetch api.groq.com/chat/completions → 顯示回答 + 參考文件
```

## 放到 GitHub

1. 建 Repository（例如 `a2o-qa`），把本資料夾的 `index.html`、`README.md` 上傳
2. Settings → Pages → Source 選 `main` / `root`→ Save
3. 網址即為 `https://<你的帳號>.github.io/a2o-qa/`

> 安全提醒：此頁面不含任何硬編碼 Key，Key 由使用者自行輸入、存瀏覽器 localStorage。**不要**把任何 `.env` 或含 key 的檔案上傳到公開倉庫。
