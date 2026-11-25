# References — 章節變動紀錄

- **對應論文區段**：[ICEIB paper/main.txt](../../../../ICEIB%20paper/main.txt#L315-L335) / [docs/ICEIB_Paper_A-Z.md](../../../../docs/ICEIB_Paper_A-Z.md)
- **格式標準**：IEEE Conference (`\begin{thebibliography}{00}`)

## 1. 已完成變動（相較原始 Proposal）
- 將原 Proposal 第 6 節 `[A1]–[A3]` 與 `[D1]–[D3]` 轉換為 IEEE 標準 `\bibitem` 條目（作者縮寫、雙引號篇名、斜體期刊／會議名、DOI 與 `\url{...}`）。

## 2. 待修改變動（Next Revisions）
- **【重要】依正文首次引用順序重排 `\bibitem`**：目前排列為 `VIPER [1] → CoLLMLight [2] → VTP [3] → HK Pilot [4] → Wu et al. [5] → FHWA [6]`，但 Section I 第一段先引用 `HK Pilot` 與 `Wu et al.`。依 IEEE 規範應配合正文重排為 `[1]` 起算之連續引用順序。
- **補上線上文獻存取日期**：如 `[4]`（香港政府新聞處）與 `[6]`（FHWA 手冊 PDF）建議依 IEEE 線上引用格式補上 `(accessed Mon. Day, Year)`；若 `[2]`、`[3]` 投稿前已有正式會議或期刊出版，應更新為正式書目。
