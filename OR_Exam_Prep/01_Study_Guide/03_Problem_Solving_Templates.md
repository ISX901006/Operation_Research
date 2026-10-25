# 03 解題模板（SOP）

共 18 個模板。每個模板依序寫：辨識特徵 → 方法判斷 → 要確認的條件 → 步驟 → 公式 → 中間表格 → 停止條件與驗證 → 常見失分 → 考卷寫法。

題號來源：T = Tutorial，FE = 2025-26 期末考，L = 講義。

---

## 速查：看到題目先問自己

| 題目關鍵 | 用哪個模板 |
|---|---|
| 文字敘述、要求 formulate | S1 |
| 兩個變數、要求圖解 | S2 |
| 給一個點，問是否為 CPF | S3 |
| 給 CPF，問 (improving) edges 或相鄰 CPF | S4 |
| 給方程組與變數集合，問 basis / BFS / adjacent | S5 |
| 給 SEF 與 feasible basis，用代數或 tableau 解 | S6、S7 |
| 給 tableau，問三種規則或 Bland 下的進出變數 | S8 |
| 約束含 $\ge$、$=$、負 RHS，或明說 artificial / two-phase | S9 |
| 明說 revised，或給了 $B^{-1}$ | S10 |
| 寫 dual（SIF） | S11 |
| 寫 dual（一般形式：混合約束、free 或 $\le0$ 變數） | S12 |
| 證明 weak duality 或 C.S. 恆等式 | S13 |
| 給 $x^*$，問是否最優，或要「algebraic proof of optimality」 | S14 |
| 目標係數是符號，問什麼條件下 $\bar x$ 最優 | S15 |
| 給主問題基底，求 complementary basis / solution | S16 |
| 問 primal / dual 的狀態，或要求證明不可行 | S17 |
| 給最優 $J_B$、$B^{-1}$、$y$，問參數的範圍、shadow price、新變數 | S18 |

---

## S1 建模

- **辨識**：一段情境，問 decision variables、objective、constraints、complete model。
- **方法**：L1 的四步建模（L1 p33）。
- **要確認**
  - 變數的單位（每週、每批、每公斤）。
  - 約束是 $\le$、$\ge$ 還是 $=$：「至少」寫 $\ge$；「最多」寫 $\le$；「恰好」或「固定合約」寫 $=$。
  - 是否需要非負限制。
- **步驟**
  1. 「Let $x_1=$ …（單位）」。
  2. 「Objective: maximize / minimize $Z=\dots$（單位）」。
  3. 逐條寫出約束，每條後面括號註明意義。
  4. 寫出完整模型。
- **驗證**：用一個簡單的點代入，確認單位一致、方向合理。
- **常見失分**
  - 把「恰好」寫成 $\le$（T1 Q3）。
  - 漏寫非負限制。
  - 係數的行列對錯：每條約束對應一種資源，不是一種產品。
- **考卷寫法**：直接仿 T1 Q1(a)–(d) 的格式。

---

## S2 二維圖解

- **辨識**：兩個變數，要求 graphically solve，或判斷 infeasible / unbounded / multiple optima。
- **步驟**
  1. 每條約束畫邊界線（取兩個截距），代入原點判斷可行側。
  2. 標出可行域的所有頂點：解每兩條相交邊界的方程組。
  3. 列表計算每個頂點的 $Z$。
  4. 判斷狀態：

| 狀態 | 判斷依據 |
|---|---|
| 最優解唯一 | 最好的頂點只有一個 |
| multiple optima | 有兩個頂點同為最好，且它們之間的邊與等值線平行；整條邊都最優（T1 Q9） |
| unbounded | 可行域在變好的方向無界；給一條射線 $x(t)$ 並寫出 $Z(t)\to\infty$（T1 Q10） |
| infeasible | 約束互相矛盾；寫出代數理由（T1 Q11：前兩條約束下 $x+y\le4<8$） |

- **中間表格**：Corner ｜ $Z$。
- **常見失分**
  - 可行域無界就直接說 unbounded（T1 Q12 其實有最優解）。
  - 沒有指出 redundant 約束（T1 Q13）。
- **考卷寫法**：頂點表、最優解、最優值，加一句狀態說明。

---

## S3 判斷 CPF

