# CLAUDE.md

這個 repo 用提示詞把課程材料轉成學習成果。

- `prompts/`：提示詞，換課程時不修改
- `standard-cards/`：驗收標準，跟提示詞同名，按 Must Have／Must Preserve／Must Fit／Must Not 分類
- `workflow/`：每次執行的設定（課程名稱、逐字稿路徑、輸出位置），換課程時只改這裡
- `課程材料/`：逐字稿等輸入
- `output/`：產出結果

Git：直接在 `main` 上 commit，不開 feature branch。

撰寫或修改提示詞時，遵守下面這份提示詞最佳實踐：

@docs/claude-prompt-best-practices.md
