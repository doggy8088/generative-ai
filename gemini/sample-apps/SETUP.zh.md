# 自主步調環境設定

1. 登入至[Google Cloud Console](http://console.cloud.google.com/)並建立新的專案或重複使用現有的專案。如果您還沒有 Gmail 或 Google Workspace 帳戶，您必須[建立一個](https://accounts.google.com/SignUp)。

    ![選擇專案](assets/select_project.png "選擇專案")

    - **專案名稱**是此專案參與者的顯示名稱，是用於 Google API 的字元字串，您可以隨時更新。

    - **專案 ID**在所有 Google Cloud 專案中都是唯一的，而且不可變更 (設定後無法變更)。Cloud Console 會自動產生唯一的字串；通常您不需在意內容為何。在大部分 Codelab 中，您需要參照您的`專案 ID` (通常識別為 PROJECT_ID)。如果您不喜歡產生的 ID，您可以產生另一個隨機 ID。或者，您可以嘗試自行輸入，看看是否可使用。完成此步驟後無法變更，專案期限內維持不變。

    - 您的資訊，有一個第三個值，**專案編號**，其中一些 API 會使用。在文件中深入了解這三個值。

2. 接下來，您需要在 Cloud Console 中[啟用帳單](https://console.cloud.google.com/billing)才能使用 Cloud 資源/API。執行此 Codelab 的成本很低，甚至沒有任何成本。若要關閉資源以避免產生此教學課程以外的帳單，您可以刪除您建立的資源或刪除專案。Google Cloud 新使用者有資格參加[$300 美元免費試用](http://cloud.google.com/freeselec) 計畫。

## 啟動 Cloud Shell

雖然 Google Cloud 可以從您的筆電遠端操作，但在此 Codelab 中您將使用[Google Cloud Shell](https://cloud.google.com/cloud-shell/)，一個在 Cloud 中執行的命令列環境。

從[Google Cloud Console](https://console.cloud.google.com/)，按一下右上方工具列上的 Cloud Shell 圖示：

![Cloud Shell 圖示](assets/cloud_shell_icon.png "Cloud Shell 圖示")

供應並連線到環境僅需花費幾分鐘。完成後，您應該會看到類似這樣的畫面：

![Cloud Shell 端末機](assets/cloud_shell_terminal.png "Cloud Shell 端末機")

這個虛擬機器載入了您需要的全部開發工具。它提供了永久性的 5 GB 個人主目錄，而且在 Google Cloud 上執行，大幅提升網路效能和驗證。您可以在瀏覽器中完成在此 Codelab 中的全部工作。您不需要安裝任何東西。

連線到 Cloud Shell 後，您應該看到您已經完成驗證，而且專案已經設定到您的專案 ID。

在 Cloud Shell 中執行以下指令確認您已經驗證：

連線到 Cloud Shell 後，您應該看到您已經完成驗證，而且專案已經設定到您的`專案 ID``。

```bash
gcloud auth list
```

指令輸出：

```bash
已憑證驗證的帳戶：
 - <myaccount>@<mydomain>.com (active)
```

```bash
gcloud config list project
```

指令輸出：

```bash
[core]
project = <PROJECT_ID>
```

如果出於某種原因專案尚未設定，請直接下達下列指令：

```bash
gcloud config set project <PROJECT_ID>
```

Cloud Shell 預設也設定了一些環境變數，您執行後續指令時可能會使用它們。

```bash
echo $GOOGLE_CLOUD_PROJECT
```

指令輸出：

```bash
<PROJECT_ID>
```



## 啟用語 Google Cloud API

為了使用本專案各處需要的各項服務，我們會啟用語一些 API。執行 Cloud Shell 中的下列指令來這麼做：

```bash
gcloud services enable cloudbuild.googleapis.com cloudfunctions.googleapis.com run.googleapis.com logging.googleapis.com storage-component.googleapis.com aiplatform.googleapis.com
```

一段時間後，您應該會看到操作已成功完成：

```bash
操作「operations/acf.5c5ef4f6-f734-455d-b2f0-ee70b5a17322」已成功完成。
```

## 克隆儲存庫

我們已將本專案所需的所有範例放進 `sample-apps` 資料夾的 Git 儲存庫中。使用以下指令在 Cloud Shell 中複製儲存庫：

```bash
git clone https://github.com/GoogleCloudPlatform/generative-ai.git
```



