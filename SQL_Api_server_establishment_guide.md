# SQL-API-SERVER
## 步驟
### 設定 Ubuntu Server 環境
  - 安裝 MySQL Server環境
  ```
  sudo apt update && sudo apt upgrade -y
  sudo apt install mysql-server -y
  ```
  - 啟動並設定 MySQL：
  ```
  sudo systemctl enable mysql
  sudo systemctl start mysql

  ```
  - 進入 MySQL 並建立資料庫：
  ```
  mysql -u root -p
  CREATE DATABASE csv_database;
  EXIT;
  ```
  - 安裝`phpmyadmin`
  ```
  sudo apt update
  sudo apt install phpmyadmin -y
  ```
  - 安裝`phpmyadmin`一樣勾選`apache2`,後續安裝會出現`「Configure database for phpmyadmin with dbconfig-common?」` 的選項：
  - 請勾選:
  ```
  cancel
  ```
  - 進入`phpmyadmin`配置文件
  ```
  sudo nano /etc/dbconfig-common/phpmyadmin.conf
  ```
  - 如果檔案存在，請確保 dbc_dbuser 設定為 phpmyadmin，並設定你的密碼：
  ```
  dbc_dbuser='phpmyadmin'
  dbc_dbpass='你的密碼'
  ```  
  - 儲存後，重啟 `Apache2`
  ```
  sudo systemctl restart apache2
  ```
  - 進入 MySQL 並建立`phpmyadmin`帳號：
  ```
  sudo mysql -u root -p
  CREATE USER 'phpmyadmin'@'localhost' IDENTIFIED BY 'P@ssw0rd123!';
  GRANT ALL PRIVILEGES ON phpmyadmin.* TO 'phpmyadmin'@'localhost' WITH GRANT OPTION;
  FLUSH PRIVILEGES;
  EXIT;
  ```
- 設置使用者的完整權限
  ```
  GRANT ALL PRIVILEGES ON *.* TO 'phpmyadmin'@'localhost' WITH GRANT OPTION;
  FLUSH PRIVILEGES;
  ```
- 瀏覽器登入`phpmyadmin`
  ```
  http://[your_vm_ip]/phpmyadmin
  ```
- 成功登入`phpmyadmin`