- **辨識**：給一個點和一組不等式，問 "is it a CPF solution?"
- **步驟**
  1. 逐條代入，標註「active」或「slack」。**非負限制也要檢查**。
  2. 若有任何約束不成立：不可行，所以不是 CPF。
  3. 數 active 的條數 $p$，與變數個數 $n$ 比較：
     - $p<n$：不是 CPF。
     - $p\ge n$：檢查 active 方程組是否有唯一解（解出來，或看行列式）。
       - 有唯一解：是 CPF；$p>n$ 時為 degenerate。
       - 沒有唯一解：不是 CPF。
- **中間表格**：約束 ｜ 代入值 ｜ active / slack / 違反。
- **常見失分**
  - 只檢查唯一解、沒檢查可行（T2 Q7 的 $(3,3,3)$）。
  - 4 條 active 就直接說是 CPF，沒檢查它們是否相依（T2 Q1(b) 交出的是一條線）。
- **考卷寫法**：「Active constraints: … . They intersect at a unique point and $\bar x$ is feasible, hence $\bar x$ is a CPF solution.」

---

## S4 Improving edges 與相鄰 CPF（FE Q2）

- **辨識**：「Determine all (improving) edges emanating from the CPF $\bar x$」或「the CPF at the end of every edge」。
- **方法**：L2 的五步做法（L2 p60、p70）。不需要轉成 SEF。
- **要確認**
  - 題目到底有沒有寫 $x\ge0$。
  - 是 max 還是 min。
- **步驟**
  1. **列約束**：所有約束都寫成 $\le$ 型，編號 (1)(2)…；非負限制也要列。
  2. **代入 $\bar x$**：標出 active / inactive，同時確認可行。
  3. **數 active 數 $p$**：
     - $p=n$：共 $n$ 組。
     - $p>n$：共 $\binom{p}{n-1}$ 組，要準備處理重複的直線和退化 edge。
  4. **每一組**（保留 $n-1$ 條等號）：
     1. 解出直線，選一個變數當參數 $t$，其餘用 $t$ 表示。
     2. **方向**：把直線代入每一條剩下的 active 約束，得到 $t\ge t_0$ 或 $t\le t_0$。
        - 若兩條 active 約束分別給出 $t\ge t_0$ 和 $t\le t_0$：直線被夾成一點，是退化 edge，捨棄。
     3. **目標**：寫成 $Z(t)=\alpha+\beta t$，依前進方向判斷是否 improving。
     4. **端點**（題目要求時）：把直線代入所有 inactive 約束，只保留前進方向上會撞到的，取最近的一條。沒有就是 ray。
  5. **去重**：不同的組合若給出同一條線，只算一條。
  6. **結論**：列出所有 improving edges（寫參數式與範圍）。若沒有，寫「$\bar x$ is optimal」。
- **公式**：$Z(t)$ 的斜率就是 $c^Td$。
- **中間表格**

| Pair | 參數式 | 方向（來自哪條 active） | $Z(t)$ | improving？ | 擋住的約束 → 端點 |
|---|---|---|---|---|---|

- **驗證**
  - 端點要可行。
  - 端點的 active 約束應該是這組的 $n-1$ 條，加上擋住的那條。
  - 若 improving edge 是 ray，LP 就是 unbounded（T2 Q2 Pair 3、T2 Q6）。
- **常見失分**
  - 漏掉非負限制，或在題目沒寫時自己加上。
  - 退化點只檢查 $n$ 組（FE Q2 的詳解就犯了這個錯）。
  - 方向判斷錯。
  - 把斜率為 0 的 edge 算成 improving。
- **考卷寫法**：每組三行：直線、方向、$Z(t)$ 與結論。最後列出 improving edges。

---

## S5 Basis、BFS、Adjacent bases

- **辨識**：給方程組 $Ax=b$（或 SIF 轉成的 augmented form），問某組變數是否為 basis / feasible basis、某個解是否 basic、兩個 BFS 是否 adjacent。
- **步驟**
  1. **判斷 basis**：非基本變數設為 0，用 ERO 解剩下的 $m\times m$ 系統。
     - 有唯一解：是 basis。
     - 無解或無限多解：不是。也可以檢查欄是否線性相依（T3 Q7(a)）。
  2. **feasible**：解出的值全部 $\ge0$。
  3. **一個解是否 basic**：取包含所有非零分量的 $m$ 個變數，枚舉所有組合；只要有一組是 basis，它就是 basic solution。
  4. **adjacent**：兩個 basis 恰好差一個變數。
  5. **degenerate**：0 的個數多於 $n-m$。
