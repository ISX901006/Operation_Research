# A4 正面：Concepts & Formulas

**規格**：A4 直式，建議 3 欄。

> **考試規定參考紙必須手寫。** 本檔是手抄底稿，列印版不能帶進考場。

---

## 欄 1｜幾何與代數基礎

**【1】判斷 CPF**
1. 可行。
2. 找出 active 約束。
3. active 方程組有唯一解（rank $=n$）⇒ CPF。
- active $>n$ 條 ⇒ degenerate CPF。

**【2】Edge 與 adjacent CPF**
- 保留 $n-1$ 條 active ⇒ 一條直線。
- **方向**：代入剩下的 active 約束 ⇒ $t\ge t_0$ 或 $t\le t_0$。
- **improving**：沿方向，$Z$ 嚴格變好（max ↑、min ↓）；斜率 0 不算。
- **另一端**：前進方向上第一個撞到的 inactive 約束（含 $x\ge0$）。
  - 沒有約束擋住 ⇒ 射線。
  - 射線又是 improving ⇒ LP unbounded。
- **退化 CPF**（$p$ 條 active）：檢查 $\binom{p}{n-1}$ 組。
  - 被夾成一點 ⇒ 不算 edge。
  - 不同組合給出同一條線 ⇒ 只算一條。
- **沒有 improving edge ⇒ 最優**。

**【3】SEF 與 BFS**
- SEF：$\max c^Tx$，$Ax=b$，$x\ge0$。
- 約束轉換：
  - $\le$ ⇒ $+s$
  - $\ge$ ⇒ $-s$（surplus）
  - free 變數 ⇒ $x=x^+-x^-$
  - $x\le0$ ⇒ 代換 $x'=-x$
- **basis**：$B$ 可逆（非基本變數設 0 後有唯一解）。
- **BFS**：$B^{-1}b\ge0$。
- **CPF ⇔ BFS**：active ⇔ 該變數 $=0$。
- **adjacent bases**：只差一個變數（沒有遞移性）。
- **degenerate**：某個基本變數 $=0$ ⇒ 一個 BFS 對應多個 basis。

**【4】Reduced cost（max 問題）**
- $z=\bar v+\sum\bar c_jx_{N_j}$，其中 $\bar c_j$ 是沿該 edge 的斜率。
- 全部 $\bar c\le0$ ⇒ 最優。這只是**充分**條件；退化時，最優 BFS 也可能出現 $\bar c>0$。
- min 問題：全部 $\bar c\ge0$ ⇒ 最優；$\bar c<0$ 者進入。
- **MRT**：$t=\min\{\bar b_i/\bar a_{ik}:\ \bar a_{ik}>0\}$。
- **unbounded**：$\bar c_k>0$ 且該欄所有 $\bar a_{ik}\le0$。
- **增量**：$\Delta z=\bar c_k\cdot t$。

**【5】Tableau**
- z-row 存的是 $-\bar c$。
- 最優條件：
  - max：z-row 全 $\ge0$。
  - min：z-row 全 $\le0$。
- **feasible tableau**：RHS 全 $\ge0$。
- **三種進入規則**：
  - largest coefficient：受單位縮放影響。
  - smallest subscript：最簡單。
  - largest improvement：取 $\max\ \bar c\cdot t$。
- **Bland's rule**：進入與離開的平手都選最小下標（比變數下標，不是列號）⇒ 不會 cycling。
- **因果鏈**：cycling ⇒ degenerate pivot（$t=0$，$\bar b_r=0$）。
- 沒有遇到 degenerate basis ⇒ 有限步內終止。

---

## 欄 2｜Revised simplex 與 Duality

**【6】Revised simplex 公式**
$$x_B^*=B^{-1}b,\qquad y=c_B^TB^{-1},\qquad \bar c_j=c_j-ya_j$$
$$d=B^{-1}a_k,\qquad t=\min\{x^*_{B_i}/d_i:\ d_i>0\}\ \text{（沒有 }d_i>0\text{ 則 unbounded）}$$
- **更新 $x_B$**：$x_{B_i}\leftarrow x_{B_i}-d_it$（$i\ne r$），$x_k\leftarrow t$ 放在第 $r$ 位。
- **更新 $B^{-1}$**：
  - $\text{row}_r\leftarrow\text{row}_r/d_r$。
  - $\text{row}_i\leftarrow\text{row}_i-d_i\cdot(\text{新的 row}_r)$。
- **原地替換，欄的位置不換**。
- $d$ 就是 tableau 的 entering 欄；$x_B^*$ 就是 RHS 欄。
- slack 的 $\bar c_{s_i}=-y_i$。

**【7】Dual（SIF）**
- $(P)\ \max c^Tx,\ Ax\le b,\ x\ge0$
- $(D)\ \min b^Ty,\ A^Ty\ge c,\ y\ge0$
- 第 $j$ 條對偶約束用 $A$ 的第 $j$ **欄**；dual 目標係數用 $b$；對偶約束的 RHS 用 $c$。

**【8】一般形式對照表（P 為 max；P 為 min 時方向全部反轉）**

