# IV. Experiment — 章節變動紀錄

- **對應論文區段**：[ICEIB paper/main.txt](../../../../ICEIB%20paper/main.txt#L242-L288) / [docs/ICEIB_Paper_A-Z.md](../../../../docs/ICEIB_Paper_A-Z.md)
- **A–Z 對應**：`Q` (指標) → `R` (基準) → `S` (情境) → `T` (參數與階段) → `U` (初步結果與反例) → `V` (有效性與限制)

## 1. 已完成變動（相較原始 Proposal）
- 將評估計畫、指標（QVS、平均等待、剩餘車輛、方向差異、硬體回讀一致性）、對照基準與五種合成情境整理為 IEEE 論文實驗章節。
- 彙整 `Table II` 呈現兩批主機端配對結果（`-18.28%` 含 5 組退步；`-19.71%` 含 2 組退步）與板端切換驗證，嚴格不合併跨批成效數字。
- 納入 `IV-C Validity Scope and Limitations`，明確揭露簡化 FIFO 佇列假設與官方分鐘資料粒度不足之限制。

## 2. 待修改變動（Next Revisions）
- **修正公式引用（L234–L236, L248）**：為 QVS 公式加上 `\label{eq:qvs}`，正文 `QVS (1)` 改為 `QVS~\eqref{eq:qvs}`。
- **補齊情境參數表與退步案例拆解（對應 `T`, `U`）**：列出 5 種合成情境的到車率 $\lambda$、飽和流率 $\mu$、模擬長度 $T$、測試次數／隨機種子，並說明 5 組與 2 組退步案例各自所屬的情境與幅度。
- **量化板端驗證指標**：為 `Dev-Board Paired Test` 補入實測 QVS 下降數據與 ARM 推論／FPGA 切換延遲（ms）。
- **調整 `Table III` 定位**：目前 `Table III`（開發階段與驗收判準）屬於 Proposal 工作排程，在正式 ICEIB 論文中建議改為「實驗參數／硬體規格表」或併入未來工作。
