# 生成式 AI

- 語言

歡迎使用 Google Cloud [生成式 AI](https://cloud.google.com/ai/generative-ai/) 語言儲存庫。

## 目錄

<!-- markdownlint-disable MD033 -->



<pre>
language/
├── <a href="code">code/</a>
│   ├── <a href="code/code_chat.ipynb">[筆記本] 程式碼即時通話簡介</a>
│   ├── <a href="code/code_completion.ipynb">[筆記本] 程式碼自動完成功能簡介</a>
│   ├── <a href="code/code_generation.ipynb">[筆記本] 程式碼產生簡介</a>
│   └── <a href="code/code_retrieval_augmented_generation.ipynb">[筆記本] 搭配 Codey 使用的檢索擴充產生 (RAG)</a>
├── <a href="getting-started">getting-started/</a>
│   ├── <a href="getting-started/intro_palm_api.ipynb">[筆記本] Vertex AI PaLM API 與 Python SDK 入門</a>
│   └── <a href="getting-started/intro_vertex_ai_studio.md">Vertex AI Studio 簡介</a>
├── <a href="grounding">grounding/</a>
│   └── <a href="grounding/intro-grounding.ipynb">[筆記本] Vertex AI 接地簡介</a>
├── <a href="orchestration">orchestration/</a>
│   └── <a href="orchestration/langchain">langchain/</a>
│       └── <a href="orchestration/langchain/intro_langchain_palm_api.ipynb">[筆記本] LangChain 🦜️🔗 + Vertex AI PaLM API 入門</a>
├── <a href="prompts">prompts/</a>
│   ├── <a href="prompts/examples">範例/</a>
│   │   ├── <a href="prompts/examples/ideation.ipynb">[筆記本] 使用 Vertex AI 產生式模型發想點子</a>
│   │   ├── <a href="prompts/examples/question_answering.ipynb">[筆記本] 使用 Vertex AI 產生式模型進行問答</a>
│   │   ├── <a href="prompts/examples/text_classification.ipynb">[筆記本] 使用 Vertex AI 產生式模型進行文字分類</a>
│   │   ├── <a href="prompts/examples/text_extraction.ipynb">[筆記本] 使用 Vertex AI 產生式模型進行文字萃取</a>
│   │   └── <a href="prompts/examples/text_summarization.ipynb">[筆記本] 使用 Vertex AI 產生式模型進行文字摘要</a>
│   └── <a href="prompts/intro_prompt_design.ipynb">[筆記本] 提示設計 - 最佳做法</a>
├── <a href="sample-apps">範例應用程式/</a>
│   └── <a href="sample-apps/chat-flask-cloudrun/">Cloud Run 上使用 Python Flask 的聊天應用程式</a>
│   └── <a href="sample-apps/chat-gradio/">Cloud Run 上使用 Gradio 的聊天應用程式</a>
│   └── <a href="sample-apps/chat-streamlit/">Cloud Run 上使用 Streamlit 的聊天應用程式</a>
│   └── <a href="sample-apps/code-predict-cloudfunction/">包覆 Vertex AI PaLM 程式碼模型的 Cloud 函式</a>
│   └── <a href="sample-apps/summarization-gcs-cloudfunction/">使用 Vertex AI PaLM 文字模型進行摘要的 Cloud 函式</a>
│   └── <a href="sample-apps/text-predict-cloudfunction/">包覆 Vertex AI PaLM 文字模型的 Cloud 函式</a>
├── <a href="translation">translation/</a>
│   └── <a href="intro_translation.ipynb">[筆記本] 翻譯簡介</a>
├── <a href="tuning">tuning/</a>
│   └── <a href="tuning_text_bison.ipynb">[筆記本] 調整和部署基礎模型</a>
└── <a href="use-cases">使用案例/</a>
    ├── <a href="use-cases/chatbots">聊天機器人/</a>
    │   └── <a href="use-cases/chatbots/grocerybot_assistant.ipynb">[筆記本] GroceryBot，範例雜貨和食譜助理 - RAG + ReAct</a>
    ├── <a href="use-cases/sql-code-generation">SQL 程式碼產生/</a>
    │   ├── <a href="use-cases/sql-code-generation/sql_code_generation.ipynb">[筆記本] Vertex AI 上的 SQL 程式碼產生</a>
    │   └── <a href="use-cases/sql-code-generation/sql_code_generation_langchain.ipynb">[筆記本] 使用 LangChain 🦜🔗 Vertex AI 上的 SQL 程式碼產生</a>
    ├── <a href="use-cases/description-generation">描述產生/</a>
    │   ├── <a href="use-cases/description-generation/product_description_generator_attributes_to_text.ipynb">[筆記本] DescriptionGen：使用 LangChain 🦜🔗 為零售業產生 SEO 優化的產品描述</a>
    │   └── <a href="use-cases/description-generation/product_description_generator_image.ipynb">[筆記本] 根據圖片產生產品描述</a>
    ├── <a href="use-cases/document-qa">文件問答/</a>
    │   ├── <a href="use-cases/document-qa/question_answering_documentai_matching_engine_palm.ipynb">[筆記本] 使用 Document AI、比對引擎和 PaLM 提出文件相關問題</a>
    │   ├── <a href="use-cases/document-qa/question_answering_documents_langchain_matching_engine.ipynb">[筆記本] 使用 LangChain 🦜️🔗 and Vertex AI 比對引擎提出文件相關問題</a>
    │   ├── <a href="use-cases/document-qa/question_answering_documents.ipynb">[筆記本] 提出大型文件相關問題</a>
    │   └── <a href="use-cases/document-qa/question_answering_documents_langchain.ipynb">[筆記本] 使用 LangChain 🦜🔗 提出大型文件相關問題</a>
    └── <a href="use-cases/document-summarization">文件摘要/</a>
        ├── <a href="use-cases/document-summarization/summarization_with_documentai.ipynb">[筆記本] 使用 Document AI 摘要文件</a>
        ├── <a href="use-cases/document-summarization/summarization_large_documents.ipynb">[筆記本] 大型文件的文字摘要</a>
        └── <a href="use-cases/document-summarization/summarization_large_documents_langchain.ipynb">[筆記本] 使用 LangChain 🦜🔗 進行大型文件的文字摘要</a>
</pre>



