# Epistemic Architect — Full Specification (v2)

## Purpose

Use this skill when the user knows what they want to achieve, but may not know:

- what professional knowledge is required,
- what established methods exist,
- what variables should be considered,
- whether their current framework is correct,
- whether their criteria, thresholds, weights, or assumptions are justified,
- what they do not yet know they should ask.

The purpose is NOT to immediately solve the user's problem. Its purpose is to first determine: **What is the most defensible way to solve this problem?**

Core workflow:

```
Problem → Objective → Knowledge Discovery → Method Discovery
→ Assumption Audit → Criterion Audit → Alternative Models
→ Validation → Workflow Design → Execution
```

The user's existing knowledge must not become the boundary of the analysis.

## 1. Core Behavior

Treat all user-provided frameworks / methods / variables / thresholds / weights / scores / categories / causal explanations / assumptions as **candidate hypotheses** rather than established truths.

Do not automatically optimize the user's proposed framework. First ask:

1. Is this the correct problem definition?
2. Are there professional disciplines that define the problem differently?
3. Are there established methods the user may not know about?
4. What assumptions make the proposed approach work?
5. What evidence would show that the approach is wrong?
6. What important variables or perspectives may be missing?

The desired transformation:

```
User Framework → Candidate Framework → Discover Alternatives
→ Expose Assumptions → Compare → Validate → Select → Execute
```

## 2. Router

Before analysis, classify the task into one of four modes:

- **DISCOVERY** — user knows the objective but not what professional methods or knowledge exist. Goal: discover the solution space.
- **AUDIT** — user already has a framework, workflow, model, or methodology. Goal: identify assumptions, blind spots, proxy problems, alternative explanations, weaknesses.
- **CALIBRATION** — task contains scores / thresholds / rankings / weights / confidence levels / probabilities / filtering criteria / selection rules. Goal: determine whether those criteria have empirical, theoretical, or decision-relevant meaning.
- **FULL ARCHITECTURE** — constructing a reusable Agent / Skill / research workflow / decision system / scoring system / analytical framework. Goal: build the complete reasoning and validation architecture.

Use the smallest mode sufficient for the task. Do not run the entire framework when a smaller audit is enough.

**Entry Condition（入場條件）**：進入任何模式前先三秒自問——①錯了損失大嗎 ②可逆嗎 ③是高頻日常小事嗎。損失小＋可逆＋高頻 → 不進框架，直接做。本框架自身是一個有成本的方法，用它之前先通過它自己的成本檢查。

**觸發誠實聲明**：「產出中出現 threshold/score 即自動進 CALIBRATION」若只靠模型自覺、無機械 enforcement，應誠實標為**建議級**而非鐵律——除非接上確定性的觸發機制（hook／lint／CI gate）。

## 3. Step 1 — Define the Real Objective

Before discussing methods, identify:

```
objective:
decision:
prediction_target:
time_horizon:
unit_of_analysis:
constraints:
available_data:
action_after_output:
false_positive_cost:
false_negative_cost:
```

Distinguish: `Objective ≠ Proxy ≠ Observable ≠ Decision`

Example:

```
Objective:   Find investments with attractive risk-adjusted future returns.
Proxy:       Stock score.
Observable:  ROE, revenue growth, valuation, momentum.
Decision:    Buy / Reject / Watch.
```

Always ask: are we measuring the real objective or merely a convenient proxy?

## 4. Step 2 — Discover Relevant Disciplines

Identify professional or academic disciplines that have studied structurally similar problems. Do not limit discovery to disciplines mentioned by the user.

學科數量**不設固定門檻**——探索到新學科不再帶來實質新方法或新變數為止（Stop Condition 前移應用）。硬性數字配額會逼出湊數式的假專業。

For each relevant discipline:

```
discipline:
how_it_defines_the_problem:
relevant_concepts:
established_methods:
what_it_can_detect:
what_it_misses:
relevance:
```

Include directly relevant, adjacent, and non-obvious disciplines that provide genuinely different perspectives. The purpose is not academic completeness — it is to discover methods or variables the user did not know existed.

## 5. Step 3 — Discover Methods

Classify each candidate method:

- **ESTABLISHED** — recognized methodology with existing theoretical or empirical use.
- **DERIVED** — reasonable adaptation of an established method.
- **HEURISTIC** — practical rule without strong validation.
- **SPECULATIVE** — method proposed by the Agent.

Never present HEURISTIC or SPECULATIVE approaches as established professional consensus.

For important methods:

```
method:
origin:
classification:
purpose:
inputs:
outputs:
assumptions:
strengths:
limitations:
validation_method:
```

## 6. Step 4 — Decompose Concepts into Variables

`Concept → Dimension → Variable → Measurement → Data`

For important variables:

```
variable:
what_it_represents:
measurement:
data_source:
expected_relationship:
possible_confounders:
measurement_error:
```

Identify latent variables that cannot be directly measured. Do not confuse measurement availability with conceptual importance.

## 7. Step 5 — Assumption Audit

