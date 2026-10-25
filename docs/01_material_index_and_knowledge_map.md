# 第一階段：教材盤點與課程知識地圖

課程：MH6503 Mathematical Programming and Optimisation（NTU MSc Modelling and Simulation，講師 Ng Keng Meng）
盤點日期：2026-10-25
盤點範圍：`After/`（10 份）、`Tutorial/`（10 份）、`MH6503_2025_26_Full_Solutions.pdf`（1 份），共 21 份 PDF。

> 標記說明：〔講義〕＝老師正式投影片；〔手寫〕＝投影片上的課堂手寫筆記；〔補充〕＝本文件的整理或推論，非老師原文。

---

## 1. 教材索引

### A. 上課講義（After）

檔名中的編號與講次**不一致**，下表以實際講次排序。

| 檔名 | 實際講次與標題 | 頁數 | 含手寫頁數 | 主要內容 |
|---|---|---|---|---|
| After 2.pdf | L1 Foundations of Optimization Models | 70 | 28 | OR 歷史與六階段、模型三要素、可行/不可行/無界、LP 四假設、Diet / 放射治療 / 排班建模、圖解法、三種特殊情況 |
| After 1.pdf | L2 The Geometry of the Simplex Method | 72 | 30 | CPF 解、active constraint、defining equations、edge、improving edge、adjacent CPF、無界邊 |
| After 3.pdf | L3 From Geometry to Algebra | 63 | 37 | SIF / SEF、augmented form、basis、BFS、feasible basis、CPF⇔BFS 定理、adjacent bases、由 BFS 寫出 edge |
| After 4.pdf | L4 Assembling the Simplex Method | 81 | 38 | reduced cost、entering variable、optimality test（含證明）、minimum ratio test、unboundedness 判定（含證明）、代數 simplex 五步驟、ERO |
| After 5.pdf | L5 The Simplex Method in Tabular Form | 51 | 26 | tableau、feasible/optimal tableau、pivot 公式、三種 tie-breaking rule、degeneracy、cycling（Beale 例）、Bland's rule、有限終止定理 |
| After 6.pdf | L6 The Two-Phase Simplex Method | 59 | 26 | 轉 SEF（slack / surplus / free 變數拆分）、artificial variable 三規則、Phase 1 判斷不可行、殘留 artificial 的移除、Phase 2、Fundamental Theorem of LP |
| After 7.pdf | L7 The Simplex Method in Matrix Notation | 53 | 26 | $B, N, c_B, c_N$、$y=c_B^TB^{-1}$、$\bar c_{N_j}=c_{N_j}-ya_{N_j}$、$d=B^{-1}a_{N_k}$、$B^{-1}$ 更新、Revised Simplex Method |
| After 8.pdf | L8 Duality in Linear Programming | 79 | 15（集中在 p17–39） | Two-phase revised simplex、代數最優性證明、Weak Duality（證明）、寫 dual 六規則、C.S. Lemma、Complementary basic solution (I)(II)、Strong Duality、PERT/CPM |
| After 9.pdf | L8 第二次上課（L8 投影片 p34–79 的重複） | 46 | 24 | 與 After 8 第 34–79 頁文字完全相同；手寫筆記不同（經逐頁比對，27 頁有差異）。重點在 C.S. Lemma 證明、complementary basis、Strong Duality 證明、PERT |
| After 10.pdf | L9 Duality Theory, Continued, and Sensitivity Analysis | 50 | 20 | C.S. Theorem 與三步檢驗法、一般形式 LP 的 dual、Primal-Dual Relation Theorem、可行性判準（Farkas 型）、Sensitivity：非基本變數目標係數範圍、Leopard Airlines 案例 |

### B. 練習題與詳解（Tutorial）

