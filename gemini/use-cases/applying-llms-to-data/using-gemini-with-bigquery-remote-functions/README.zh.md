# 分析圖像和文本，並透過 BigQuery 和遠端函式使用 Gemini

| |
|-|-|
|作者 | [Shane Glass](https://github.com/shanecglass)

## 概要

此儲存庫提供範例，說明如何使用 Google 最大且功能最強大的 AI 模型 [Gemini](https://blog.google/technology/ai/gemini-api-developers-cloud/)，來分析您的 BigQuery 資料。可以在 Google Cloud 上使用 BigQuery 和 [遠端函式](https://cloud.google.com/bigquery/docs/remote-functions) 分析影像和文字輸入，方法是利用 [Vertex AI Gemini API](https://cloud.google.com/vertex-ai/docs/generative-ai/start/quickstarts/quickstart-multimodal)。下列說明應有助於您入門。

## 使用 SQL 呼叫 Gemini

此儲存庫讓您可以使用 SQL 傳送要求給 Gemini，並像針對任何其他 BigQuery 查詢一樣取得結果。這種做法有幾個優點：

- 讓熟悉 SQL 的使用者能夠利用 Gemini 的功能，而無需撰寫其他程式碼
- 您可以更輕易地分析大量資料，而不必針對每一張影像或文字提示個別提出要求
- 您無需先將資料匯出 BigQuery，才能使用 Gemini 分析資料

## 關於此示範

我們建立了一個 Terraform 模組，用於部署所有必要的資源，以便在 BigQuery 中使用 SQL 呼叫 [Vertex AI Gemini API](https://cloud.google.com/vertex-ai/docs/generative-ai/start/quickstarts/quickstart-multimodal)。

部署模組後，您將能夠使用兩個 [BigQuery 遠端函式](https://cloud.google.com/bigquery/docs/remote-functions)：

- 使用 `gemini_bq_demo_image` 分析影像和文字 (多模態輸入)：此遠端函式取得 GCS 中的影像作為輸入，並提示 Gemini 1.0 Pro Vision 模型建立影像的簡要說明
- 使用 `gemini_bq_demo_text` 分析文字： 此遠端函式直接取得 BigQuery 表格中的文字作為提示，然後讓 Gemini 1.0 Pro 模型傳回回應

您還可以使用兩個 BigQuery 儲存程序，讓您輕鬆使用實際影像和文字資料測試每個遠端函式：

- `image_query_remote_function_sp`: 此 SQL 查詢使用 `gemini_bq_demo_image` 遠端函式，將儲存在物件表格 (作為模組的一部分加以部署) 中的影像 URI 清單連同提示傳送給 Gemini
- `text_query_remote_function_sp`: 此 SQL 查詢使用 `gemini_bq_demo_text` 遠端函式，將附有預先撰寫文字提示的範例 BigQuery 表格 (作為模組的一部分加以部署) 傳送給 Gemini

## 入門

### 部署基礎架構

**注意：**雖然不一定要為這個範例使用新的 GCP 專案，但使用新的 GCP 專案可能會更為容易。這可以讓清理工作更容易進行，因為您可以刪除整個專案，以確保移除所有資產，並確保沒有任何潛在的衝突會與現有資源發生。您也可以在部署資源後執行 `terraform destroy` 來移除資源，但這也會停用相關的 API。

#### 1. 在 Cloud Shell 中複製此儲存庫

您需要在 Cloud Shell 中設定 Google Cloud 專案，首先在本地複製此儲存庫，然後將工作目錄設定為這個資料夾，方式如下所示。

```shell
  gcloud config set project <PROJECT ID>
  git clone  https://github.com/doggy8088/generative-ai/
  cd ./generative-ai/gemini/use-cases/applying-llms-to-data/using-gemini-with-bigquery-remote-functions
  ```

#### 2. 啟用 Cloud Resource Manager API



檢查以確定已啟用 [雲端資源管理員 API](https://console.cloud.google.com/apis/library/cloudresourcemanager.googleapis.com)

#### 3. 初始化 Terraform

首先，透過執行下列指令來初始化 Terraform

```shell
  terraform init
  ```

#### 4. 查看資源

查看已在設定中定義的資源：

``` shell
  terraform plan
  ```

#### 5. 部署 Terraform 腳本

```shell
  terraform apply
  ```

當系統提示你執行動作時，請輸入 `yes`。Terraform 會提示你提供專案 ID 和區域資訊。此範例已使用 `us-central1` 區域進行測試。Terraform 將顯示訊息，顯示部署進度。

建立所有資源後，Terraform 會顯示以下訊息：

```shell
  Apply complete!
  ```

Terraform 輸出中也會列出你需要的其他資訊，如下：

- 開啟 BigQuery 編輯器連結，以呼叫 `image_query_remote_function_sp` 儲存程序，分析所提供的範例圖片
- 開啟 BigQuery 編輯器連結，以呼叫 `text_query_remote_function_sp` 儲存程序，分析所提供的範例文字提示

如果你需要再度查看 Terraform 輸出，只要在命令列中輸入 `terraform output` 即可。

## 使用你的新部署分析範例資料

資源已部署完成，因此 BigQuery 遠端函式已準備好在 SQL 查詢中使用。

### 1. 分析文字和圖片 (多模式)

當你呼叫 `image_query_remote_function_sp` 儲存程序時，Gemini 會分析範例圖片。只需為儲存程序按一下 `呼叫儲存程序`，然後為產生的查詢按一下 `執行`，即可透過遠端函式取得 Gemini 產生的圖片說明。

<p align="center">
  <img src="./src/examples/image_query_experience.gif" alt="展示如何於主控台中分析文字提示的示範" width=1600px>
</p>

### 2. 只分析文字

當你呼叫 `text_query_remote_function_sp` 儲存程序時，Gemini 會分析預先寫好的文字提示。只需按一下 `呼叫儲存程序`，然後在產生的查詢中按一下 `執行`，即可透過遠端函式取得 Gemini 產生的回應。

<p align="center">
  <img src="./src/examples/text_query_experience.gif" alt="展示如何於主控台中分析文字提示的示範" width=1600px>
</p>

## 運作原理

### 架構圖

#### 影像分析

<p align="center">
  <img src="./src/architecture/image_analysis_diagram.png" alt="分析圖片的架構圖" width=800px>
</p>

<ol>
  <li>範例圖片上傳到 Cloud Storage 儲存貯體，並在 BigQuery 中建立 GCS 物件資料表</li>
  <li>Cloud Workflows 在 BigQuery 中建立儲存程序，其中包含範例查詢，此查詢會參照步驟 1 中建立的物件資料表，藉由使用 Vertex AI Gemini API 將圖片傳遞到遠端函式進行分析</li>
  <li>步驟 2 的儲存程序用於透過 BigQuery 連線來呼叫 Cloud Functions</li>
  <li>Cloud Functions 透過將範例圖片傳遞到 Vertex AI Gemini API (步驟 5) 來分析這些範例圖片，以簡要說明範例圖片，並將 Vertex AI Gemini API 的結果傳回，作為查詢結果</li>
</ol>

#### 文字分析



<p align="center">
  <img src="./src/architecture/text_analysis_diagram.png" alt="" width=800px>
</p>
<ol>
  <li>Cloud Workflows 建立包含範例查詢 BigQuery 中的儲存程序，並提供包含用於說明各種地標範例文字提示的 <code>sample_text_prompts</code> 表格。範例查詢利用 Vertex AI Gemini API 將這些提示傳遞給遠端函式進行分析</li>
  <li>步驟 2 的儲存程序用於透過 BigQuery 連線呼叫 Cloud 函式</li>
  <li>Cloud 函式分析範例文字的文字輸入，將它們傳遞給 Vertex AI Gemini API (步驟 4) 以取得每個提示的文字回應，並將結果從 Vertex AI Gemini API 傳回為查詢結果</li>
</ol>

## 價格估計

每日各執行 4 次文字和影像分析並安裝此展示 (在 Cloud Shell CLI 中執行 `terraform apply`)，每月成本約為 0.06 美元。詳情請參閱 [Google Cloud 價格計算器](https://cloud.google.com/products/calculator/#id=d3f64c61-9afb-4467-a6af-2bdd9540d489)。總月費將根據使用情況而有所不同，包括部署和終止此展示的頻率。

**注意**：多模組模型在 Vertex AI 中使用，費用於 2024 年 1 月 15 日開始。我們估計每日執行此展示 4 次，總費用每月將增加 *3.73 美元*。有關完整詳情，請參閱 [Vertex AI 價格頁面，以取得生成式 AI](https://cloud.google.com/vertex-ai/pricing#generative_ai_models)。以下是這項估計的細目：

- 文字分析
  - 文字輸入每月 0.02 美元
  - 文字輸出每月 0.23 美元

- 影像分析
  - 影像輸入每月 3.30 美元
  - 文字輸出每月 0.18 美元

請記住，像 Gemini 的生成式 AI 模型是非決定論的，因此相關成本會根據輸出長度有所不同，無法明確估計。

## 改造成你的專屬範例

你可以針對自己的使用案例調整此展示！查看下列文字和影像分析說明。

### 分析影像

你可以開始分析上傳至 Cloud Storage 的任何影像，方式如下：

1. [建立 Cloud Storage 物件表格](https://cloud.google.com/bigquery/docs/object-tables)

如果你的儲存貯存在與你部署此範例相同的地區，你應該可以重複使用現有的 BigQuery 連線。如果不是，你可能需要建立新的連線。

1. 修改 Cloud 函式第 40 行的 `context` 變數

你可以編輯已部署的 `gemini-bq-demo-image` 來執行此動作。按一下 Function Details 頁面頂部的編輯按鈕，然後按一下下一步以查看內嵌編輯器。變更 `content` 變數的值，以告訴 Gemini 該如何處理你的影像，然後按一下部署。

查看 [此範例筆記本](https://github.com/doggy8088/generative-ai/blob/main/gemini/use-cases/intro_multimodal_use_cases.zh.ipynb) 來獲得靈感並取得想法，看看你可以要求 Gemini 對影像執行哪些操作。

1. 更新 `image_query_remote_function_sp` 儲存程序並執行

更新儲存程序第 5 行，以參考你在步驟 1 中建立的物件表格，然後執行查詢。

### 分析文字



你可以透過分析你自己的文字輸入來開始，而不需要去修改現有的 Cloud Function。只要將在儲存程序 `text_query_remote_function_sp` 第 3 行的 `text_prompt` 替換成你想分析的文字即可。你可以輸入一個文字字串，或是你也可以從 BigQuery 表格中參考文字提示的欄位。如果你要使用 BigQuery 表格中的一個欄位，請確認更新儲存程序第 5 行的表格參考。

## 清理

在你完成示範後，你可以透過以下步驟刪除你所建立的所有資源：

1. 更新 `variables.tf` 檔案。

    將 `force_destroy` 變數的預設值從 `false` 改為 `true`。將 `deletion_protection` 變數的預設值從 `false` 改為 `true`。

1. 執行 `terraform apply`。

    這套用你於步驟 1 所做的變更到你的資源中，以便讓它們容易地被刪除。

1. 刪除 BigQuery 資料集。

    於你的 CLI 中執行以下指令來刪除所建立的 BigQuery 資料集：

    ```shell
        bq rm -r -f -d gemini_demo
    ```

1. 執行 `terraform destroy`。

    這會刪除你所建立的所有剩餘資源。



