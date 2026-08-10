# Epistemic Workflow — 完整流程（Phase 0–16）

> Unknown Knowledge Discovery & Decision Calibration
> 使用方式與輕重兩檔判準見 [README.md](README.md)。

---

# Phase 0 — Decision Definition

在研究方法之前，先定義最後要做的決策。

回答：

1. 最後需要預測、解釋、分類、生成，還是做決策？
2. 決策的時間尺度是什麼？
3. 錯誤的代價是什麼？
4. False Positive 與 False Negative 哪一個比較昂貴？
5. 最終輸出要影響什麼行動？

禁止在 Decision 尚未定義時直接設計評分標準。

---

# Phase 1 — Problem Decomposition

重新定義使用者提出的問題。

區分：

- Objective：真正目標
- Proxy：目前拿什麼東西代表目標
- Constraint：現實限制
- Decision：最後要做什麼選擇
- Observable：目前有哪些資料可以觀察

特別檢查：

> 使用者目前提出的問題，是否其實只是一個 Proxy，而不是最終問題？

---

# Phase 2 — Discipline Discovery

找出至少 5 個研究過相似問題的專業領域。

每個領域說明：

- 領域名稱
- 它如何定義這個問題
- 它關心哪些變數
- 常用哪些方法
- 它可能忽略什麼

不要因為使用者提出某個領域，就假設那是唯一正確的問題框架。

---

# Phase 3 — Method Discovery

對每個候選領域尋找：成熟方法、學術方法、業界方法、統計方法、計算方法、實驗方法。

區分：

### A. Established Method
已有成熟名稱與使用紀錄。

### B. Derived Method
由成熟方法合理延伸。

### C. Heuristic
經驗法則。

### D. Speculative Method
Agent 自行提出的方法。

不得將 C、D 包裝成既有專業共識。

---

# Phase 4 — Observable Decomposition

把抽象概念轉換成可以觀察的變數。

對每個變數定義：

- Variable
- Measurement
- Unit
- Data source
- Expected relationship
- Possible confounders
- Measurement error

建立：

Concept → Dimension → Variable → Measurement → Data

---

# Phase 5 — Assumption Audit

任何模型、標準或門檻，都必須列出成立前提。

對每個假設回答：

1. 為什麼相信這個假設？
2. 有什麼證據支持？
3. 在什麼條件下成立？
4. 在什麼條件下可能失效？
5. 如果假設錯誤，結果會受到多大影響？

將假設分類：

- Structural assumption
- Statistical assumption
- Behavioral assumption
- Environmental assumption
- Data assumption
- Causal assumption

禁止將 Assumption 當成 Fact。

---

# Phase 6 — Criterion Audit

如果分析中出現任何：threshold / score / ranking / weight / cutoff / confidence level，必須追問：

> 為什麼是這個數值？

例如：Score > 70。必須區分：

### Arbitrary Threshold
人為指定。

### Empirical Threshold
歷史資料推導。

### Theoretical Threshold
理論推導。

### Decision Threshold
根據錯誤成本決定。

### Optimized Threshold
透過 validation data 最佳化。

沒有證據時，不得將 70、80、90 等數值描述成具有客觀意義的「信心」。

---

# Phase 7 — Base Rate & Reference Class

任何「發生機率」判斷之前，先找 Base Rate。

回答：

1. 在沒有其他資訊之前，這件事情本來多常發生？
2. 正確的 Reference Class 是什麼？
3. 不同 Reference Class 是否會產生不同結果？

例如「這家公司未來一年股價上漲」不能直接判斷 80%，應先知道：
相似市場環境 × 相似公司 × 相似估值 × 相似時間尺度 的歷史 Base Rate。

---

# Phase 8 — Alternative Hypotheses

禁止只驗證原始假說。至少建立：

- H1：主要假說
- H2：競爭解釋
- H3：反向解釋
- H4：Null hypothesis

詢問：

> 哪些資料如果出現，會讓我們放棄 H1？

如果不存在可以推翻假說的證據條件，該假說不可視為可靠模型。

---

# Phase 9 — Sensitivity Analysis

測試：

> 結論是否只是特定參數設定的產物？

例如原設定 ROE > 20%，必須測試附近範圍：10% / 15% / 20% / 25% / 30%。

觀察：

- 結果是否穩定
- Ranking 是否大幅改變
- 樣本數是否崩潰
- Performance 是否突然改變

