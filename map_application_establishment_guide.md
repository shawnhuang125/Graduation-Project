# google-map-api-VM製作

- 目標:實現這個需求的完整流程和步驟，包含如何導入 Google Maps API 到本地運行的開發專案，並通過前端輸入關鍵字，將結果存儲到 MySQL 資料庫中。

1. 申請 Google Maps API Key
- 首先，需申請一個 Google Cloud API 金鑰來使用 Google Maps 的服務：

- 註冊並登入 Google Cloud Console.
- 創建一個新的專案。
- 啟用 Google Maps APIs，例如：
- Places API（查詢 POI 資訊）
- Geocoding API（地理編碼）
- Maps JavaScript API（前端地圖展示，可選）
- 生成 API 金鑰，並設置 IP 限制以防被濫用。

2. 建立專案架構
- 在 VS Code 中創建你的專案目錄，假設名稱為 `google-maps-app`，並按照以下結構組織：

```
google-maps-api-app/
├── app.py              # 後端 Flask 程式
├── requirements.txt    # Python 套件依賴
├── .env                # 環境變數
├── Dockerfile          # Docker 設定
├── templates/          # 存放 HTML 檔案
│   └── index.html      # 主頁面
└── static/             # 靜態資源 (CSS/JS)
    └── style.css       # 頁面樣式

```

3. 開發專案
### 3-1.建置 Python 虛擬環境
- 為了避免套件衝突，建議為專案建立一個 Python 虛擬環境：

- 步驟
- 創建虛擬環境：

```
python -m venv [your_env_name]
```
- 這會在專案目錄中創建一個名為 venv 的虛擬環境文件夾。

- 啟動虛擬環境：

- Windows：
```
.\venv\Scripts\activate
```
- Linux/Mac：
```
source venv/bin/activate
```
### 3-2.建置app.py
- 實現:
    - 首頁展示
    - 功能1：
        - 檢查 Google Maps API Key 是否已加載並顯示狀態。
        - 顯示過去的搜尋結果（從本地 ./data/places.json 文件讀取）。
        - 顯示首頁模板。
        - 搜尋地點
    - 功能2：
        - 接收使用者輸入的搜尋關鍵字。
        - 調用 Google Maps Places API 進行文字搜尋，獲取地點基本資訊。
        - 使用 Places Details API 獲取每個地點的詳細資訊（店名、地址、電話、星等、營業時間、評論）。
        - 將搜尋結果保存為帶時間戳的 JSON 文件（存於 ./data/ 資料夾）。
        - 在首頁模板中顯示搜尋結果。
    - 資料儲存

        - 將搜尋結果以 JSON 格式保存到本地文件系統。
        - 文件命名格式：places_YYYYMMDD_HHMMSS.json（包含時間戳）。
    - 錯誤處理

        - 檢查是否輸入了搜尋關鍵字，若無則提示錯誤。
        - 處理 API 請求錯誤，例如：
        - 網路錯誤（如連線失敗）。
        - Google Maps API 回傳錯誤訊息（如無效 API Key）。
        - 處理 JSON 文件保存錯誤，並在頁面上顯示提示。
    - 環境變數管理

        - 使用 .env 文件存儲和加載 Google Maps API Key，避免將敏感資訊硬編碼。
    - UI 功能
        - 使用 Flask 的 flash 消息系統在頁面上提示成功或錯誤的操作結果。
        - 渲染模板 index.html，動態顯示搜尋結果和 API 狀態。
        - 靜態資源
        - 預設使用 /static/uploads/logo.png 作為圖示。