- **常見失分**
  - 以為 adjacent 有遞移性（T3 Q3(c)）。
  - 退化的 BFS 漏算了它的其他 basis（T3 Q5）。
- **考卷寫法**：「Setting $x_\cdot=x_\cdot=0$, the system … has the unique solution … , hence {…} is a (feasible) basis.」

---

## S6 代數 simplex（L4）

- **辨識**：SEF 加一個 feasible basis，要求 reduced cost、improving edge、leaving variable，或「證明最優 / 證明 unbounded」。
- **步驟**
  1. 用 ERO 把基本變數寫成非基本變數的函數：$x_B=\bar b-\bar a\,x_N$。
  2. 代入目標：$z=\bar v+\sum\bar c_jx_{N_j}$。
  3. 判斷最優：max 問題所有 $\bar c\le0$ 即最優；min 問題相反。
  4. 選 entering：$\bar c>0$ 的變數（依題目指定的規則）。
  5. MRT：只看 $x_{B_i}$ 式中 $x_{N_k}$ 係數為負的列（即 $\bar a>0$），取 $\min\bar b/\bar a$。
     - 沒有這樣的列：LP unbounded。
  6. Pivot：用 leaving 那一列解出 entering，代入其他列和 $z$。
- **證明格式**
  - **最優**（T4 Q3(c)）：對任何可行 $\bar x$，$\bar z=\bar v+\sum\bar c_j\bar x_{N_j}\le\bar v$，因為 $\bar c_j\le0$ 且 $\bar x_{N_j}\ge0$。
  - **unbounded**（T4 Q4(c)）：定義 $\bar x(l)$，令 entering $=l$、其他非基本 $=0$，驗證每個分量 $\ge0$，並寫出 $z(l)\to\infty$。
- **常見失分**
  - 代數式與 tableau 的符號混用。
  - 退化 pivot 時，在 MRT 漏掉 $t=0$ 的那一列（T4 Q2）。

---

## S7 Tableau simplex（FE Q3 的核心）

- **步驟**
  1. **建初始 tableau**：每個基本變數的欄必須是單位向量，z-row 中基本變數的位置必須是 0。
     - 若不是，先用列運算消去（T5 Q1：先做 row2 − row3）。
  2. **進入**：max 問題選 z-row 負數；min 問題選 z-row 正數。依題目指定的規則挑選。
  3. **MRT**：只對 pivot 欄中為正的列計算 RHS / 係數。平手時依規則（Bland：選下標最小的基本變數離開）。
  4. **Pivot**：
     - pivot row 除以 pivot element。
     - 其他列（含 z-row）減去適當倍數的 pivot row，使 pivot 欄變成單位向量。
  5. **重複**，直到 z-row 達到最優條件，或 MRT 無列可選（unbounded）。
- **每次迭代寫出**：基底、entering、ratio 計算、leaving、列運算、新 tableau。
- **驗證**
  - 每個基本欄都是單位向量。
  - RHS 全部 $\ge0$。
  - 最優值要等於 $c^Tx^*$ 代入原目標算出的值。
- **unbounded 的寫法**（T5 Q1、Q2）：從最後的 tableau 寫出基本變數的式子，給出 $\bar x(k)$，並寫 $z_k\to\infty$。
- **常見失分**
  - z-row 符號搞反（存的是 $-\bar c$）。
  - pivot 時用了已經更新過的列去消其他列。
  - 退化的平手沒有依規則處理。

---

## S8 Tie-breaking 規則判斷（T5 Q3）

- **步驟**
  1. 列出所有候選 entering（max 問題：z-row 為負者），寫出各自的 $\bar c$。
  2. **Largest coefficient**：選 $\bar c$ 最大者，再做 MRT 決定 leaving。
  3. **Largest improvement**：每個候選都做 MRT 得到 $t$，計算 $\Delta z=\bar c\cdot t$，選最大者。
  4. **Bland**：entering 選下標最小的候選；leaving 在平手時選下標最小的基本變數。
- **中間表格**：候選 ｜ $\bar c$ ｜ ratio ｜ $t$ ｜ $\Delta z$。
- **常見失分**
  - 把 $\Delta z$ 算成 $\bar c\cdot$ pivot element，而不是 $\bar c\cdot t$。
  - Bland 的 leaving 比的是「變數下標」，不是列的位置（T5 Q3(c)：$x_4$ 和 $x_7$ 平手，選 $x_4$，雖然它在第 4 列）。