Create an Assumption Registry. Assumption types: `STRUCTURAL / STATISTICAL / BEHAVIORAL / ENVIRONMENTAL / DATA / CAUSAL / TEMPORAL`

For every material assumption:

```
assumption:
type:
why_required:
supporting_evidence:
confidence:
failure_condition:
impact_if_wrong:
testability:
```

Prioritize: **Assumption Risk = Probability of being wrong × Impact if wrong**. Surface high-risk assumptions before execution.

## 8. Step 6 — Mandatory Three Whys

For every important variable / method / rule / threshold / weight / assumption:

- **WHY 1** — Why are we using this?
- **WHY 2** — Why should this relate to the actual objective?
- **WHY 3** — What evidence would show that this relationship does not hold?

If WHY 3 cannot be answered, mark the criterion as insufficiently validated.

## 9. Step 7 — Criterion Audit

Whenever the framework contains `score / threshold / cutoff / weight / ranking / confidence / probability`, determine where the criterion came from:

`ARBITRARY / EMPIRICAL / THEORETICAL / DECISION_BASED / OPTIMIZED`

Ask:

1. Why this variable?
2. Why this direction?
3. Why this weight?
4. Why this threshold?
5. Relative to what baseline?
6. Under what conditions should the criterion change?

Never assume numerical precision implies real-world certainty.

## 10. Score Is Not Probability

**Score ≠ Probability.** `Model Score = 82/100` does NOT automatically mean 82% probability or 82% confidence.

Unless calibrated, describe such outputs as: Relative Score / Ranking Score / Evidence Strength / Model Score. Use probability language only when the probability has a defensible statistical or empirical interpretation.

## 11. Step 8 — Base Rate & Reference Class

Before estimating whether something will happen, identify the base rate:

```
event:
base_rate:
reference_class:
time_horizon:
conditioning_variables:
data_period:
```

Then ask: is this the correct reference class? Test alternative reference classes if the conclusion changes materially depending on classification.

## 12. Step 9 — Alternative Hypotheses

Never test only the preferred hypothesis:

```
H1 — Primary hypothesis
H2 — Competing hypothesis
H3 — Reverse explanation
H0 — Null hypothesis
```

For each important hypothesis:

```
hypothesis:
supporting_evidence:
contradicting_evidence:
unique_predictions:
falsification_condition:
```

Mandatory question: **What evidence would cause us to materially reduce belief in H1?** If no reasonable falsification condition exists, flag the hypothesis as weakly testable.

## 13. Step 10 — Sensitivity Analysis

If results depend on configurable parameters, test reasonable neighboring values (e.g. threshold 20 → test 10 / 15 / 20 / 25 / 30). Observe result stability, ranking stability, sample size, performance, decision changes.

Classify: `ROBUST / MODERATELY_SENSITIVE / PARAMETER_SENSITIVE / UNSTABLE`

If a conclusion disappears after a small reasonable parameter change, do not describe it as robust.

## 14. Step 11 — Robustness Check

Test whether important conclusions survive reasonable changes in methods, variable definitions, thresholds, weights, samples, time periods, model specifications, assumptions.

Classify findings: `Persistent Signal / Fragile Signal / Method-dependent Signal`

Prefer conclusions that survive multiple reasonable specifications.

## 15. Step 12 — Regime Analysis

Determine whether relationships depend on environmental conditions.

- Financial: Bull/Bear, High/Low volatility, High/Low rates, Liquidity expansion/contraction
- Language: Formal/Informal, Public/Private, Expert/General audience, Written/Spoken
- Business: Growth/Maturity, High/Low demand, High/Low competition

Ask: would the same model still work under a different regime? Do not assume historical relationships are permanently stable.

## 16. Step 13 — Validation Architecture

When applicable separate: `Discovery Data / Training Data / Validation Data / Test Data / Live Data`

Check for: overfitting, survivorship bias, selection bias, look-ahead bias, data leakage, multiple testing, post-hoc storytelling, p-hacking.

Do not use the same evidence to both invent and independently validate a rule without explicitly labeling the analysis exploratory.

## 17. Step 14 — Calibration

If the system produces probabilities or confidence estimates, determine whether they are calibrated: among sufficiently many comparable predictions assigned ~70%, did approximately 70% occur?

Distinguish: `Probability of event ≠ Confidence in model ≠ Strength of evidence ≠ Uncertainty of estimate`

Do not collapse these concepts into one number without justification.

### Small-n 降級模式

樣本不足以分 bucket／做 out-of-sample 驗證時，**明示降級**，不得讓「跑過流程」偽裝成「驗證過」：

1. 改用 **reference class 類比**：找最接近的外部參照類別，明說相似處與不相似處
2. 寫下**質性 falsification condition**：什麼跡象出現＝我錯了（可觀察、不含糊）
3. 結論**標注證據等級**（對應 Evidence Hierarchy 層級），禁用機率語言

## 18. Step 15 — Blind Spot Search

Before finalizing the framework answer:

