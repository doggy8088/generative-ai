# 自訂進度環境設定

1. 登入 [Google Cloud 主控台](http://console.cloud.google.com/)，建立新專案，或重複使用現有的專案。如果您尚未擁有 Gmail 或 Google Workspace 帳戶，您必須 [建立一個帳戶](https://accounts.google.com/SignUp)。

    ![選擇專案](assets/select_project.png "選擇專案")

    - **專案名稱** 是這個專案參與者的顯示名稱。這是一個字串，Google API 未使用。您隨時都可以更新它。

    - **專案 ID** 在所有 Google Cloud 專案間是唯一的，且不可變更 (一旦設定後便無法變更)。Cloud 主控台會自動產生一個獨一無二的字串；通常您並不在乎它是什麼。在大部分的 codelab，您需要參照您的 `專案 ID` (通常稱為 PROJECT_ID)。如果您不喜歡產生的 ID，可以產生另一個隨機 ID。或者，您可以嘗試輸入自己的，並看看是否有用。它在這個步驟後無法變更，且延續整個專案使用時間。

    - 供您參考，有一個第三個值，**專案號碼**，一些 API 會用到。在文件當中進一步了解這三個值的全部內容。

2. 接下來，您必須在 Cloud 主控台中 [啟用帳單服務](https://console.cloud.google.com/billing) 以使用 Cloud 資源/API。執行此 Codelab 花費的成本很低，甚至可能完全免費。如要關閉資源以避免產生超出本教學範圍的帳單費用，您可以刪除您建立的資源，或刪除專案。新的 Google Cloud 使用者符合資格享有 [$300 美金免費試用](http://cloud.google.com/freeselec) 計畫。

## 開始使用 Cloud Shell

雖然 Google Cloud 可以讓您使用筆記型電腦進行遠端操作，在此 Codelab 中，您將使用 [Google Cloud Shell](https://cloud.google.com/cloud-shell/)，一個執行在 Cloud 中的命令列環境。

從 [Google Cloud 主控台](https://console.cloud.google.com/)，按一下右上角工具列中的 Cloud Shell 圖示：

![Cloud Shell 圖示](assets/cloud_shell_icon.png "Cloud Shell 圖示")

僅需要花費數分鐘的時間，即可建置並連線至環境。完成後，您應該會看到類似這樣的畫面：

![Cloud Shell Terminal](assets/cloud_shell_terminal.png "Cloud Shell Terminal")

這個虛擬機器已載入您需要的所有開發工具。它提供一個持續性的 5GB 主目錄，並執行在 Google Cloud 上，大幅提升網路效能和驗證。您可以在瀏覽器中完成本 Codelab 的所有工作。您不需要安裝任何東西。

連線到 Cloud Shell 後，您應該會看到您已經過驗證，且專案已設定為您的專案 ID。

在 Cloud Shell 中執行以下指令，確認您已完成驗證：

連線到 Cloud Shell 後，您應該會看到您已完成驗證，且專案已設定為 `PROJECT_ID`。

```bash
gcloud auth list
```

指令輸出

```bash
已驗證的帳戶：
 - <myaccount>@<mydomain>.com (active)
```

```bash
gcloud config list project
```

指令輸出

```bash
[core]
project = <PROJECT_ID>
```

如果由於某種原因專案尚未設定，請直接下達以下指令：

```bash
gcloud config set project <PROJECT_ID>
```

Cloud Shell 在預設情況下也會設定一些環境變數，當您執行後續指令時可能會用到。

```bash
echo $GOOGLE_CLOUD_PROJECT
```

指令輸出

```bash
<PROJECT_ID>
```



## 啟用 Google Cloud API

為了使用本專案中所需的各項服務，我們將啟用一些 API。我們會在 Cloud Shell 中執行下列指令來這麼做：

```bash
gcloud services enable cloudbuild.googleapis.com cloudfunctions.googleapis.com run.googleapis.com logging.googleapis.com storage-component.googleapis.com aiplatform.googleapis.com
```

過一段時間後，你應該會看到作業已成功完成：

```bash
作業「operations/acf.5c5ef4f6-f734-455d-b2f0-ee70b5a17322」已成功完成。
```

## 克隆儲存庫

我們已將本專案所需的所有範例放入 `sample_apps` 資料夾的 Git 儲存庫中。使用下列指令在 Cloud Shell 中克隆儲存庫：

```bash
git clone https://github.com/GoogleCloudPlatform/generative-ai.git
```



