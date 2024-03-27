# 雲端函式會包裝 PaLM Code Bison 模型

| |
|-|-|
| 作者 | [Romin Irani](https://github.com/rominirani)

此應用程式展示一個以 Python 編寫的雲端函式，用於初始化 Vertex AI 模組，然後提供一個端點，以呼叫 PaLM Code Bison 模型。

> 注意：**在您繼續之前，請確保您已按照 [SETUP.md](../SETUP.md) 中的說明進行操作。**
此外，請確保您已複製此存放庫，且目前處於 ```code-predict-cloudfunction``` 資料夾中。這應為您執行後續指令時的有效工作目錄。

## 需要環境變數

您的雲端函式需要存取兩個環境變數：

- `GCP_PROJECT` ：這是 Google Cloud 專案 ID。
- `GCP_REGION` ：這是您部署雲端函式的區域。例如：us-central1。

需要這些變數，因為 Vertex AI 初始化需要 Google Cloud 專案 ID 和區域。下列顯示 `main.py` 函式中的特定程式碼行：
`vertexai.init(project=PROJECT_ID, location=LOCATION)`

在 Cloud Shell 中，執行下列指令：

```bash
export GCP_PROJECT='<您的 GCP 專案 ID>'  # 變更這個
export GCP_REGION='us-central1'             # 如果您變更這個，請務必確保 Model Garden 支援此區域。如有疑問，請保留這個。
```

這些變數可透過以下 [說明] (https://cloud.google.com/functions/docs/configuring/env-var) 以下列任何方式設定：

1. 部署 Google 雲端函式時 [進行部署](https://cloud.google.com/functions/docs/configuring/env-var#setting_runtime_environment_variables)。我們將在下一個區段中部署雲端函式時使用這個方法。
2. 部署 Google 雲端函式後 [更新](https://cloud.google.com/functions/docs/configuring/env-var#updating_runtime_environment_variables) 環境變數。

## 部署雲端函式

假設您在已在當地電腦上設定 `gcloud` SDK 的情況下，擁有此專案的副本，請遵循下列步驟：

1. 移至這個專案的根資料夾。
2. 此資料夾應同時包含 `main.py` 和 `requirements.txt` 檔案。
3. 提供下列指令：

   ```bash
   gcloud functions deploy predictCode \
   --gen2 \
   --runtime=python311 \
   --region=$GCP_REGION \
   --source=. \
   --entry-point=predictCode \
   --trigger-http \
   --set-env-vars=GCP_PROJECT=$GCP_PROJECT,GCP_REGION=$GCP_REGION \
   --allow-unauthenticated
   ```

## 呼叫雲端函式

由於這個雲端函式會搭配 HTTP 觸發器進行部署，所以您可直接呼叫它。範例呼叫如下所示：

```bash
curl -m 70 -X POST https://$GCP_REGION-$GCP_PROJECT.cloudfunctions.net/predictCode \
-H "Content-Type: application/json" \
-d '{
  "prompt": "撰寫一個 Python 函式來呼叫 URL？"
}'
```

如果您希望看到一個格式更好的程式碼版本，請嘗試下列呼叫，使用新行來設定回應格式：

```bash
curl -m 70 -X POST https://$GCP_REGION-$GCP_PROJECT.cloudfunctions.net/predictCode \
-H "Content-Type: application/json" \
-d '{
"prompt": "撰寫一個 Python 函式來呼叫 URL？"
}'  | sed -e 's/\\n/\n/g'
```