- `app.py`
```
from flask import Flask, render_template, request, redirect, url_for, flash
import os
import json
import requests
from urllib.parse import quote
from datetime import datetime
from dotenv import load_dotenv

# Load environment variables explicitly
load_dotenv(dotenv_path='./.env')

# Initialize the Flask application
app = Flask(__name__)
app.secret_key = "your_secret_key"

# Google Maps API key
API_KEY = os.getenv("GOOGLE_MAPS_API_KEY")
print(f"Loaded API Key: {API_KEY}")  # Debugging to ensure correct key is loaded

# Default icon URL
icon_url = "/static/uploads/logo.png"

@app.route('/')
def index():
    """Display the home page."""
    # Check if the API key exists
    api_status = "Active" if API_KEY else "API key not provided"

    # Display the most recent search results (if available)
    places = []
    if os.path.exists('./data/places.json'):
        with open('./data/places.json', 'r', encoding='utf-8') as f:
            places = json.load(f)

    return render_template('index.html', api_status=api_status, icon_url=icon_url, places=places)

@app.route('/search', methods=['POST'])
def search_places():
    """Query the Google Maps Places API."""
    query = request.form.get('query')
    if not query:
        flash("Please enter a search query", "error")
        return redirect(url_for('index'))

    # Encode query to handle special characters
    encoded_query = quote(query)
    url = f"https://maps.googleapis.com/maps/api/place/textsearch/json?query={encoded_query}&key={API_KEY}"

    # Log API Key and URL
    print(f"Using API Key: {API_KEY}")
    print(f"Request URL: {url}")

    try:
        response = requests.get(url)
        response.raise_for_status()
        data = response.json()
        print("Full API Response:", json.dumps(data, indent=4, ensure_ascii=False))  # Log full response
    except requests.exceptions.RequestException as e:
        print("Request Error:", e)  # Log request errors
        flash(f"API request failed: {e}", "error")
        return redirect(url_for('index'))

    if "error_message" in data:
        print("API Error:", data['error_message'])  # Log API errors
        flash(f"API error: {data['error_message']}", "error")
        return redirect(url_for('index'))

    places = []
    for place in data.get('results', []):
        place_id = place.get('place_id')
        details_url = f"https://maps.googleapis.com/maps/api/place/details/json?place_id={place_id}&key={API_KEY}"
        try:
            details_response = requests.get(details_url)
            details_response.raise_for_status()
            details_data = details_response.json()
            detailed_place = details_data.get('result', {})

            places.append({
                'name': detailed_place.get('name'),
                'address': detailed_place.get('formatted_address'),
                'phone_number': detailed_place.get('formatted_phone_number'),
                'rating': detailed_place.get('rating'),
                'opening_hours': detailed_place.get('opening_hours', {}).get('weekday_text', []),
                'reviews': [
                    {
                        'author_name': review.get('author_name'),
                        'rating': review.get('rating'),
                        'text': review.get('text')
                    }
                    for review in detailed_place.get('reviews', [])
                ]
            })
        except requests.exceptions.RequestException as e:
            print(f"Details Request Error for place_id {place_id}:", e)

    # Save the search results to a JSON file with a timestamped filename
    if not os.path.exists('./data'):
        os.makedirs('./data')
    timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
    filename = f"./data/places_{timestamp}.json"
    try:
        with open(filename, 'w', encoding='utf-8') as f:
            json.dump(places, f, ensure_ascii=False, indent=4)
        print(f"File saved successfully as {filename}!")
    except Exception as e:
        print("File Save Error:", e)
        flash("Failed to save search results.", "error")

    # Pass the search results to the front-end template
    flash("Search successful!", "success")
    return render_template('index.html', icon_url=icon_url, api_status="Active", places=places)

if __name__ == '__main__':
    app.run(debug=True)

```
- `index.html`
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dashboard</title>
  <link rel="icon" href="/static/uploads/logo.png" type="image/x-icon">
  <link rel="stylesheet" href="/static/style.css">
