# OR_Exam_Prep：MH6503 期末考複習文件

這是 NTU MH6503 Mathematical Programming and Optimisation 的完整複習資料，依據以下教材整理：

- 10 份上課講義（`After 1–10.pdf`，含手寫筆記）
- 10 份 Tutorial 與詳解
- 2025-26 期末考原卷與詳解

說明一律使用繁體中文，術語保留英文，數學式以 LaTeX 撰寫；只有 `04_Cheatsheet/` 中的 .txt 檔改用 Unicode 符號，方便貼到 Canva。

## 檔案與狀態

| 檔案 | 用途 | 狀態 |
|---|---|---|
| `01_Study_Guide/01_OR_Knowledge_Map.md` | 講次與檔名對照、課程主線、15 個主題總表（附講義頁碼、題號、考點）、題型對照、去年考點、教材之間的差異 | 完成 |
| `01_Study_Guide/02_Concepts_and_Derivations.md` | 主要教材。15 個主題，每個都依「直覺 → 定義 → 公式 → 推導 → 範例 → 講義補充 → 易混淆 → 關聯」的順序寫 | 完成 |
| `01_Study_Guide/03_Problem_Solving_Templates.md` | 18 個解題 SOP（S1–S18），包含辨識方式、步驟、表格格式、驗證、失分點、考卷寫法 | 完成 |
| `02_Practice/04_Exercise_Solutions.md` | T1–T10 全部 73 題，依章節排列，數值都經 Python 驗算 | 完成 |
| `02_Practice/05_Common_Mistakes.md` | 常見錯誤，分 A–H 八類，每條附原因、正確觀念、避免方法 | 完成 |
| `03_Final_Exam/06_Past_Exam_Analysis.md` | 2025-26 期末考逐題（含所有子題）完整解析、考卷作答版、對應的 Cheatsheet 內容 | 完成 |
| `03_Final_Exam/07_Exam_Strategy.md` | 章節重要度、考點分布、必備技能、時間分配、複習清單、優先練習題 | 完成 |
| `04_Cheatsheet/08_Cheatsheet_Front.md` | A4 正面：Concepts & Formulas（3 欄） | 完成 |
| `04_Cheatsheet/09_Cheatsheet_Back.md` | A4 背面：Algorithms & Problem-Solving（3 欄） | 完成 |
| `04_Cheatsheet/10_Cheatsheet_Canva_Ready.txt` | 正反面濃縮後的最終純文字版，可直接貼到 Canva | 完成 |
| `04_Cheatsheet/OR_Cheatsheet_Complete.txt` | 解題導向完整版：23 個題型，各含辨識、邏輯、SOP、公式、完整實戰案例、易錯、速查；附相似題型與停止條件總表 | 完成 |
| `04_Cheatsheet/OR_Cheatsheet_Quick_Reference.txt` | 由完整版濃縮的速查版：辨識、方法選擇、公式、步驟、停止條件、驗證、易錯 | 完成 |

## 建議閱讀順序

1. **01 知識地圖**：先看全貌，掌握各主題之間的依賴關係。
2. **02 概念推導 + 03 模板**：一個主題一個主題讀。讀完一個主題，就到 04 做對應的題目。
   - 建議順序：主題 3–4 → 5–7 → 8 → 9 → 10–12 → 13 → 14 → 1–2、15。
3. **04 練習題**：先遮住解答自己做，再對照。
4. **05 常見錯誤**：每做完一個章節就對照一次，把自己犯過的錯標出來。
5. **06 期末考**：先不看解析，限時 2 小時寫完，再對答案。
6. **07 策略**：考前一週看。
7. **08 / 09 / 10**：考前把內容**手寫**到 A4 參考紙上。

## 重要注意

- **參考紙必須手寫。** 期末考原卷規定只能帶「ONE DOUBLE-SIDED A4 REFERENCE SHEET WITH TEXTS HANDWRITTEN ON THE A4 PAPER」。Canva 印出來的版本只能當抄寫底稿，不能帶進考場。
- **期末考 Q2 的詳解檔有誤。** 詳解檔漏看了原卷的 $x\ge0$。本文件依原卷重解：該點有 4 條 active 約束，屬於退化情形，要檢查 6 組。結論與詳解檔相同，但過程不同，詳見 06。
- **T10 Q2、Q4 的最優值。** PDF 文字層把分數抽錯了，正確值是 $\tfrac\varepsilon3+\tfrac{13}4$ 與 $1+\tfrac\varepsilon2$，已用 Python 驗證，詳見 04。
- **L10 講義缺漏。** 依使用者指示不處理；sensitivity 中講義沒有涵蓋的部分，以 Tutorial 10 為準。

## 標記說明

| 標記 | 意義 |
|---|---|
| 〔講義〕 | 老師投影片的內容 |
| 〔手寫〕 | 課堂手寫筆記 |
| 〔原解〕 | 老師詳解的內容 |
| 〔補充〕 | 整理者自己的解釋、推導、驗證或延伸 |
| 〔事實〕 | 可以從教材或原卷直接確認的內容 |
| 〔建議〕 | 根據去年考題推出的準備建議，不是對今年考題的預測 |

## 驗證方式

所有數值答案都用 Python 驗證過：
- scipy `linprog`：檢查最優值與可行性。
- `fractions` / sympy：精確重算 tableau、$B^{-1}$、基本解。
- 自寫的 edge 列舉程式：檢查 improving edges。