---

## S9 Two-phase（FE Q3）

- **辨識**：有 $\ge$ 或 $=$ 約束、負的 RHS，或題目要求 "artificial problem"。
- **步驟**
  1. **轉成 SEF**：$\le$ 加 slack；$\ge$ 減 surplus；free 變數拆成 $x^+-x^-$；$x\le0$ 代換 $x'=-x$。
  2. **逐列套三條規則**：
     - 有只出現在這一列、且係數與 RHS 同號的變數：當作 slack。
     - 否則加一個 artificial，係數 $\pm1$，與 RHS 同號。
  3. **寫出 artificial problem**：$\min W=\sum w$，含全部約束與非負限制。**這一步本身就有分數**。
  4. **初始 z-row**：
     - $W$ 列 = 所有含 artificial 的列相加（artificial 欄設為 0）。
     - RHS = 這些列的 RHS 相加。
  5. **Phase 1**：z-row 為正者進入（建議用 Bland），做 MRT 與 pivot。artificial 離開後可以刪掉它的欄。
  6. **Phase 1 結束**：
     - $W^*>0$：原 LP 不可行，結束。
     - $W^*=0$ 但仍有 artificial 在基底中：在該列找一個係數 $\ne0$ 的非基本原變數 pivot（退化 pivot，$t=0$）。
  7. **Phase 2**：刪掉 artificial 欄，用原目標重寫 z-row，並消去所有基本變數。
     - 寫法：$z=c_Bx_B+\dots$，把每個基本變數用非基本變數表示後代入。
  8. 以 max（或原問題的方向）的規則繼續 simplex，直到最優或 unbounded。
- **驗證**
  - 最優解代回原約束要成立。
  - $c^Tx^*$ 要等於 tableau 的 RHS。
- **常見失分**
  - artificial 的符號錯。
  - Phase 1 用了 max 的進入規則。
  - Phase 2 的 z-row 忘記消去基本變數。
  - 忘了 surplus 變數也是 SEF 的變數。
- **考卷寫法**：仿 FE Q3 詳解：Step 1 建 artificial problem；Phase 1 每次迭代一張 tableau；判定可行；Phase 2 的 tableau；最優解。

---

## S10 Revised simplex（FE Q4）

- **辨識**：題目明說 revised simplex，或給了 $B^{-1}$。
- **初始化**
  - 寫出 augmented form 與變數順序，列出 $A$、$b$、$c$。
  - 起始基底通常是全部 slack：$B=B^{-1}=I$，$x_B^*=b$。
- **每次迭代**
  1. $c_B$：依 $J_B$ 的順序寫出。
  2. $y=c_B^TB^{-1}$。
  3. 每個非基本變數：$\bar c_j=c_j-y\,a_j$。
     - max 問題全部 $\le0$：最優，停止。
     - 否則依規則選 entering（Bland：$\bar c>0$ 中下標最小者）。
  4. $d=B^{-1}a_{N_k}$。
  5. ratio：對 $d_i>0$ 的列計算 $x^*_{B_i}/d_i$；取最小值 $t$，平手時依 Bland 選下標最小者。沒有 $d_i>0$：unbounded。
  6. 更新 $J_B$：在 leaving 的位置**原地**換上 entering。
  7. 更新 $x_B$：$x^*_{B_i}-d_it$（$i\ne r$），第 $r$ 個位置放 $t$。
  8. 更新 $B^{-1}$：
     - 第 $r$ 列除以 $d_r$。
     - 其他列 $i$ 減去 $d_i$ 倍的（已縮放的）第 $r$ 列。
     - 這等同於「其他列減 $d_i/d_r$ 倍的原第 $r$ 列」。
  9. 計算 $z=c_B^Tx_B^*$，確認它增加了 $\bar c_{N_k}\cdot t$。
- **中間格式**：$J_B$、$x_B^*$、$c_B$、$B^{-1}$、$y$、各 $\bar c_j$、entering、$d$、ratios、leaving、$t$。
- **驗證**
  - $B^{-1}B=I$：抽一欄檢查即可。
  - 最優解代回原約束要成立。
  - $y$ 是 dual 可行的，且 $b^Ty=z^*$。
- **常見失分**
  - $c_B$ 的順序與 $J_B$ 不一致。
  - 調換了欄的位置。
  - 平手時沒用 Bland。
  - 更新 $B^{-1}$ 時用錯列。
