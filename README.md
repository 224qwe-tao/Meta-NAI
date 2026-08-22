# 圖片元數據提取器

這是可直接放到 GitHub Pages 的靜態網站版本，介面維持原有設計，並已加入 **NovelAI Diffusion V5** 元數據支援。

## 支援的 NovelAI 版本

- NovelAI Diffusion V3
- NovelAI Diffusion V4 / V4 Curated
- NovelAI Diffusion V4.5 / V4.5 Curated
- NovelAI Diffusion V5 Full
- NovelAI Diffusion V5 Curated
- 對未來可能更換 model hash 的 V5 圖片保留通用 `NovelAI Diffusion V5` 辨識

## V5 更新內容（2026-08-22）

- 保留 NovelAI 官方目前使用的 `stealth_pngcomp` Alpha-LSB 元數據提取方式。
- 讀取 V5 新增／使用的 `model_name`、`model_hash`、`request_type`、`quality_boost`、`tag_hint_transparent_background` 等欄位。
- 辨識 V5 Full / Curated，並在格式化結果顯示 V5 型號與 model hash。
- 支援 V5 的自由角色定位座標。V5 不再只限舊式 5×5 位置網格，因此角色 `c` 方塊會顯示實際 X/Y 百分比位置。
- 自由定位座標只作畫面提示，不會改寫 `c=` 的原始提示詞，避免影響「复制」結果。
- 改善 PNG Text fallback：當 Alpha-LSB metadata 遺失／受損時，會嘗試重用普通 PNG Text Chunk 的 `Source`、`Description`、`Comment` 等資料。
- 舊版 V3 / V4 / V4.5 的格式化和方塊顯示維持相容。

目前程式內包含發佈時觀察到的 V5 model hash 對應：

- `0ADF9AB7` → V5 Full
- `DB276663` → V5 Curated

即使日後 NovelAI 更新 V5 model hash，只要 `Source` 或 `model_name` 仍標示為 `NovelAI Diffusion V5`，提取器仍會識別為 V5，而不會錯誤退回 NAI3。

## 保留功能

- 選擇多張圖片
- 拖放圖片
- 貼上圖片
- 支援 PNG、JPG/JPEG、WEBP
- 優先讀取 NovelAI `stealth_pngcomp` LSB 元數據
- 顯示 AI 繪圖機器人指令
- 使用不同顏色方塊分開顯示 `prompt`、`c`、`uc` 和 `ntags`
- 每個提示詞方塊均有獨立「复制」按鈕，會連同 `prompt=`、`c=`、`uc=` 或 `ntags=` 前綴複製
- 多行角色提示詞會完整保留在同一個 `c` 方塊，配對的 `uc` 會獨立顯示
- 原始 JSON 預設完全折疊，按「显示全部」才展開完整內容
- 顯示及複製原始 JSON
- 最新結果顯示在上方
- 清空所有結果

## 已移除的額外功能

- Pixiv URL／用戶作品抓取
- Cloudflare Worker／代理設定
- 作品數量限制及掃描控制
- 下載全部圖片
- 匯出結果 JSON
- 執行記錄及額外統計面板

## 驗證

V5 更新已以 NovelAI 官方 V5 發佈頁面的多張原始 PNG 樣本進行 metadata 解析測試，確認可讀取：

- `Source: NovelAI Diffusion V5 ...`
- `model_name`
- `model_hash`
- Prompt / Negative Prompt
- Sampler / Steps / Scale / CFG Rescale / Noise Schedule / Seed
- `v4_prompt` / `v4_negative_prompt` 中的 Character Prompt
- V5 自由 Character Positioning 座標

## GitHub Pages 發佈

1. 建立 GitHub repository。
2. 將本資料夾內所有檔案上傳到 repository 根目錄。
3. 到 **Settings → Pages**。
4. 在 **Build and deployment** 選擇 **Deploy from a branch**。
5. Branch 選擇 `main`，資料夾選擇 `/ (root)`，然後儲存。

網站使用 CDN 載入 Tailwind CSS、pako、js-yaml 及 ExifReader，因此開啟網站時需要網絡連線。圖片只在瀏覽器本機處理，不會由此程式上傳到伺服器。
