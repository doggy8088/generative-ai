# Cloud Run 實作應用使用 Streamlit Framework，展示如何使用 Vertex AI Gemini API

| |
|-|-|
|作者 | [Lavi Nigam](https://github.com/lavinigam-gcp)

此應用展示如何在 Cloud Run 應用中使用 [Streamlit](https://streamlit.io/) 架構。

以下顯示應用的範例截圖和影片示範：

## 應用截圖

<img src="https://storage.googleapis.com/github-repo/img/gemini/sample-apps/gemini-streamlit-cloudrun/assets/gemini_pro_text.png" width="50%"/>

## 在本地執行應用程式 (在 Cloud Shell 中)

> 注意：**在繼續之前，請務必遵循 [SETUP.md](../SETUP.md) 中的說明。**
另外，請務必複製這個存放庫，而且目前位於 `gemini-streamlit-cloudrun` 資料夾中。此資料夾應為其他命令的目前有效工作目錄。

若要在本地執行 Streamlit Application (在 Cloud Shell 中)，我們需要執行下列步驟：

1. 設定 Python 虛擬環境並安裝依賴關係：

    在 Cloud Shell 中，執行下列命令：

    ```bash
    python3 -m venv gemini-streamlit
    source gemini-streamlit/bin/activate
    pip install -r requirements.txt
    ```

2. 你的應用程式需要存取兩個環境變數：

   - `GCP_PROJECT`：這是 Google Cloud 專案 ID。
   - `GCP_REGION`：這是用於部署 Cloud Run 應用程式的區域。例如：us-central1。
  
    由於 Vertex AI 初始化需要 Google Cloud 專案 ID 和區域，因此需要這些變數。`app.py` 函式的特定程式碼行在此處顯示：
    `vertexai.init(project=PROJECT_ID, location=LOCATION)`

    在 Cloud Shell 中，執行下列命令：

    ```bash
    export GCP_PROJECT='<你的 GCP 專案 Id>'  # 變更此專案
    export GCP_REGION='us-central1'             # 如果變更這個區域，請務必確認區域受支援。
    ```

3. 若要本地執行應用程式，請執行下列命令：

    在 Cloud Shell 中，執行下列命令：

    ```bash
    streamlit run app.py \
      --browser.serverAddress=localhost \
      --server.enableCORS=false \
      --server.enableXsrfProtection=false \
      --server.port 8080
    ```

這個應用程式將啟動，而且系統會提供一個前往應用的 URL。請使用 Cloud Shell 的 [網頁預覽](https://cloud.google.com/shell/docs/using-web-preview) 功能啟動預覽頁面。你也可以在瀏覽器中瀏覽該頁面以檢視應用程式。選擇你想要查看的功能，而該應用程式會提示 Vertex AI Gemini API 並顯示回應內容。

## 建立並將應用部署到 Cloud Run

> 注意：**在繼續之前，請務必遵循 [SETUP.md](../SETUP.md) 中的說明。**
另外，請務必複製這個存放庫，而且目前位於 `gemini-streamlit-cloudrun` 資料夾中。此資料夾應為其他命令的目前有效工作目錄。

若要在 [Cloud Run](https://cloud.google.com/run/docs/quickstarts/deploy-container) 中部署 Streamlit Application，我們需要執行下列步驟：



1.您的 Cloud Run 應用程式需要存取兩個環境變數：

- `GCP_PROJECT`：這是 Google Cloud 專案 ID。
- `GCP_REGION`：這是您在其中部署 Cloud Run 應用程式的區域。例如：us-central1。

這些變數非常重要，因為 Vertex AI 初始化需要 Google Cloud 專案 ID 和區域。以下是 `app.py` 函式的特定程式碼行：
`vertexai.init(project=PROJECT_ID, location=LOCATION)`

在 Cloud Shell 中，執行以下指令：

```bash
export GCP_PROJECT='<您的 GCP 專案程式碼>'  # 變更為您的資料
export GCP_REGION='us-central1'             # 如果你變更此項目，請確定該區域獲得支援。
```

2.現在，您可為應用程式建置 Docker 映像檔，並將其推播至 Artifact Registry。為此，您需要設定一個會指向 Artifact Registry 名稱的環境變數。以下指令碼包含一個指令，可為您建立此 Artifact Registry 存放庫。

在 Cloud Shell 中，執行以下指令：

```bash
export AR_REPO='<以您的 AR 存放庫名稱取代>'  # 變更為您的資料
export SERVICE_NAME='gemini-streamlit-app' # 這是我們的應用程式和 Cloud Run 服務的名稱。您可以變更為您想要的。

# 確定您位於 'gemini-streamlit-cloudrun' 的現行目錄中
gcloud artifacts repositories create "$AR_REPO" --location="$GCP_REGION" --repository-format=Docker
gcloud auth configure-docker "$GCP_REGION-docker.pkg.dev"
gcloud builds submit --tag "$GCP_REGION-docker.pkg.dev/$GCP_PROJECT/$AR_REPO/$SERVICE_NAME"
```

3.最後一個步驟是在 Cloud Run 中使用我們已建置並在上一個步驟推播至 Artifact Registry 的映像檔來部署服務：

在 Cloud Shell 中，執行以下指令：

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

在部署成功後，您會收到一個指向 Cloud Run 服務的網址。您可以在瀏覽器中瀏覽該網址，以查看您剛部署的 Cloud Run 應用程式。選擇您想要查看的功能，應用程式會提示 Vertex AI Gemini API 並顯示回應。

恭喜！



