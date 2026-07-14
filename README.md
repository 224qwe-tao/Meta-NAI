# 圖片元數據提取器

這是可直接放到 GitHub Pages 的靜態網站版本，介面與 `html.txt` 及參考圖片一致。

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

## GitHub Pages 發佈

1. 建立 GitHub repository。
2. 將本資料夾內所有檔案上傳到 repository 根目錄。
3. 到 **Settings → Pages**。
4. 在 **Build and deployment** 選擇 **Deploy from a branch**。
5. Branch 選擇 `main`，資料夾選擇 `/ (root)`，然後儲存。

網站使用 CDN 載入 Tailwind CSS、pako、js-yaml 及 ExifReader，因此開啟網站時需要網絡連線。圖片只在瀏覽器本機處理，不會由此程式上傳到伺服器。
