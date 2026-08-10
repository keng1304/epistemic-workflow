---
name: epistemic-workflow
description: 🔬 認知與決策校準工作流（Epistemic Workflow）— 先審判標準，再使用標準。任何出現 threshold/score/ranking/weight/cutoff/信心數字的分析，或要建立可重複使用的模型/評分系統時觸發。輕檔=Three Whys + Criterion Audit + Base Rate；重檔=Phase 0-16 完整跑。觸發關鍵字：「認知校準」「epistemic」「校準標準」「審判標準」「這個門檻哪來的」「為什麼是 20%」「base rate」「out-of-sample」「標準背後的假設」「告訴我我不知道的事」。
user_invocable: true
---

# epistemic-workflow — 認知與決策校準

**全文**：Read 同目錄的 `epistemic-workflow.md`（Phase 0-16 完整流程），照裡面的 Phase 執行。本檔只放路由邏輯。

## 核心命題

我們永遠在用可觀察指標，代理一個真正關心但不能直接觀察的目標。所以：

> **先審判標準，再使用標準。**
> Agent 的工作是發現候選標準、揭露標準背後的假設、用現實資料校準標準——不是替使用者決定標準。

## Step 0 — 判斷輕重檔

- **輕檔（日常預設）**：分析產出裡出現任何 threshold / score / ranking / weight / cutoff / 「信心 X%」→ 跑 **Three Whys**（為什麼用它 / 為什麼信它跟目標有關 / 什麼證據會推翻）＋ **Criterion Audit**（這數值是 Arbitrary / Empirical / Theoretical / Decision / Optimized threshold？）＋ **Base Rate**（正確 reference class 的歷史基準率）。
- **重檔（完整 Phase 0-16）**：建可重複使用的模型或評分系統 / 量化選股類 / 高錯誤成本決策 / 使用者明說「跑完整認知校準」→ Read 全文檔，逐 Phase 執行。

## 輸出紀律（不分輕重檔都適用）

1. Score ≠ Probability：沒做過 calibration 驗證，不准用「N% 信心」描述結果，改用 High/Medium/Low evidence 或 ranking。
2. Heuristic / Speculative method 不得包裝成專業共識（對應 Phase 3 的 A/B/C/D 分級）。
3. Assumption 不得當 Fact 陳述。
4. 小幅改參數就翻盤的結論標 **Parameter Sensitive**，不得稱 Robust。
5. 結論輸出走 Phase 16 Decision Layer 格式：Decision / Evidence / Assumptions / Confidence / Uncertainty / Failure Conditions / Next Information。

$ARGUMENTS
