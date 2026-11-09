## 使用情況調查（2026-11-09）

> 本節為 hanlin-edu-tech repo 清理作業的調查紀錄，待負責人確認後決定封存或刪除。

- 調查結論：仍在使用
- 建議處置：保留，理由：正式環境運行中的 tutor-cashflow 依賴本 repo 發布的 `com.eHanlin.api:e-invoice-client:0.0.4`。
- 最後更新：pushedAt 2021-06-18；最後 commit `443f110` 2021-06-18 AaronChuang [ch-947] 移植舊有lib至gcs上, 更新lib
- 用途：ezPay（智付寶）電子發票 API 的 Java 用戶端函式庫（開立、觸發開立、作廢、查詢），以 Gradle `maven-publish` 發布為 `com.eHanlin.api:e-invoice-client`（目前版本 0.0.4）到公司 GCS Maven 套件庫；本身無獨立部署。

### 檢查結果

| 檢查項目 | 結果 | 依據 |
|---|---|---|
| GitHub 活動 | 2021-06-18 後無 commit | 共 16 個 commit（2017-09-12～2021-06-18，Rodick.Huang 15、AaronChuang 1）；分支僅 `master`；tag 0、release 0；PR 0、issue 0；Actions workflow 0、執行紀錄 0；webhook 0；非 fork；無 Dockerfile、cloudbuild.yaml |
| org 內程式碼引用 | tutor-cashflow 依賴本 repo 0.0.4 | `gh search code --owner hanlin-edu-tech`：`e-invoice-client` 除本 repo 外只命中 tutor-cashflow（private）的 Gradle 依賴宣告；`pay2GoInvoice` 除本 repo 外命中 tutor-cashflow 的發票設定與服務程式，其餘命中（tutor-coupon 文件、crm-lite、tutor-customer-service 等）為訂單欄位名稱，非引用本 repo。tutor-cashflow 正式環境運行版本對應的原始碼同樣宣告此依賴，GCS 套件庫中 0.0.4 的 jar 於 2021-06-18 上傳。已查核，細節記錄於內部調查報告 |
| GCP 部署 | 本 repo 無部署；依賴方 tutor-cashflow 在正式環境運行中 | 19 個 GCP 專案的 Cloud Run、Cloud Functions、Cloud Build trigger、GCR、Artifact Registry、Cloud Scheduler、App Engine 清單與 8 個 GKE 叢集以 `e-invoice`、`invoice`、`pay2go`、`ezpay` 搜尋 0 筆；依賴方部署已查核，細節記錄於內部調查報告 |
| AWS 部署 | 查無 | 4 個 AWS 帳號的 Lambda、API Gateway（REST 與 HTTP API）、CloudFront、ECR、ECS、EventBridge、SQS、S3 以 `e-invoice`、`invoice`、`pay2go`、`ezpay` 搜尋 0 筆 |

### 待確認事項
- 本 repo 內容有一項安全事項需處理，細節記錄於內部調查報告，請 tutor-cashflow 負責人確認後處理。

# e-invoice-client
eHanlin 電子發票客戶端程式
