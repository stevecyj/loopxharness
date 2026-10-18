# loopxharness

這個專案把課程材料依序整理成學習成果與 blog 草稿。每次換課程，在 `workflow/` 更新本次使用的材料與輸出路徑。

## 執行順序

1. 將逐字稿等輸入放入 `課程材料/`，設定並執行[重建學習成果 workflow](workflow/預期學習成果/workflow-重建學習成果.md)。
2. 確認學習成果的實際檔名，將其填入[轉成 blog workflow](workflow/blog/workflow-轉成blog.md) 的「Prompt 1：進階學習筆記」欄位，再執行該 workflow。

## 驗收方式

每份 workflow 指向對應提示詞；提示詞引用同名的 Standard Card，要求 Agent 寫入前逐條檢查、不符合就修改並重新檢查。Standard Card 保存固定標準與訂立原因，不記錄單次執行的 Pass／Fail。