- **補充**：退化（某個 $x_B=0$）時仍照常進行（FE Q4 iteration 2 的 $s_6=0$）。

---

## S11 寫 dual（SIF）

- **步驟**
  1. 確認主問題是 max、$\le$、$x\ge0$。若不是，改用 S12。
  2. 每條主約束給一個對偶變數 $y_i$。
  3. dual 目標：$\min\sum b_iy_i$。
  4. 第 $j$ 條對偶約束：$\sum_i a_{ij}y_i\ge c_j$，也就是**主問題第 $j$ 欄**的係數。
  5. $y\ge0$。
- **驗證**：dual 的約束條數等於主問題變數個數；dual 變數個數等於主問題約束條數。
- **常見失分**：把列當成欄（沒有轉置）。

---

## S12 寫 dual（一般形式，T9 Q2、Q5）

- **步驟**
  1. 確認主問題是 max 還是 min。
  2. 查對照表（主問題為 max）：

| 主約束 | 對偶變數 | 主變數 | 對偶約束 |
|---|---|---|---|
| $\le$ | $\ge0$ | $\ge0$ | $\ge c_j$ |
| $\ge$ | $\le0$ | $\le0$ | $\le c_j$ |
| $=$ | free | free | $=c_j$ |

     主問題為 min 時，dual 是 max，表中的方向全部反過來。
  3. 每個對偶變數、每條對偶約束都標註符號或型別。
- **常見失分**：主問題為 min 時沒有反轉方向。

---

## S13 證明 weak duality / C.S. 恆等式（FE Q1(a)(ii)、T8 Q2、T8 Q4）

- **寫法 A（講義順序）**
  1. 主約束乘 $\bar y_i\ge0$ 並加總：$\sum\bar y_ib_i\ge\sum_j\big(\sum_i\bar y_ia_{ij}\big)\bar x_j$。
  2. 對偶約束乘 $\bar x_j\ge0$ 並加總：$\sum_j\big(\sum_i\bar y_ia_{ij}\big)\bar x_j\ge\sum c_j\bar x_j$。
  3. 兩式相接。
- **寫法 B（FE 詳解順序）**：先用 $\bar x\ge0$ 與對偶約束，再重新分組，最後用 $\bar y\ge0$ 與主約束。
- **每一步都要寫明用了哪個條件**："since $\bar x_j\ge0$ and … $\ge c_j$"。
- **C.S. 恆等式**：$b^T\bar y-c^T\bar x=\sum\bar y_i\bar s_i+\sum\bar v_j\bar x_j$，展開後中間的雙重和互相抵消。
- **若題目要求等號成立的條件**：等號成立 ⇔ 每一步的不等式都是等號 ⇔ C.S.（T8 Q2(a)）。

---

## S14 用 C.S. 判斷 / 證明 $x^*$ 最優（FE Q1(a)(iv)、T9 Q1、T9 Q4）

- **步驟**
  1. **寫出 dual**（S11 或 S12）。
  2. **檢查主問題可行**：每條約束代入，標出 tight / slack（列出 slack 的值）。
  3. **由 C.S. 列方程**
     - slack $>0$ 的主約束：對應的 $y_i=0$。
     - $x_j^*>0$：第 $j$ 條對偶約束取等號。
  4. 解出 $y^*$。
  5. **檢查對偶可行**：$y^*\ge0$（或符合一般形式的符號），且其餘對偶約束都成立。
  6. **結論**
     - 可行：「By the C.S. Theorem, $x^*$ is optimal」，並寫出 $c^Tx^*=b^Ty^*$ 作為驗證。
     - 不可行：「the unique $y$ satisfying C.S. is not dual feasible, so $x^*$ is not optimal」。
- **「algebraic proof」的寫法**（T9 Q1）：用 $y^*$ 當乘數把主約束組合起來，得到 $(\cdot)\le b^Ty^*$；再說明 $c^Tx\le(\cdot)$，因為係數差乘上 $x\ge0$。
- **若不是最優，要找更好的解**（T9 Q4(c)）：
  - $y_i<0$ 代表放鬆第 $i$ 條約束會改善目標。
  - 保持其他約束 tight，解方向 $d$（使 $Ad=-e_i$），沿 $d$ 走到某個變數為 0。
