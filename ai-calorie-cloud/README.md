# AI 熱量計算器｜雲端部署版

這是一個純靜態 HTML / JavaScript 專案，不需要 Node.js、後端或資料庫即可先部署使用。

## 專案檔案

- `index.html`：主程式
- `manifest.webmanifest`：PWA / 加入主畫面設定
- `sw.js`：基本離線快取
- `icon.svg`：網站 / PWA 圖示
- `data/taiwan_foods.json`：內建台灣食品熱量／主要營養資料（食藥署 2,161 筆＋臺大盤菜／自助餐熱量表 86 筆，共 2,247 筆）
- `vercel.json`：Vercel 靜態部署設定
- `.nojekyll`：GitHub Pages 靜態檔支援

## Vercel 部署

### 方法 1：從 GitHub 匯入
1. 建立 GitHub repository。
2. 將本資料夾全部檔案上傳到 repository 根目錄。
3. 在 Vercel 新增 Project，匯入該 repository。
4. Framework Preset 可使用 `Other` / 靜態網站。
5. 不需要 Build Command。
6. 部署完成後即可取得 HTTPS 網址。

### 方法 2：Vercel CLI
在此專案資料夾執行：

```bash
vercel
```

正式發布：

```bash
vercel --prod
```

## GitHub Pages 部署

1. 將本資料夾全部檔案放在 repository 根目錄。
2. 到 repository 的 `Settings > Pages`。
3. `Build and deployment` 選 `Deploy from a branch`。
4. Branch 選 `main`，資料夾選 `/ (root)`。
5. 儲存後等待 Pages 網址產生。

## 手機使用

網站部署成 HTTPS 後，可直接以 Safari / Chrome 開啟。
瀏覽器支援時可使用「加入主畫面」，以接近 App 的方式啟動。

## 目前資料保存方式

目前飲食紀錄、個人設定是使用瀏覽器 `localStorage` 保存。

這代表：
- 同一瀏覽器再次開啟網站，資料通常仍在。
- 換手機、換電腦或清除網站資料後，不會自動同步。
- 若下一版需要跨裝置同步，建議加入登入與 Supabase / Firebase 等雲端資料庫。

## 台灣食品熱量／營養資料庫

本版已內建 `data/taiwan_foods.json`，頁面啟動後會自動載入 2,247 筆台灣食品／餐點資料，不需要使用者先下載資料。其中包含食藥署 2,161 筆，以及國立臺灣大學膳食協調委員會「熱量表【盤菜、自助餐類】」86 筆。主要可查詢：

- 熱量／修正熱量
- 蛋白質、脂肪、碳水化合物
- 膳食纖維、糖、飽和脂肪、反式脂肪
- 鈉、鉀、鈣、磷、鎂、鐵、鋅等
- 部分維生素資料

資料來源對應衛生福利部食品藥物管理署「食品營養成分資料集」（政府資料開放平臺資料集 8543 / InfoId 20），授權方式為「政府資料開放授權條款-第1版」。

另收錄國立臺灣大學膳食協調委員會熱量表：https://meals.ntu.edu.tw/CampusDining/kcal/buffets 。該頁共收錄主食 4、主菜 30、副菜 27、青菜 25 筆（合計 86 筆）。主食依頁面列示份量換算並保留原始份量，其餘三類依頁面 100g 基準儲存。臺大資料僅提供熱量時，其他未提供的營養素在介面顯示為「—」，避免誤示為 0。

網頁仍保留官方更新功能：
- 下載官方新版資料
- 匯入官方 JSON / ZIP
- 線上更新官方資料

若官方資料更新，可用上述功能覆蓋本次瀏覽工作階段中的內建資料；若線上更新受跨網域政策阻擋，內建資料庫仍可照常使用。
