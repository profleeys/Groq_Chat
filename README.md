# Streamlit + Groq API AI Chatbot

使用 **Streamlit** 建立網頁聊天介面，透過 **Groq API** 呼叫大型語言模型，實作簡單的生成式 AI 多輪對話應用。

目前程式使用的模型為 `openai/gpt-oss-120b`。

## 功能特色

- **互動式聊天介面**：使用 Streamlit 的 `st.chat_input` 與 `st.chat_message`。
- **多輪對話**：將目前工作階段的聊天紀錄一併傳送給模型，讓回覆能參考先前內容。
- **聊天紀錄管理**：利用 `st.session_state` 保存目前工作階段的訊息。
- **新聊天**：按下「新聊天」按鈕即可清除目前的聊天紀錄。
- **API 錯誤處理**：在 API 呼叫失敗時顯示錯誤資訊。

## 使用技術

- Python
- [Streamlit](https://streamlit.io/)
- [Groq API](https://console.groq.com/)
- 模型：`openai/gpt-oss-120b`

## 專案結構

```text
.
├── groq_chat.py     # Streamlit 聊天應用程式
└── README.md        # 專案說明文件
```

## 安裝與執行

### 1. 下載專案

將專案從 GitHub 下載或使用 `git clone`，並進入專案資料夾。

### 2. 安裝必要套件

建議使用 Python 虛擬環境，然後執行：

```bash
pip install streamlit groq
```

### 3. 取得 Groq API Key

前往 [Groq Console](https://console.groq.com/keys) 建立 API Key。

程式中的 `Groq()` 會讀取環境變數 `GROQ_API_KEY`，請在執行前設定。

**Windows PowerShell：**

```powershell
$env:GROQ_API_KEY="your_groq_api_key"
```

**Windows CMD：**

```cmd
set GROQ_API_KEY=your_groq_api_key
```

**macOS / Linux：**

```bash
export GROQ_API_KEY="your_groq_api_key"
```

請將 `your_groq_api_key` 替換為自己的金鑰。**不要將真實 API Key 寫入程式或上傳至 GitHub。**

### 4. 啟動應用程式

```bash
streamlit run groq_chat.py
```

啟動後，在瀏覽器開啟 Streamlit 顯示的本機網址（通常為 `http://localhost:8501`）。

## 使用方式

1. 在聊天輸入框輸入問題。
2. 程式將目前的對話紀錄傳送給 Groq API。
3. 模型生成回覆後，介面會顯示使用者訊息與 AI 回應。
4. 可以繼續提問，進行多輪對話。
5. 按下「新聊天」即可清空目前工作階段的對話紀錄。

## 模型設定

目前 `groq_chat.py` 中的 API 呼叫設定如下：

```python
completion = client.chat.completions.create(
    model="openai/gpt-oss-120b",
    messages=messages,
    temperature=0,
    max_completion_tokens=1024,
    top_p=0.5,
    stream=False,
    stop=None,
)
```

可以依 Groq 平台實際提供的模型及帳號權限調整 `model`。模型供應、額度與速率限制可能變動，請以 [Groq 官方文件](https://console.groq.com/docs/models) 為準。

## 注意事項

- 需要網路連線與有效的 Groq API Key。
- 對話紀錄保存在 Streamlit 的工作階段狀態中，並非永久儲存；重新建立工作階段後可能消失。
- 目前程式採非串流回應（`stream=False`），需等待模型完成回覆後才顯示。
- 程式介面文字目前提到 Llama，但實際呼叫的是 `openai/gpt-oss-120b`，建議同步修改介面描述。
- 使用 Groq API 時請遵守平台的服務條款與使用限制。

## 後續可擴充功能

- 模型選擇功能
- 串流輸出回覆
- 自訂 system prompt
- 對話紀錄匯出與儲存
- 多使用者登入與權限管理

## 授權

本專案尚未指定授權條款。如需開放他人使用、修改與散布，建議另外加入 `LICENSE` 檔案（例如 MIT License）。
