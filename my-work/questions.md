# 課前問題紀錄（30 分鐘停損規則用）

> 規則：任何安裝、API 呼叫或工具設定卡住超過 20–30 分鐘，立刻停手，
> 把**確切的步驟**與**完整錯誤訊息**貼到這裡，帶到課堂討論。

---

## Q1 — 本機沒有 Git，無法確認 fork 的 remote ✅ 已解決 (2026-11-02)

- **做了什麼**：
  1. `git --version` → 指令不存在
  2. `Get-Command git` → 無結果
  3. 檢查 `C:\Program Files\Git\cmd\git.exe` 等常見安裝路徑 → 皆無檔案
  4. 以 registry 重建 PATH 後重測 → 仍無（確認是真的沒裝，不是 PATH 問題）
- **當時的錯誤訊息**：
  ```
  git : The term 'git' is not recognized as the name of a cmdlet, function,
  script file, or operable program.
  CategoryInfo          : ObjectNotFound: (git:String) [], CommandNotFoundException
  FullyQualifiedErrorId : CommandNotFoundException
  ```
- **解法**（經使用者同意後執行）：
  ```powershell
  winget install --id Git.Git -e --accept-package-agreements --accept-source-agreements
  ```
- **結果**：`git version 2.56.0.windows.4`，clone 與 remote 設定均正常。

---

## Q2 — `my-work/` 該放在哪一層 ✅ 已解決 (2026-11-02)

- **原本的疑慮**：clone 之前，暫建的 `my-work/` 落在非倉庫目錄，
  不確定應放倉庫根目錄或 `students/<名字>/`。
- **答案**：放在**倉庫根目錄**的 `my-work/`。
  證據：upstream repo 的 tree 本身即含 `my-work/sources/raw/`、
  `sources/processed/`、`research/`、`artifacts/`（各附 README.md），
  且根目錄 `.gitignore` 已寫入 `my-work/artifacts/*` 規則。
- **處理**：已將暫建檔案移入 `C:\Users\Rachel\Documents\art-ai-workshop-2026\my-work\`，
  未覆寫任何課堂附帶的 README。

---

## Q3 — clone 時 PowerShell 回報 NativeCommandError ⚠️ 誤判，非問題

- **現象**：`git clone` 後 PowerShell 顯示紅字 `NativeCommandError`、`Exited with code 1`。
- **原因**：git 把進度訊息寫到 stderr，PowerShell 會把 stderr 視為錯誤。
  實際 clone 成功（`.git` 存在、`origin` 正確、`git log` 正常）。
- **對策**：不必處理。日後可用 `git ... 2>&1 | Out-String` 或忽略此類紅字。

---

## 尚未解決 / 待課堂確認

- [ ] 是否需要建立 `my-work/self-introduction.md`（challenge 2；repo 內只有 `self-introduction.example.md` 範本）
- [ ] 本機 commit 後推上 fork 的驗證方式（第一次 `git push` 可能需要 GitHub 認證）
- [ ] 材料尚未放入 `sources/raw/`：目前僅有測試示例，正式研究需替換為自己的 10–20 張圖或 1–2 份 PDF
