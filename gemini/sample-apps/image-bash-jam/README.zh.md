# 從 Bash 測試 Gemini

| |
|-|-|
|作者 | [Riccardo Carlesso](https://github.com/palladius)

注意：我在 Medium 上寫了一篇與此 README 非常相似的文章 😊

連結：<https://medium.com/@palladiusbonton/hey-gemini-explain-me-these-pictures-in-bash-06c03d0d0512>

注意：此程式碼已經在本地端和 Cloud Shell 上進行測試。若要獲得更輕鬆的驗證體驗，請考慮在 [Cloud Shell](https://cloud.google.com/shell/docs/using-cloud-shell) 上執行此程式碼。

## 設定

1. 首先讓我們下載 repo 並把自己放在正確的資料夾中：

```bash
cd
git clone  https://github.com/GoogleCloudPlatform/generative-ai
cd generative-ai/gemini/sample-apps/image-bash-jam/

# [選用] 如果您喜歡有顏色的 shell，請這麼做。如果沒有，指令碼會偵測其不存在，並只會以 shell 的預設顏色顯示 (請參閱 `_common.sh` 中的 `_lolcat`)。
gem install lolcat
```

1. 首先檢查驗證。請務必使用 gcloud (或您希望使用的任何登入方式) 登入並正確設定 project_id。

```bash
# 如果您在 Cloud Shell 上，您可以略過這個步驟。您只需要按一下即可進行驗證。
gcloud auth login
```

如果您登入時遇到問題，可以使用以下指令設定 project_id (它也支援本機金鑰，請查看檔案頂端的說明文件)：

```bash
cp .envrc.dist .envrc
vim .envrc # 變更 PROJECT_ID 和 ACCOUNT 為您的專案和電子郵件。
./01-setup.sh # 設定驗證，並包含 `make images` 以在本地端下載資源。
```

## 簡單測試

1. 執行最簡單的指令碼作為測試：

`./gemini-why-is-the-sky-blue.sh`

回應：



```JSON
{
  "candidates": [
    {
      "content": {
        "role": "model",
        "parts": [
          {
            "text": "天空呈藍色的原因是一種稱為瑞利散射的現象。以下是科學解釋：\n\n1. 陽光成分：陽光是一種由太陽發出的電磁輻射，由不同波長和顏色的光波光譜組成。這些顏色包括紅色、橙色、黃色、綠色、藍色、靛藍色和紫色，這些顏色共同組成了彩虹光譜。\n\n2. 光的散射：當陽光進入地球大氣層時，它會與空氣中的分子和粒子發生相互作用，包括氮氣 (N2) 和氧氣 (O2) 分子，以及氣溶膠、灰塵和其他顆粒。這些粒子將入射陽光向所有方向散射。\n\n3. 瑞利散射：散射的量取決於光的波長和粒子的尺寸。較短波長的光 (例如藍色和紫羅蘭色) 比較長波長的光 (如紅色和橙色) 散射得更有效。這種現象稱為瑞利散射，以在 19 世紀後期研究和解釋這種現象的瑞利勳爵命名。\n\n4. 散射強度：散射強度與光的波長的四次方成反比。這意味著波長較短的藍光比波長較長的紅光散射約 16 倍。\n\n5. 藍天外觀：由於瑞利散射，波長較短的藍色和紫羅蘭色由大氣中的分子和粒子散射得更強。當我們仰望天空時，我們主要看到的是這些粒子向所有方向散射的藍光，這使得天空在白天呈現藍色。\n\n6. 顏色的變化：散射強度會根據一天中的時間、大氣條件以及空氣中汙染物或顆粒的含量而異。在日出和日落時，陽光必須穿過更多的大氣層，更多的短波長光被散射掉，留下紅色和橙色等較長波長的顏色，從而產生我們在那些時刻看到的彩色天空。\n\n7. 藍色主色：儘管紫羅蘭光的波長比藍光稍短，但它被地球大氣層和臭氧層吸收得更多，臭氧層保護地球免受有害紫外線 (UV) 輻射的侵害。因此，我們主要感知散射的藍光，這使得天空在我們眼中呈現藍色。"
          }
        ]
      }
    }
  ],
  "usageMetadata": {
    "promptTokenCount": 6,
    "candidatesTokenCount": 485,
    "totalTokenCount": 491
  }
}
```

賓果！它告訴你關於瑞利散射的資訊，以及你花了多少錢 (491 個代幣，應該低於 1 美分)。

如果這有效，太棒了，我們可以轉到更有趣的事情！

## 嘿 Gemini，描述你看到什麼

讓我們開始向 Gemini 詢問圖像！

讓我們從我最喜歡的所有專輯之一開始：**Selling England by the pound**。

![其他文字](https://storage.googleapis.com/github-repo/use-cases/image-bash-jam/img/genesis-selling-england.jpg "Genesis - Selling England by the pound (有史以來最好的專輯之一！)")



```bash
./gemini-generic.sh images/genesis-selling-england.jpg 賣英格蘭什麼由來
# 🤌  問題：賣英格蘭什麼由來
# 🌡️ 溫度：0.2
# 👀 檢查圖片 images/genesis-selling-england.jpg：JPEG 圖像資料，JFIF 標準 1.01，解析度 (DPI)，密度 96x96，區段長度 16，基本，精度 8，536x528，元件 3。
# ♊ Gemini no Saga 回答您：
英國藝術家 Paul Whitehead 的畫作描繪了 Genesis 樂團的《Selling England by the Pound》專輯封面。這幅畫描繪了一群人在一座公園中，一名男子在前方的長椅上睡著。這些人穿著 20 或 30 年代的服裝，畫作散發出懷舊，幾乎超現實的感覺。色彩柔和，人物有些模糊，賦予這幅畫夢幻的品質。這幅畫也充滿了象徵意義，睡著的男人代表英格蘭，他周圍的人代表英國社會的不同面向。這幅畫被用許多不同的方式詮釋，但通常被視為對 70 年代英國狀態的評論。
```

快速搜尋後可以證實 <https://en.wikipedia.org/wiki/Paul_Whitehead> 確實為我歷來最喜愛的專輯繪製封面。如果您也喜愛 Genesis 並希望看到我彈奏 Firth of Fifth，歡迎到 <https://www.youtube.com/watch?v=4VBxd9n1dSU> 觀看。

**備註**：如果指令碼失敗，請確認 `images/genesis-selling-england.jpg` 存在 (或重新執行 `make images`)，且驗證透過 (查看 `.tmp*` 檔案可取得更多詳細輸出)。

## 現在來比較兩張圖片

由於我們正在慶祝 Gemini 發表，而我又是漫畫/動畫《聖鬥士星矢》的超級粉絲，所以我請 Gemini 比較他身邊的兩件事：

<table align=center >
  <tr  valign=top >
    <td valign=top >
        雙子座星座
    </td>
    <td  valign=top>
        《聖鬥士星矢》中的雙子座聖鬥士 (撒卡) 
    </td>
  </tr>
  <tr  valign=top >
    <td valign=top >
        <img src="https://storage.googleapis.com/github-repo/use-cases/image-bash-jam/img/gemini-constellation.png"  alt="雙子座星座" width=360px >
    </td>
    <td  valign=top>
        <img src="https://storage.googleapis.com/github-repo/use-cases/image-bash-jam/img/saga-blue-hair.jpg" alt="藍色頭髮的雙子座 no-saga" width=360px >
    </td>
  </tr>
</table>

```bash
$ make compare-two-geminis
$ ./gemini-generic-two-pics.sh  images/gemini-constellation.png   images/saga-blue-hair.jpg
♊️ 問題：您能否強調兩者之間的相似處和不同處？此外，您是否認出兩者中的人物相同？
 👀 檢查 image1 images/gemini-constellation.png：images/gemini-constellation.png：PNG 圖像資料，1675 x 1302，8 位元/色彩 RGBA，非交錯。
 👀 檢查 image2 images/saga-blue-hair.jpg：images/saga-blue-hair.jpg：JPEG 圖像資料，JFIF 標準 1.01，長寬比，密度 1x1，區段長度 16，基本，精度 8，193x261，元件 3。
♊️ 描述附檔圖片：
這兩張圖片分別是雙子座星座和動畫角色雙子座撒卡。據說這個星座代表雙胞胎卡斯托耳和波魯克斯，而動畫《聖鬥士星矢》中的角色則是雙子座聖鬥士。兩張圖片都描繪了兩個相互連結的人。星座由星星組成，而角色則是人類。
```

幹得好，Gemini！就像蘇格拉底會說的：「認識你自己」。
請注意，這些圖片是 PNG 和 JPG，但是這無法阻止 Gemini 進行比較！

## 介紹聲音

何不加一點聲音讓事情變得更有趣？

我的 `./tts.sh` 能夠將 ARGV 中的英文 (或義大利文！) 文字製成 MP3。夠方便吧？



```bash
$ make 年齡測試
# 相當於：
$ GENERATE_MP3=true ./gemini-generic.sh 圖片/ricc-family-with-santa.jpg 告訴我你看到的這些人的年齡，由左到右。
# 🤌 問題：告訴我你看到的這些人的年齡，由左到右。
# 🌡️ 溫度：0.2
# 👀 檢查圖片 images/ricc-family-with-santa.jpg：JPEG 影像資料、JFIF 標準 1.01、長寬比、密度 1x1、片段長度 16、Exif 標準：[TIFF 影像資料、小端序、direntries=3、軟體=Google]、基線、精準度 8、1164x826、元件 3。
# ♊ Gemini 沒有沙加的答案提供給你：
1. 30-35 歲
2. 2-3 歲
3. 40-45 歲
4. 2-3 歲
5. 60-65 歲
[..]
一切都很好。已建立 MP3 [..]
```

現在，有趣的是，它也建立了答案的 MP3。雖然這些數字聽起來不太有趣，但對於較長的詳細答案來說可能會是很棒的功能。你可以開啟 `output/` 資料夾中的檔案來聆聽它。(<a href="https://storage.googleapis.com/github-repo/use-cases/image-bash-jam/mp3/ricc-family-with-santa.jpg.mp3" >images/mp3/ricc-family-with-santa.jpg.mp3</a>)。

### 疑難排解

有時你可能會遇到驗證警告 (特別是在使用文字轉語音 API 時)。
你可以透過 ADC 重新驗證身分來修復問題：

```bash
gcloud auth application-default login
gcloud auth application-default set-quota-project "$PROJECT_ID"
```

另一種方式是下載金鑰，並將其放置在 `private/YOUR_PROJECT_ID.json` 下。

腳本 `01-setup.sh` 內建了一些神奇的功能，會自動找出金鑰並透過它登入 :)

更多資訊請見：<https://cloud.google.com/docs/authentication/troubleshoot-adc#user-creds-client-based>

## 用義大利文說明的一張義大利圖片

為什麼不試試相同的步驟，但搭配義大利文字和音效來增加趣味性？

![替代文字](https://storage.googleapis.com/github-repo/use-cases/image-bash-jam/img/italian-town.jpg "Trento 市照片")

```bash
./gemini-explain-image.sh 圖片/italian-town.jpg
# 🤌 問題：說明你所看到的內容
# 🌡️ 溫度：0.2
# 👀 檢查圖片：JPEG 影像資料、JFIF 標準 1.01、長寬比、密度 1x1、片段長度 16、Exif 標準：[TIFF 影像資料、小端序、direntries=1、軟體=Google]、基線、精準度 8、926x1230、元件 3。
# ♊ Gemini 沒有沙加的答案提供給你：
這是從 Buonconsiglio 城堡拍攝的義大利 Trento 市景觀。
```

這樣很不錯！我不知道攝影師是從 Buonconsiglio 城堡拍攝的。太棒了。不過它是英文的。

```bash
$ GENERATE_MP3=true ./gemini-explain-image-italian.sh 圖片/italian-town.jpg
# 🤌 問題：Descrivimi cosa vedi in questa immagine
# 🌡️ 溫度：0.2
# 👀 檢查圖片 images/italian-town.jpg：JPEG 影像資料、JFIF 標準 1.01、長寬比、密度 1x1、片段長度 16、Exif 標準：[TIFF 影像資料、小端序、direntries=1、軟體=Google]、基線、精準度 8、926x1230、元件 3。
# ♊ Gemini 沒有沙加的答案提供給你：
La foto mostra una loggia con delle colonne in pietra che incorniciano la vista di una città.
La città è circondata da montagne e si possono vedere i tetti delle case e le torri delle chiese.
Il cielo è azzurro e ci sono delle nuvole bianche.
# TTS_LANG: it-IT
已寫入 .tmp.tts-output.json。curl_ret=0
t.audio.encoded：ASCII 文字，有非常長的列 (65536)、沒有行結尾符
t.mp3：           MPEG ADTS、第 III 層、v2、32 kbps、24 kHz、單聲道
t.mp3：           MPEG ADTS、第 III 層、v2、32 kbps、24 kHz、單聲道
一切都很好。已建立 MP3：'t.La foto mostra una loggia con delle colonne in pie.mp3'
```



如你所見，義大利語較為冗長，且對特倫托較為了解，但它卻不知道「*Buonconsiglio 宮殿*」。
有趣！我猜測義大利模型比英語還少訓練資料。這蠻有道理的。

順帶一提，我強力推薦特倫托，我曾騎自行車在那附近遊覽：風景壯麗、美酒醇香！

現在，為了建立義大利語 MP3，我必須在 `TTS_LANG: it-IT` 將我想要的聲音類型硬編碼進去。
這是在 `./gemini-explain-image-italian.sh` 中新增的唯一值，因此你應該能夠無縫轉換成你最喜歡的語言。TextToSpeech API 支援將近 200 種語言！

MP3 檔案方便地複製到 [🇮🇹 images/mp3/italian-town.jpg.mp3](https://storage.googleapis.com/github-repo/use-cases/image-bash-jam/mp3/italian-town.jpg.mp3)。

## 現在開始講一些實用的東西：了解流程圖

我在工作場合有一副很讚的耳機，但我永遠記不住如何開關機；如果我充電後取下，它會自動為我開機，但如果我昨天晚上忘記充電怎麼辦？這正是今早發生在我身上的事。

Gemini 救星來了！

1. Google 搜尋「Accrux 耳機使用者手冊並取得 PDF」。 => `images/instruction-manuals/Acrux-User-Manual-4700503.pdf`
2. 由於 Gemini 尚未 (從 UI) 讀取 PDF，因此以下提供 PNG 檔案：<a href="https://storage.googleapis.com/github-repo/use-cases/image-bash-jam/instruction-manuals/Acrux-User-Manual-4700503.png" >images/instruction-manuals/Acrux-User-Manual-4700503.png</a>。
3. 這個步驟最困難。我們現在來發問。我使用 UI 問了三個問題：

![圖片說明](cloudconsole-screenshot.png?raw=true "Riccardo 使用 DevConsole 一鍵發問 Gemini")

1. 我們從 CLI 來做同樣的事：

```bash
$ make read-instruction-manual-for-me
[..]
./gemini-generic.sh images/instruction-manuals/Acrux-User-Manual-4700503.png '1. 如何開啟？2. 電源按鈕位於何處？3. 這是所謂的 ANC 嗎？'
# 🤌 問題：1. 如何開啟？2. 電源按鈕位於何處？3. 這是所謂的 ANC 嗎？
# 🌡️ 溫度：0.2
# 👀 檢視影像 images/instruction-manuals/Acrux-User-Manual-4700503.png：PNG 影像資料，1664 x 929，8 位元/色彩 RGBA，非交錯式。
# ♊ Gemini no Saga 的答案：
1. 長按電源按鈕 2 秒鐘。
2. 電源按鈕位於右耳罩。
3. 是的，這是所謂的 ANC。
# 注意事項：未產生 mp3 檔案 (使用 GENERATE_MP3=true 來產生 mp3 檔案) 
```

好的，按鈕就是 ANC 按鈕，我猜對了！謝謝 Gemini！

## 一個意想不到的《冰與火之歌》劇情反轉

這是我在 Google 使用的頭像。我隨意問了這個問題：

![圖片說明](https://storage.googleapis.com/github-repo/use-cases/image-bash-jam/img/ricc-logo.png "Riccardo GCP 商標 - 取自阿姆斯特丹辦公室")

```bash
$ ./gemini-explain-image.sh images/ricc-logo.png
[..]
這是站在 Google Cloud Platform 標誌後方的男人照片。
這個男人笑容滿面，穿著一件寫著「這是我在做的事，
我喝酒且我知道一些事」的襯衫。背景是一面磚牆，帶有藍色
和白色色調。
```

我想！當然，這是《冰與火之歌》中最棒的 T 恤。

讓我們問 Gemini：

```bash
$ GENERATE_MP3=true ./gemini-generic.sh images/ricc-logo.png 辨識圖片中這件 T 恤的台詞
[..]
「這是我在做的事，我喝酒且我知道一些事」，這句話出自電視影集《冰與火之歌》，
是由提利昂·蘭尼斯特飾演的角色所說。
```



* MP3： <a href='https://storage.googleapis.com/github-repo/use-cases/image-bash-jam/mp3/ricc-logo.png.mp3' >images/mp3/ricc-logo.png.mp3</a> (我不確定 GitHub 是否支援播放此聲音，但你可以下載並聆聽)。

* <audio controls="controls">
  <source type="audio/mp3" src="https://storage.googleapis.com/github-repo/use-cases/image-bash-jam/mp3/ricc-logo.png.mp3"></source>
  <p>🔇 喔不，您的瀏覽器或 GitHub markdown 不支援聲音元素。</p>
  </audio>

* 回應：「「這就是我做的事情，我喝酒且我知道很多事情」是電視節目冰與火之歌中，由角色提利昂·蘭尼斯特所說的話。」

哇喔：*小醜*, Gemini！