| 檔名 | 對應講次 | 頁數 | 題數 | 有無詳解 | 題型 |
|---|---|---|---|---|---|
| Tutorial_1_Solutions | L1 | 9 | 14 | 有 | 建模（Q1–3）、可行性判斷（Q4–5）、unbounded 觀念（Q6）、LP 假設（Q7）、圖解法與特殊情況（Q8–14） |
| Tutorial_2_Solutions | L2 | 6 | 8 | 有 | CPF 判斷（Q1, Q7）、improving edges（Q2, Q4a, Q5a, Q6, Q8）、edge 終點 adjacent CPF（Q3, Q4b, Q5b）、degenerate corner（Q5） |
| Tutorial_3_Solutions | L3 | 6 | 8 | 有 | 用 ERO 寫 edge（Q1–2）、basis / BFS / adjacent（Q3, Q7）、CPF⇔BFS（Q4–5）、無界 edge（Q6）、基本解與幾何對應（Q8） |
| Tutorial_4_Solutions | L4 | 3 | 4 | 有 | reduced cost 與 improving edge（Q1）、degenerate pivot（Q2）、optimality 證明（Q3）、unboundedness 證明（Q4） |
| **Tutorial_5.pdf** | L5 | 2 | 4 | **無（只有題目）** | tableau simplex（Q1–2）、三種 tie-breaking rule（Q3）、degeneracy（Q4） |
| Tutorial_6_Solutions | L6 | 7 | 5 | 有 | 建 artificial problem（Q1）、Phase 1 判不可行（Q2）、殘留 artificial（Q3）、完整 two-phase（Q4）、定理證明（Q5） |
| Tutorial_7_Solutions | L7 | 5 | 5 | 有 | revised simplex（Q1, Q2, Q4）、$[B\mid I]$ 求 $B^{-1}$（Q3）、$B^{-1}$ 更新原理與效率（Q5） |
| Tutorial_8_Solutions | L8 | 6 | 7 | 有 | 寫 dual 與 C.S.（Q1）、weak duality 證明（Q2）、complementary basis（Q3, Q5）、C.S. 恆等式（Q4）、矩陣證明（Q6）、diet 對偶與 shadow price 解釋（Q7） |
| Tutorial_9_Solutions | L9 | 7 | 8 | 有 | C.S. 檢驗最優（Q1, Q4）、一般形式 dual（Q2, Q5）、非基本係數範圍（Q3, Q8）、Primal-Dual 狀態（Q6）、Farkas（Q7） |
| Tutorial_10_Solutions | **超出 L9 投影片** | 16 | 10 | 有 | 非基本 / 基本 $c$ 的範圍與超出後重新最佳化（Q1–4）、RHS $b$ 範圍（Q5, Q7）、新增變數（Q6, Q8）、shadow price（Q7, Q10）、證明（Q9）、綜合應用（Q10） |

### C. 考古題

| 檔名 | 頁數 | 題數與配分 | 有無詳解 | 備註 |
|---|---|---|---|---|
| MH6503_2025_26_Full_Solutions.pdf | 18 | Q1–Q4，各 25 分，共 100 分 | 有（排版詳解） | **檔案標題寫的是「2025/26 Trimester 1 – Midterm Test」**，不是期末考 |

### D. 閱讀狀態

| 項目 | 狀態 |
|---|---|
| 21 份 PDF 文字層 | 全部讀完 |
| 講義中以圖片呈現的公式與表格（文字層抽不到） | 已渲染成圖逐頁檢查 |
| 手寫筆記 | 以顏色偵測找出 270 頁含手寫的頁面，全部渲染檢視。After 3 Part 4–5 與 After 4 少數頁只抽查，未逐字轉錄 |
| After 8 與 After 9 的關係 | 文字比對：After 9 = After 8 的 p34–79；像素比對：27 頁手寫不同 |

---

## 2. 課程知識地圖

整門課只有一條主線：**Linear Programming**，從幾何走到代數、矩陣，再到對偶與敏感度分析。教材沒有 Integer Programming、Network Optimization、Dynamic Programming 或隨機模型。

```
L1 建模 + 圖解
   └─► L2 幾何 simplex（CPF / edge）
          └─► L3 代數化（SEF / basis / BFS）
                 └─► L4 代數 simplex（reduced cost / ratio test）
                        └─► L5 tableau（tie-breaking / Bland）
                               ├─► L6 two-phase（artificial / Fundamental Thm）
                               └─► L7 revised simplex（B⁻¹）
                                      └─► L8 duality（weak / C.S. / strong / PERT）
                                             └─► L9 C.S. Theorem / general dual / sensitivity
                                                    └─► Tutorial 10：完整 sensitivity（投影片缺）
```

