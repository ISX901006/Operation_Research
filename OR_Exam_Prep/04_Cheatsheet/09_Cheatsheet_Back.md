# A4 背面：Algorithms & Problem-Solving Steps

**版面**：A4 直式，3 欄。
**用途**：考試規定參考紙必須手寫；本檔是手抄底稿。

---

## 欄 1｜Edges、Tableau、Tie-break

**【A】Improving edges（FE Q2 型）**
1. 列出所有約束，**一定要確認有沒有 $x\ge0$**。
2. 代入 $\bar x$，標出 active 的約束，數 $p$。
   - $p=n$：共 $n$ 組。
   - $p>n$：共 $\binom{p}{n-1}$ 組。
3. 每一組：
   1. 寫出直線 $x(t)$。
   2. 用剩下的 active 約束判定 $t$ 的方向。
   3. 寫出 $Z(t)$，判斷是否 improving。
   4. 代入 inactive 約束，找最近的一條，得到端點。
4. 去重；被夾成一點的組合刪掉。
5. 列出 improving edges（寫出範圍）。若一條都沒有，$\bar x$ 就是最優解。

**表格欄位**：Pair ｜ $x(t)$ ｜ 方向（由哪條約束決定）｜ $Z(t)$ ｜ improving？｜ 端點（由哪條約束擋住）

**【B】Tableau simplex（max）**
0. 每個基本變數的欄必須是單位向量；z-row 中基本變數的位置必須是 0。不是的話先做列運算。
1. 選 z-row 為負的一欄進入（min 問題則選為正的）。z-row 沒有可選的 ⇒ 最優。
2. MRT：只看該欄 $>0$ 的列，計算 RHS／係數，取最小。沒有 $>0$ 的列 ⇒ unbounded。
3. Pivot：
   - pivot row 除以 pivot 元素。
   - 其他列減去「該列在 pivot 欄的係數 × 新的 pivot row」。
4. 檢查：每個基本變數的欄是單位向量，RHS $\ge0$。

**無界的寫法**：$\bar x(k)$：entering 變數 $=k$、其他非基本變數 $=0$、基本變數由 tableau 讀出，則 $z_k\to\infty$。

**【C】Tie-break**

| 規則 | 進入 | 離開 |
|---|---|---|
| LC（largest coefficient） | $\bar c$ 最大 | — |
| LI（largest improvement） | 每個候選先做 MRT 得 $t$，取 $\bar c\cdot t$ 最大 | — |
| Bland | 下標最小 | 平手時取下標最小 |

列表：候選 ｜ $\bar c$ ｜ $t$ ｜ $\Delta z$

---

## 欄 2｜Two-phase、Revised simplex

**【D】Two-phase（FE Q3 型）**
1. 化成 SEF：$\le$ 加 $+s$；$\ge$ 加 $-s$。
2. 逐列檢查：若有變數只出現在這一列、且係數與 RHS 同號 ⇒ 當作 slack；否則加 $\pm w$（與 RHS 同號）。
3. **完整寫出** artificial problem：$\min W=\sum w$、所有約束、所有變數 $\ge0$。
4. W 列 = 所有含 $w$ 的列相加（$w$ 的欄填 0）。進入規則：**W 列為正者進入**（min）。
5. Phase 1 迭代（建議用 Bland）；artificial 離開基底後可刪掉該欄。
6. 判斷：
   - $W^*>0$ ⇒ 原問題 infeasible，結束。
   - $W^*=0$ 但仍有 $w$ 在基底中 ⇒ 在該列找一個非零係數（正負皆可）pivot 掉（退化 pivot，$t=0$）。
7. Phase 2：
   - 用原目標，把基本變數代換掉：$Z=\dots$，寫成 z-row。
   - 用 max 規則繼續，直到最優或 unbounded。
8. 結論：$W^*=0$ ⇒ feasible；最後寫出 $x^*$ 與 $Z^*$。

**【E】Revised simplex（FE Q4 型）**

**初始**：$J_B=(s_1,\dots,s_m)$，$B^{-1}=I$，$x_B=b$。

