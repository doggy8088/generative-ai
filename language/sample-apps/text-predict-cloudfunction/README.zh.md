# 雲端函式封裝 PaLM 文字 Bison 模型

| |
| - | - |
| 作者 | [Romin Irani](https://github.com/rominirani)

此應用程式展示一個使用 Python 編寫的雲端函式，用於初始化 Google AI 頂點模組，並提供 API 端點呼叫 PaLM 文字 Bison 模型。

> 注意：**在開始之前，請務必遵循 [SETUP.md](../SETUP.zh.md) 中的說明。**
另外，請確定您已經複製這個倉庫，而且目前位於```text-predict-cloudfunction```資料夾。這是您在輸入其他命令時應該所在的目前工作目錄。

## 所需的環境變數

您的雲端函式需要使用兩個環境變數：

- `GCP_PROJECT`：這是 Google Cloud 專案 ID。
- `GCP_REGION`：這是您要部署雲端函式的區域。例如，us-central1。

這些變數是必要的，因為 Google AI 頂點的初始化需要 Google Cloud 專案 ID 和區域。來自 `main.py` 函式的特定程式碼行在此處顯示：
`vertexai.init(project=PROJECT_ID, location=LOCATION)`

在 Cloud Shell 中執行下列指令：

```bash
export GCP_PROJECT='<您的 GCP 專案 ID>'  # 變更這個變數
export GCP_REGION='us-central1'             # 如果您變更這個變數，請確定 Model Garden 支援此區域。如有疑問，請保留這個變數。
```

這些變數可透過任何下列方式設定為下列 [說明](https://cloud.google.com/functions/docs/configuring/env-var)：

1. 在 [部署](https://cloud.google.com/functions/docs/configuring/env-var#setting_runtime_environment_variables) Google Cloud 函式時。我們會在下一節部署 Cloud Function 時使用這個方法。
2. 在部署 Google Cloud 函式後 [更新](https://cloud.google.com/functions/docs/configuring/env-var#updating_runtime_environment_variables) 環境變數。

## 部署雲端函式

假設您的機器具備 `gcloud` SDK 架設和本地端專案副本，請遵循下列步驟：

1. 前往這個專案的根資料夾。
2. 此資料夾內應該要有 `main.py` 和 `requirements.txt` 檔案。
3. 輸入下列指令：

   ```bash
   gcloud functions deploy predictText \
   --gen2 \
   --runtime=python311 \
   --region=$GCP_REGION \
   --source=. \
   --entry-point=predictText \
   --trigger-http \
   --set-env-vars=GCP_PROJECT=$GCP_PROJECT,GCP_REGION=$GCP_REGION \
   --allow-unauthenticated
   ```

## 呼叫雲端函式

由於這個雲端函式使用 HTTP 引發器進行部署，因此您可以直接呼叫它。範例呼叫如下所示：

```bash
curl -m 70 -X POST https://$GCP_REGION-$GCP_PROJECT.cloudfunctions.net/predictText \
-H "Content-Type: application/json" \
-d '{
  "prompt": "美國最棒的旅遊景點有哪些？"
}'
```



