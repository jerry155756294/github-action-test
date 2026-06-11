# Windows noVNC Remote Desktop via GitHub Actions

這是一個透過 GitHub Actions 啟動臨時 Windows 環境，並使用 noVNC 在瀏覽器中訪問的解決方案。

## 🎯 功能特點

- ✅ 在 GitHub Actions 上運行 Windows 環境
- ✅ 使用 TightVNC 作為 VNC 服務器
- ✅ 使用 noVNC 提供瀏覽器訪問
- ✅ 使用 ngrok 創建公開隧道
- ✅ 無需本地安裝任何軟件
- ✅ 最長可運行 6 小時

## 📋 系統架構

```
GitHub Actions (Windows Runner)
  ↓
TightVNC Server (Port 5900)
  ↓
websockify Proxy (Port 6080)
  ↓
ngrok Tunnel (HTTPS)
  ↓
Your Browser → noVNC Client
```

## 🚀 使用方法

### 步驟 1: Fork 或使用此倉庫

如果您還沒有此倉庫，可以直接使用或 fork 它。

### 步驟 2: (可選) 設置 ngrok Token

**注意**: 免費的 ngrok 可以工作，但有時間限制。建議設置 token 以獲得更好的體驗。

1. 前往 [ngrok 註冊頁面](https://dashboard.ngrok.com/signup) 創建免費帳戶
2. 在 [ngrok dashboard](https://dashboard.ngrok.com/get-started/your-authtoken) 獲取您的 auth token
3. 在 GitHub 倉庫中設置 Secret:
   - 前往 **Settings** → **Secrets and variables** → **Actions**
   - 點擊 **New repository secret**
   - Name: `NGROK_AUTH_TOKEN`
   - Value: 貼上您的 ngrok token

### 步驟 3: 運行 Workflow

1. 前往您倉庫的 **Actions** 標籤頁
2. 選擇左側的 **Windows noVNC Remote Desktop** workflow
3. 點擊右上角的 **Run workflow** 按鈕
4. 設置 VNC 密碼（建議 8 個字符以上）
5. 點擊綠色的 **Run workflow** 按鈕

### 步驟 4: 獲取訪問 URL

1. 等待 workflow 運行（大約 2-3 分鐘）
2. 點擊正在運行的 workflow job
3. 展開 **Get ngrok Public URL** 步驟
4. 複製顯示的 URL（格式類似：`https://xxxx.ngrok-free.app/vnc.html`）

### 步驟 5: 在瀏覽器中連接

1. 在瀏覽器中打開獲取到的 URL
2. 如果使用免費 ngrok，可能需要點擊 "Visit Site" 按鈕
3. 在 noVNC 界面中點擊 **Connect**
4. 輸入您設置的 VNC 密碼
5. 享受您的 Windows 遠程桌面！

## 🔧 技術細節

### 使用的組件

- **TightVNC**: 輕量級 VNC 服務器
- **noVNC**: HTML5 VNC 客戶端（在瀏覽器中運行）
- **websockify**: WebSocket 到 TCP 代理
- **ngrok**: 創建公開隧道以暴露本地端口

### 端口配置

- VNC Server: `5900`
- noVNC (websockify): `6080`
- ngrok API: `4040`

### 時間限制

- GitHub Actions 免費用戶: 單個 job 最長 6 小時
- ngrok 免費版: 隧道每 2 小時需要重新連接（但 workflow 會自動處理）

## ⚠️ 重要注意事項

1. **安全性**: 
   - 這個環境是臨時的，每次運行都是全新的
   - 不要在這個環境中處理敏感數據
   - 使用強密碼保護 VNC 連接

2. **資源限制**:
   - GitHub Actions 有[使用限制](https://docs.github.com/en/actions/learn-github-actions/usage-limits-billing-and-administration)
   - 不要濫用此服務

3. **停止會話**:
   - 使用完畢後，請在 GitHub Actions 頁面手動取消 workflow
   - 或等待 6 小時自動超時

## 🛠️ 故障排除

### 問題: ngrok URL 無法訪問

**解決方案**:
- 檢查是否正確設置了 `NGROK_AUTH_TOKEN`
- 查看 workflow 日誌中的錯誤信息
- 嘗試重新運行 workflow

### 問題: 連接後看不到桌面

**解決方案**:
- 確認 VNC 密碼輸入正確
- 等待幾秒鐘讓桌面完全加載
- 檢查瀏覽器控制台是否有錯誤

### 問題: noVNC 連接斷開

**解決方案**:
- 刷新瀏覽器頁面
- 檢查 workflow 是否仍在運行
- 確認網絡連接穩定

## 📚 相關資源

- [TightVNC 官網](https://www.tightvnc.com/)
- [noVNC GitHub](https://github.com/novnc/noVNC)
- [ngrok 文檔](https://ngrok.com/docs)
- [GitHub Actions 文檔](https://docs.github.com/en/actions)

## 🤝 貢獻

歡迎提交 Issues 和 Pull Requests！

## 📄 授權

此項目使用 MIT 授權。

## 🙏 致謝

感謝以下開源專案：
- noVNC 項目
- TightVNC 團隊
- ngrok 團隊
- GitHub Actions
