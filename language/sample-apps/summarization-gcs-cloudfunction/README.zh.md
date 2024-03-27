# 雲端函式示範如何處理 Google Cloud Storage 中上傳的檔案，並使用 PaLM Vertex AI API 對內容進行摘要

| |
|-|-|
|作者 | [Romin Irani](https://github.com/rominirani)

此應用程式展示了一個以 Python 編寫的雲端函式，當檔案上傳到設定好的特定的 Google Cloud Storage 儲存區時觸發。它會執行下列動作：

- 讀取檔案內容。
- 使用提示字串呼叫 PaLM Text Bison 模型以摘要內容。
- 將摘要資料寫入另一個 Google Cloud Storage (GCS) 儲存區。

> 注意：**在繼續之前，請務必按照 [SETUP.md](../SETUP.zh.md) 中的說明進行。**
此外，請確保您已複製這個存放庫並目前位於 ```summarization-gcs-cloudfunction``` 資料夾。在接下來的指令中，此資料夾應為您目前的有效工作目錄。

## 所需的環境變數

您的雲端函式需要存取兩個環境變數：

- `GCP_PROJECT` ：此為 Google Cloud 專案 ID。
- `GCP_REGION` ：此為您會部署雲端函式的區域，例如 us-central1。

這些變數是必要的，因為 Vertex AI 初始化需要 Google Cloud 專案 ID 和區域。`main.py` 函式中有顯示特定程式碼程式碼列：
`vertexai.init(project=PROJECT_ID, location=LOCATION)`

在 Cloud Shell 中，執行下列指令：

```bash
export GCP_PROJECT='<Your GCP Project Id>'  # Change this
export GCP_REGION='us-central1'             # If you change this, make sure region is supported by Model Garden. When in doubt, keep this.
```

這些變數可以透過下列任何方式，使用下列 [說明](https://cloud.google.com/functions/docs/configuring/env-var) 設定：

1. 在 [部署](https://cloud.google.com/functions/docs/configuring/env-var#setting_runtime_environment_variables) Google Cloud 函式時。我們會在下一個區塊部署雲端函式時使用這個方法。
2. 在部署 Google Cloud 函式後 [更新](https://cloud.google.com/functions/docs/configuring/env-var#updating_runtime_environment_variables) 環境變數。

## 部署雲端函式和相關雲端資源

### 建立 GCS 儲存區

我們需要建立 2 個 GCS 儲存區：

- 第一個儲存區用於上傳要摘要的檔案。讓我們將儲存區命名為 `$BUCKETNAME`。建立環境變數來儲存您的儲存區名稱，如下所示：



```bash
export BUCKET_NAME='Your GCS Bucket Name'
```

- 第二個儲存區會有 `-summaries` 的字首。

您可以在 Google Cloud Console 或透過 `gsutil` 指令從命令列建立儲存區。在 Cloud Shell 中執行下列指令。

```bash
gsutil mb -l $GCP_REGION gs://"$BUCKET_NAME"
gsutil mb -l $GCP_REGION gs://"$BUCKET_NAME"-summaries
```

### 部署函式

假設您在個人電腦上有一份這個專案且上面已設定好 `gcloud` SDK，請執行下列步驟：



1. 前往此專案的根資料夾。
2. 此資料夾必須同時包含 `main.py` 和 `requirements.txt` 檔案。
3. 提供下列指令：

   ```bash
   gcloud functions deploy summarizeArticles \
   --gen2 \
   --runtime=python311 \
   --source=. \
   --region=$GCP_REGION \
   --project=$GCP_PROJECT \
   --entry-point=summarize_gcs_object \
   --trigger-bucket=$BUCKET_NAME \
   --set-env-vars=GCP_PROJECT=$GCP_PROJECT,GCP_REGION=$GCP_REGION \
   --max-instances=1 \
   --quiet
   ```

## 呼叫雲端函式

由於此雲端函式是使用 GCS 觸發器進行部署，因此您需要執行下列步驟才能看到完整流程：

1. 確保您已建立以下 GCS 儲存空間：`$BUCKET_NAME` 和 `$BUCKET_NAME-summaries`。
2. 上傳包含文字的檔案 (已提供範例檔案 [story.md](story.zh.md)) 到 `$BUCKET_NAME` 儲存空間。
3. 此時應觸發 `summarizeArticles` 函式，在幾秒內，您應該會看到在 `$BUCKET-summaries` 儲存空間中建立的 `story.md` (摘要形式) 檔案。



