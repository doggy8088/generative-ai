# 設定配備說明，在 Google Cloud 上使用生成式 AI

此資料夾包含下列說明：

- 設定 Google Cloud 專案
- 筆記本環境
  - 設定 Colab
  - 設定 Vertex AI Workbench
- Vertex AI 的 Python SDK

## 設定 Google Cloud 專案

1. [選取或建立 Google Cloud 專案](https://console.cloud.google.com/cloud-resource-manager)。
當您第一次建立帳戶時，您會享有 300 美元的免費額度，可運用於您的運算/儲存成本。

2. [請確定已為您的專案啟用帳單](https://cloud.google.com/billing/docs/how-to/modify-project)。

3. [啟用 Vertex AI API](https://console.cloud.google.com/flows/enableapi?apiid=aiplatform.googleapis.com)。

## 筆記本環境

### Colab

[Google Colab](https://colab.research.google.com/) 讓您能在瀏覽器中撰寫並執行 Python 程式碼，而且設定步驟極為精簡。

如要將 Colab 與此儲存庫搭配使用，請按一下此儲存庫中任何筆記本檔案頂端的「在 Colab 中開啟」連結，即可在 Colab 中開啟檔案。接著依照檔案中的說明進行操作。

在 Colab 中，您需要進行驗證，才能從 Colab 使用 Google Cloud：

```py
from google.colab import auth
auth.authenticate_user()
```

使用 Vertex AI Python SDK 時，您還需要透過 GCP `project_id` 和 `location` 進行初始化：

```py
PROJECT_ID = "your-project-id"
LOCATION = "" #例如：us-central1

import vertexai
vertexai.init(project=PROJECT_ID, location=LOCATION)
```

### Vertex AI Workbench

[Vertex AI Workbench](https://cloud.google.com/vertex-ai-workbench) 是 Google Cloud 上的 JupyterLab 筆記本環境，讓您可以建立和自訂筆記本執行個體。您不必執行其他驗證步驟。

#### 在 Vertex AI Workbench 上建立筆記本執行個體

如要在 Vertex AI Workbench 上建立新的 JupyterLab 執行個體，請依照[此處說明建立使用者管理的筆記本執行個體](https://cloud.google.com/vertex-ai/docs/workbench/user-managed/create-new)。

#### 在 Vertex AI Workbench 上使用此儲存庫

啟動筆記本執行個體後，您可以在 JupyterLab 環境中複製此儲存庫。若要執行此動作，請在 JupyterLab 中開啟終端機。接著執行下列指令，將儲存庫複製到您的執行個體中：

```sh
git clone https://github.com/doggy8088/generative-ai.git
```

#### 本機開發

- 安裝 [Google Cloud SDK](https://cloud.google.com/sdk)。

- 取得驗證憑證。透過執行下列指令並遵循 OAuth 2 流程，建立本機憑證 (在此處進一步了解此指令 [說明](https://cloud.google.com/sdk/gcloud/reference/beta/auth/application-default/login))：

  ```bash
  gcloud auth application-default login
  ```

## Python 函式庫

安裝最新的 Python SDK：

```sh
!pip install google-cloud-aiplatform --upgrade
```

您需要使用 `project_id` และ `location` 初始化 `vertexai`：

```py
PROJECT_ID = "your-project-id"
LOCATION = "" #例如：us-central1

import vertexai
vertexai.init(project=PROJECT_ID, location=LOCATION)
```