**每次迭代**依序寫出：
1. $J_B$（有順序）、$x_B^*$、$c_B$（順序與 $J_B$ 相同）。
2. $y=c_B^TB^{-1}$。
3. 每個非基本變數 $\bar c_j=c_j-ya_j$。全部 $\le0$ ⇒ 最優。
4. 進入：Bland 取 $\bar c>0$ 中下標最小者。
5. $d=B^{-1}a_k$；ratio $=x_{B_i}/d_i$（只看 $d_i>0$）。平手取下標最小者離開。
6. 在原位置換上進入變數；$x_{B_i}\leftarrow x_{B_i}-d_it$；$x_k\leftarrow t$。
7. $B^{-1}$ 列運算：$R_r\leftarrow R_r/d_r$；$R_i\leftarrow R_i-d_iR_r$。
8. 驗算 $z$ 增加了 $\bar c_k\cdot t$。

**最優時檢查**
- $b^Ty=z^*$。
- $y\ge0$（SIF 的情況）。
- 把 $x^*$ 代回約束。

**two-phase revised**：殘留 $w_r$ ⇒ 取 $B^{-1}$ 第 $r$ 列乘以各 $a_j$，找一個 $\ne0$ 的 pivot。

---

## 欄 3｜Duality 解題、Sensitivity、易失分

**【F】C.S. 三步（FE Q1(a)(iv) 型）**
0. 寫出 dual。
1. 主問題可行：逐條標 tight／slack（寫出 slack 值）。
2. C.S.：
   - $s_i>0$ ⇒ $y_i=0$。
   - $x_j>0$ ⇒ 第 $j$ 條對偶約束取等號。
   - 解出 $y^*$。
3. 對偶可行：$y^*\ge0$，且**其餘**對偶約束（對應 $x_j=0$）都成立。
   - 成立 ⇒ 最優，並驗算 $c^Tx^*=b^Ty^*$。
   - 不成立 ⇒ 不是最優（若 $y$ 唯一）。

**參數版本（FE Q1(b)）**：用 $c$ 表示 $y(c)$，再列出 $y(c)\ge0$ 與其餘對偶約束 ⇒ 得到 $c$ 的條件。

**若不是最優、要改進（T9 Q4）**：$y_i<0$ ⇒ 放鬆約束 $i$；解 $Ad=-e_i$，沿 $d$ 走到某個變數變成 0。

**【G】Weak duality 證明**
$$c^T\bar x\ \overset{\text{D 可行},\ \bar x\ge0}{\le}\ \sum_j(A^T\bar y)_j\bar x_j\ =\ \sum_i(A\bar x)_i\bar y_i\ \overset{\text{P 可行},\ \bar y\ge0}{\le}\ b^T\bar y$$
每一個 $\le$ 都要註明依據。

**【H】Sensitivity 步驟**
1. 判斷變數是 basic 還是 nonbasic。
2. 改 $c$：
   - nonbasic：只算一個 $\bar c$。
   - basic：用參數重算 $y$，所有非基本變數的 $\bar c(\cdot)\le0$，取交集。
3. 改 $b$：$x_B=B^{-1}b(\theta)\ge0$，取交集；最優值 $z^*+y\Delta b$。
4. 新變數：$\bar c_0=c_0-ya_0$。
5. 超出範圍：讓 $\bar c>0$ 的變數進入，繼續 revised simplex。

**【I】易失分**
- 漏掉 $x\ge0$，或題目沒寫卻自己加上 $x\ge0$。
- 退化點只檢查 $n$ 組。
- z-row 的正負號弄反；Phase 1 用了 max 的進入規則。
- MRT 把負值或 0 也算進去。
- Bland 比較的是列號而不是變數下標。
- Phase 2 的 z-row 沒有消去基本變數。
- $c_B$ 順序錯；換了 $J_B$ 的位置。
- 改基本 $c$ 只檢查一個 $\bar c$。
- 超出範圍仍用 shadow price 預測。
- 宣稱 unbounded 或 infeasible 卻沒有給證明（序列，或 $W^*>0$）。
- 沒有寫最後的結論句和目標值。

**【J】考場流程**
- 開頭先標出：max／min？有沒有 $x\ge0$？題目指定什麼方法？
- 每題約 25 分鐘。
- 最後 10 分鐘驗算 $c^Tx^*=b^Ty^*$，並把解代回約束。
