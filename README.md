
# 專題團隊管理制度 v5.5

## 一、宣言與承諾

我們是一個以目標為導向的實踐型團隊。專題不只是學校的作業，這份專題代表著每一位成員的努力、責任與價值，將成為我們未來升學、求職、甚至創業時最重要的作品集之一。

**承諾：**
- 每個人都對自己的工作負責，不推卸、不敷衍，專注解決問題。
- 尊重他人專業分工，不干涉他人領域，不隨意批評，只提出建設性建議。
- 共同維護團隊秩序，任何問題及時溝通，並以成果為導向作為最終決策標準。
- 在遇到困難時，提出解決方案，而不是抱怨；遇到瓶頸時，尋求協助，而不是躲避。
- 每次會議後留下書面紀錄，確保資訊透明與責任明確。
- 所有的工作成果，將真實記錄在專題成果報告中，並公平分配在個人作品集與專題發表資料上，讓每一位成員的貢獻都能被看見。

## 二、角色與權責分工

| 角色 | 負責範圍 | 決策權限 |
| ---- | -------- | -------- |
| 技術負責人 | 最終決策權、專題總負責人、技術方向決策、進度協調、問題排解、團隊會議主持、成員績效評估 | 最終決定權 |
| 前端負責人 | APP 介面設計、APP 前端邏輯實作、前端元件架構設計、前端與 API 串接整合、確保前端功能與體驗流暢 | 前端專責權限 |
| 後端負責人 (API/資料庫) | API 設計與實作、資料庫設計與管理、資料庫配置與處理、API 安全性與權限控制、後端邏輯優化 | 後端專責權限 |
| 後端負責人 (FoodChatBot) | FoodChatBot 功能設計與實作、FoodChatBot 專屬模組開發、API 對接與整合、聊天功能驗證 | FoodChatBot 專責權限 |
| 後端負責人 (STT) | 語音功能服務 (STT) 設計與實作、STT 模組整合與優化、API 對接 STT、語音轉文字服務驗證與測試 | STT 專責權限 |
| 後端負責人 (Map API) | Map API 調用與整合、資料查詢與篩選功能設計、API 對接與資料展示、使用者地理定位功能優化 | Map API 專責權限 |
| 文件負責人 | 專題簡報製作、專案報告文件撰寫、系統架構圖與流程圖繪製、需求文件與技術文檔編寫、期末成果報告整理 | 文件專責權限 |
| 測試負責人 | 系統功能測試、API 測試、版本驗收、Bug 回報、測試案例撰寫、協助調試並提出改進建議 | 測試專責權限 |

## 三、PDCA 持續改進循環

為了確保團隊專題進度與成果品質，專題管理採用 PDCA 持續改進循環，具體實施方式如下：
- **Plan（計劃）**：由技術負責人主持會議，明確分工、進度安排、交付標準與責任人，使用 GitHub Issues/Projects 記錄各項任務。
- **Do（執行）**：各成員根據分工執行任務，並於 GitHub 回報進度；每週至少回報一次，未完成者持續回報，已完成項目可結束回報。
- **Check（檢查）**：每週舉行進度會議，技術負責人及文件負責人對照 GitHub 回報與目標，檢視進度與問題，將會議紀錄整理存檔於 Google Docs。
- **Act（改進）**：若發現進度落後、分工不均、制度不完善，需提出改進方案；改進方案可由任何成員提出，經技術負責人審核後執行。重大改進（如制度調整、技術方向變更）需記錄於《技術調整紀錄表》。

## 四、進度回報機制（使用 GitHub）

所有成員需在 GitHub Repository 上建立自己的進度回報 Issue，或使用 Project 功能管理進度。每次回報需更新進度、遇到的問題、解決方案、下一步計畫，並至少每週更新一次。

**回報格式範例：**

```
日期：YYYY/MM/DD
今日進度：
- 完成了什麼？
遇到問題：
- 有什麼卡關？
明日計畫：
- 預計明天完成什麼？
```

## 五、延期處理機制

為確保專題進度，允許在必要時申請延期，需遵守以下原則：
- 必須在原定交付日「前一天」提出延期申請，不接受事後告知。
- 延期原因需具體說明（如卡在哪個功能、需要什麼協助）。
- 申請時須提出新的交付日期，並承諾進度更新時間。
- 每個人最多一個月可申請三次延期，同一問題不得無限延期。
- 未主動提出延期，直接未交付視為無故拖延，依照團隊處理流程辦理（提醒 → 警告 → 移出團隊）。
- **延期申請格式範例**
```
### 延期申請

- **申請人**：請填寫名字
- **原定交付日期**：YYYY/MM/DD
- **延期申請時間**：YYYY/MM/DD（提出申請的時間）
- **延期原因**：
  - 例如：API 串接遇到技術問題，需要額外調查
- **預計完成時間**：YYYY/MM/DD
- **是否需要協助**：（是/否，若需要請說明）
  - 例如：需要前端提供接口文件
```
## 六、技術選型與架構調整容許機制

專題開發過程中，允許在遇到無法實現或技術瓶頸時，提出架構修改或技術選型調整，但必須遵守以下原則：
- 必須提前提出（至少提前一週或在問題發生後 24 小時內），不得事後才說。
- 需清楚說明問題原因（例如無法實現、效能問題、技術限制）。
- 必須提出可行的替代方案，不能只說問題沒有解法。
- 需經團隊討論後由技術負責人最終拍板決定。
- 修改決策必須記錄於《技術調整紀錄表》。

