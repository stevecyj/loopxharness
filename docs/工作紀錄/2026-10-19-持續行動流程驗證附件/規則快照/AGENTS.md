# CLAUDE.md

這個 repo 用提示詞把課程材料轉成學習成果。

- `prompts/`：提示詞，換課程時不修改
- `standard-cards/`：驗收標準，跟提示詞同名，按 Must Have／Must Preserve／Must Fit／Must Not 分類
- `workflow/`：每次執行的設定（課程名稱、逐字稿路徑、輸出位置），換課程時只改這裡
- `課程材料/`：逐字稿等輸入
- `output/`：產出結果

`prompts/`、`standard-cards/`、`workflow/`、`output/` 統一依用途分成 `預期學習成果/`、`blog/` 子目錄。文件中的路徑以 repo 根目錄為基準。

修改 `prompts/`、`standard-cards/`、`workflow/` 前，先讀取並遵守 `docs/project-constitution.md` 的專案共用規則。

Git：直接在 `main` 上 commit，不開 feature branch。

## Herdr 協作

只在使用者明確要求用 Herdr 或呼叫其他 agent 時才使用。

1. 先確認 `HERDR_ENV=1`，不成立就告知使用者並停止。
2. 用 `herdr --skill` 查功能與操作規則；指令語法以已安裝 CLI 的 `herdr --help`、`herdr agent`、`herdr pane` 輸出為準。不要執行裸 `herdr` 探查，因為它會開啟 TUI。
3. 用 `herdr pane layout --current` 看目前 pane 形狀，寬的往 `right`、窄或高的往 `down`，在目前 cwd 建立 sibling pane：`herdr pane split --current --direction <right|down> --cwd "$PWD" --no-focus`。pane ID 從回傳 JSON 的 `.result.pane.pane_id` 取得，不要猜。
4. 使用者指定 yolo 時，用 `herdr pane run <pane-id> "yolo"` 啟動 Claude Code。`yolo` 是 `claude --dangerously-skip-permissions` 的本機 shell alias。
5. 用 `herdr agent prompt <pane-id> "<明確任務>" --wait --timeout <ms>` 提交任務，再用 `herdr agent wait <pane-id>`／`herdr agent read <pane-id> --source recent-unwrapped` 確認狀態和結果。timeout 不代表沒送出，先讀取狀態與輸出，確認後再決定是否重送。
6. 只操作本次任務建立的 pane，不關閉其他人的 pane。協作結果由主 agent 自己檢查檔案與 `git diff`，不要只採信對方回報。

撰寫或修改提示詞時，遵守下面這份提示詞最佳實踐：

@docs/claude-prompt-best-practices.md
