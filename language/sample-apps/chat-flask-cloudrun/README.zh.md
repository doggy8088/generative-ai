# 具有 Web UI 的 Cloud Run 應用程式，展示與 Vertex AI API 合作

| |
|-|-|
|作者 | [Romin Irani](https://github.com/rominirani)

此應用程式展示一個 Cloud Run 應用程式，其有一個簡單的表單式 UI，代表一個聊天小工具。你可以輸入你的查詢，它會在背景中呼叫 PaLM Chat Bison 模型並取得回應。這是一個簡單的範例，但你可以考慮將它嵌入更大的 Web 應用程式中。

![Flask 聊天應用程式畫面](../assets/flaskapp-screen.png "Flask 聊天應用程式")

## 建立應用程式並將其部署到 Cloud Run

> 注意：**在你繼續之前，請務必按照 [SETUP.md](../SETUP.md) 中的說明進行操作。**
此外，請務必複製此存放庫並將其目前處於 ```chat-flask-cloudrun``` 資料夾中。這應該是你在接下來命令的實際工作目錄。

若要將 Flask 應用程式部署在 [Cloud Run](https://cloud.google.com/run/docs/quickstarts/deploy-container) 中，我們需要執行下列步驟：

1. 你的 Cloud 函式需要存取兩個環境變數：

   - `GCP_PROJECT`：這是 Google Cloud 專案 ID。
   - `GCP_REGION`：這是你部署 Cloud 函式的區域。例如：us-central1。
  
    需要這些變數，因為 Vertex AI 初始化需要 Google Cloud 專案 ID 和區域。以下是 `main.py` 函式中特定程式碼行的範例：
    `vertexai.init(project=PROJECT_ID, location=LOCATION)`

    在 Cloud Shell 中執行下列命令：

    ```bash
    export GCP_PROJECT='<你的 GCP 專案 ID>'  # 更改此項目
    export GCP_REGION='us-central1'             # 如果你更改此項目，請務必使用 Model Garden 支援的區域。有疑慮時，請保留這個區域。
    ```

2. 我們現在將建立應用程式的 Docker 映像，並將其推播至 Artifact Registry。為此，我們需要設定一個環境變數以指向 Artifact Registry 名稱。我們有一個命令會為你建立此存放區。

   在 Cloud Shell 中執行下列命令：

   ```bash
   export AR_REPO='<取代成你的 AR 存放區名稱>'  # 更改此項目
   export SERVICE_NAME='chat-flask-app' # 這是我們的應用程式和 Cloud Run 服務的名稱。如果你願意，可以更改它。
   gcloud artifacts repositories create "$AR_REPO" --location="$GCP_REGION" --repository-format=Docker
   gcloud auth configure-docker "$GCP_REGION-docker.pkg.dev"
   gcloud builds submit --tag "$GCP_REGION-docker.pkg.dev/$GCP_PROJECT/$AR_REPO/$SERVICE_NAME"
   ```

3. 最後一個步驟是在 Cloud Run 中部署我們在先前的步驟建立並推播至 Artifact Registry 的映像的服務：

    在 Cloud Shell 中執行下列命令：

    ```bash
    gcloud run deploy "$SERVICE_NAME" \
      --port=8080 \
      --image="$GCP_REGION-docker.pkg.dev/$GCP_PROJECT/$AR_REPO/$SERVICE_NAME" \
      --allow-unauthenticated \
      --region=$GCP_REGION \
      --platform=managed  \
      --project=$GCP_PROJECT \
      --set-env-vars=GCP_PROJECT=$GCP_PROJECT,GCP_REGION=$GCP_REGION
    ```

成功部署後會提供 Cloud Run 服務 URL。你可以在瀏覽器中瀏覽它以檢視你剛部署的應用程式。針對你選擇的幾個查詢進行查詢，應用程式會查詢 Vertex AI 聊天模型並向你提供回應。