| 主約束 | 對偶變數 | 主變數 | 對偶約束 |
|---|---|---|---|
| $\le$ | $y\ge0$ | $x\ge0$ | $\ge$ |
| $\ge$ | $y\le0$ | $x\le0$ | $\le$ |
| $=$ | free | free | $=$ |

**【9】Weak duality**
- $c^T\bar x\le b^T\bar y$（$\bar x$ 為 P 可行、$\bar y$ 為 D 可行）。
- 推論：兩者可行且目標值相等 ⇒ 兩者都最優。
- 推論：P unbounded ⇒ D infeasible。

**【10】C.S. 恆等式**
$$b^T\bar y-c^T\bar x=\sum_i\bar y_i\bar s_i+\sum_j\bar v_j\bar x_j$$
- $\bar s=b-A\bar x$（主問題 slack），$\bar v=A^T\bar y-c$（對偶 slack）。
- **C.S. 條件**：$y_is_i=0$、$x_jv_j=0$。意思是「至少一個為 0」。
- 兩者可行時：兩者都最優 ⇔ C.S. 條件成立。
- **C.S. Theorem**：可行的 $x^*$ 最優 ⇔ 存在對偶可行的 $y^*$，與 $x^*$ 滿足 C.S.

**【11】Complementary basis**
- 配對：$x_j\leftrightarrow v_j$，$s_i\leftrightarrow y_i$。
- $K_N$ = 與主問題**非基本**變數配對的對偶變數。
- $y^{*T}=c_B^TB^{-1}$，$\bar c_j=-v_j$，$\bar c_{s_i}=-y_i$。
- 主問題最優（$\bar c\le0$）⇔ 對偶可行。
- 兩邊目標值永遠相等；但兩者都可行，才代表都最優。

**【12】Strong duality**
- P 有最優解 ⇒ D 有最優解，且最優值相等。

**【13】Primal–Dual 狀態相容表**

| P \ D | D 最優 | D 不可行 | D 無界 |
|---|---|---|---|
| P 最優 | ✓ | × | × |
| P 不可行 | × | ✓ | ✓ |
| P 無界 | × | ✓ | × |

**【14】Farkas**
- $Ax\le b,\ x\ge0$ 無解 ⇔ 存在 $l\ge0$，$A^Tl\ge0$，$b^Tl<0$。
- $Ax=b,\ x\ge0$ 無解 ⇔ 存在 $y$（free），$A^Ty\ge0$，$b^Ty<0$。

---

## 欄 3｜Sensitivity 與方法選擇

**【15】Sensitivity（$J_B$ 最優；$a_{s_i}=e_i$，$c_s=0$）**

| 改變 | 條件 | 最優值 |
|---|---|---|
| 非基本 $c_k$ | $c_k^{\text{new}}\le ya_k$（即 $c_k-\bar c_k$） | 不變 |
| 基本 $c_r$ | 用參數重算 $y$；**每一個**非基本 $\bar c_j(c_r)\le0$，取交集 | $c_B^Tx_B^*$ |
| $b_i$ | $B^{-1}b(b_i)\ge0$，逐分量取交集 | $z^*+y_i\Delta b_i$ |
| 多個 $b_i$ | $x_B^*+B^{-1}\Delta b\ge0$ | $z^*+y^T\Delta b$ |
| 新變數 $a_0$ | $\bar c_0=c_0-ya_0\le0$ | 不變 |

- **shadow price** $=y_i$，只在 $b_i$ 的範圍內有效；不 tight 的約束 $y_i=0$。
- 某個非基本變數 $\bar c=0$ ⇒ 有替代最優解。
- **超出範圍** ⇒ 從原 $J_B$ 繼續做 revised simplex。
- **經濟意義**：$\bar c_j=c_j-ya_j$ = 利潤 − 所用資源以 shadow price 計的價值。

**【16】題型 → 方法**

| 看到 | 用 |
|---|---|
| 給一個 CPF，問 edges | 幾何法，保留 $n-1$ 條 active |
| 有 $\ge$、$=$ 或負的 RHS | two-phase |
| 題目寫「revised」或給 $B^{-1}$ | revised simplex |
| 給 $x^*$，問是否最優 | C.S. 三步檢驗 |
| 目標係數是參數，問 $x^*$ 何時最優 | C.S. 解出 $y(c)$，再要求對偶可行 |
| 給最優基底，問參數範圍 | sensitivity 表 |
| 證明無解 | Phase 1 $W^*>0$、約束組合出矛盾，或 Farkas |
| 證明 unbounded | 構造 $\bar x(l)$，說明 $z\to\infty$ |

**【17】易混淆**
- 可行域無界 ≠ LP unbounded（反方向也不成立）。
- 主、對偶目標值相等 ≠ 都最優（還需要兩者都可行）。
- 主問題不可行時，對偶是不可行**或**無界。
- 判斷 CPF：「唯一解」與「可行」缺一不可。
- 退化 pivot：$t=0$，BFS 不變，但 basis 改變。
- surplus 的係數是 $-1$；artificial 的係數 $\pm1$，與 RHS 同號。
