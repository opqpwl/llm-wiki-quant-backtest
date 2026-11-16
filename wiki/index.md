# 量化交易回測知識庫索引（Wiki Index）

歡迎查閱「量化交易回測的常見陷阱與過擬合防範」Wiki 知識庫。本索引即時記錄知識庫各模組之分類與條目狀態。

---

## 條目分類目錄

### 1. 數據與資訊偏誤（Data & Information Biases）
- [前視偏誤 (Look-ahead Bias)](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/look_ahead_bias.md) — 探討未來資訊洩漏（Future Leakage）之成因、時序對齊陷阱與 Point-in-Time 防範機制。
- [倖存者偏誤 (Survivorship Bias)](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/survivorship_bias.md) — 剖析靜態股票池忽略退市標的之後果、危害與無偏誤歷史資料集標準。

### 2. 模型調校與統計驗證（Model Tuning & Statistical Validation）
- [過擬合與樣本外測試 (Overfitting and OOS)](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/overfitting_and_oos.md) — 解構數據窺探、參數孤島與非平穩市場特性，建立 OOS、WFA 與 Purged CV 驗證體系。

### 3. 交易摩擦與執行成本（Execution & Friction Costs）
- [手續費與滑價耗損模型 (Slippage and Fees)](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/slippage_and_fees.md) — 解析顯性規費、買賣價差與平方根市場衝擊成本，避免回測獲利在實盤被摩擦吞噬。

### 4. 風險計量與績效評估（Risk Metrics & Evaluation）
- [最大回撤與夏普比率 (MDD and Sharpe)](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/mdd_and_sharpe.md) — 剖析夏普比率的常態假設缺陷、上行波動扣分問題，以及回撤持續期（Drawdown Duration）與水下曲線分析。

---

## 知識庫總覽統計
- 目前條目數：5
- 待處理來源檔案：0（全數處理完畢）
- 最近更新條目：最大回撤與夏普比率（MDD and Sharpe Ratio）
- 最後更新時間：2026-11-16 14:54:18
