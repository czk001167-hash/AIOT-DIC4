# III. Proposed Design — 章節變動紀錄

- **對應論文區段**：[ICEIB paper/main.txt](../../../../ICEIB%20paper/main.txt#L149-L311) / [docs/ICEIB_Paper_A-Z.md](../../../../docs/ICEIB_Paper_A-Z.md)
- **A–Z 對應**：`P` / `PA`–`PM`（整合原 Proposal 第 4 節 Deep Research 與第 5.1–5.4 節 Proposed Scheme）

## 1. 已完成變動
- 將 `M1`–`M5` 與 `C1`–`C3` 整併為 `III-A Domain Design Rationale and Trade-offs`。
- **（2026-11-25 修訂）修復 `Algorithm 1` LaTeX 標籤錯誤**：改用 `\usepackage{algorithm}` 與 `\begin{algorithm}[t]\caption{...}\label{alg:control_loop}`，確保 `Algorithm~\ref{alg:control_loop}` 正確解析為 `Algorithm 1`。
- **（2026-11-25 修訂）補入向量架構圖與流程圖（`Fig. 1`、`Fig. 2`）**：以自包含 `TikZ` 繪製 8 模組閉迴路架構圖（區分實線既有核心模組與虛線待整合模組，含狀態回饋與生效證據雙迴路）與執行流程圖，不需額外圖檔即可於 Overleaf 編譯。
- **（2026-11-25 修訂）補入佇列守恆更新式**：於 `III-D` 新增離散時間 FIFO 更新式 $q_d(t+1)=\max(0, q_d(t)+a_d(t)-s_d(t))$（`\label{eq:queue_update}`）並為 QVS 公式加上 `\label{eq:qvs}`。

## 2. 仍需補齊項目
- 從實作程式碼匯出三種配時方案的具體秒數（$G_{\min}$、$G_{\max}$、週期長度）以及決策樹深度與 out-of-domain 判定門檻填入 `III-D`。
