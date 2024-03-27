# Vertex AI 對話

| |
|-|-|
|作者 | [Kristopher Overholt](https://github.com/koverholt)

## 概述

[資料儲存代理程式](https://cloud.google.com/generative-ai-app-builder/docs/agent-intro)
是
[Vertex AI 對話](https://cloud.google.com/generative-ai-app-builder)
中的一項功能，建構於
[Dialogflow CX](https://cloud.google.com/dialogflow)
的功能之上。

![Vertex AI 對話示範](static/vertex-ai-conversation.png)

使用資料儲存代理程式時，您可以提供一個網站網域、結構化資料或
非結構化資料，然後，資料儲存代理程式會分析您的內容並建立一個
由資料儲存和大型語言模型支援的虛擬代理程式。您的客戶和最終用戶
之後就能與代理程式對話，並詢問有關該內容的問題。請參閱
[資料儲存代理程式文件](https://cloud.google.com/generative-ai-app-builder/docs/agent-usage)
和 Codelab，以
[使用 Vertex AI 對話建立自然語言對話應用程式](https://codelabs.developers.google.com/codelabs/vertex-ai-conversation)
，取得更多資訊。

## 建置網頁應用程式的步驟

1. 使用優先選用的方式或套件管理員安裝 [Node.js](https://nodejs.org/en)
1. 從這個目錄執行 `npm install`
1. 執行 `npm run build` 以在 `build` 目錄中生成靜態網站

## 將網頁應用程式部署至 Firebase 的步驟

1. 導航至 [Firebase 控制台](https://console.firebase.google.com/)
1. 在新的或現有的 GCP 專案中配置 Firebase
1. 在 Firebase 控制台中，前往「Hosting」，然後新增一個網站 (例如
   `your-firebase-app-name`) 
1. 安裝 [Firebase CLI](https://firebase.google.com/docs/cli)
1. 在應用程式根目錄執行 `firebase init`，然後按照提示選擇「Hosting」，使用 `build` 目錄，並對後續關於重寫、部署、404 和索引頁面的問題回答「N」。
1. 執行
   `firebase target:apply hosting your-firebase-app-name your-firebase-app-name`
   其中 `your-firebase-app-name` 是您在先前步驟中建立的 Firebase Hosting 網站名稱
1. 若要設定預設部署目標，請在 `firebase.json` 中加入一行，寫入 Firebase Hosting 網站的名稱，例如：

   ```json
   {
     "hosting": {
       "target": "your-firebase-app-name",  # <--- 加入這行
       "public": "build",
       "ignore": [
         "firebase.json",
         "**/.*",
         "**/node_modules/**"
       ]
     }
   }
   ```

1. 執行 `firebase deploy`

## 存取應用程式

在瀏覽器中，使用類似於下列網址的網址前往已部署的應用程式：

[https://vertex-ai-conversation.web.app/](https://vertex-ai-conversation.web.app/)

恭喜您，成功部署了 Vertex AI 對話示範！

## 其他資源

您可以繼續透過這些指南和資源了解對話式 AI 和生成式 AI：

- [Vertex AI 對話簡介](https://cloud.google.com/generative-ai-app-builder/docs/agent-intro)
- [建立和使用資料儲存代理程式](https://cloud.google.com/generative-ai-app-builder/docs/agent-usage)
- [Dialogflow CX 文件](https://cloud.google.com/dialogflow/cx/docs)
- [資料儲存代理程式文件](https://cloud.google.com/dialogflow/cx/docs/concept/data-store-agent)
- [Google Cloud 中的生成式 AI](https://cloud.google.com/ai/generative-ai)



