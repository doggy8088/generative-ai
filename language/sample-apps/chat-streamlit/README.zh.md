# Cloud Run 應用程式使用 Streamlit Framework，展示如何搭配 Vertex AI API 作業

| |
|-|-|
|作者 | [Romin Irani](https://github.com/rominirani)

這個應用程式展示一個使用 [Streamlit](https://streamlit.io/) 框架的 Cloud Run 應用程式。

![Streamlit 聊天應用程式畫面](../assets/streamlitapp-screen.png "Streamlit 聊天應用程式")

## 建置並將應用程式部署到 Cloud Run

> 注意：**在繼續之前，請務必遵循 [SETUP.md](../SETUP.zh.md) 中的說明。**
此外，請務必複製這個儲存庫，目前在 ```chat-streamlit``` 中。這應該是您在其他指令中的主要工作目錄。

若要將 Streamlit 應用程式部署在 [Cloud Run](https://cloud.google.com/run/docs/quickstarts/deploy-container) 中，我們需要執行下列步驟：

1. Cloud Functions 需要存取兩個環境變數：

   - `GCP_PROJECT` ：這是 Google Cloud 專案 ID。
   - `GCP_REGION` ：這是您部署 Cloud Functions 的區域。例如：us-central1。
  
    由於 Vertex AI 初始化需要 Google Cloud 專案 ID 和區域，所以需要這些變數。以下是 `main.py`
    函式中特定程式碼列：
    `vertexai.init(project=PROJECT_ID, location=LOCATION)`

    在 Cloud Shell 中，執行下列指令：

    ```bash
    export GCP_PROJECT='<您的 GCP 專案 ID>'  # 變更這個
    export GCP_REGION='us-central1'             # 如果您變更這個，請確定 Model Garden 支援這個區域。有疑問時，請保留這個。
    ```

2. 我們現在要為應用程式建置 Docker 映像，並將它推送到 Artifact Registry。為這麼做，我們需要設定一個指向 Artifact Registry 名稱的環境變數。我們有一個指令將為您建立這個儲存庫。

   在 Cloud Shell 中，執行下列指令：

   ```bash
   export AR_REPO='<用您的 AR 儲存庫名稱取代>'  # 變更這個
   export SERVICE_NAME='chat-streamlit-app' # 這是我們的應用程式和 Cloud Run 服務的名稱。如果您希望，可以變更這個。 
   gcloud artifacts repositories create "$AR_REPO" --location="$GCP_REGION" --repository-format=Docker
   gcloud auth configure-docker "$GCP_REGION-docker.pkg.dev"
   gcloud builds submit --tag "$GCP_REGION-docker.pkg.dev/$GCP_PROJECT/$AR_REPO/$SERVICE_NAME"
   ```

3. 最後的步驟是使用我們在先前步驟建置並推送到 Artifact Registry 的映像在 Cloud Run 中部署服務：

    在 Cloud Shell 中，執行下列指令：

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

成功部署後，您會收到 Cloud Run 服務的 URL。您可以使用瀏覽器瀏覽該 URL，查看您剛才部署的應用程式。輸入您的查詢，應用程式會提示 Vertex AI 文字模型並顯示回應。



