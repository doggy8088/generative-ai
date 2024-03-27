# 範例應用程式可以協助您加速 Google Cloud 上的 Gen AI 應用程式

想建立與 Vertex AI PaLM 基礎模型整合的 Gen AI 應用程式嗎？您想要使用 Python Flask、Streamlit、Gradio 等標準架構在 Google Cloud 上架設這些應用程式嗎？那麼您來對地方了。

所列出的範例應用程式會提供您可以使用的應用程式範本。這些應用程式的關鍵目標是協助您快速入門，並協助您瞭解如何整合 Vertex PaLM API 和將這些應用程式部署到 Google Cloud 所需的指令。

您可以瀏覽不同應用程式，然後選取一個或兩個感興趣的應用程式。按一下任一件應用程式，即可查看詳細的文件、範本和在 Google Cloud 上部署的說明。

## 設定環境

我們會在 [Cloud Shell](https://cloud.google.com/shell) 中提供設定環境的說明。在執行任何範例應用程式之前，請務必依照 [SETUP.md](SETUP.zh.md) 中的說明進行操作。

## 範例應用程式

需求 | 應用程式名稱 | 使用的技術 |
|---|---|---|
|開發使用 Python Flask 架構和 Vertex AI PaLM API 模型的聊天應用程式。 |[chat-flask-cloudrun](chat-flask-cloudrun)|Cloud Run、Python Flask|
|開發使用 [Gradio](https://www.gradio.app/) 架構和 Vertex AI PaLM API 模型的聊天應用程式。|[chat-gradio](chat-gradio)|Cloud Run、Gradio、Python|
|開發使用 [Streamlit](https://streamlit.io/) 架構和 Vertex AI PaLM API 模型的聊天應用程式。|[chat-streamlit](chat-streamlit)|Cloud Run、Streamlit、Python|
|為客戶端應用程式提供 Vertex AI PaLM 程式碼模型的 API。|[code-predict-cloudfunction](code-predict-cloudfunction)|Cloud Functions v2、Python|
|為客戶端應用程式提供 Vertex AI PaLM 文字模型的 API。|[text-predict-cloudfunction](text-predict-cloudfunction)|Cloud Functions v2、Python|
|開發處理上傳檔案並摘要其內容的事件驅動應用程式。如果您正在尋找包含參考架構的詳細摘要解決方案，請參閱我們的 [Jump Start Solution - Generative AI Document Summarization](https://cloud.google.com/architecture/ai-ml/generative-ai-document-summarization)。|[summarization-gcs-cloudfunction](summarization-gcs-cloudfunction) |Cloud Functions v2、Cloud Storage、Python

## (選擇性)使用 Cloud Code for VS Code 外掛程式使用自訂範例

如果您不想使用 Cloud Shell，而且想使用像 VS Code 的開發人員 IDE，我們支援在 IDE 環境中匯入並執行/部署這些應用程式。

[Cloud Code for VS Code](https://cloud.google.com/code/docs/vscode) 為 Kubernetes 和 Cloud Run 應用程式的完整開發週期提供 IDE 支援，從建立叢集到執行您的完成應用程式。我們以自訂應用程式的形式提供完整的應用程式清單，您可以在已設定 Cloud Code 的 VS Code 中直接匯入這些清單。

假設您有 Visual Studio Code 和 Cloud Code 外掛程式設定，請按一下狀態列中的「Cloud Code」連結。

- 按一下「新增應用程式」
- 選擇「自訂應用程式」
- 當要求提供 Git 存放庫網址時，請輸入這個存放庫的網址：[https://github.com/doggy8088/generative-ai/language/sample-apps](https://github.com/doggy8088/generative-ai/language/sample-apps)
- 您會看到所有專案。選取您選擇的一個專案。
- 完成其他步驟將專案匯入 Visual Studio Code。



在下方觀看螢幕錄影：
<img src="assets/import-apps-into-cloudcode.gif" alt="將自訂應用程式匯入至雲端程式碼"/>