| # | 主題（英文） | 核心概念 | 關鍵定義與公式 | 講義 | 練習題 | 先備 | 考古題 |
|---|---|---|---|---|---|---|---|
| T1 | 建模 (Model Formulation) | decision variables、objective、constraints；LP 四假設 | 一般模型 $\max/\min f(x)$ s.t. $g_i(x)\le0,\ h_j(x)=0,\ x\in S$；假設：proportionality、additivity、divisibility、certainty | L1 Part 2–4 | T1 Q1–7 | 無 | 未出 |
| T2 | 圖解法與模型狀態 (Graphical Method) | 可行區域、等值線、三種狀態 | infeasible / unbounded / multiple optima；bounded LP 的最優解必有一個在 CPF | L1 Part 5 | T1 Q8–14 | T1 | 未出 |
| T3 | CPF 解 (Corner-Point Feasible Solution) | $n$ 條 active constraint 唯一交點且可行 | 判斷三步：可行 → 找 active → active 方程組有唯一解；active 多於 $n$ 條為 degenerate | L2 Part 3 | T2 Q1, Q7；T3 Q4–5 | 線代 | Q2（隱含） |
| T4 | Edge、Improving edge、Adjacent CPF | $n-1$ 條邊界交出的可行線段 | 參數化 edge → 用剩下的 active 約束定方向 → 代入 $Z$ 看斜率 → 第一個碰到的 inactive 邊界就是相鄰 CPF；沒有邊界擋住則為無界射線 | L2 Part 4–6 | T2 Q2–6, Q8 | T3 | **Q2（25 分）** |
| T5 | SEF、Augmented form、BFS | active ⇔ 變數為 0 | SEF：$\max c^Tx$ s.t. $Ax=b,\ x\ge0$；slack $s=b-a^Tx$；CPF ⇔ augmented solution 是 BFS；adjacent bases 只差一個變數 | L3 | T3 | T3–T4 | 間接 |
| T6 | 代數 Simplex (Reduced cost, Ratio test) | 把 $z$ 和基本變數都寫成非基本變數的函數 | $z=\bar v+\sum_j \bar c_{N_j}x_{N_j}$；max 問題 $\bar c_{N_j}>0$ 為 improving；全部 $\le0$ 即最優（逆命題不成立）；MRT $t=\min\{\bar b_{B_i}/\bar a_{B_i,N_k}:\bar a_{B_i,N_k}>0\}$；沒有正係數即 unbounded | L4 | T4 | T5 | 間接 |
| T7 | Tableau Simplex、tie-breaking、cycling | z-row 存的是 $-\bar c$ | max：z-row 有負數就繼續，全 $\ge0$ 最優；min：反過來。Pivot：pivot row $\div$ pivot，其他列減倍數。三種規則：largest coefficient、smallest subscript、largest improvement（$\Delta z=\bar c_{N_k}\cdot t$）。Bland's rule：進出都用最小下標，保證不 cycle | L5 | T5（無解）；T6 | T6 | Q3、Q4 使用 |
| T8 | Two-Phase Simplex | 用 artificial 找起始可行基底 | 轉 SEF：$\le$ 加 slack，$\ge$ 減 surplus，free 變數 $x=x^+-x^-$；artificial 三規則；Phase 1 $\min\sum w$，最優值 $>0$ 即原問題不可行；殘留 $w=0$ 在基底中要找該列非零係數 pivot 出去；Fundamental Theorem | L6；L8 Part 1 | T6 | T7 | **Q3（25 分）** |
| T9 | Revised Simplex | 只維護 $B^{-1}$ | $x_B^*=B^{-1}b$；$y=c_B^TB^{-1}$；$\bar c_{N_j}=c_{N_j}-ya_{N_j}$；$d=B^{-1}a_{N_k}$；$t=\min\{x^*_{B_i}/d_{B_i}:d_{B_i}>0\}$；更新 $x_{B_i}\leftarrow x^*_{B_i}-d_{B_i}t$；$B^{-1}$ 用列運算把 $d$ 變成 $e_r$；欄位置不交換 | L7；L8 Part 1 | T7 | T7 | **Q4（25 分）** |
| T10 | Weak Duality 與 Dual LP | 用約束的非負組合替目標設上界 | SIF 的 dual：$\min b^Ty$ s.t. $A^Ty\ge c,\ y\ge0$；Weak Duality $c^T\bar x\le b^T\bar y$（五步證明）；六條寫 dual 規則 | L8 Part 2–3 | T8 Q1–2 | T6 | **Q1(a)(i)(ii)** |
| T11 | Complementary Slackness | 主問題 slack × 對偶變數 = 0；主變數 × 對偶 slack = 0 | 恆等式 $b^T\bar y-c^T\bar x=\sum_i\bar y_i\bar s_i+\sum_j\bar v_j\bar x_j$；C.S. 定理三步：主可行 → 用 C.S. 解 $y^*$ → 檢查對偶可行 | L8 Part 4；L9 Part 1 | T8 Q4；T9 Q1, Q4 | T10 | **Q1(a)(iii)(iv)、Q1(b)** |
| T12 | Complementary Basic Solution、Strong Duality | 每個主基底對應一個對偶基底 | $K_N$＝配對主問題非基本變數的對偶變數；$y^{*T}=c_B^TB^{-1}$；$\bar c_j=-v_j$、$\bar c_{s_i}=-y_i$；主最優 ⇔ 對偶可行；Strong Duality | L8 Part 5–7 | T8 Q3, Q5, Q6 | T9, T11 | 未直接出 |
| T13 | 一般形式的 Dual、Primal-Dual Relation | 任意 $\le,\ge,=$ 與變數符號 | max 問題：$\le\to y\ge0$，$\ge\to y\le0$，$=\to y$ free；$x\ge0\to\ \ge$，$x\le0\to\ \le$，$x$ free $\to =$（min 問題反過來）；狀態相容表；Farkas 型可行性判準 | L9 Part 2 | T9 Q2, Q5, Q6, Q7 | T10 | 未出 |
| T14 | Sensitivity Analysis | 最優基底在參數變動下多久仍最優 | 非基本 $c_{N_k}$：$c_{N_k}\le c_{N_k}-\bar c_{N_k}$；基本 $c_{B_r}$：$y$ 改變，所有 $\bar c$ 都要重算；$b$：$x_B^*+B^{-1}\Delta b\ge0$，$\Delta z=y^T\Delta b$；新增變數：$\bar c_0=c_0-ya_0$；shadow price $=y$ | L9 Part 3（僅非基本 $c$） | T9 Q3, Q8；**T10 全部** | T9, T12 | 未出 |
| T15 | 應用：PERT/CPM、Leopard Airlines | dual 的經濟意義 | PERT 的 dual 是最長路徑；shadow price 用於定價 | L8 Part 8；L9 Part 3 | T8 Q7；T10 Q10 | T10–T14 | 未出 |