</head>
<body>
  <header class="header">
    <div class="logo">
      <img src="/static/logo.png" alt="Default Logo" class="header-icon">
      <h1 class="title">Dashboard</h1>
    </div>
    <div class="search-bar">
      <form method="POST" action="{{ url_for('search_places') }}">
        <input type="text" name="query" placeholder="例如：崑山科大附近的美食">
        <button type="submit">Search</button>
      </form>
    </div>
  </header>
  



  <!-- 主內容區域 -->
  <div class="container content">
    <!-- 左邊欄位 -->
    <div class="left-panel">
      

      <!-- Google Maps API 狀態 -->
      <div class="card">
        <h2>Google Maps API Status</h2>
        <p>Status： 
          <span class="api-status {{ 'active' if api_status == 'Active' else 'inactive' }}">
            {{ api_status }}
          </span>
        </p>
      </div>

      <!-- SQL 上傳表單 -->
      <div class="card">
        <h2>SQL Server URL</h2>
        <form method="POST" action="/upload" class="form-inline">
          <label for="sql_server_url">SQL Server URL：</label>
          <div class="input-group">
            <input type="text" id="sql_server_url" name="sql_server_url" placeholder="Enter SQL Server API URL" required>
            <button type="submit">Upload</button>
          </div>
        </form>
      </div>
      
    </div>


    <!-- 右邊查詢結果 -->
    <div class="right-panel">
      

      <!-- 結果展示 -->
      <div class="card result-card">
        <h2>Result</h2>
        <div class="results">
            {% if places %}
            <ul>
                {% for place in places %}
                {% if loop.index0 == 0 or places[loop.index0 - 1].name != place.name %} 
                <!-- 只顯示每家店的第一條數據 -->
                <li>
                    <strong>{{ place.name }}</strong><br>
                    Address: {{ place.address }}<br>
                    Phone: {{ place.phone }}<br>
                    
                </li>
                {% endif %}
                {% endfor %}
            </ul>
            {% else %}
            <p>No results found</p>
            {% endif %}
        </div>
    </div>
    
    </div>
  </div>
  

</body>
</html>
```
- `style.css`
```
/* Header 樣式 */
.header {
    background-color: #404040; /* 背景色 */
    color: white; /* 字體顏色 */
    height: 50px; /* Header 高度適中 */
    display: flex; /* 使用 flex 布局 */
    align-items: center; /* 垂直置中 */
    justify-content: space-between; /* 左右對齊 */
    padding: 0 20px; /* 左右內距 */
    font-size: 14px; /* 字體大小調整 */
    font-weight: bold; /* 字體加粗 */
    position: fixed; /* 固定在頁面頂部 */
    top: 0; /* 靠近頂部 */
    left: 0; /* 靠近左邊 */
    width: 100%; /* 寬度填滿整個畫面 */
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1); /* 添加陰影效果 */
    z-index: 1000; /* 確保 header 顯示在最上層 */
    box-sizing: border-box; /* 包括內邊距在內 */
}

/* Logo 和標題樣式 */
.logo {
    display: flex; /* 圖標與標題水平排列 */
    align-items: center; /* 垂直置中 */
    gap: 10px; /* 圖標與標題間距 */
}

.header .header-icon {
    width: 24px; /* 圖標寬度 */
    height: 24px; /* 圖標高度 */
}

/* 標題 */
.header .title {
    font-size: 16px; /* 字體大小 */
    margin: 0; /* 無外邊距 */
    line-height: 50px; /* 與 Header 一致的高度 */
}
/* 搜尋區域 */
.header .search-bar {
    display: flex; /* 搜尋欄水平排列 */
    align-items: center; /* 垂直置中 */
    gap: 10px; /* 搜尋框和按鈕的間距 */
    height: 100%; /* 高度填滿 Header */
    max-width: 1900px; /* 搜尋區域的最大寬度，進一步拓寬 */
    margin-left: auto; /* 搜尋欄靠右 */
    padding-right: 10px; /* 與右側保持間距 */
}

/* 搜尋框 */
.header .search-bar input[type="text"] {
    flex-grow: 1; /* 搜尋框填滿剩餘空間 */
    max-width: 1700px; /* 搜尋框的最大寬度，延伸更多 */
    padding: 5px 10px; /* 內邊距調整，確保易讀性 */
    border-radius: 5px; /* 圓角 */
    border: 1px solid #ddd; /* 邊框樣式 */
    font-size: 14px; /* 字體大小 */
    height: 30px; /* 與按鈕高度一致 */
    box-sizing: border-box; /* 包括邊框在內的寬高 */
    background-color: #fff; /* 背景顏色 */
    outline: none; /* 聚焦時移除邊框 */
}

