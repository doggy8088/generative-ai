# Generative AI - Gemini

歡迎使用 Google Cloud [Generative AI](https://cloud.google.com/ai/generative-ai/) - Gemini 資料夾。

## Gemini

<!-- markdownlint-disable MD033 -->

<img src="https://lh3.googleusercontent.com/eDr6pYKs1tT0iK0nt3pPhvVlP2Wn96fbGqbWgBAARRZ7isej037g_tWobjV8zQkxOsWzJuEH8p-fksczXUOeqxGZZIo_HUCdkn8q-a4fuwATD7Q9Xrs=w2456-l100-sg-rj-c0xffffff" style="width:35em" alt="歡迎進入 Gemini 時代">
<!-- markdownlint-enable MD033 -->

Gemini 是由 Google DeepMind 研發的一系列生成式 AI 模型，適用於多模態使用案例。您可以透過 Gemini API 存取 Gemini Pro Vision 和 Gemini Pro 模型。

### Vertex AI Gemini API

在 Google Cloud 上，Vertex AI Gemini API 提供一個統一介面與 Gemini 模型互動。目前在 Gemini API 中提供兩個模型：

- **Gemini Pro 模型** (`gemini-pro`)：設計用於處理自然語言任務、多輪文字和程式碼對話，以及程式碼產生。
- **Gemini Pro Vision 模型** (`gemini-pro-vision`)：支援多模態提示字元。您可以在提示字元要求中納入文字、圖片和影片，並取得文字或程式碼回應。

本資料夾中的筆記本和範例著重於使用 **Vertex AI SDK for Python** 來呼叫 Vertex AI Gemini API。

## 使用此存放庫

<!-- markdownlint-disable MD033 -->



<table>
  <tr>
    <th></th>
    <th style="text-align: center;">說明</th>
    <th style="text-align: center;">內容</th>
  </tr>
  <tr>
    <td>
      <img src="https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/flag/default/40px.svg" alt="flag">
      <br>
      <a href="getting-started/"><code>getting-started/</code></a>
    </td>
    <td>開始使用 Vertex AI Gemini API：
      <ul>
        <li><code>gemini-pro</code> 模組</li>
        <li><code>gemini-pro-vision</code> 模組</li>
      </ul>
    </td>
    <td><a href="getting-started/">入門筆記本</a></td>
  </tr>
  <tr>
    <td>
      <img src="https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/deployed_code/default/40px.svg" alt="deployed_code">
      <br>
      <a href="sample-apps/"><code>sample-apps/</code></a>
    </td>
    <td>探索由 Gemini 支援的範例應用程式</td>
    <td><a href="sample-apps/">範例應用程式</a></td>
  </tr>
  <tr>
    <td>
      <img src="https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/manufacturing/default/40px.svg" alt="manufacturing">
      <br>
      <a href="use-cases/"><code>use-cases/</code></a>
    </td>
    <td>
      探索 Gemini 支援的產業使用案例 (例如零售、教育)
    </td>
    <td><a href="use-cases/">範例使用案例</a></td>
  </tr>
  <tr>
    <td>
      <img src="https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/radar/default/40px.svg" alt="radar">
      <br>
      <a href="evaluation/"><code>evaluation/</code></a>
    </td>
    <td>深入了解如何使用 Vertex AI Model Evaluation for GenAI 評量 Gemini</td>
    <td><a href="evaluation/">範例筆記本</a></td>
  </tr>
  <tr>
    <td>
      <img src="https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/terminal/default/40px.svg" alt="terminal">
      <br>
      <a href="function-calling/"><code>function-calling/</code></a>
    </td>
    <td>
        深入了解如何使用 Gemini 的<a href="https://cloud.google.com/vertex-ai/docs/generative-ai/multimodal/function-calling">函式呼叫</a>功能
    </td>
    <td><a href="function-calling/">範例筆記本</a></td>
  </tr>
  <tr>
    <td>
      <img src="https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/grass/default/40px.svg" alt="grass">
      <br>
      <a href="grounding/"><code>grounding/</code></a>
    </td>
    <td>
        深入了解如何使用 Gemini 的<a href="https://cloud.google.com/vertex-ai/docs/generative-ai/grounding/ground-language-models">基礎</a>功能
    </td>
    <td><a href="grounding/">範例筆記本</a></td>
  </tr>
  <tr>
    <td>
      <img src="https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/health_and_safety/default/40px.svg" alt="health_and_safety">
      <br>
      <a href="responsible-ai/"><code>responsible-ai/</code></a>
    </td>
    <td>深入了解如何使用 Vertex AI Gemini API 的安全評分和臨界值。</td>
    <td><a href="responsible-ai/">範例筆記本</a></td>
  </tr>
  <tr>
    <td>
      <img src="https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/build/default/40px.svg" alt="build">
      <br>
      <a href="../setup-env/"><code>setup-env/</code></a>
    </td>
    <td>說明如何在 Google Colab 和 Vertex AI Workbench 上設定 Google Cloud、Vertex AI Python SDK 和筆記本環境。</td>
    <td><a href="../setup-env">設定說明</a></td>
  </tr>
  <tr>
    <td>
      <img src="https://fonts.gstatic.com/s/i/short-term/release/googlesymbols/media_link/default/40px.svg" alt="media_link">
      <br>
      <a href="../RESOURCES.md"><code>RESOURCES.md</code></a>
    </td>
    <td>Google Cloud 上的 Generative AI 學習資源 (例如：部落格、YouTube 播放清單)</td>
    <td><a href="../RESOURCES.md">資源 (例如：影片、部落格文章、學習路徑)</a></td>
  </tr>



</table>
<!-- markdownlint-enable MD033 --><保持這個符號>

