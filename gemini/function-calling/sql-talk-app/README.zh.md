# SQL Talk：以 Gemini 的函式呼叫在 BigQuery 實現自然語言

| |
|-|-|
|作者 | [Kristopher Overholt](https://github.com/koverholt)

## 概觀

此應用展示了
[Gemini 函式呼叫](https://cloud.google.com/vertex-ai/docs/generative-ai/multimodal/function-calling)
功能的強大，讓使用者能以自然語言查詢和瞭解他們
[BigQuery](https://cloud.google.com/bigquery) 資料庫。
忘記複雜的 SQL 語法，以對話方式與資料互動。

Gemini 的函式呼叫讓開發人員能在程式碼中建立函式的描述，然後在請求中將該描述傳遞至語言模型。模型的回應包含搭配描述的函式名稱和呼叫函式所用的引數。

立即試用簡式應用程式！ [https://sql-talk-r5gdynozbq-uc.a.run.app/](https://sql-talk-r5gdynozbq-uc.a.run.app/)

![SQL Talk 範例應用程式](sql-talk.png)

## 先決條件

- 已啟用帳單功能的 Google Cloud 專案
- BigQuery 資料集 (我們使用
  [`thelook_ecommerce` 公用資料集](https://console.cloud.google.com/marketplace/product/bigquery-public-data/thelook-ecommerce)) 
- 已啟用 Vertex AI 和 BigQuery API
- 熟悉 Python 和 SQL 概念

## 在本機執行應用程式

1. 將此儲存庫複製下來
2. `cd` 到 `gemini/function-calling/sql-talk-app` 目錄
3. 使用 `pip install -r requirements.txt` 安裝相依性
4. 使用 `streamlit run app.py` 執行應用程式
5. 在瀏覽器中導航到應用程式，網址類似於：`http://localhost:8501`

## 設定服務帳戶

將此應用程式部署至 Cloud Run 時，建議做法是
[建立服務帳戶](https://cloud.google.com/iam/docs/service-accounts-create) 並附加下列角色，這些角色是應用程式讀取 BigQuery 資料，執行 BigQuery 工作，以及在 Vertex AI 中使用資源所需要的權限：

- [BigQuery 資料查看者](https://cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) (`roles/bigquery.dataViewer`)
- [BigQuery 工作使用者](https://cloud.google.com/bigquery/docs/access-control#bigquery.jobUser) (`roles/bigquery.jobUser`)
- [Vertex AI 使用者](https://cloud.google.com/vertex-ai/docs/general/access-control#aiplatform.user) (`roles/aiplatform.user`)

## 將應用程式部署至 Cloud Run

若要將此應用程式部署至
[Cloud Run](https://cloud.google.com/run/docs/deploying-source-code)，請執行下列指令，讓應用程式透過 Cloud Build 建置並部署至 Cloud Run，將 `service-account` 和 `project` 值換成你自己的值，類似於：

```shell
gcloud run deploy sql-talk --allow-unauthenticated --region us-central1 --service-account SERVICE_ACCOUNT_NAME@PROJECT_ID.iam.gserviceaccount.com --source .
```

## 存取已部署的應用程式

部署應用程式後，你應該可以瀏覽應用程式網址，網址類似於：

[https://sql-talk-r5gdynozbq-uc.a.run.app/](https://sql-talk-r5gdynozbq-uc.a.run.app/)

恭喜你，你已成功部署 SQL Talk 範例應用程式！

## 延伸應用程式

試著改寫函式定義和應用程式碼來嘗試新事物！
考慮加入工具來執行：

- 資料視覺化：建立圖表來總結發現
- 其他資料庫整合：支援 PostgreSQL、MySQL 等
- API：連接至天氣 API、翻譯服務等等.

## 其他資源

你可以透過這些指南和資源進一步瞭解 Gemini 的函式呼叫：



- [Gemini 的函式呼叫文件](https://cloud.google.com/vertex-ai/docs/generative-ai/multimodal/function-calling?hl=zh-tw)
- [如何使用 Gemini 中的函式呼叫與 API 互動的 Codelab](https://codelabs.developers.google.com/codelabs/gemini-function-calling?hl=zh-tw)
- [使用 Gemini API 進行函式呼叫的範例筆記本](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/function-calling/intro_function_calling.ipynb)



