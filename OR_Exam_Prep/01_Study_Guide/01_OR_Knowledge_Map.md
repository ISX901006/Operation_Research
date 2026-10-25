# 01 OR 課程知識地圖

MH6503 Mathematical Programming and Optimisation（NTU，2026/27 Trimester 1，講師 Ng Keng Meng）

**標記**
- 〔講義〕：老師的投影片原文。
- 〔手寫〕：投影片上的課堂手寫筆記。
- 〔補充〕：本文件自行整理或推論，不是老師原文。

**頁碼格式**："L4 p19" 指第 4 講、PDF 第 19 頁。各講次與檔名的對照見第 1 節。

**題號格式**："T2 Q4" 指 Tutorial 2 第 4 題；"FE Q2" 指 2025-26 期末考第 2 題。

---

## 1. 教材與講次對照

| 講次 | 檔名 | 頁數 | 標題 |
|---|---|---|---|
| L1 | After 2.pdf | 70 | Foundations of Optimization Models |
| L2 | After 1.pdf | 72 | The Geometry of the Simplex Method |
| L3 | After 3.pdf | 63 | From Geometry to Algebra（SEF、BFS） |
| L4 | After 4.pdf | 81 | Assembling the Simplex Method |
| L5 | After 5.pdf | 51 | The Simplex Method in Tabular Form |
| L6 | After 6.pdf | 59 | The Two-Phase Simplex Method |
| L7 | After 7.pdf | 53 | The Simplex Method in Matrix Notation |
| L8 | After 8.pdf | 79 | Duality in Linear Programming |
| L8' | After 9.pdf | 46 | L8 p34–79 的第二次上課（文字相同，手寫不同）。頁碼換算：After 9 p.k = L8 p.(k+33) |
| L9 | After 10.pdf | 50 | Duality Theory, Continued, and Sensitivity Analysis |

其他資料：
- Tutorial 1–10 均有詳解（T5 詳解另外補上）。
- 期末考：`Final_Exam.pdf`（原卷，2025-26 Trimester I，2 小時，4 題各 25 分）與 `MH6503_2025_26_Full_Solutions.pdf`（詳解；頁首誤標為 Midterm）。

課程範圍只有 Linear Programming，沒有 Integer Programming、Network、DP 或隨機模型。

---

## 2. 主線與依賴關係

```
L1 建模、圖解法
 └► L2 幾何 simplex：CPF、edge、improving edge、adjacent CPF
     └► L3 代數化：SEF、augmented form、basis、BFS、CPF⇔BFS
         └► L4 代數 simplex：reduced cost、optimality test、MRT、unbounded
             └► L5 tableau：pivot、tie-breaking、degeneracy、cycling、Bland
                 ├► L6 two-phase：轉 SEF、artificial、Phase 1/2、Fundamental Thm
                 └► L7 revised simplex：B⁻¹、y、d、B⁻¹ 更新
                     └► L8 duality：two-phase revised、weak duality、dual 六規則、
                         C.S. Lemma、complementary basic solution、strong duality、PERT
                         └► L9 C.S. Theorem、一般形式 dual、Primal-Dual Relation、
                             Farkas 型判準、sensitivity（非基本 c）
                             └► T10：sensitivity 完整版（基本 c、b、新變數、shadow price）
```

---

## 3. 主題總表

