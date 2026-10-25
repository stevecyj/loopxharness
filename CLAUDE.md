# CLAUDE.md

這個 repo 用提示詞把課程材料轉成學習成果。

- `prompts/`：提示詞，換課程時不修改
- `standard-cards/`：驗收標準，跟提示詞同名，按 Must Have／Must Preserve／Must Fit／Must Not 分類
- `workflow/`：固定執行規則與「材料 ↔ 輸出」產出對應表；新增材料時直接放入 `課程材料/`，由 Agent 自動掃描、確認是否重跑並維護對應表
- `課程材料/`：逐字稿等輸入（每個檔案代表一份獨立材料）
- `output/`：產出結果

`prompts/`、`standard-cards/`、`workflow/`、`output/` 統一依用途分成 `預期學習成果/`、`blog/` 子目錄。文件中的路徑以 repo 根目錄為基準。

執行 workflow 時：
- 「跑 workflow」或同時指定兩份 workflow：依序執行 `workflow/預期學習成果/workflow-重建學習成果.md` 與 `workflow/blog/workflow-轉成blog.md`。
- 「用 `課程材料/xxx.md` 跑 workflow」：只針對該份材料執行流程。
- 「跑學習成果 workflow」或「跑 blog workflow」：只執行指定階段。
- 動工前先讀取 `workflow/` 的「產出對應表」並只列出 `課程材料/` 與 `output/` 的檔名（確認前不讀取材料內文，以免篇幅長或檔案多時卡在讀取），向使用者回報現況、確認要處理哪些材料、既有輸出是否覆蓋，以及有無額外課程筆記或個人實作經驗／想法（預設為無）後，才讀取規則與目標材料內文執行；完成後自動更新對應表。

修改 `CLAUDE.md`、`AGENTS.md`、`docs/`、`prompts/`、`standard-cards/`、`workflow/` 的規則前，先讀取並遵守 `docs/project-constitution.md`（含第 08 節規則修改連動檢查），並保持 `CLAUDE.md` 與 `AGENTS.md` 一致。

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
