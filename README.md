# 崑山美食機器人專案開發
## 專題目標

- **核心目標**
    - Specific（具體）：解決使用者無法及時獲取附近美食詳細資訊及推薦文之問題
    - Measurable（可衡量）：使用者可以即時通過手機app服務獲取附近的餐廳名稱,地址,電話,評價及推薦文
    - Achievable（可實現）：目前開發團隊共計五人,分別各自開發或配置部件最後前後端整合進行使用者測試
    - Relevant（相關性）：使用者可最快時間獲取附近餐廳訊息
    - Time-bound（時限）：20250630(可討論)
## 規範
- **每日/每週進度回報機制**:
  - 放置檔案下載連結至底下的*職責規劃區*中的*說明文件下載連結*
  - 說明文件格式為:
    - PowerPoint簡報
- **統一版本管理方式**:
  - 在此Github專案下製作說明文件並提供說明文件檔案下載連結
  - 各自於家中完成開發設計
  - (討論部屬地點)
- **固定溝通時間**:
  - 原則上有上課的每個禮拜二下午1:30-2:30
- **開會地點**:
  - 圖書館討論室
  
## **團隊組織與分工**
-  **定義團隊角色**
- **專案管理**：(暫定)黃律嘉
- **技術負責人**（Tech Lead）：(全體組員)負責技術決策、(全體組員)架構設計
- **開發者**：(全體組員)負責程式撰寫與實作
- **文檔與測試負責人**：(全體組員)撰寫報告、(全體組員)測試系統
- **簡報負責人**：(暫定)黃律嘉(專門負責對外展示與報告)
## 專案資料流規劃圖
- ![ARCHITECTURE](https://github.com/user-attachments/assets/22a20f77-2b16-47df-84de-988e1069d095)
## 最新版database
- [下載連結](https://1drv.ms/u/c/2246da9308bf8a0b/EYr1AdYlxGJHtgkyPYOJpTMBgO_IT5jbMH9XH_GsDwhDCQ?e=xXhBeZ)

## 進度總攬(截至20250428)
- **SQL Server + Main Server(API)**
    -  [說明文件下載連結](https://docs.google.com/presentation/d/13eR6K0OvtLCKswd_teb7XAT-YY66nJXI/edit?usp=sharing&ouid=106887199356708617838&rtpof=true&sd=true)
    -  [Main Server(API)部署說明文件下載連結]()
    -  說明文件下載連結.....
    ```
    SQL Server:規劃架構與技術選型(吳富民)(已完成)
    SQL Server:配置PHPmyadmin(吳富民)(已完成)
    SQL Server:配置Mysql(吳富民)(已完成)
    SQL Server:部屬(吳富民)
    Main Server(API):配置(吳富民)(已完成)
    Main Server(API):API連線說明文件製作(吳富民)(已完成)
    Main Server(API):部署說明文件
    ```
- **Food-Data Service Server**
    -  [說明文件下載連結](https://1drv.ms/p/c/2246da9308bf8a0b/ET37_BkFFsRLsb-BHIPy7QQB9ZdrLuaBUBnml9bjtL-oQw?e=i4WvHO)
    -  [Food-Data Service Server部署說明文件下載連結]()
    -  說明文件下載連結.....
    ```
    Food-Data Service Server:規劃架構與技術選型(黃律嘉)(已完成)
    Food-Data Service Server:設計(黃律嘉)(已完成)
    Food-Data Service Server 部屬(黃律嘉)
    Food-Data Service Server:API整合資料庫檔案傳送(黃律嘉)(已完成)
    Food-Data Service Server:Food-Data Service Server部署說明文件
    ```
- **FoodChatBot Server**
    -  [說明文件下載連結](https://docs.google.com/presentation/d/1tlU4ICzwZ8mPA4F13kG6lmIv51HImycuguh58RysZjw/edit?usp=sharing)
    -  [FoodChatBot Service Server部署說明文件下載連結]()
    -  說明文件下載連結.....
    ```
    FoodChatot Server:規劃架構與技術選型(陳名輔)(已完成)
    FoodChatot Server:設計(陳名輔)
    FoodChatot Server:部屬(陳名輔)
    FoodChatot Server:API整合資料庫搜尋功能(陳名輔)
    FoodChatot Server:API整合POST手機APP聊天結果(陳名輔)
    FoodChatot ServerFoodChatBot Service Server部署說明文件
    ```
- **手機APP**
    -  [說明文件下載連結](https://1drv.ms/f/c/3538e5ec697121cc/EsJL1Ko_uCxOshPMCgd-IkYBMVwdePoDAk_nxbGDvxJiaw?e=2zXGqx)
    -  [API操作元件說明文件下載連結]()
    -  說明文件下載連結.....
    ```
    手機APP:規劃架構與技術選型(林聖峰)(已完成)
    手機APP:設計(林聖峰)(已完成)
    手機APP:部屬(林聖峰)
    手機APP:API整合ChatGPT-API Server(林聖峰)
    手機APP:整合口譯功能(林聖峰)
    手機APP:API操作元件說明文件
    ```
- **口譯功能服務**
    - [說明文件下載連結](https://docs.google.com/presentation/d/1b-JDRvySwyjfmx6IcQbTskFVm9phBgWz/edit?usp=drive_link&ouid=108367324358752546044&rtpof=true&sd=true)
    - [說明文件下載連結](https://docs.google.com/presentation/d/1SgvoiNP5a1w3FEKKdz6k3pUUXypjBPpW/edit?usp=sharing&ouid=108367324358752546044&rtpof=true&sd=true)
    - [STT Service Server部署說明文件下載連結]()
    ```
    口譯功能服務:規劃架構與技術選型(王羿辰)(已完成)
    口譯功能服務:設計(王羿辰)(已完成)
    口譯功能服務:部屬(王羿辰)
    口譯功能服務:API整合手機APP請求(王羿辰)
    口譯功能服務:STT Service Server部署說明文件
    ```
- 使用者測試
    - 說明文件下載連結.....
    - 說明文件下載連結.....
    - 說明文件下載連結.....
    ```
    使用者測試:操作
    使用者測試:紀錄
    使用者測試:說明文件製作
    ```
## 開會總攬
- [20250325開會紀錄](https://1drv.ms/p/c/2246da9308bf8a0b/EY8s_3oZB7dFvPo1tj1f-BQBF-IP_tmFVuH6YqcgQ0rsUA?e=fmK296)