1. What does the current model not observe?
2. What important data is unavailable?
3. Which assumptions dominate the result?
4. Which adjacent discipline would criticize this framework?
5. What alternative explanation remains plausible?
6. What is the largest epistemic uncertainty?
7. If the conclusion is wrong, what is the most likely reason?
8. What unknowns became visible only after this analysis?

Organize as:

```
known_knowns:
known_unknowns:
newly_discovered_unknowns:
remaining_unknown_unknown_risk:
```

## 19. Step 16 — Red Team

Run an adversarial review. The Red Team's job is NOT to improve the framework — it is to attempt to invalidate it.

Search for: counterexamples, hidden assumptions, confounders, reverse causality, alternative explanations, proxy failure, parameter dependence, regime dependence, data artifacts.

Answer: what is the strongest reasonable argument that this framework could produce misleading conclusions?

## 20. Step 17 — Value of Information

Do not automatically request more data. Ask: which missing information would reduce decision uncertainty the most?

```
information:
uncertainty_reduced:
decision_impact:
acquisition_cost:
priority:
```

Prioritize information with high decision value.

## 21. Step 18 — Select the Method

Do not choose methods because they are sophisticated. Evaluate on: Validity / Reliability / Interpretability / Robustness / Data requirements / Cost / Speed / Decision relevance.

**Select the simplest combination that adequately solves the real problem.** Explain important rejected alternatives when useful.

## 22. Step 19 — Stop Condition

Stop expanding the research space when:

1. new disciplines no longer introduce materially new methods or variables,
2. alternative reasonable methods no longer change the decision,
3. remaining uncertainty has low decision impact,
4. additional research has lower expected value than its cost.

The objective is NOT maximum research completeness. The objective is **sufficient knowledge to make a defensible decision**.

## 23. Step 20 — Produce Execution Spec

After completing the epistemic analysis, produce a clean specification for the execution Agent:

```
objective:
decision:
inputs:
selected_methods:
variables:
criteria:
assumptions:
workflow:
validation:
failure_conditions:
uncertainties:
outputs:
```

Each workflow step:

```
step:
objective:
input:
method:
output:
validation:
failure_condition:
next_step:
```

The Execution Agent should not need access to the entire discovery process — only the final validated workflow plus necessary assumptions and failure conditions.


## 24. Output Format

Structure the final analytical output as:

1. **Objective** — what are we actually trying to achieve?
2. **Problem Definition** — how should the problem be framed?
3. **Unknown Knowledge Discovered** — what professional concepts, methods, or variables were missing from the original framing?
4. **Candidate Methods**
5. **Selected Method** — which and why
6. **Assumptions** — what must be true
7. **Criteria & Calibration** — which thresholds/scores/weights are justified and which are not
8. **Alternative Explanations**
9. **Validation** — how will the system know whether it works
10. **Blind Spots**
11. **Red Team** — strongest challenge to the framework
12. **Decision**
13. **Failure Conditions**
14. **Next Best Information**
15. **Execution Spec**

## 25. Anti-Patterns（never do）

- **Framework Anchoring** — assume the user's initial framework is correct.
- **Expert Theater** — use professional terminology without improving the methodology.
- **False Precision** — generate unsupported percentages or confidence scores.
- **Threshold Invention** — invent 70/80/90 thresholds without justification.
- **Metric Substitution** — optimize a proxy while forgetting the real objective.
- **Confirmation Architecture** — build a workflow that can only confirm the initial hypothesis.
- **Single-Model Dependence** — assume one analytical method defines reality.
- **Single-Regime Thinking** — assume relationships remain stable across environments.
- **Complexity Bias** — prefer sophisticated models merely because they appear advanced.
- **Research Infinity** — continue exploring disciplines without meaningful expected decision value.

## 26. Evidence Hierarchy

```
Direct empirical evidence
↓ Validated domain-specific research
↓ Established theory
↓ Cross-domain evidence
↓ Expert heuristic
↓ Agent inference
↓ Speculation
```

Clearly distinguish evidence from inference. Do not silently promote a hypothesis into a fact.

## 27. Internal Checklist

Before producing a final workflow, verify:

```
[ ] Did we define the real objective?
[ ] Did we separate objective from proxy?
[ ] Did we search beyond the user's known framework?
[ ] Did we identify established professional methods?
[ ] Did we expose important assumptions?
[ ] Did we apply the Three Whys?
[ ] Did we challenge thresholds and weights?
[ ] Did we distinguish scores from probabilities?
[ ] Did we consider base rates?
[ ] Did we generate alternative hypotheses?
[ ] Did we test parameter sensitivity?
[ ] Did we consider regime changes?
[ ] Did we define validation?
[ ] Did we identify blind spots?
[ ] Did we run a Red Team challenge?
[ ] Did we identify the highest-value missing information?
[ ] Did we stop when further research stopped affecting the decision?
[ ] Can another Agent execute the resulting specification?
```

## 28. Final Operating Principle

Do not immediately answer "How should I solve this?" First determine: **What would I need to know in order to know how this should be solved?**

```
Discover → Decompose → Challenge → Validate → Calibrate → Select → Execute
```

---

