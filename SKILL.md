---
name: epistemic-workflow
description: 🔬 認知與決策校準工作流 v2（Epistemic Architect）— 先審判標準，再使用標準。四模式 Router：DISCOVERY（知道目標不知道有哪些專業方法）/ AUDIT（已有框架，找假設盲點）/ CALIBRATION（出現 threshold/score/ranking/weight/信心數字）/ FULL ARCHITECTURE（建可重複使用的 Agent/Skill/決策系統/評分系統，Step 1-20 完整跑＋Execution Spec 交棒）。觸發關鍵字：「認知校準」「epistemic」「epistemic architect」「校準標準」「審判標準」「這個門檻哪來的」「為什麼是 20%」「base rate」「out-of-sample」「標準背後的假設」「告訴我我不知道的事」「我不知道我不知道什麼」。
user_invocable: true
---

# epistemic-workflow v2 — Epistemic Architect

**全文**：Read 同目錄的 `epistemic-architect.md`（Router + Step 1-20 + Anti-Patterns + Evidence Hierarchy + Internal Checklist），照裡面執行。v1 線性版在 `epistemic-workflow.md`。本檔只放路由邏輯。

## 核心命題

我們永遠在用可觀察指標，代理一個真正關心但不能直接觀察的目標。所以：

> **先審判標準，再使用標準。**
> The system should not merely follow the user's standards. It should first determine whether those standards deserve to be followed.

使用者的既有知識，不得成為分析的邊界。使用者給的框架/門檻/權重/因果解釋，一律當 **candidate hypothesis**，不當 established truth。

## Step 0 — Router（先判模式，用足夠小的模式就好）

| 模式 | 何時用 | 跑什麼 |
|---|---|---|
| **DISCOVERY** | 知道目標，不知道有哪些專業方法/知識存在 | Step 1-3（Objective → Disciplines → Methods）＋ Step 17 Value of Information |
| **AUDIT** | 已有框架/工作流/模型要體檢 | Step 5-9（Assumption/Three Whys/Criterion/Base Rate/Alt Hypotheses）＋ Step 15-16（Blind Spot + Red Team） |
| **CALIBRATION** | 出現 score/threshold/ranking/weight/信心數字 | Three Whys ＋ Criterion Audit（Arbitrary/Empirical/Theoretical/Decision/Optimized）＋ Base Rate ＋ Score≠Probability |
| **FULL ARCHITECTURE** | 建可重複使用的 Agent/Skill/研究工作流/決策系統/評分系統 | Step 1-20 完整跑，結尾產 Execution Spec |

小 audit 夠用就不要跑全架構（Step 19 Stop Condition：sufficient knowledge > maximum completeness）。

## 輸出紀律（所有模式都適用）

1. **Score ≠ Probability**：沒做 calibration 驗證，不准用「N% 信心」，改用 Relative Score / Ranking / Evidence Strength（High/Medium/Low）。
2. Method 分級 ESTABLISHED / DERIVED / HEURISTIC / SPECULATIVE——後兩者不得包裝成專業共識。
3. Assumption 不得當 Fact；高風險假設（P(wrong) × Impact）先浮出再執行。
4. 小幅改參數就翻盤 → 標 **Parameter Sensitive**，不得稱 Robust。
5. Evidence Hierarchy 分層引用：empirical > validated research > theory > cross-domain > heuristic > agent inference > speculation，不得靜默升級。
6. Anti-Patterns 自檢：Framework Anchoring / Expert Theater / False Precision / Threshold Invention / Metric Substitution / Confirmation Architecture / Complexity Bias / Research Infinity。
7. 完整跑時結論走 Output Format 15 段；交棒執行 agent 只給 Execution Spec（不用給整個 discovery 過程）。

$ARGUMENTS
