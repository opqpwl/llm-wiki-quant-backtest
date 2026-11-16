# 過擬合與樣本外測試（Overfitting and Out-of-Sample Testing）

---

### 【一句話白話定義】
策略只是死記硬背了過去歷史資料中的雜訊與巧合，在過去考題中拿滿分，一旦遇到沒見過的新市場考題就徹底當掉。

---

### 【生活化比喻】
> 就像一個學生**把歷屆考古題的選項順序（例如「第 1 題選 C、第 2 題選 A」）死記硬背下來**，模擬考時拿到滿級分；但這名學生根本沒有掌握解題的物理或數學原理，只要正式大考題目的數字或選項順序稍微變動，立刻交白卷或考出零分。

---

### 【深入技術解析】
金融市場具備高度非平穩性（Non-Stationarity）與極低信噪比（Low Signal-to-Noise Ratio）。過擬合（Overfitting）在量化領域常透過以下途徑滲透進策略研發中：
1. **數據窺探（Data Snooping）與多重假設檢定（Multiple Testing）**：
   在同一個資料集上測試 10,000 組技術指標參數，即使市場純屬隨機漫步，統計上根據 p-value 5% 的水準也必然會產出 500 組「顯著獲利」的偽指標（False Positives）。
2. **過度參數化與複雜模型**：
   引入過多層神經網路或繁複的濾網條件（如「當 RSI < 21.5 且 週二且成交量是 3.2 倍時進場」），耗盡系統自由度，將歷史隨機行情的特定噪點當作真理。
3. **時序漏水交叉驗證**：
   在時序數據上誤用傳統隨機 K-Fold 交叉驗證，使相鄰時間點的持倉期重疊資訊滲漏至訓練集。

---

### 【錯誤 vs. 正確對照】

| 評估維度 | 常見錯誤實作（造成過擬合） | 標準正確做法（防範過擬合） |
| :--- | :--- | :--- |
| **參數尋優準則** | 在全歷史資料集上進行暴力網格搜索（Grid Search），選取全歷史累積淨值最高、夏普比率最高的單一參數組合。 | 尋找**寬廣的參數平原（Parameter Plateau）**而非孤島；採用樣本外步進測試（Walk-Forward Analysis）檢驗參數跨期穩定性。 |
| **資料集劃分** | 隨意使用全歷史資料進行調參，或反覆調整模型直到樣本外（OOS）表現變好（使 OOS 淪為變相的訓練集）。 | 嚴格劃分 **In-Sample（訓練集）** 與 **Out-of-Sample（盲測外樣本）**。OOS 數據在策略結構凍結前嚴禁讀取，僅能執行單次檢驗。 |
| **交叉驗證方法** | 使用標準機器學習的隨機洗牌 K-Fold CV（Shuffle Split）。 | 使用 Marcos López de Prado 提出的 **淨化與禁運交叉驗證（Purged & Embargoed K-Fold CV）**，排除時序重疊洩漏。 |
| **績效顯著性檢驗** | 僅依據單次回測的夏普比率（如 SR > 2.0）即認定策略有效。 | 計算 **折減夏普比率（Deflated Sharpe Ratio, DSR）**，扣除多重回測試驗次數與偏態肥尾帶來的虛增效果。 |

---

### 【防範實務檢核點】
1. **OOS 衰退率檢驗**：計算樣本外夏普比率與樣本內夏普比率之比值（$OOS\_SR / IS\_SR$），若低於 50% 應高度警惕過擬合。
2. **參數敏感度分析（Sensitivity Test）**：將最佳參數上下浮動 10%～20%，若淨值曲線發生劇烈回撤，該參數組合屬於隨機孤島。
3. **虛擬隨機數據置換（White's Reality Check / Permutation Test）**：將市場行情報酬隨機打亂重組，檢驗策略在合成無意義數據上的表現，確認 alpha 信號的統計顯著性。

---

### 【關聯條目連結】
- [前視偏誤 (Look-ahead Bias)](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/look_ahead_bias.md)：前視偏誤常在樣本內產生近乎神級的偽高報酬，形式上與極端過擬合極為相似，兩者皆會導致樣本外暴跌。
- [倖存者偏誤 (Survivorship Bias)](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/survivorship_bias.md)：若在存在倖存者偏誤的無效母體上進行最佳化調參，所得出的參數僅是在「倖存贏家」身上過度擬合的假象。
- [手續費與滑價耗損模型 (Slippage and Fees)](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/slippage_and_fees.md)：過擬合的日內高頻交易策略在未考慮真實摩擦成本時最為致命。
- [最大回撤與夏普比率 (MDD and Sharpe)](file:///c:/Users/User/Desktop/llm-wiki-hw10/wiki/mdd_and_sharpe.md)：過擬合最顯著的外在徵兆就是樣本內夏普比率異常虛高與 MDD 人為平滑。

---

### 【資料來源】
資料來源：[raw/03_overfitting_and_oos.md](file:///c:/Users/User/Desktop/llm-wiki-hw10/raw/03_overfitting_and_oos.md)