**技術調整紀錄表格式：**
```
問題模組：
問題描述：
原因分析：
新方案：
團隊討論結論：
最終拍板（技術負責人簽名）：
修改日期：
```

## 七、嚴重違規處理流程

任何成員皆可提出對違反規範成員的移除建議，需基於實際紀錄（如三次拖延、干涉他人、無故缺席等）。

流程為：
1. 提案人提出 GitHub Issue 或會議紀錄記錄具體事實
2. 團隊討論（不超過 20 分鐘）
3. 技術負責人根據制度最終拍板決定是否請對方離開。

原則為：只看事實，不看人情。決議結果必須公開透明。

## 八.專案資料流規劃圖
- ![ARCHITECTURE](https://github.com/user-attachments/assets/22a20f77-2b16-47df-84de-988e1069d095)
## 最新版database
- [下載連結](https://1drv.ms/u/c/2246da9308bf8a0b/EYr1AdYlxGJHtgkyPYOJpTMBgO_IT5jbMH9XH_GsDwhDCQ?e=xXhBeZ)

## 九.進度總攬(截至20250428)
- **SQL Server + Main Server(API)**
    -  [說明文件下載連結](https://docs.google.com/presentation/d/13eR6K0OvtLCKswd_teb7XAT-YY66nJXI/edit?usp=sharing&ouid=106887199356708617838&rtpof=true&sd=true)
    -  [Main Server(API)部署說明文件下載連結]()
    -  說明文件下載連結.....
    ```
    SQL Server:規劃架構與技術選型(吳富民)(已完成)
    SQL Server:配置PHPmyadmin(吳富民)(已完成)
    SQL Server:配置Mysql(吳富民)(已完成)
    SQL Server:部屬(吳富民)
    Main Server(API):API開發測試(吳富民)
    Main Server(API):API連線說明文件製作(吳富民)
    Main Server(API):部署說明文件(吳富民)
    ```
- **Map-API Service**
    -  [說明文件下載連結](https://1drv.ms/p/c/2246da9308bf8a0b/ET37_BkFFsRLsb-BHIPy7QQB9ZdrLuaBUBnml9bjtL-oQw?e=i4WvHO)
    -  [Food-Data Service Server部署說明文件下載連結]()
    -  說明文件下載連結.....
    ```
    Map-API Service:規劃架構與技術選型(黃律嘉)(已完成)
    Map-API Service:設計(黃律嘉)(已完成)
    Map-API Service:部屬(黃律嘉)
    Map-API Service:API整合資料庫檔案傳送(黃律嘉)(已完成)
    Map-API Service:Food-Data Service Server部署說明文件(黃律嘉)
    ```
- **FoodChatBot Server**
    -  [說明文件下載連結](https://docs.google.com/presentation/d/1tlU4ICzwZ8mPA4F13kG6lmIv51HImycuguh58RysZjw/edit?usp=sharing)
    -  [FoodChatBot Service Server部署說明文件下載連結]()
    -  說明文件下載連結.....
    ```
    FoodChatot Service:規劃架構與技術選型(陳名輔)(已完成)
    FoodChatot Service:設計(陳名輔)
    FoodChatot Service:API整合開發測試(陳名輔)
    FoodChatot Service:部屬(陳名輔)
    FoodChatot Service:FoodChatBot Service部署說明文件(陳名輔)
    ```
- **手機APP**
    -  [說明文件下載連結](https://1drv.ms/f/c/3538e5ec697121cc/EsJL1Ko_uCxOshPMCgd-IkYBMVwdePoDAk_nxbGDvxJiaw?e=2zXGqx)
    -  [API操作元件說明文件下載連結]()
    -  說明文件下載連結.....
    ```
    手機APP:規劃架構與技術選型(林聖峰)(已完成)
    手機APP:設計(林聖峰)(已完成)
    手機APP:部屬(林聖峰)
    手機APP:API整合開發測試(林聖峰)
    手機APP:整合口譯功能(林聖峰)
    手機APP:API操作元件說明文件(林聖峰)
    ```
- **口譯功能服務**
    - [說明文件下載連結](https://docs.google.com/presentation/d/1b-JDRvySwyjfmx6IcQbTskFVm9phBgWz/edit?usp=drive_link&ouid=108367324358752546044&rtpof=true&sd=true)
    - [說明文件下載連結](https://docs.google.com/presentation/d/1SgvoiNP5a1w3FEKKdz6k3pUUXypjBPpW/edit?usp=sharing&ouid=108367324358752546044&rtpof=true&sd=true)
    - [STT Service Server部署說明文件下載連結]()
    ```
    口譯功能服務:規劃架構與技術選型(王羿辰)(已完成)
    口譯功能服務:設計(王羿辰)(已完成)
    口譯功能服務:API整合開發測試(王羿辰)
    口譯功能服務:部屬(王羿辰)
    口譯功能服務:STT Service Server部署說明文件完成(王羿辰)
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
## 下載專區
- [文章爬蟲程式git連結](https://github.com/shawnhuang125/pyscraper_selenium)
## 開會總攬
- [20250325開會紀錄](https://1drv.ms/p/c/2246da9308bf8a0b/EY8s_3oZB7dFvPo1tj1f-BQBF-IP_tmFVuH6YqcgQ0rsUA?e=fmK296)