| # | 主題 | 核心概念 | 必背公式或判準 | 講義 | 練習題 | 期末考 |
|---|---|---|---|---|---|---|
| 1 | 建模 | 變數、目標、約束；LP 四假設 | 四步建模；proportionality、additivity、divisibility、certainty | L1 p17–47 | T1 Q1–7 | — |
| 2 | 圖解法與模型狀態 | 可行域、等值線、infeasible、unbounded、multiple optima | bounded 且可行的 LP，最優解必在 CPF 上 | L1 p49–69 | T1 Q8–14 | — |
| 3 | CPF | active constraint、defining equations、degenerate | CPF ⇔ 可行，且 active 約束組有唯一解 | L2 p16–33 | T2 Q1, Q7；T3 Q4–5 | FE Q2 |
| 4 | Edge、improving edge、adjacent CPF | 保留 $n-1$ 條 active；方向；第一個碰到的邊界 | 見 02 §4 | L2 p36–70 | T2 Q2–6, Q8 | **FE Q2** |
| 5 | SEF、BFS | slack、basis、feasible basis、adjacent basis | CPF ⇔ augmented solution 是 BFS | L3 p7–60 | T3 Q1–8 | 間接 |
| 6 | 代數 simplex | reduced cost、entering、leaving、MRT | $z=\bar v+\sum\bar c_{N_j}x_{N_j}$；$\bar c\le0$ 即最優（max） | L4 p9–79 | T4 Q1–4 | 間接 |
| 7 | Tableau、tie-breaking、cycling | z-row 存 $-\bar c$；pivot | 三種規則；Bland；有限終止定理 | L5 p6–50 | T5 Q1–4 | FE Q3、Q4 |
| 8 | Two-phase | 轉 SEF、artificial、Phase 1/2 | artificial 最優值 $>0$ ⇔ 原問題不可行 | L6 p7–58；L8 p5–13 | T6 Q1–5 | **FE Q3** |
| 9 | Revised simplex | 只更新 $B^{-1}$ | $y=c_B^TB^{-1}$，$\bar c_j=c_j-ya_j$，$d=B^{-1}a_{N_k}$ | L7 p5–52 | T7 Q1–5 | **FE Q4** |
| 10 | Weak duality、dual LP | 用約束的非負組合替目標設上界 | $c^T\bar x\le b^T\bar y$；寫 dual 的六規則 | L8 p16–33 | T8 Q1–2 | **FE Q1(a)(i)(ii)** |
| 11 | Complementary slackness | 主 slack×$y_i=0$；$x_j$×對偶 slack$=0$ | 恆等式 $b^T\bar y-c^T\bar x=\sum\bar y_i\bar s_i+\sum\bar v_j\bar x_j$；三步檢驗 | L8 p36–42；L9 p6–13 | T8 Q4；T9 Q1, Q4 | **FE Q1(a)(iii)(iv)、Q1(b)** |
| 12 | Complementary basic solution、strong duality | $K_N$；$y^T=c_B^TB^{-1}$；$\bar c_j=-v_j$ | 主問題最優 ⇔ 對偶可行；最優值相等 | L8 p45–70 | T8 Q3, Q5, Q6 | — |
| 13 | 一般形式 dual、Primal-Dual Relation、Farkas | 約束類型 ↔ 變數符號 | 對應規則表；3×3 狀態相容表 | L9 p16–30 | T9 Q2, Q5, Q6, Q7 | — |
| 14 | Sensitivity analysis | 最優基底在參數變動下的有效範圍 | 非基本 $c$ 只改一個 $\bar c$；基本 $c$ 改變 $y$；$b$ 看 $B^{-1}b\ge0$；新變數算 $\bar c_0$ | L9 p33–50 | T9 Q3, Q8；T10 Q1–10 | — |
| 15 | 應用 | PERT 的 dual 是最長路徑；shadow price 用於定價 | — | L8 p73–79；L9 p34–50 | T8 Q7；T10 Q10 | — |

---

## 4. 各主題細項

### 主題 1 建模（L1）
- **概念**
  - 模型三要素（L1 p26–28）。
  - 一般最佳化模型（L1 p20）。
  - feasible / infeasible / optimal / unbounded 的定義（L1 p31–32、p25）。
  - unbounded 與可行域是否有界無關：L1 p25 的兩個反例 $\max 1/x$、$\min x$。
- **LP 四假設**（L1 p34–36）
  - proportionality：違反例如啟動成本、規模經濟。
  - additivity：違反例如交叉項 $x_Dx_W$。
  - divisibility：違反時要改用 integer programming。
  - certainty：違反時要做 sensitivity analysis。
- **例子**
  - Wyndor：$\max 3x_D+5x_W$，最優 $(2,6)$、$Z=36$。
  - Diet：最小化熱量。
  - Radiation：最優 $(7.5,4.5)$、$Z=5.25$。
  - Personnel scheduling：$Z=30610$。
- **練習題**：T1 Q1–3 建模；Q4–5 判斷可行；Q6 unbounded 觀念；Q7 假設。

### 主題 2 圖解法（L1 p53–69）
- **方法**：兩點決定一條邊界線；用原點判斷可行的一側；移動等值線（L1 p58）。
- **三種特殊情況**（L1 p63–66）
  - infeasible：加入 $3x_D+5x_W\ge50$。
  - multiple optima：$Z=3x_D+2x_W$，與 Plant 3 邊界平行。
  - unbounded：$\min -4x_1+x_2$。
