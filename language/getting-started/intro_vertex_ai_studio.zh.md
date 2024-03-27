# Vertex AI Studio 使用入門

| |
|-|-|
|作者 | [Thu Ya Kyaw](https://github.com/iamthuya)

本指南提供如何透過 Google Cloud 控制台使用 Vertex AI Studio 的說明，無需使用 API 或 Python SDK。

## Google Cloud 上的 Vertex AI Studio

[Vertex AI Studio](https://cloud.google.com/generative-ai-studio) 是一個雲端平台，使用者可以在此建立生成式 AI 模型並進行實驗。此平台提供許多工具和資源，即使沒有機器學習背景也能輕鬆入門生成式 AI。

![圖片](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/overview_one.jpg)

---

## 語言

有兩種方法可以在 Google Cloud 上的 Vertex AI Studio 存取語言服務：

- 按一下 Vertex AI Studio 總覽頁面上 **語言** 方塊底部的 **開啟** 按鈕。



按一下後，系統會顯示以下頁面。

![生成式 AI 的語言頁面](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/landing_one.jpg)

---

## 開始使用

### 建立提示

建立提示可以根據與您的商業個案相關的任務 (包括產生程式碼) 設計提示。為開始使用，請按一下下圖所示的 **+ 文字提示** 按鈕

![建立提示](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/click_create_prompt.jpg)

按一下後，系統會重新引導您至以下頁面。您可以懸停或按一下 **?** 按鈕，以進一步了解每個欄位和參數。此外，已對以下圖片加上註解，以快速說明介面。

![圖片](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/new_prompt_annotated.jpg)

您可以提供期望的輸入文字給模型，例如問題。然後模型會根據您建構提示的方式提供回應。找出最佳輸入文字 (提示) 以從模型取得期望回應的過程稱為 **提示設計**。

目前還沒有設計提示的最佳方式。通常，您可以使用 3 種方法來以期望的方式調整模型的回應。

- **零次學習提示** - 在此方法中，不會提供 LLM 有關其受要求執行特定任務的額外資料。只會提供描述該任務的提示。例如，如果您希望 LLM 回答一個問題，您只要提示「什麼是提示設計？」
- **一次學習提示** - 在此方法中，會提供 LLM 關於其受要求執行任務的一個範例。例如，如果您希望 LLM 寫一首詩，您可能給它一個單一範例詩作。
- **少量學習提示** - 在此方法中，會提供 LLM 少量關於其受要求執行任務的範例。例如，如果您希望 LLM 寫一篇新聞文章，您可能給它幾篇新聞文章閱讀。

您可能也會在上述圖片中看到 **自由格式** 和 **結構化** 標籤。這些是設計提示時可使用的兩種模式。



- **自由形式** - 此模式提供一種自由且輕鬆的方式來設計提示。它適用於沒有其他範例的小提示和實驗提示。您將使用此模式來探索零次提示。
- **結構化** - 此模式提供一種易於使用的範本方法來提示設計。在此模式中可以將內容和多個範例新增到提示中。這對於您稍後將探索的一次和少次提示法特別有用。

---

### 自由形式模式

您將在 **自由形式** 模式中嘗試零次提示。若要開始，

- 將「什麼是提示畫廊？」複製到提示輸入欄位
- 按一下頁面右側的 **提交** 按鈕

模型將回應提示畫廊一詞的完整定義。

![image](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/new_prompt_freeform.jpg)

以下是可以供您探索的一些探討練習。

- 將 `記號極限` 參數調整為 `1`，然後按一下 **提交** 按鈕
- 將 `記號極限` 參數調整為 `1024`，然後按一下 **提交** 按鈕
- 將 `溫度` 參數調整為 `0.5`，然後按一下 **提交** 按鈕
- 將 `溫度` 參數調整為 `1.0`，然後按一下 **提交** 按鈕

檢查回應是否在更改參數時會改變？

---

### 結構化模式

使用 **結構化** 模式，您可以更組織的方式設計提示。您也可以在各自的輸入欄位中提供 **內容** 和 **範例**。這是學習一次和少次提示的好機會。

在本節中，您將要求模型完成一個句子。回到 **文字提示** 視窗，

- 如果您尚未執行此動作，請按一下 **結構化** 標籤
- 在 **輸入** 欄位中複製「天空的顏色是」
- 按一下頁面右側的 **提交** 按鈕

您會看到與下方圖片中顯示的結果類似。

![image](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/new_prompt_structured_zero_shot.jpg)

模型給予一個完整的句子作為回應，而不是完成句子，這並不是我們想要的。您可以使用一次提示來嘗試影響模型的回應。這一次，您將新增一個範例作為模型輸出的基礎。

在 **範例** 欄位下方，

- 將「草的顏色是」複製到 **輸入** 欄位
- 將「綠色」複製到 **輸出** 欄位
- 按一下頁面右側的 **提交** 按鈕。

現在模型將回應並完成句子。
回應應類似於此。

![image](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/new_prompt_structured_one_shot.jpg)

恭喜！您已成功地影響模型產出回應的方式。

---

對於下一個任務，您將使用模型對句子執行情緒分析，例如判定電影評論是正面的還是負面的。回到 **文字提示** 視窗，

- 將提示「這段時光過得很好！」複製到 **輸入** 欄位
- 按一下頁面右側的 **提交** 按鈕

![image](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/new_prompt_structured_sentiment_zero_shot.jpg)



如你所見，模型沒有足夠的資訊來了解你是要進行情緒分析。可透過提供模型幾個你正在尋找的範例來改善此問題。

請嘗試新增範例，如下圖所示：

**輸入**                         | **輸出** |
|-----------------------------------|------------|
| 結構和娛樂效果良好的電影 | 正面   |
| 我在 10 分鐘後睡著了    | 負面   |
| 這部電影還可以                  | 中立

然後按一下頁面右側的 **SUBMIT** 按鈕。

![圖片](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/new_prompt_structured_sentiment_few_shot.jpg)

現在，模型會以你想要的方式回應。它應該回應為 **正面**。

你也可以儲存新設計的提示。如要儲存提示，按一下 **儲存** 按鈕，並隨意命名。

![圖片](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/new_prompt_save_prompt.jpg)

已儲存的提示將顯示在 **我的提示** 標籤中。

![圖片](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/my_prompts_saved.jpg)

---

### 建立聊天提示

回到 **語言** 頁面，然後按一下 **+ 文字聊天** 按鈕建立新的聊天提示。

![文字提示](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/click_create_chat_prompt.jpg)

你會看到新的聊天提示頁面。這與你稍早看過的新提示頁面類似。

![圖片](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/new_chat_prompt.jpg)

在此部分，你會將內容新增至聊天中，並讓模型根據所提供的內容回應。我們將這些內容新增至 **內容** 欄位。

- 將這些內容複製至 **內容** 欄位

>> 你的名字是 Roy。 <br/>
>> 你是 IT 部門的技術支援人員。 <br/>
>> 你只能對任何疑問回答「你是否已嘗試關機再重開？」。

- 將「我的電腦好慢」複製至聊天方塊，然後
- 按 **Enter** 鍵或按一下傳送訊息按鈕 (右箭頭按鈕)

![圖片](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/new_chat_prompt_with_context.jpg)

模型會考慮提供的其他內容，並在限制內回答問題。

## 提示範例庫

提示範例庫讓你探索生成式 AI 模型如何適用於各種使用案例。有各種主題：摘要、分類、萃取、寫作和創意構思，供你探索。返回 **開始** 頁面，然後依自己的步調探索這些主題。

![文字生成式 AI 的語言頁面](https://storage.googleapis.com/github-repo/img/gen-ai-studio/language/prompt-gallery/landing_one.jpg)