/* 搜尋按鈕 */
.header .search-bar button {
    padding: 5px 15px; /* 按鈕內邊距調整 */
    border-radius: 5px; /* 圓角 */
    background-color: #555; /* 按鈕背景色 */
    color: white; /* 按鈕文字顏色 */
    border: none; /* 移除邊框 */
    cursor: pointer; /* 滑鼠指針 */
    font-size: 14px; /* 字體大小 */
    height: 30px; /* 與搜尋框高度一致 */
    transition: background-color 0.3s ease; /* 過渡效果 */
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* 添加輕微陰影 */
}

/* 按鈕懸停效果 */
.header .search-bar button:hover {
    background-color: white; /* 懸停背景色 */
    color: #404040; /* 確保文字顏色對比 */
}





/* 主體內容加上內距，避免被 Header 遮擋 */
.content {
    margin-top: 50px; /* 根據 header 的高度調整 */
    padding: 20px;
}




/* 左右欄樣式 */
.container {
    display: flex; /* 左右分欄 */
    gap: 20px; /* 左右欄間距 */
}

/* 左欄 */
.left-panel {
    flex: 1; /* 左欄占據剩餘空間 */
    max-width: 400px; /* 設定最大寬度 */
}

/* 右欄 */
.right-panel {
    flex: 2; /* 右欄占據更多空間 */
    height: calc(100vh - 60px); /* 減去 header 的高度，確保卡片高度動態調整 */
    
}

/* Result 卡片滾動設置 */
.card.result-card {
    height: 100%; /* 卡片填滿右欄 */
    overflow-y: auto; /* 開啟垂直滾動條 */
    padding-right: 10px; /* 給滾動條留間距 */
    scrollbar-width: thin; /* Firefox 滾動條寬度 */
    scrollbar-color: #ccc transparent; /* Firefox 滾動條顏色 */
}

/* 滾動條樣式（Chrome、Safari、Edge） */
.card.result-card::-webkit-scrollbar {
    width: 8px; /* 滾動條寬度 */
}

.card.result-card::-webkit-scrollbar-thumb {
    background-color: #aaa; /* 滾動條滑塊顏色 */
    border-radius: 4px; /* 圓角 */
}

.card.result-card::-webkit-scrollbar-thumb:hover {
    background-color: #888; /* 滑鼠懸停時滑塊顏色 */
}

.card.result-card::-webkit-scrollbar-track {
    background: transparent; /* 滑道背景透明 */
}


/* 卡片內表單樣式 */
.card form {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

/* 卡片樣式 */
.card {
    background-color: #fff;
    border-radius: 5px;
    padding: 15px;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    margin-bottom: 15px;
}

/* 查詢結果樣式 */
.results ul {
    list-style: none; /* 移除列表符號 */
    padding: 0; /* 移除內距 */
    margin: 0; /* 移除外距 */
}

.results li {
    margin-bottom: 10px; /* 每項結果之間的間距 */
    padding: 10px;
    border: 1px solid #ddd; /* 添加邊框 */
    border-radius: 5px; /* 圓角 */
    background-color: #f9f9f9; /* 淺色背景 */
}

/* 按鈕樣式 */
button {
    background-color: #404040; /* 按鈕背景色 */
    color: white; /* 按鈕文字色 */
    border: none; /* 移除邊框 */
    padding: 10px 20px; /* 內距 */
    border-radius: 5px; /* 圓角 */
    cursor: pointer; /* 滑鼠指標 */
    font-size: 14px; /* 字體大小 */
    transition: background-color 0.3s; /* 添加過渡效果 */
}

button:hover {
    background-color: white; /* 滑鼠懸停背景色 */
    color: #404040; /* 按鈕文字色 */
}

```
- `requirements.txt`
```
Flask
requests
python-dotenv
pandas
```
- `.env`,在這個檔案裏要放置你取得的api key
```
GOOGLE_MAPS_API_KEY=""
```
