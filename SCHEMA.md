# 量化交易回測 Wiki 架構與維護規範 (SCHEMA)

本文件定義量化交易回測知識庫（LLM Wiki）之資料夾結構、命名慣例、內容格式以及 Ingest 流程規範。

---

## 1. 資料夾結構

```text
llm-wiki-hw10/
├── SCHEMA.md                 # 知識庫結構與流程規範說明文件
├── raw/                      # 原始技術筆記資料夾（不可修改的資料來源）
│   ├── 01_look_ahead_bias.md
│   ├── 02_survivorship_bias.md
│   ├── 03_overfitting_and_oos.md
│   ├── 04_slippage_and_fees.md
│   └── 05_mdd_and_sharpe.md
└── wiki/                     # LLM Wiki 結構化知識庫
    ├── index.md              # 知識庫分類總索引
    ├── log.md                # 異動與 Ingest 歷史日誌
    ├── look_ahead_bias.md    # 概念條目：前視偏誤
    ├── survivorship_bias.md  # 概念條目：倖存者偏誤
    ├── overfitting_and_oos.md# 概念條目：過擬合與樣本外測試
    ├── slippage_and_fees.md  # 概念條目：手續費與滑價耗損模型
    └── mdd_and_sharpe.md     # 概念條目：最大回撤與夏普比率
```

---

## 2. 概念條目結構規範

每個位於 `wiki/*.md` 的概念頁面，皆必須嚴格遵守以下段落結構：

1. **標題**：`# 概念名稱（英文名稱）`
2. **【一句話白話定義】**：簡明扼要、不含高深術語的核心定義。
3. **【生活化比喻】**：利用日常情境（如學生考試、減肥、買菜、歷史回顧等）說明該概念機制。
4. **【深入技術解析】**：深入說明其成因、在回測程式碼中可能出現的情境與影響。
5. **【錯誤 vs. 正確對照】**：使用表格或對照區塊列出「常見錯誤實作／錯誤認知」與「標準修正做法」。
6. **【防範實務檢核點】**：工程師或研究員在回測流程中必須執行的檢查步驟。
7. **【關聯條目連結】**：指向其他相關 `wiki/*.md` 條目的雙向連結（Bidirectional Links）。
8. **【資料來源】**：必須明確指向 `raw/` 下對應的原始筆記，格式為 `資料來源：[raw/檔名.md](file:///c:/Users/User/Desktop/llm-wiki-hw10/raw/檔名.md)`。

---

## 3. 逐篇 Ingest 流程與檢查機制

知識庫更新必須遵循「單篇循序處理迴圈」（One-at-a-time Ingest Pipeline）：

```
[讀取 raw/ 檔案]
       ↓
[查詢並更新 wiki/index.md] (納入分類索引與狀態)
       ↓
[生成 / 增修 wiki/概念.md] (依循條目結構規範)
       ↓
[執行品質檢查點 (Checkpoints)]
   ├── 檢查 1：是否標註資料來源 (raw/檔案)？
   ├── 檢查 2：是否包含生活化比喻？
   └── 檢查 3：是否與現有其他 Wiki 條目建立雙向連結？
       ↓
   (未通過) ──> [退回補充修改，並於 log.md 記錄退回原因]
       ↓ (通過)
[寫入 wiki/log.md] (記錄處理時間、檢查結果與異動摘要)
```
