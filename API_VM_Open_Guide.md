# API Server Open Guide
### 1. 檢查已存在的docker image
```
sudo docker ps -a
```
### 2. 開啟`FLASK-API` Docker
```
sudo docker start flask-api
```
### 3. 開啟瀏覽器並在上方網址欄輸入VM-IP與Port
```
http://[your_ip]:8487
```
### 4. flask API使用指南

> API Key Registration欄位輸入要註冊的使用者,按下Register API Key生成一個api金鑰 

> 生成金鑰之後可以按下複製按鈕,複製金鑰

> 可透過生成的API Key來傳輸數據或請求數據,類似於前後端之間的溝通鏈結

> API Key Verification欄位可以輸入生成金鑰,驗證屬於哪一個使用者的,若API Key未註冊過則獲顯示沒有此金鑰