---

## 3. 章節與題型對照表

| 題型 | 辨識特徵 | 方法 | 練習題 | 考古題 |
|---|---|---|---|---|
| 文字題建模 | 情境敘述，要求定義變數、目標、約束 | 四步建模 | T1 Q1–3；T7 Q4(a)；T8 Q7(a)；T10 Q10 | — |
| 判斷可行 / 計算目標值 | 給一組點 | 逐條代入 | T1 Q4–5 | — |
| 二維 LP 圖解 | 兩個變數 | 畫區域、比較頂點 | T1 Q8–14 | — |
| 判斷是否為 CPF | 給點與不等式組 | 可行 → active → 唯一解 | T2 Q1, Q7；T3 Q4(a), Q5(a) | — |
| 找 improving edges / 相鄰 CPF | 給 CPF，問 edges | 兩兩取 active 約束參數化 | T2 Q2–6, Q8 | **Q2** |
| 判斷 basis / BFS / adjacent | 給方程組與變數集合 | 解子系統 | T3 Q3, Q5, Q7, Q8 | — |
| 由基底寫 edges | 給方程組與基底 | ERO 解出基本變數 | T3 Q1–2, Q6 | — |
| 代數 simplex 一步或多步 | 給 SEF 與起始基底 | reduced cost → MRT → pivot | T4 Q1–2 | — |
| 證明最優 / 證明無界 | 要求「證明」 | $\bar z\le\bar v$；構造序列 $\bar x(l)$ | T4 Q3(c), Q4(c)；T5 Q2 | — |
| Tableau simplex | 給 SEF 與基底 | 表格 pivot | T5 Q1–2, Q4；T6 | Q3 |
| Tie-breaking 規則 | 給 tableau 問進出變數 | 三規則 + Bland | T5 Q3 | Q4（Bland） |
| Two-phase | 有 $\ge$、$=$ 或負 RHS | artificial → Phase 1 → 清除 → Phase 2 | T6 Q1–5 | **Q3** |
| Revised simplex | 題目要求 revised 或給 $B^{-1}$ | $y$、$\bar c$、$d$、$t$、更新 $B^{-1}$ | T7 Q1–4；T10 Q2, Q4, Q8, Q10 | **Q4** |
| 寫 dual（SIF） | max、$\le$、$x\ge0$ | 六規則 | T8 Q1, Q3, Q5 | **Q1(a)(i)** |
| 寫 dual（一般形式） | 混合約束或變數符號 | 對應規則表 | T9 Q2, Q5 | — |
| 證明 weak duality | 要求代數證明 | 先用對偶可行、再用主問題可行 | T8 Q2 | **Q1(a)(ii)** |
| 寫 C.S. 條件 | 要求列出 | slack × 變數 | T8 Q1(b) | **Q1(a)(iii)** |
| 用 C.S. 檢驗是否最優 | 給 $x^*$ | 三步檢驗 | T9 Q1, Q4 | **Q1(a)(iv)** |
| 參數條件使 $x^*$ 最優 | 目標係數是符號 | C.S. 解出 $y(c)$ 再要求對偶可行 | — | **Q1(b)** |
| Complementary basis | 給主基底 | 配對並解對偶子系統 | T8 Q3, Q5 | — |
| Primal-dual 狀態 | 問 optimal / infeasible / unbounded | 相容表 | T9 Q6；T8 Q2(c) | — |
| Farkas 證書 | $Ax=b, x\ge0$ 無解 | 找 $y$ 使 $A^Ty\ge0,\ b^Ty<0$ | T9 Q7 | — |
| 敏感度：$c$ 範圍 | 給最優基底資料 | 非基本只算一個 $\bar c$；基本需重算 $y$ | T9 Q3, Q8；T10 Q1, Q3, Q10(b) | — |
| 敏感度：$b$ 範圍 | 改 RHS | $B^{-1}b\ge0$ | T10 Q5, Q7, Q10(c) | — |
| 新增變數 | 給新欄 $a_0$ | $\bar c_0=c_0-ya_0$ | T10 Q6, Q8, Q10(d) | — |
| 超出範圍後重新最佳化 | 「just outside the range」 | 從原基底續跑 revised simplex | T10 Q2, Q4, Q8(b), Q10(d) | — |