- **練習題**
  - T1 Q8 最優 $(4,4)$、20。
  - T1 Q9 multiple optima。
  - T1 Q10 unbounded。
  - T1 Q11 infeasible。
  - T1 Q12 可行域無界但有最優解。
  - T1 Q13 redundant 約束。
  - T1 Q14 可行域只有一點。

### 主題 3–4 幾何 simplex（L2）
- **三個觀察**（L2 p6–9）：最優解在角落；局部檢查 edge 即可判斷最優；unbounded 會沿著某條 edge 出現。
- **定義**
  - active（L2 p23）。
  - CPF（L2 p24）。
  - defining equations（L2 p25）。
  - edge（L2 p38）。
  - improving edge（L2 p47）。
  - adjacent CPF（L2 p56）。
- **步驟**
  - edges 三步（L2 p45）。
  - improving 三步（L2 p52）。
  - 找相鄰 CPF 五步（L2 p60、p70）。
- **退化角落**：$(0,0,2)$ 有 5 條 active（L2 p32、p44、p51、p62）。
- **無界 edge**：L2 p63–64。
- **完整範例**：L2 p65–69，$(2,0,1)$ 最優，$Z=13$。
- **練習題**：T2 全部。**FE Q2**。

### 主題 5 SEF 與 BFS（L3）
- **形式**：SIF（L3 p7）、SEF（L3 p11–12）、augmented form（L3 p13–15）、augmented solution（L3 p16–17）。
- **定理**：CPF ⇔ augmented solution 是 BFS（L3 p23–28，證明標為 optional）。
- **定義**：basis、basic coefficient matrix 可逆、BFS、feasible basis（L3 p31–35）。
- **例子**：Q1–Q4 判斷 basis（L3 p36–39）；不可行 basis（L3 p41）。
- **adjacent bases**：定義與定理（L3 p45–54）。
- **由 BFS 寫 edges**：L3 p55–59。
- **練習題**：T3 全部。

### 主題 6 代數 simplex（L4）
- **reduced cost**（L4 p9–14）
  - 〔手寫 L4 p14〕max 問題 improving ⇔ $\bar c>0$；min 問題 improving ⇔ $\bar c<0$。
- **optimality test 與證明**（L4 p19–21）
  - 〔手寫 L4 p19〕逆命題不成立；但只要 BFS 最優，必存在某個基底使所有 $\bar c\le0$。
- **optimal basis**（L4 p22）
  - 〔手寫〕min 問題的條件是可行且所有 $\bar c\ge0$。
- **例子**：同一系統、兩個目標（L4 p23–27）。
- **leaving variable、MRT**：L4 p30–35。
- **unbounded 判定與證明**：L4 p38–43。
- **五步演算法**：L4 p46–51。
- **Wyndor 三次迭代**：L4 p54–62。
- **ERO 與較難的例子**：L4 p69–77。
- **練習題**：T4 全部。

### 主題 7 Tableau（L5）
- **tableau 結構**（L5 p6–9）：z-row 存 $-\bar c$。
- **feasible / optimal tableau**（L5 p9、p11–12）：max 問題 z-row 全 $\ge0$；min 問題全 $\le0$。
- **pivot 公式**（L5 p19）；**Wyndor 例子**（L5 p22–29）。
- **三種 tie-breaking 規則**（L5 p33–38）
  - 〔手寫 L5 p36–37〕largest improvement 的增量 $\Delta z=\bar c_{N_k}\cdot t$。
- **degeneracy 與 cycling**（L5 p41–46）：Beale 1955 的例子。
- **定理與規則**：有限終止定理（L5 p47）、Bland's rule（L5 p48）。
- **練習題**：T5 全部。

### 主題 8 Two-phase（L6、L8 Part 1）
- **轉 SEF**（L6 p7–10）：slack、surplus、free 變數拆成 $x^+-x^-$。
- **artificial**（L6 p13–18）：三條規則（L6 p14）。
- **min 問題的進入規則**（L6 p20）：z-row 正數者進入。
- **判斷不可行**（L6 p23–26）。
- **殘留 artificial**（L6 p31–39）。
- **完整流程**（L6 p42–49）：例題 Phase 2 最後發現 unbounded。
- **Fundamental Theorem**（L6 p52–54）。
- **Two-phase revised**（L8 p5–13）：殘留 $w_7$ 的處理公式見 L8 p10。
- **練習題**：T6 全部。**FE Q3**。

