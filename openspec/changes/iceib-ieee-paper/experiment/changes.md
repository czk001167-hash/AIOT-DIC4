# IV. Experiment — 章節變動紀錄

- **對應論文區段**：[ICEIB paper/main.txt](../../../../ICEIB%20paper/main.txt#L316-L363) / [docs/ICEIB_Paper_A-Z.md](../../../../docs/ICEIB_Paper_A-Z.md)
- **A–Z 對應**：`Q` (指標) → `R` (基準) → `S` (情境) → `T` (參數與階段) → `U` (初步結果與反例) → `V` (有效性與限制)

## 1. 已完成變動
- 保留兩批主機端配對測試結果（`-18.28%` 含 5 組退步；`-19.71%` 含 2 組退步）、開發板切換驗證與 FIFO／分鐘資料限制聲明。
- **（2026-11-25 修訂）**：正文改用 `\eqref{eq:queue_update}` 與 `\eqref{eq:qvs}` 動態引用公式。
- **（2026-11-25 修訂）**：將原本偏 Proposal 排程的開發階段進度表替換為 **Table II: Synthetic Evaluation Regimes and Benchmark Purpose**（整理五種交通情境與測試目標），並將未整合模組現況併入 `IV-C Validity Scope and Limitations`。

## 2. 仍需補齊項目（須依實測數據填入）
- 補入五種合成情境的具體參數值（到車率 $\lambda$、飽和流率 $\mu$、模擬長度 $T$、測試次數與隨機種子）。
- 補入 5/18 與 2/6 退步案例的情境分佈與幅度拆解，以及開發板實測 QVS 下降數據與推論／切換延遲（ms）。
