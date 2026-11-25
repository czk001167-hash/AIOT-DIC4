# III. Proposed Design — 章節變動紀錄

- **對應論文區段**：[ICEIB paper/main.txt](../../../../ICEIB%20paper/main.txt#L149-L237) / [docs/ICEIB_Paper_A-Z.md](../../../../docs/ICEIB_Paper_A-Z.md)
- **A–Z 對應**：`P` / `PA`–`PM`（整合原 Proposal 第 4 節 Deep Research 與第 5.1–5.4 節 Proposed Scheme）

## 1. 已完成變動（相較原始 Proposal）
- **章節整併**：依使用者指定論文架構，將五個核心思維（`M1`–`M5`）與三個專業爭論（`C1`–`C3`）整併為 `III-A Domain Design Rationale and Trade-offs`，直接銜接系統設計。
- **8 模組閉迴路架構（`III-B`）**：完整保留①～⑧模組與「核心已就緒（Core Ready）／待整合（Integration Target）」區分，以及狀態回饋／生效證據雙迴路。
- **流程與核心偽碼（`III-C`）**：納入 12 行邏輯（`Algorithm 1`），並保留資料不足、模型超界、僅檢視模式與硬體回讀四種檢查分支。
- **案例設計與數學式（`III-D`）**：補入 `QVS` 累積排隊車秒數學定義式（Equation 1）。

## 2. 待修改變動（Next Revisions）
- **【LaTeX Bug 必改】`Algorithm 1` 標籤失效（L187–L225）**：目前將演算法置於無 `\caption` 的 `figure` 環境中並放置 `\label{alg:control_loop}`，會導致 L185 `Algorithm~\ref{alg:control_loop}` 顯示錯誤編號。須改用 `\usepackage{algorithm}` 與 `\begin{algorithm}[t]\caption{...}\label{alg:control_loop}`。
- **補入架構圖與流程圖（`Fig. 1`、`Fig. 2`）**：將 Proposal 原有的 8 模組系統架構圖與處理流程圖轉為高解析 PDF/PNG 或 TikZ 圖嵌入本節（對應 `PG`、`PH`）。
- **補齊工程參數與佇列轉移式**：明確列出三種配時方案的綠／黃／全紅秒數（$G_{\min}$、$G_{\max}$）、決策樹深度與 out-of-domain 門檻，以及佇列守恆更新式 $q(t+1)=\max(0, q(t)+a(t)-s(t))$。
