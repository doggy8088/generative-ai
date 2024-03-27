# 如何貢獻

我們很樂意接受您改善此專案的程式碼修補程式與貢獻。您只需要遵循幾個小指南即可。

## 貢獻者授權協議

貢獻本專案必須附上貢獻者授權協議。閣下 (或您的雇主) 保留對您的貢獻之著作權；這僅表示我們可以將您的貢獻作為本專案的一部份來使用和重新發佈。請前往 <https://cla.developers.google.com/> 查看您目前已簽署的協議，或簽署新的協議。

您通常只需提交一次 CLA，因此如果您已提交過一次 (即使是針對其他專案)，可能就不需要再提交一次。

## 筆記本範本

如果您要建立 Jupyter 筆記本，請使用 `/gemini/getting-started/intro_gemini_python.ipynb` 作為範本。

## 程式碼品質檢查

本專案中的所有筆記本皆會進行格式化和樣式檢查，以確保一致的體驗。如要在提交拉取要求前測試筆記本，您可以執行下列步驟。

從命令行介面終端機 (例如 Vertex Workbench 或本機) 安裝程式碼分析工具：

```shell
pip3 install --user -U nbqa black flake8 isort pyupgrade git+https://github.com/tensorflow/docs
```

您可能需要將安裝這些工具的目錄新增到 PATH 中：

```shell
export PATH="$HOME/.local/bin:$PATH"
```

接下來，為您的筆記本 (或目錄) 設定環境變數：

```shell
export notebook="your-notebook.ipynb"
```

最後，執行此程式碼區塊來檢查是否有錯誤。每一步驟都會嘗試自動修復任何問題。如果修復無法自動執行，您需要在提交公關要求前親自處理。

注意：官方政策是每次公關要求僅提交一份筆記本。

```shell
docker run -v ${PWD}:/setup/app gcr.io/cloud-devrel-public-resources/notebook_linter:latest your_notebook
```

## 程式碼檢閱

所有提交，包括專案成員的提交，都需要審查。我們會使用 GitHub 拉取要求來執行這項工作。請參考 [GitHub 說明](https://help.github.com/articles/about-pull-requests/)，進一步瞭解如何使用拉取要求。

## 社群指南

本專案遵循 [Google 的開放原始碼社群指南](https://opensource.google/conduct/)。

## 貢獻者指南

如果您是開放原始碼的新手，可以在此貢獻者指南中找到一些有用的資訊。

您可以遵循下列步驟進行貢獻：

1. **複製官方版本庫。** 這樣會在您自己的帳戶中建立一個官方版本庫的副本。
2. **同步分支。** 這樣可以確保您版本庫的副本與官方版本庫中的最新變更同步。
3. **在您版本庫的分支 dev 中工作。**您可以在此變更程式碼。
4. **在您版本庫的 dev 分支中提交更新。**這樣可以將您對版本庫副本的變更儲存起來。
5. **針對官方版本庫的 main 分支提交拉取要求。**這樣可以要求將您的變更合併到官方版本庫中。
6. **解決任何程式碼審查問題。**這樣可以確保您的變更格式正確。

![image](https://storage.googleapis.com/github-repo/img/contributing/contributor-guide-diagram.jpg)

在此過程中，以下是需要注意的一些事項：



- **請閱讀 [Google 開源社群指南](https://opensource.google/conduct/)。**貢獻指南會提供更多有關專案和如何參與貢獻的資訊。
- **測試你的變更。**在提交拉取請求前，請確認你的變更發揮預期功能。
- **請耐心等待。**審查和合併拉取請求可能需要一些時間。



