# SQL-API-SERVER
## 步驟
### 1. 設定 Ubuntu Server 環境
  - 1-1. 安裝 MySQL Server環境
  ```
  sudo apt update && sudo apt upgrade -y
  sudo apt install mysql-server -y
  ```
  - 啟動並設定 MySQL：
  ```
  sudo systemctl enable mysql
  sudo systemctl start mysql

  ```
  - 設定 MySQL root 密碼
  ```
  sudo mysql_secure_installation
  ```
  - 進入 MySQL 並建立資料庫：
  ```
  mysql -u root -p
  CREATE DATABASE csv_database;
  EXIT;
  ```
  - 1-2. 安裝 Python 及 Flask（作為 API 伺服器）
  ```
  
  ```
  - 1-3. 安裝 pymysql（Python 連接 MySQL）
  ```
  
  ```
  - 1-4. 安裝 pandas（處理 CSV）
  ```
  
  ```
### 2. 設計 API
  - 2-1. 使用 Flask 建立 API，接收 CSV 檔案
  - 2-2. 解析 CSV 檔案，動態建立 MySQL 表格
  - 3-3. 插入 CSV 數據到新建的表格
### 3. 測試 API
  - 3-1. 用 Postman 或 cURL 測試上傳 CSV
  - 3-2. 確認 MySQL 生成新表並存入數據