- **常見失分**
  - $x_j^*=0$ 的那幾條對偶約束忘了檢查。
  - 把 slack 和 tight 弄反。

---

## S15 參數化目標使 $\bar x$ 最優（FE Q1(b)）

- **步驟**
  1. 寫出含符號 $c$ 的 dual。
  2. 檢查 $\bar x$ 可行，標出 tight / slack。
  3. 由 C.S.：$\bar x_j>0$ 的對偶約束取等號；slack 主約束的 $y_i=0$。
  4. 用 $c$ 表示解出 $y$。
  5. 要求對偶可行：$y\ge0$，且其餘對偶約束成立。每個條件都是 $c$ 的不等式。
  6. 化簡並寫出條件。
- **驗證**：取一組滿足條件的 $c$ 與一組不滿足的 $c$，分別代入檢查（例如用 LP solver）。
- **常見失分**：只寫 $y\ge0$，漏了 $x_j=0$ 對應的那條對偶約束。

---

## S16 Complementary basis / solution（T8 Q3、Q5）

- **步驟**
  1. 寫出 augmented 主問題與 augmented dual：$A^Ty-v=c$。
  2. 主問題的非基本變數依配對（$x_j\leftrightarrow v_j$、$s_i\leftrightarrow y_i$）得到 $K_N$。
  3. 不在 $K_N$ 中的對偶變數設為 0，解出 $K_N$ 中的變數。
  4. 判斷：
     - 主問題可行：$x_B\ge0$。
     - 對偶可行：$(y,v)\ge0$。
     - 兩者皆可行：最優。
  5. 驗證：$c^Tx=b^Ty$（一定成立）；$\bar c_j=-v_j$、$\bar c_{s_i}=-y_i$。

---

## S17 Primal-Dual 狀態與 Farkas（T9 Q6、Q7）

- **證明 unbounded**：給一條射線 $x(t)$，驗證對所有 $t\ge0$ 都可行，且目標趨近 $\infty$。
- **證明不可行**：
  - 把約束組合出矛盾（例如兩式相加得 $0\le-2$）。
  - 或給 Farkas 證書 $y$，使 $A^Ty\ge0$、$b^Ty<0$。
- **由 primal 的狀態推 dual 的狀態**：用相容表。
- **常見失分**：以為主問題不可行，dual 就一定 unbounded；dual 也可能不可行（T9 Q6(c)）。

---

## S18 Sensitivity analysis（T9 Q3、Q8；T10 全部）

- **前置**：確認題目給了 $J_B$、$x_B^*$、$B^{-1}$、$y$、$\bar c_N$。slack 欄 $a_{s_i}=e_i$，$c_{s_i}=0$。
- **判斷是哪一種變動，再選做法**

| 變動 | 做法 | 最優值 |
|---|---|---|
| 非基本 $c_k$ | $\bar c_k^{\text{new}}=c_k^{\text{new}}-ya_k\le0$，解出 $c_k\le ya_k$ | 不變 |
| 基本 $c_{B_r}$ | 以符號重算 $y=c_B^TB^{-1}$；對**每一個**非基本 $j$ 寫出 $\bar c_j(c_{B_r})\le0$；取交集 | $c_B^Tx_B^*$（含新的 $c_{B_r}$） |
| $b_i$ | $x_B=B^{-1}b(b_i)\ge0$，逐分量解不等式後取交集 | $z^*+y_i\,\Delta b_i$ |
| 同時改多個 $b_i$ | 直接檢查 $x_B^*+B^{-1}\Delta b\ge0$，不能套單一範圍 | — |
| 新增變數 $x_0$ | $\bar c_0=c_0-ya_0$；$\le0$ 則原基底仍最優；$>0$ 則讓 $x_0$ 進入繼續 revised simplex | — |
| shadow price | $y_i$；有效範圍就是 $b_i$ 的範圍 | — |
| 超出範圍 | 從原 $J_B$ 用 revised simplex 繼續迭代（一般用 Bland） | — |

- **中間格式**：寫出含參數的 $y$、每個 $\bar c_j$ 的不等式、最終的區間。
- **驗證**
  - 在區間內取一個值，用 LP 重解確認。
  - 區間端點通常會出現替代最優解（某個 $\bar c=0$）。
- **常見失分**
  - 基本變數的係數只檢查了一個 $\bar c$。
  - $b$ 的範圍忘了取所有分量的交集。
  - 超出範圍仍用 shadow price 預測最優值。