---

## 4. 重複、互補與差異

### 重複
- After 9 是 After 8 第 34–79 頁的重複（同一份投影片，第二次上課的手寫）。兩份要合讀：After 8 的手寫多在 Part 2–4（代數最優證明、weak duality、C.S. 例題），After 9 的手寫多在 C.S. Lemma 證明、complementary basis、Strong Duality、PERT。
- Tutorial 9 Q3 與 Tutorial 10 Q1 是同一題（同一組 $A,b,c,B^{-1}$）。
- Wyndor 例題貫穿 L1–L7：二維版最優解 $(2,6)$、$Z=36$；三維版（加天窗）最優解 $(2,6,0)$、$Z=36$。

### 互補
- 手寫補充的重點（〔手寫〕）：
  - L4 p14：max 問題 improving ⇔ $\bar c_{N_j}>0$；min 問題 improving ⇔ $\bar c_{N_j}<0$。
  - L4 p19：最優測試的逆命題不成立，但若 BFS 是最優的，一定存在某個基底使所有 reduced cost $\le 0$。
  - L4 p22：min 問題的 optimal basis 條件是「可行，且所有 reduced cost $\ge 0$」。
  - L5 p9：min 問題 optimal tableau 為 z-row 全 $\le0$；max 問題為全 $\ge0$。
  - L5 p36–37：largest improvement 的計算為 $\Delta z=\bar c_{N_k}\times t$。
  - L5 p42、p47：degenerate pivot 的原因是 $t=\bar b_{B_r}/\bar a_{B_r,N_k}=0$，因此 $\Delta z=t\cdot\bar c_{N_k}=0$。
  - L6 p12–14：若原問題為 SIF 且 $b\ge0$，slack 本身就是可行基底；artificial 的目的是讓每條約束都有一個「係數與 RHS 同號」的 slack 型變數。
  - L6 p19：建 artificial problem 時先把 slack/artificial 的係數縮放成 $+1$。
  - L7 p22–24：$d$ 就是 tableau 中 entering 欄，$x_B^*$ 就是 RHS 欄。
  - L9 p17–21：一般形式 dual 的推導方式：$\ge$ 乘 $-1$、$=$ 拆成兩個不等式、free 拆 $x^+-x^-$、$x\le0$ 代換 $x'=-x$。
  - L9 p47：非基本係數範圍寫成 $c_{N_k}+\Delta\le c_{N_k}-\bar c^{\,old}_{N_k}$。
