# Epistemic Workflow — 認知與決策校準工作流

> **先審判標準，再使用標準。**
> Audit your criteria before you use them. A decision-calibration workflow for working with AI agents.

## 這是什麼

我們永遠在用某些**可觀察指標**，去代理一個**真正關心、但不能直接觀察的目標**。

選股用 ROE > 20%、客戶評分用 Score > 80、內容用互動率——這些不是「事實」，是**決策規則**。真正該追問的是：

- 為什麼是 20%？誰定的？根據什麼？
- Score 80 分，等於 80% 機率嗎？（不等於，除非驗證過 calibration）
- 這個門檻在什麼市場狀態下成立？換個環境還成立嗎？

多數人用 AI 的方式是「幫我照這套標準分析」。這個工作流把它反過來：

> **不要讓 Agent 幫你決定標準；讓 Agent 幫你發現候選標準、揭露標準背後的假設、再用現實資料校準標準。**

適用範圍不限量化投資：客戶評分、專案風險、商業策略、內容成效評估——底層都是同一類問題。

## 怎麼用

### 輕檔（日常預設）

任何分析裡出現 threshold / score / ranking / weight / cutoff / 「信心 X%」時，至少跑三件事：

1. **Three Whys** — 為什麼用這個門檻？為什麼相信它跟真正目標有關？什麼證據會推翻這個關係？（第三題答不出來 = 標準未完成驗證）
2. **Criterion Audit** — 這個數值是人為指定（Arbitrary）、歷史資料推導（Empirical）、理論推導（Theoretical）、錯誤成本決定（Decision）、還是 validation data 最佳化（Optimized）？
3. **Base Rate** — 在沒有其他資訊之前，這件事本來多常發生？正確的 reference class 是什麼？

### 重檔（完整 Phase 0–16）

建立可重複使用的模型或評分系統、量化選股、高風險決策時，走完整流程：

```
Phase 0   Decision Definition      先定義決策，才准設計評分標準
Phase 1   Problem Decomposition    Objective / Proxy / Constraint 拆開
Phase 2   Discipline Discovery     找 5 個研究過這問題的專業領域
Phase 3   Method Discovery         方法分級：成熟 / 延伸 / 經驗法則 / 推測
Phase 4   Observable Decomposition 抽象概念 → 可測變數
Phase 5   Assumption Audit         假設不是事實，列出成立前提
Phase 6   Criterion Audit          每個門檻追問「為什麼是這個數值」
Phase 7   Base Rate                先找基準率，再談機率
Phase 8   Alternative Hypotheses   H1 之外至少建 H2 / H3 / Null
Phase 9   Sensitivity Analysis     參數微調就翻盤 = Parameter Sensitive
Phase 10  Robustness Check         怎麼改方法都活著的結論才是 Signal
Phase 11  Regime Analysis          模型依賴什麼環境
Phase 12  Calibration              Score ≠ Probability
Phase 13  Out-of-Sample            同一批資料發現規則又宣稱有效 = 禁止
Phase 14  Blind Spot Search        模型看不到什麼
Phase 15  Adversarial Review       紅隊專職證明你是錯的
Phase 16  Decision Layer           最後才回答「該做什麼」
```

全文：[epistemic-workflow.md](epistemic-workflow.md)

### 當 Claude Code / Agent skill 用

把 [SKILL.md](SKILL.md) 放進 `~/.claude/skills/epistemic-workflow/`，之後說「認知校準」「這個門檻哪來的」「告訴我我不知道的事」就會觸發。

## 核心原則

不要問「哪個模型最好？」要問：

> 在什麼條件、資料、目標與錯誤成本下，哪個模型的決策品質最好？

不要問「70 分以上是不是好股票？」要問：

> 歷史上被評為 70–80 分的樣本，在未參與模型建立的資料中，實際結果如何？

不要把模型輸出的精確數字，誤認成世界本身具有同樣程度的精確性。

## License

MIT