### 主題 9 Revised simplex（L7）
- **矩陣表示**（L7 p5–10）。
- **reduced cost 公式**（L7 p13–14）；**$[B\mid I]$ 求逆**（L7 p16–17）。
- **ratio test 用 $d$**（L7 p22–26）。
  - 〔手寫 L7 p22–24〕$d$ 就是 tableau 的 entering 欄，$x_B^*$ 就是 RHS 欄。
- **$B^{-1}$ 更新**（L7 p29–32）；**BFS 更新**（L7 p35–36）。
- **演算法總結**（L7 p40–45）：「Do NOT exchange column positions」（L7 p43）。
- **完整例子**（L7 p46–49）。
- **練習題**：T7 全部。**FE Q4**。

### 主題 10–12 Duality（L8）
- **代數最優證明**（L8 p16–21）。
- **weak duality 與證明**（L8 p25–27）。
- **dual LP**：定義（L8 p29）、六規則（L8 p30）。
- **C.S. Lemma 與證明**（L8 p36–42；L8' p3–9 有不同的手寫）。
- **complementary basic solution (I)**（L8 p45–55）、**(II)**（L8 p58–63）。
- **strong duality**（L8 p66–70）。
- **PERT**（L8 p73–79）：關鍵路徑 DIG→FOUND→WALLS→RAFTERS→ROOF→FINISH，27 天。
- **練習題**：T8 全部。**FE Q1(a)**。

### 主題 11、13、14（L9）
- **C.S. Theorem 與三步檢驗**（L9 p6–13）：例題 $x^*=(2,1,0)$。
- **一般形式 dual**（L9 p16–22）；**Primal-Dual Relation Theorem**（L9 p23–26）；**Farkas 型判準**（L9 p27–30）。
- **Sensitivity**（L9 p33–50）
  - Leopard Airlines 例子。
  - 非基本 $c$ 的範圍：$c_{N_k}\in(-\infty,\,c_{N_k}-\bar c_{N_k}]$（L9 p47）。
  - 新產品的損益平衡價 $p_9>2100$（L9 p48–49）。
- **練習題**：T9 全部、T10 全部。**FE Q1(a)(iv)、Q1(b)**。

---

## 5. 題型與教材對照

| 題型 | 方法 | 練習題 | 期末考 |
|---|---|---|---|
| 文字題建模 | 四步建模 | T1 Q1–3；T7 Q4(a)；T8 Q7(a)；T10 Q10 | — |
| 判斷可行、計算目標值 | 逐條代入 | T1 Q4–5 | — |
| 二維圖解 | 畫圖、比較頂點 | T1 Q8–14 | — |
| 判斷 CPF | 可行 → active → 唯一解 | T2 Q1, Q7；T3 Q4(a), Q5(a) | — |
| improving edges／相鄰 CPF | 兩兩保留 active 約束並參數化 | T2 Q2–6, Q8 | **Q2** |
| 判斷 basis、BFS、adjacent | 解子系統 | T3 Q3, Q5, Q7, Q8 | — |
| 由 BFS 寫 edges | 用 ERO 解出基本變數 | T3 Q1, Q2, Q6 | — |
| 代數 simplex | reduced cost → MRT → pivot | T4 Q1–2 | — |
| 證明最優、證明無界 | $\bar z\le\bar v$；構造序列 $\bar x(l)$ | T4 Q3(c), Q4(c)；T5 Q1–2 | — |
| Tableau simplex | 表格 pivot | T5 Q1, Q2, Q4 | Q3 |
| tie-breaking | 三種規則與 Bland | T5 Q3 | Q4 |
| Two-phase | artificial → Phase 1 → 清除殘留 → Phase 2 | T6 Q1–5 | **Q3** |
| Revised simplex | $y$、$\bar c$、$d$、$t$、$B^{-1}$ | T7 Q1–4；T10 Q2, Q4, Q8, Q10 | **Q4** |
| 寫 dual（SIF） | 六規則 | T8 Q1, Q3, Q5 | **Q1(a)(i)** |
| 寫 dual（一般形式） | 對應規則表 | T9 Q2, Q5 | — |
| 證明 weak duality | 先用對偶可行、再用主可行 | T8 Q2 | **Q1(a)(ii)** |
| 寫 C.S. 條件 | slack × 變數 = 0 | T8 Q1(b) | **Q1(a)(iii)** |
| 用 C.S. 檢驗是否最優 | 三步檢驗 | T9 Q1, Q4 | **Q1(a)(iv)** |
| 參數化目標使給定解最優 | 用 C.S. 解出 $y(c)$，再要求對偶可行 | — | **Q1(b)** |
| Complementary basis | 配對變數、解子系統 | T8 Q3, Q5, Q6 | — |
| Primal-dual 狀態判斷 | 相容表 | T9 Q6；T8 Q2(c) | — |
| Farkas 證書 | 找 $y$ 使 $A^Ty\ge0$、$b^Ty<0$ | T9 Q7 | — |
| Sensitivity：$c$ | 非基本 / 基本兩種情況 | T9 Q3, Q8；T10 Q1, Q3, Q10(b) | — |
| Sensitivity：$b$ | $x_B^*+B^{-1}\Delta b\ge0$ | T10 Q5, Q7, Q9, Q10(c) | — |
| 新增變數 | $\bar c_0=c_0-ya_0$ | T10 Q6, Q8, Q10(d) | — |
| 超出範圍後重新最佳化 | 從原基底續跑 revised simplex | T10 Q2, Q4, Q8(b), Q10(d) | — |

