# 檢索增強產生

使用 Google Cloud Vertex AI 檢索、PaLM 和 LangChain

---

## Vertex AI 檢索

_**重點提示：**大型語言模型 (LLM) 在與搜尋引擎等資訊檢索工具結合使用時，最為用途廣泛。如此可確保產生的內容建立在經過驗證、相關且最新的資訊上。_
_此資料夾示範如何使用 Google Cloud [Vertex AI 檢索](https://cloud.google.com/enterprise-search) 達成此目的。_

### 什麼是 Vertex AI 檢索？

Vertex AI 檢索讓開發人員能快速輕鬆地運用 Google 基礎模型、搜尋專業知識和對話式 AI 技術，建立企業等級的生成式 AI 應用程式，即使其機器學習技能有限亦是如此。

Vertex AI 檢索讓組織可以快速為客戶和員工建立由生成式 AI 提供支援的搜尋引擎。該解決方案透過 Google Cloud Console 提供，也可以透過 API 整合進企業工作流程或大型語言模型。

### 使用 Vertex AI 檢索

以文件、網站或關聯式資料庫的形式上傳資料，然後使用者可以使用自然語言查詢檢索最相關的文件區塊。API 提供特定組態選項，這些選項的設計目的在能與 LLM 順暢搭配，例如選擇不同的文件區塊類型。

### 將 Vertex AI 檢索與 LLM 結合

隨著 LLM 在功能和受歡迎程度方面持續爆炸性成長，資訊檢索工具已日益明顯成為堆疊中不可或缺的一部分，以解鎖生成式 AI 許多最有價值的使用案例。

這些檢索工具讓您能有效率地從自己的資料中擷取資訊，並將最相關的摘錄直接插入 LLM 提示中。如此可讓您將生成式 AI 輸出建立在您已知相關、經過驗證和最新的資料中。

大多數檢索方式通常需要建立文件嵌入和設定向量搜尋引擎。此類自訂解決方案耗時且建立、維護和主控複雜。反觀 Vertex AI 檢索是一個即開即用搜尋引擎，以管理服務的形式提供 Google 等級的結果。

python [檢索器](https://python.langchain.com/docs/modules/data_connection/retrievers.html) 類別已於 `/utils/retriever.py` 中提供，讓您能夠針對 Vertex AI 檢索引擎執行搜尋。

## 目錄

請注意：這些範例使用 Vertex AI 和 Vertex AI 檢索 API，它們是付費服務。

有關如何提供協助、設定環境以及生成式 AI 和 Google 工具的概況說明，請參閱儲存庫根目錄中的 [README](../README.zh.md)。

```text
檢索增強產生/     - 此目錄
├── 範例/
    ├── question_answering.ipynb    - 文件問答範例
    ├── summarization.ipynb         - 文件摘要範例 (即將推出) 
```