- Tutorial 10 補了 L9 投影片沒有的內容：基本變數目標係數範圍、RHS 範圍、新增變數、shadow price 的有效範圍、同時變動多個 $b_i$ 不能直接套單一範圍。

### 差異（記號或用詞不一致）

| 項目 | 差異 | 處理建議〔補充〕 |
|---|---|---|
| 三維 Wyndor 的第三個變數 | L2 寫 $x_T$，L3 之後寫 $x_L$ | 同一個變數 |
| $\ge$ 約束的新增變數 | L6 摘要與 T6 稱「slack（減去）」；L6 正文與考古題 Q3 稱 surplus | 考試寫 surplus 較清楚 |
| Tableau 是否列 $z$ 欄 | 講義與 T6 有 $z$ 欄；考古題詳解省略 $z$ 欄 | 兩者都可，與考卷要求一致即可 |
| min 問題的進入規則 | L6：z-row 正數進入；L8 revised：reduced cost 為負進入 | 同一件事的兩種表述（z-row 存 $-\bar c$） |
| L4 p34 手寫 | 寫「Note: this corresponds to the CPF origin」 | 指 $J_B=\{s_1,s_2,s_3\}$ 對應原點 |
| L5 投影片結尾 | 預告「Next lecture: Sensitivity Analysis」，但 L6 實際是 two-phase；L6、L7 也有同樣的預告 | 投影片預告不可靠，以實際講次為準 |

---

## 5. 未辨識清楚或缺漏的資訊

1. **考古題不是期末考**：檔案每頁標題為「2025/26 Trimester 1 – Midterm Test」，內容只到 L8–L9 的對偶與 C.S.，沒有 sensitivity analysis。需要確認：是否另有真正的期末考考古題？
2. **Tutorial 5 沒有詳解**：只有題目（`MH6503_Tutorial_5.pdf`）。之後練習時我會自行求解並用 Python 驗證，標為〔補充〕。
3. **L10 投影片可能缺漏**：Tutorial 10 涵蓋基本係數、RHS、新增變數的 sensitivity；L9 投影片 Part 3 明說「Other kinds of changes are covered in the next section」，但資料夾沒有這一份。需要確認是否有第 10 講講義。
4. **手寫內容**：絕大部分可辨識，以重述投影片為主。少數字跡潦草處（例如 L4 p21 上方被塗掉的字、L4 p69 的「~~leaving~~ entering」更正）不影響理解。After 3 Part 4–5 與 After 4 少數頁未逐字轉錄。
5. **考古題 Q2 附註**：題目寫「(3) 的 RHS 由 −6 改為 −5（As on the supplied paper）」，且沒有非負限制；詳解特別指出這點，作答時不能自動加上 $x\ge0$。

---

## 6. 建議複習順序

依照依賴關係與考試權重排列：

| 順序 | 主題 | 理由 |
|---|---|---|
| 1 | T3–T4 CPF、Edge、Improving edge | 考古題 Q2（25 分）；也是後面所有代數方法的幾何基礎 |
| 2 | T5–T6 SEF、BFS、Reduced cost、MRT | 理解 simplex 每一步為什麼成立 |
| 3 | T7 Tableau 與 Bland's rule | Q3、Q4 都用到 |
| 4 | T8 Two-Phase | 考古題 Q3（25 分） |
| 5 | T9 Revised Simplex | 考古題 Q4（25 分）；也是 sensitivity 的計算工具 |
| 6 | T10–T11 Dual、Weak Duality、C.S. | 考古題 Q1（25 分） |
| 7 | T12–T13 Strong Duality、一般形式 dual、狀態表 | 期末可能出的證明與 dual 題 |
| 8 | T14 Sensitivity | 期末考很可能出（Tutorial 10 篇幅最大），但考古題沒有 |
| 9 | T1–T2、T15 建模、圖解、應用 | 難度低，最後快速複習 |
