# 雲端執行序應用程式使用 Gradio 架構，說明如何搭配 Vertex AI API 操作

| |
|-|-|
|作者| [Romin Irani](https://github.com/rominirani)

此應用程式說明如何使用 [Gradio](https://www.gradio.app/) 架構的雲端執行序應用程式。

![Gradio 聊天應用程式畫面](../assets/gradio-app-screen.png "Gradio 聊天應用程式")

## 建置並將應用程式部署到雲端執行序

> 注意：**請在繼續之前，務必按照 [SETUP.md](../SETUP.md) 中的說明操作。**
另外，請確認您已複製這個存放庫，並且目前位於 ```chat-gradio``` 資料夾中。在進行其他指令時，此資料夾應為您的目前工作目錄。

若要在 [雲端執行序](https://cloud.google.com/run/docs/quickstarts/deploy-container) 中部署 Gradio 應用程式，我們需要執行下列步驟：

1. 雲端函式需要存取兩個環境變數：

   - `GCP_PROJECT` ：這組 Google Cloud 專案 ID。
   - `GCP_REGION` ：這是您要部署雲端函式的區域。例如，us-central1。

    這些變數之所以是必要的，是因為 Vertex AI 初始化需要 Google Cloud 專案 ID 和區域。以下是 `main.py` 函式中特定程式碼列：

`vertexai.init(project=PROJECT_ID, location=LOCATION)`

    請在 Cloud Shell 中執行下列指令：

    ```bash
    export GCP_PROJECT='<您的 GCP 專案 ID>'  # 變更此變數
    export GCP_REGION='us-central1'             # 如果你變更此變數，請確認 Model Garden 支援此區域。有疑慮時，請保留此變數。
    ```

2. 我們現在將為應用程式建置 Docker 映像，並把它推送到 Artifact Registry。為此，我們需要設定一個指向 Artifact Registry 名稱的環境變數。我們有一個指令可以為您建立此存放庫。

   請在 Cloud Shell 中執行下列指令：

   ```bash
   export AR_REPO='<以您的 AR 存放庫名稱取代>'  # 變更此變數
   export SERVICE_NAME='chat-gradio-app' # 這是我們的應用程式和雲端執行序服務的名稱。如果您喜歡，可以變更這個名稱。
   gcloud artifacts repositories create "$AR_REPO" --location="$GCP_REGION" --repository-format=Docker
   gcloud auth configure-docker "$GCP_REGION-docker.pkg.dev"
   gcloud builds submit --tag "$GCP_REGION-docker.pkg.dev/$GCP_PROJECT/$AR_REPO/$SERVICE_NAME"
   ```

3. 最後一個步驟，我們要將服務部署到雲端執行序，而我們會使用上一步驟建置並推送到 Artifact Registry 的映像：

    請在 Cloud Shell 中執行下列指令：

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



部署成功後，您會收到一個連往雲端執行序的 URL。您可以透過瀏覽器瀏覽這個網址，以檢視您剛才部署的應用程式。從其中一筆預先定義的查詢中進行選擇，而應用程式將會查詢 Vertex AI 文字模型並提供回應給您。



