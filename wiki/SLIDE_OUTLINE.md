# 量化交易回測簡報大綱（SLIDE_OUTLINE.md）

本文件規劃為完全零基礎初學者設計的教學型簡報結構，總計 10 頁，內容 100% 忠於 `wiki/` 目錄中各條目內容，不引入任何外部未收錄之術語。

---

## 簡報頁面規劃清單

### 第 1 頁：封面（Title Slide）
- **頁面主題**：量化交易回測的常見陷阱與過擬合防範 — 從「紙上富貴」到「實盤生存」的必修課
- **對應 Wiki 檔案**：[wiki/index.md](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/index.md)
- **核心內容**：
  - 副標題：零基礎量化研究員與投資人的避坑指南
  - 核心痛點提問：為什麼歷史回測曲線年化獲利驚人，實盤上線卻立刻面臨資產崩跌？
- **Wiki 一致性核對**：採用 `wiki/index.md` 總體架構定位，無外部術語。

---

### 第 2 頁：學習目標與核心迷思（Learning Objectives）
- **頁面主題**：看懂回測的真相：回測是「證偽工具」，不是「造神機器」
- **對應 Wiki 檔案**：[wiki/index.md](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/index.md)
- **核心內容**：
  - 初學者三大常見迷思：回測賺錢不等於實盤賺錢、夏普比率越高不代表風險越低、歷史表現不能無腦外推。
  - 本堂課學習三大目標：
    1. 識別數據端的「偷看答案」與「只看贏家」偏誤。
    2. 理解模型訓練中「死背考古題」的過擬合陷阱。
    3. 掌握真實交易的摩擦耗損與風險計量標準。
- **Wiki 一致性核對**：聚焦 `wiki/index.md` 所歸納的四大知識模組與核心痛點。

---

### 第 3 頁：核心架構總覽（Architecture Overview）
- **頁面主題**：量化回測崩盤的 4 大面向與 5 大致命陷阱
- **對應 Wiki 檔案**：[wiki/index.md](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/index.md)
- **核心內容**：
  - 模組 1【數據與資訊偏誤】：前視偏誤（Look-ahead Bias）、倖存者偏誤（Survivorship Bias）
  - 模組 2【模型調校與統計驗證】：過擬合與樣本外測試（Overfitting & OOS）
  - 模組 3【交易摩擦與執行成本】：手續費與滑價耗損模型（Slippage and Fees）
  - 模組 4【風險計量與績效評估】：最大回撤與夏普比率（MDD and Sharpe Ratio）
- **Wiki 一致性核對**：完全對應 `wiki/index.md` 的四大分類與條目。

---

### 第 4 頁：陷阱 1 — 前視偏誤（Look-ahead Bias）
- **頁面主題**：偷看未來答案的作弊考生
- **對應 Wiki 檔案**：[wiki/look_ahead_bias.md](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/look_ahead_bias.md)
- **核心內容**：
  - 白話定義：在回測做決策時偷看或引用了「當下時間點根本還不知道的未來資訊」。
  - 生活化比喻：考試開考前就先拿到印有參考答案的解答本，考場上 100 分，正式大考交白卷。
  - 對比表格：
    - 回測假象：當天以收盤價算指標，並在當天以收盤價或當日最低價買入。
    - 實盤真相：收盤價確認時市場已休市；最低價是盤後才確認的極值。
  - 修正關鍵：落實 `shift(1)` 訊號位移與 Point-in-Time（PIT）真實揭露時間對齊。
- **Wiki 一致性核對**：完全取自 `wiki/look_ahead_bias.md`。

---

### 第 5 頁：陷阱 2 — 倖存者偏誤（Survivorship Bias）
- **頁面主題**：只看生還者的二戰轟炸機
- **對應 Wiki 檔案**：[wiki/survivorship_bias.md](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/survivorship_bias.md)
- **核心內容**：
  - 白話定義：選股時只挑今天活得很好的成功公司，把歷史上破產倒閉的倒楣鬼全都當作不存在。
  - 生活化比喻：統計飛回基地的轟炸機彈孔（機翼最多）就決定強化機翼，忽略座艙中彈的飛機根本回不來。
  - 對比表格：
    - 回測假象：拿當前 S&P 500 或台灣 50 清單回測 20 年，避開了所有破產歸零公司。
    - 實盤真相：2000 年網路泡沫與 2008 年金融海嘯時，多數持倉成分可能遭遇下市爆倉。
  - 修正關鍵：採用無偏誤資料集（Survivorship-Bias-Free Dataset）與歷史當期動態成分股名單。
- **Wiki 一致性核對**：完全取自 `wiki/survivorship_bias.md`。

---

### 第 6 頁：陷阱 3 — 過擬合與樣本外測試（Overfitting & OOS）
- **頁面主題**：把考古題選項死背下來的學生
- **對應 Wiki 檔案**：[wiki/overfitting_and_oos.md](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/overfitting_and_oos.md)
- **核心內容**：
  - 白話定義：策略死記硬背了過去歷史資料中的雜訊與巧合，在過去考題中拿滿分，遇到新市場徹底當掉。
  - 生活化比喻：學生死記「第 1 題選 C、第 2 題選 A」，考題數字稍有變動即考 0 分。
  - 對比表格：
    - 回測假象：測試 1 萬組參數找出最孤立的完美參數組合，樣本內夏普比率高達 3.5。
    - 實盤真相：市場充滿非平穩雜訊，參數孤島在新行情中完全失效。
  - 修正關鍵：嚴格劃分樣本外（OOS）、尋找寬廣參數平原、步進分析（WFA）與淨化交叉驗證（Purged CV）。
