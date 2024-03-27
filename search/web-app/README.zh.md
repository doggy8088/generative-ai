# Vertex AI 搜尋示範

> 注意：此示範中的一些功能需要允許清單存取權。如果您想搶先存取，請申請成為 [Google Cloud 生成式 AI 的值得信賴測試員][trustedtester]。

此示範說明如何使用 [Vertex AI 搜尋][enterprisesearch](以前稱為企業搜尋) 搜尋文件資料庫。

其他功能還包括如何使用 [企業知識圖表][enterpriseknowledgegraph] API 搜尋公共的雲端知識圖表。

## 架構

### 使用的 Google Cloud 產品

- [Vertex AI 搜尋][enterprisesearch]
- [Vertex AI 搜尋：推薦事項][try_recommendations]
- [Cloud Run][cloudrun]
- [企業知識圖表][enterpriseknowledgegraph]

## 設定

- 按照 [針對非結構化資料開始使用 Vertex AI 搜尋][try_search] 中的步驟操作。

  - 已部署示範中使用的範例資料源：
    - [合約理解 Atticus 資料集 (CUAD)](https://www.atticusprojectai.org/cuad)
      - `gs://cloud-samples-data/gen-app-builder/search/CUAD_v1`
    - [Alphabet 收益報告](https://abc.xyz/investor/)
      - `gs://cloud-samples-data/gen-app-builder/search/alphabet-investor-pdfs`

- 按照 [針對網站開始使用 Vertex AI 搜尋][try_search] 中的步驟操作。

  - [Google Cloud 網站](https://cloud.google.com)
    - `https://cloud.google.com`

- 按照 [針對非結構化資料開始使用推薦事項][try_recommendations] 中的步驟操作。

  - 已部署示範中使用的範例資料源：
    - [ArXiv 中的自然語言文件](https://arxiv.org)
      - `gs://cloud-samples-data/gen-app-builder/search/arxiv`

### 依賴項

1. [安裝 Python](https://www.python.org/downloads/)
2. 安裝 [Google Cloud SDK](https://cloud.google.com/sdk/docs/install)
3. 安裝必要條件：
   - `pip install -r requirements.txt`
4. 執行 `gcloud init`，建立新的專案，然後
   [啟用帳單服務](https://cloud.google.com/billing/docs/how-to/modify-project#enable_billing_for_a_project)
5. 啟用 Vertex AI 搜尋 API：
   - `gcloud services enable discoveryengine.googleapis.com`
6. 啟用企業知識圖表 API：
   - `gcloud services enable enterpriseknowledgegraph.googleapis.com`
7. 啟用 Cloud Run：
   - `gcloud services enable run.googleapis.com`
8. 設定應用程式預設驗證，執行：
   - `gcloud auth application-default login`
9. 給予 Cloud Run 服務帳戶必要的權限：

   ```sh
   gcloud projects add-iam-policy-binding [PROJECT_ID] \
      --member='serviceAccount:[PROJECT_ID]-compute@developer.gserviceaccount.com' \ 
      --role='roles/discoveryengine.viewer'
   ```

10.  (選擇性) 如果您的 Google Cloud 組織有原則 [限制按網域分享](https://cloud.google.com/resource-manager/docs/organization-policy/restricting-domains)，您需要將此設定變更為允許所有網域，以讓 Cloud Run 應用程式公開於公共網路。

### 示範部署



1. 使用您的 `PROJECT_ID` 和 `LOCATION` 更新 `consts.py` 檔案。

2. 設定 Vertex AI 搜尋

   - 若要在 Cloud Console for Enterprise 中使用雲端平台提供的預建置小工具，請從 `整合 > 小工具` 標籤中的 `<gen-search-widget>` 中複製 `configId`。
     - ![configId](img/configId.png)
     - 部署後，請務必將授權類型設為 `公開存取`，並將您的網路應用程式網址新增至 `允許的網域`。
     - 將 `搜尋引擎` 的 `configId` 新增至 `consts.py` 中的 `WIDGET_CONFIGS`
   - 如要使用自訂 UI，請將搜尋引擎的資料儲存 ID 新增至 `consts.py` 中的 `CUSTOM_UI_DATASTORE_IDS`
     - 這是 Cloud Console URL 中 `/engines/` 之後的字串。
       - `https://console.cloud.google.com/gen-app-builder/engines/website-search-engine_1681248733152/...`
       - 資料儲存 ID 為 `website-search-engine_1681248733152`

3. 設定建議

   - 將建議引擎的資料儲存 ID 和引擎 ID 新增至 `consts.py` 中的 `RECOMMENDATIONS_DATASTORE_IDs`。
   - 資料儲存 ID 會顯示在 `資料 > 詳細資料` 頁面上。
   - 引擎 ID 是 Cloud Console URL 中 `/engines/` 之後的字串。
     - `https://console.cloud.google.com/gen-app-builder/engines/contracts-personalize_1687884886933/data/records`
     - 引擎 ID 為 `contracts-personalize_1687884886933`

4. 設定圖片搜尋

   - 按照說明文件中的說明 [啟用圖片搜尋](https://cloud.google.com/generative-ai-app-builder/docs/image-search#enable-advanced) 以取得網站搜尋引擎。
      - 注意：您必須啟用 [進階網站索引](https://cloud.google.com/generative-ai-app-builder/docs/about-advanced-features#advanced-website-indexing)，這需要 [驗證網域](https://cloud.google.com/generative-ai-app-builder/docs/domain-verification)。
   - 將搜尋引擎的資料儲存 ID 新增至 `consts.py` 中的 `IMAGE_SEARCH_DATASTORE_IDs`。

5. 在您的專案中部署 Cloud Run 應用程式。

   - `gcloud run deploy vertex-ai-search-demo --source .`

   - 在本機測試：`flask --app main run`

6. 拜訪已部署的網頁
   - 例如：[`https://vertex-ai-search-demo-lnppzg3rxa-uc.a.run.app`](https://vertex-ai-search.web.app/)

---

> 版權所有 2023 Google LLC
> 作者：Holt Skinner @holtskinner

# Vertex AI 搜尋示範

> 注意：此示範中的部分功能需要允許名單權限。