如果小幅修改參數就導致完全不同結論，標記 **Parameter Sensitive**，不得描述為 Robust Result。

---

# Phase 10 — Robustness Check

同一問題至少嘗試：不同方法 / 不同資料區間 / 不同市場環境 / 不同變數定義 / 不同 threshold / 不同模型。

尋找：

> 哪些結論不管怎麼合理地改變方法，仍然存在？

這些才是較高可信度的 Signal。

---

# Phase 11 — Regime Analysis

檢查模型是否依賴環境。金融問題至少考慮：

Bull / Bear market、High / Low inflation、High / Low interest rate、High / Low volatility、Liquidity expansion / contraction。

不要假設歷史資料來自同一個 Data Generating Process。

---

# Phase 12 — Calibration

區分：**Score ≠ Probability**。

模型給 82/100，不代表 82% 機率發生。

如果要使用 Probability / Confidence，必須檢查 Calibration：

> 所有模型預測為 70% 的事件中，長期是否約有 70% 真正發生？

如果沒有驗證，不使用「70% 信心」描述結果。改用：

- High / Medium / Low evidence
- Relative score
- Ranking score
- Model confidence（需定義）
- Empirical probability（需有驗證）

---

# Phase 13 — Out-of-Sample Validation

任何從歷史資料找到的規則，都必須區分 Training / Validation / Test。

禁止在同一批資料：發現規則 → 調整規則 → 宣稱規則有效。

特別檢查：

- Overfitting
- Look-ahead bias
- Survivorship bias
- Selection bias
- Data leakage
- Multiple testing
- P-hacking

---

# Phase 14 — Blind Spot Search

完成模型後強制回答：

1. 目前模型看不到什麼？
2. 哪些變數可能重要，但目前沒有資料？
3. 有哪些相鄰學科會完全不同地理解這個問題？
4. 目前最大的 epistemic uncertainty 是什麼？
5. 如果目前結論是錯的，最可能錯在哪個假設？

---

# Phase 15 — Adversarial Review

建立一個獨立角色：**Red Team Agent**。

它的任務不是改善模型，而是證明模型可能是錯的。要求尋找：

- Counterexample
- Hidden assumption
- Confounder
- Alternative explanation
- Data artifact
- Parameter dependency
- Regime dependency

直到無法找到新的重大反例。

---

# Phase 16 — Decision Layer

最後才回答：根據目前證據，應該做什麼？輸出：

## Decision
推薦行動。

## Evidence
支持決策的主要證據。

## Assumptions
決策依賴哪些假設。

## Confidence
信心來自哪裡。

## Uncertainty
目前不知道什麼。

## Failure Conditions
什麼情況發生時，應重新評估。

## Next Information
如果只能再取得一項資訊，什麼資訊最能降低不確定性？

---

# Mandatory Three Whys

遇到任何重要標準時，執行：

### Why 1
為什麼使用這個變數／方法／門檻？

### Why 2
為什麼相信它與真正目標存在關係？

### Why 3
什麼證據會證明這個關係其實不存在？

如果第三題無法回答，該標準尚未完成驗證。

---

# Core Principle

不要問「哪個模型最好？」而是問：

> 「在什麼條件、資料、目標與錯誤成本下，哪個模型的決策品質最好？」

不要問「70 分以上是不是好股票？」而是問：

> 「歷史上被模型評為 70–80 分的樣本，在未參與模型建立的資料中，實際結果如何？」

不要把模型輸出的精確數字誤認成世界本身具有同樣程度的精確性。

## 三個常見盲點

1. **Method ≠ Truth**：找到專業方法還不夠，專家方法本身帶有假設，必須追問「這個方法在什麼條件下有效」。
2. **Threshold illusion**：`Score > 80 → 強烈買進` 的問題不是權重準不準，而是 80 這個數字還沒有機率意義。正確方向反過來：模型產生 Score → 歷史 out-of-sample 樣本 → 分 bucket → 觀察實際結果，資料告訴你 80+ 曾經對應到什麼結果——不是你「決定」80 = 高信心。
3. **缺 Objective Function**：「最優」是對什麼而言？勝率 78%/報酬 +6% vs 勝率 57%/報酬 +18% vs 勝率 65%/報酬 +12%/回撤 -8%——沒有 Objective Function 就不存在「最佳模型」。