---

## 6. 期末考（2025-26）考點分布

| 題 | 分數 | 主題 | 對應講義 | 最相近的練習題 |
|---|---|---|---|---|
| Q1(a)(i) | — | 寫 dual（SIF） | L8 p29–30 | T8 Q1(a) |
| Q1(a)(ii) | — | weak duality 證明 | L8 p25–27 | T8 Q2(a) |
| Q1(a)(iii) | — | C.S. 條件 | L8 p39 | T8 Q1(b) |
| Q1(a)(iv) | — | C.S. 檢驗是否最優 | L9 p9–13 | T9 Q1, Q4 |
| Q1(b) | — | 參數化目標的 C.S. | L9 p9 | 無直接對應（新題型） |
| Q2 | 25 | improving edges（退化 CPF） | L2 p36–52 | T2 Q5 |
| Q3 | 25 | two-phase tabular | L6 | T6 Q3, Q4 |
| Q4 | 25 | revised simplex 搭配 Bland | L7 | T7 Q2, Q4 |

Q1 共 25 分，但原卷沒有列出各子題的分數。

去年沒有考的：建模、圖解法、basis 判斷、cycling、一般形式 dual、Primal-Dual 狀態、Farkas、sensitivity、PERT。

---

## 7. 教材之間的差異

| 項目 | 差異 | 處理 |
|---|---|---|
| 三維 Wyndor 的第三個變數 | L2 寫 $x_T$，L3 以後寫 $x_L$ | 同一個變數 |
| $\ge$ 約束新增的變數 | L6 p27 與 T6 稱為「減去的 slack」；L6 p8、p55 與 FE Q3 詳解稱為 surplus | 考試寫 surplus 比較清楚 |
| min 問題的進入條件 | tableau 寫「z-row 正數進入」（L6 p20）；revised 寫「$\bar c<0$ 進入」（L8 p6） | 同一件事，因為 z-row 存的是 $-\bar c$ |
| Tableau 是否列 $z$ 欄 | 講義有；FE 詳解省略 | 兩種都可以 |
| FE Q2 的非負限制 | 原卷有 $x_1,x_2,x_3\ge0$；詳解檔誤以為沒有 | 以原卷為準，見 06 |
| FE Q3 Phase 1 第 3 次迭代 | 詳解選 $s_5$ 進入；若照 Bland 應選 $x_3$ | 題目沒指定規則，兩條路徑都對，見 06 |
| T10 Q2、Q4 最優值 | PDF 文字層把分數抽成「$3\varepsilon+\tfrac{13}{4}$」「$2\varepsilon+1$」 | 以 Python 驗算：應為 $\tfrac{\varepsilon}{3}+\tfrac{13}{4}$ 與 $\tfrac{\varepsilon}{2}+1$（文字擷取的排版問題，原 PDF 應正確） |
| L5–L7 結尾預告 | 都寫「Next lecture: Sensitivity Analysis」 | 預告不準，以實際講次為準 |