- **Wiki 一致性核對**：完全取自 `wiki/overfitting_and_oos.md`。

---

### 第 7 頁：陷阱 4 — 手續費與滑價耗損（Slippage and Fees）
- **頁面主題**：二手跳蚤市場批發公仔的殘酷過路費
- **對應 Wiki 檔案**：[wiki/slippage_and_fees.md](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/slippage_and_fees.md)
- **核心內容**：
  - 白話定義：真實買賣每次都要抽稅與手續費，想買的價格早已被搶光；若當成 0 耗損就是白日夢。
  - 生活化比喻：想在跳蚤市場每次加價 5 元轉賣賺快錢，卻忽略了入場攤位費、交易稅與搶購滑價，交易越頻繁虧越多。
  - 對比表格：
    - 回測假象：假設 0 滑價、0 手續費，每日高頻衝進衝出累積虛擬獲利。
    - 實盤真相：市價單穿透委託簿造成 1~2 Tick 滑價，加上交易稅，毛利完全無法覆蓋成本。
  - 修正關鍵：加入固定 Tick 滑價、保守稅費設定、限制成交量佔比（2%~5%）與計算盈虧平衡交易成本（BETC）。
- **Wiki 一致性核對**：完全取自 `wiki/slippage_and_fees.md`。

---

### 第 8 頁：陷阱 5 — 最大回撤與夏普比率（MDD and Sharpe Ratio）
- **頁面主題**：長途客運司機的平穩駕駛 vs. 飆車玩命
- **對應 Wiki 檔案**：[wiki/mdd_and_sharpe.md](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/mdd_and_sharpe.md)
- **核心內容**：
  - 白話定義：夏普比率看「每分風險換到多少報酬」，最大回撤（MDD）告訴你「最衰時會賠掉幾成身家」。
  - 生活化比喻：客運司機 A 平穩駕駛準時抵達（高夏普）；司機 B 狂飆闖紅燈差點墜崖（超大 MDD），中途乘客早就心臟病發。
  - 對比表格：
    - 回測假象：只看常態分佈夏普比率 > 2.0，看到歷史 MDD 僅 15% 就認為安全。
    - 實盤真相：金融市場有肥尾黑天鵝，且忽略在水下（Underwater）漫長沉浮 3~4 年的心心理折磨。
  - 修正關鍵：輔以索提諾比率（Sortino）與卡瑪比率（Calmar），審查水下時間曲線與蒙地卡羅重組分析。
- **Wiki 一致性核對**：完全取自 `wiki/mdd_and_sharpe.md`。

---

### 第 9 頁：實戰避坑檢查清單（Quant Backtesting Checklist）
- **頁面主題**：策略上線前必做的 5 步關鍵自我檢核
- **對應 Wiki 檔案**：綜合 `wiki/look_ahead_bias.md`、`wiki/survivorship_bias.md`、`wiki/overfitting_and_oos.md`、`wiki/slippage_and_fees.md`、`wiki/mdd_and_sharpe.md`
- **核心內容**：
  1. [ ] **時序位移**：所有信號是否已執行 `.shift(1)`？基本面是否採用 Point-in-Time 發布日？
  2. [ ] **資產池純淨**：回測名單是否包含歷史退市與倒閉股票？
  3. [ ] **樣本外盲測**：保留 20%~30% OOS 數據進行單次盲測，拒絕在參數孤島上優化？
  4. [ ] **摩擦耗損加倍**：手續費與滑價是否採用保守或 1.5 倍壓力測試？BETC 是否 > 15 bps？
  5. [ ] **水下持續期**：最大回撤修復期是否在投資人資金耐受天數內？是否考量肥尾非對稱風險？
- **Wiki 一致性核對**：所有檢查項目皆萃取自 5 篇條目中的【防範實務檢核點】。

---

### 第 10 頁：總結與核心心法（Conclusion）
- **頁面主題**：成為敬畏市場的理性量化交易者
- **對應 Wiki 檔案**：[wiki/index.md](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/index.md)
- **核心內容**：
  - 三大核心鐵律：
    1. **誠實面對數據**：寧可在回測中看到平庸卻真實的報酬，也不要在虛擬世界自欺欺人。
    2. **給市場留餘量**：任何未經摩擦壓力測試與極端衝擊檢驗的策略都不具生命力。
    3. **敬畏尾部風險**：高夏普不等於零風險，活得久比短期賺得多更重要。
  - 延伸學習指引：查閱 `wiki/` 目錄深入研讀各篇公式推導與實務防範策略。
- **Wiki 一致性核對**：完全基於 Wiki 整體精神與結論。

---

## 自我審查結論（Self-Check Verification）
- [x] 頁數符合規範：共 10 頁（包含封面、學習目標、核心架構、5 大陷阱各 1 頁、避坑清單、總結）。
- [x] 每頁皆清楚標註對應的 `wiki/xxx.md` 檔案名稱。
- [x] 嚴格檢查所有名詞與數據：所有技術詞彙（如 Point-in-Time、shift(1)、Survivorship-Bias-Free、OOS、WFA、Purged CV、DSR、Tick 滑價、BETC、Calmar Ratio、Underwater Duration、肥尾風險等）均 100% 收錄於對應 Wiki 檔案中，無任何脫離 Wiki 的外部捏造名詞或無關資料。
