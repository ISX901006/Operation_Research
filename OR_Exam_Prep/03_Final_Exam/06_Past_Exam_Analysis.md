# 06 去年期末考逐題解析（MH6503 Trimester I Examination 2025-2026）

## 考試規格（原卷 `Final_Exam.pdf`）

| 項目 | 規定 |
|---|---|
| 時間 | 2 小時 |
| 題數與配分 | 4 題，每題 25 分，全部作答 |
| 作答要求 | 每題從新的一頁開始；可用計算機，但要「systematically」寫出步驟 |
| 參考紙 | **Restricted open book**：可帶 **一張雙面 A4 參考紙**，內容必須手寫在紙上，不可黏貼或釘附其他紙張 |

## 資料來源

- **原卷**：`Final_Exam.pdf`。
- **老師版詳解**：`MH6503_2025_26_Full_Solutions.pdf`。頁首誤標為「Midterm Test」，但題目與原卷完全相同。
- 以下解答都用 Python（scipy、Fraction 精確算術）重新驗算過。

## 與詳解檔不一致之處

1. **Q2 的非負限制**：原卷寫 $x_1,x_2,x_3,\ge0$（多了一個逗號）。詳解檔誤以為題目沒有非負限制，本文依原卷加上 $x\ge0$ 重解。結論不變，但過程不同。
2. **Q2 的 RHS**：詳解檔附註「(3) 的 RHS 由 −6 改為 −5」。原卷本來就印 −5，以原卷為準。
3. **Q3 Phase 1 第 3 次迭代**：詳解檔選 $s_5$ 進入，若照 Bland's rule 應選 $x_3$。題目沒有指定規則，兩種都正確，下面兩條路徑都列出。

---

## Question 1（25 分；原卷沒有標出各子題的分數）

### Q1(a) 題目

$$(P)\quad\max\ 2x_1+2x_2+4x_3\quad\text{s.t.}\quad 9x_1+x_2\le4,\quad x_1+x_3\le3,\quad x_2+2x_3\le5,\quad x\ge0.$$

- (i) 寫出 (P) 的 dual，對偶變數用 $y_1,y_2,y_3$。
- (ii) 證明 $z_P\le z_D$。
- (iii) 寫出 complementary slackness 條件。
- (iv) 用 C.S. 判斷 $x=(\tfrac49,0,\tfrac52)$ 是否為最優解。

**考點**
- dual 的寫法（L8 p29–30）
- weak duality 的證明（L8 p25–27）
- C.S. 條件（L8 p39）
- C.S. Theorem 的三步檢驗（L9 p9）

**最相近的練習題**：T8 Q1、T8 Q2、T9 Q1。

---

#### (i) 寫 dual

**題意**：(P) 是 SIF（max、全部 $\le$、$x\ge0$），直接套六條規則。

**解**
- dual 目標係數 = 主問題的 RHS $(4,3,5)$。
- dual 約束的係數 = 主問題係數矩陣的轉置，RHS = 主問題目標係數 $(2,2,4)$。

$$(D)\quad\min\ 4y_1+3y_2+5y_3\quad\text{s.t.}\quad 9y_1+y_2\ge2,\quad y_1+y_3\ge2,\quad y_2+2y_3\ge4,\quad y\ge0.$$

**驗證**：轉置檢查。
- $x_1$ 那一欄是 $(9,1,0)$，所以第 1 條 dual 約束是 $9y_1+y_2$。
- $x_2$ 那一欄是 $(1,0,1)$，所以第 2 條是 $y_1+y_3$。
- $x_3$ 那一欄是 $(0,1,2)$，所以第 3 條是 $y_2+2y_3$。

**常見失分**：沒有轉置，把主問題的列直接抄成 dual 約束。

---

#### (ii) 證明 weak duality

**解**：設 $\bar x$ 對 (P) 可行，$\bar y$ 對 (D) 可行。

第一步，用 $\bar x_j\ge0$ 和 dual 約束：

$$z_P=2\bar x_1+2\bar x_2+4\bar x_3\ \le\ (9\bar y_1+\bar y_2)\bar x_1+(\bar y_1+\bar y_3)\bar x_2+(\bar y_2+2\bar y_3)\bar x_3.$$

第二步，依 $\bar y_i$ 重新分組：

$$=\ (9\bar x_1+\bar x_2)\bar y_1+(\bar x_1+\bar x_3)\bar y_2+(\bar x_2+2\bar x_3)\bar y_3.$$

第三步，用 $\bar y_i\ge0$ 和主問題約束：

$$\le\ 4\bar y_1+3\bar y_2+5\bar y_3=z_D.\qquad\blacksquare$$

**常見失分**
- 每一個不等號都要寫出依據：第一個 $\le$ 用的是 dual 可行與 $\bar x\ge0$；第二個 $\le$ 用的是主問題可行與 $\bar y\ge0$。
- 中間的等號是重新分組，要讓閱卷者看得出來。

---

#### (iii) C.S. 條件

$$(4-9x_1-x_2)\,y_1=0,\qquad (3-x_1-x_3)\,y_2=0,\qquad (5-x_2-2x_3)\,y_3=0,$$

$$(9y_1+y_2-2)\,x_1=0,\qquad (y_1+y_3-2)\,x_2=0,\qquad (y_2+2y_3-4)\,x_3=0.$$

前三條是「主問題 slack × 對偶變數 = 0」，後三條是「對偶 slack × 主變數 = 0」。

---

#### (iv) 用 C.S. 判斷 $x^*=(\tfrac49,0,\tfrac52)$

**Step 1：主問題可行性**

| 約束 | 代入 | 結果 |
|---|---|---|
| $9x_1+x_2\le4$ | $9\cdot\tfrac49+0=4$ | tight，$s_1=0$ |
| $x_1+x_3\le3$ | $\tfrac49+\tfrac52=\tfrac{53}{18}$ | $s_2=\tfrac1{18}>0$ |
| $x_2+2x_3\le5$ | $0+5=5$ | tight，$s_3=0$ |
| $x\ge0$ | — | 成立 |

所以 $x^*$ 可行。

**Step 2：由 C.S. 解出 $y$**
- $s_2>0$，所以 $y_2=0$。
- $x_1>0$，所以第 1 條 dual 約束取等號：$9y_1+y_2=2$，得 $y_1=\tfrac29$。
- $x_3>0$，所以第 3 條 dual 約束取等號：$y_2+2y_3=4$，得 $y_3=2$。
- 得 $y^*=(\tfrac29,0,2)$。

**Step 3：對偶可行性**
- $y^*\ge0$。
- 第 2 條 dual 約束（對應 $x_2=0$，沒有在 Step 2 用到）：$y_1+y_3=\tfrac29+2=\tfrac{20}9\ge2$，成立。

**結論**：由 Complementary Slackness Theorem，$x^*$ 是最優解。
- 主問題目標值：$Z^*=2\cdot\tfrac49+4\cdot\tfrac52=\tfrac89+10=\tfrac{98}9$。
- 對偶目標值：$4\cdot\tfrac29+5\cdot2=\tfrac{98}9$，兩者相等。

**驗證**：LP solver 算出主問題與 dual 的最優值都是 10.8889 $=\tfrac{98}9$，最優解分別是 $(0.444,0,2.5)$ 與 $(0.222,0,2)$。

**常見失分**
- 漏掉 Step 3 裡第 2 條 dual 約束的檢查。
- 把 $\tfrac{53}{18}$ 算錯，誤判第 2 條為 tight。

**考卷作答版**
> Feasible: $9(\tfrac49)=4$ (tight), $\tfrac49+\tfrac52=\tfrac{53}{18}<3$ (slack), $5=5$ (tight).
> C.S.: $s_2>0\Rightarrow y_2=0$; $x_1>0\Rightarrow 9y_1+y_2=2\Rightarrow y_1=\tfrac29$; $x_3>0\Rightarrow y_2+2y_3=4\Rightarrow y_3=2$.
> Check: $y\ge0$, $y_1+y_3=\tfrac{20}9\ge2$ ✓. Dual feasible ⇒ by the C.S. Theorem $x^*$ is optimal, $Z^*=\tfrac{98}9=b^Ty^*$.

---

### Q1(b) 題目

$$(Q)\quad\max\ c_1x_1+c_2x_2+c_3x_3\quad\text{s.t.}\quad x_1+x_2+x_3\le4,\quad 2x_1+x_2\le5,\quad x\ge0.$$

用 C.S. Theorem 求出 $c_1,c_2,c_3$ 的條件，使 $\bar x=(1,3,0)$ 是最優解。

**考點**：C.S. Theorem，參數化版本（L9 p6–9）。練習題中沒有完全相同的題型，是新題型。

**方法**：$\bar x$ 最優 ⇔ 存在對偶可行的 $y$ 與 $\bar x$ 滿足 C.S.。所以把 $y$ 用 $c$ 表示出來，再要求它對偶可行。

**解**

**Dual**：
$$\min\ 4y_1+5y_2\quad\text{s.t.}\quad y_1+2y_2\ge c_1,\quad y_1+y_2\ge c_2,\quad y_1\ge c_3,\quad y\ge0.$$

**主問題可行性**：$1+3+0=4$，$2+3=5$，兩條約束都 tight。所以 C.S. 不會強迫任何 $y_i=0$。

**由 C.S. 解出 $y$**：$\bar x_1,\bar x_2>0$，所以前兩條 dual 約束取等號。
- $y_1+2y_2=c_1$、$y_1+y_2=c_2$。
- 兩式相減：$y_2=c_1-c_2$。代回：$y_1=2c_2-c_1$。
- 這是唯一滿足 C.S. 的 $y$。

**要求對偶可行**
| 條件 | 來源 |
|---|---|
| $y_2=c_1-c_2\ge0$ | $y_2\ge0$ |
| $y_1=2c_2-c_1\ge0$ | $y_1\ge0$ |
| $y_1=2c_2-c_1\ge c_3$ | 第 3 條 dual 約束（對應 $x_3=0$） |

**答**
$$c_2\le c_1\le2c_2\qquad\text{且}\qquad c_3\le2c_2-c_1.$$

**驗證**：隨機取 4000 組整數 $c\in[-5,5]^3$，用 LP solver 判斷 $(1,3,0)$ 是否最優，結果與上述條件**完全一致**，沒有任何反例。

**常見失分**
- 漏掉第 3 個條件（$x_3=0$ 那條 dual 約束）。
- 只寫 $y\ge0$，沒有寫第 3 條 dual 約束。

**考卷作答版**
> Dual: $\min 4y_1+5y_2$ s.t. $y_1+2y_2\ge c_1$, $y_1+y_2\ge c_2$, $y_1\ge c_3$, $y\ge0$.
> $\bar x$ feasible with both constraints tight. $\bar x_1,\bar x_2>0\Rightarrow y_1+2y_2=c_1$, $y_1+y_2=c_2\Rightarrow y=(2c_2-c_1,\ c_1-c_2)$ (unique).
> Dual feasibility: $c_1-c_2\ge0$, $2c_2-c_1\ge0$, $2c_2-c_1\ge c_3$.
> ⇒ $\bar x$ optimal iff $c_2\le c_1\le2c_2$ and $c_3\le2c_2-c_1$.

**Cheatsheet 需要**：C.S. 三步檢驗，以及「$x_j=0$ 對應的 dual 約束仍要檢查」。

---

## Question 2（25 分）

### 題目（依原卷）

$$\max\ 2x_1+4x_2-x_3$$

| 編號 | 約束 |
|---|---|
| (1) | $-x_1+2x_2+x_3\le3$ |
| (2) | $2x_1+x_2-2x_3\le4$ |
| (3) | $-3x_1-x_2\le-5$ |
| (4) | $x_1+3x_2+2x_3\le9$ |
| (5) | $-x_1+x_2-x_3\le2$ |
| (N1)(N2)(N3) | $x_1,x_2,x_3\ge0$ |

求從 CPF $\bar x=(1,2,0)$ 出發的所有 improving edges。

**考點**：edge、improving edge、退化 CPF（L2 p36–52、p44；T2 Q5）。

**方法**：用幾何的 edge 方法（S4），保留 $n-1=2$ 條 active 約束。

### Step 1：代入 $\bar x$

| 約束 | 代入 | 狀態 |
|---|---|---|
| (1) | $-1+4+0=3$ | active |
| (2) | $2+2-0=4$ | active |
| (3) | $-3-2=-5$ | active |
| (4) | $1+6+0=7<9$ | inactive |
| (5) | $-1+2-0=1<2$ | inactive |
| N1、N2 | $x_1=1>0$，$x_2=2>0$ | inactive |
| N3 | $x_3=0$ | **active** |

共有 **4 條 active**：(1)(2)(3)(N3)。$n=3$，所以這是**退化 CPF**，要檢查 $\binom42=6$ 組。

### Step 2：六組逐一檢查

**Pair (1)(2)**
- 消去 $x_1$ 得 $x_2=2$，再得 $x_1=1+x_3$。令 $t=x_3$：直線 $(1+t,\ 2,\ t)$。
- 方向：(3) 化為 $-3t\le0$，即 $t\ge0$；(N3) 化為 $-t\le0$，即 $t\ge0$。所以 $t$ 從 0 往上走。
- 目標：$Z=2(1+t)+8-t=10+t$，隨 $t$ 增加，**improving**。
- 端點：(4) 化為 $7+3t\le9$，即 $t\le\tfrac23$，最先擋住。(5) 化為 $1-2t\le2$，往上走時不會擋住。
- 端點為 $t=\tfrac23$：$(\tfrac53,2,\tfrac23)$，$Z=\tfrac{32}3$。

**Pair (1)(3)**
- 直線 $(t,\ 5-3t,\ -7+7t)$。
- 方向：(2) 化為 $19-15t\le4$，即 $t\ge1$；(N3) 化為 $-7+7t\ge0$，即 $t\ge1$。所以 $t$ 從 1 往上走。
- 目標：$Z=2t+4(5-3t)-(-7+7t)=27-17t$，遞減，**不是 improving**。
- 端點：(4) 化為 $1+6t\le9$，即 $t\le\tfrac43$，最先擋住；N2 給出 $t\le\tfrac53$。端點為 $(\tfrac43,1,\tfrac73)$。

**Pair (2)(3)**
- 直線 $(t,\ 5-3t,\ \tfrac{1-t}2)$。
- 方向：(1) 化為 $-\tfrac{15}2t+\tfrac{21}2\le3$，即 $t\ge1$；但 (N3) 要求 $\tfrac{1-t}2\ge0$，即 $t\le1$。
- 兩者夾住，只剩 $t=1$ 這一點：**退化 edge，不算 edge**。

**Pair (1)(N3)**
- $x_3=0$，$x_1=2x_2-3$。令 $s=x_2$：直線 $(2s-3,\ s,\ 0)$。
- 方向：(2) 化為 $5s-6\le4$，即 $s\le2$；(3) 化為 $-7s+9\le-5$，即 $s\ge2$。
- 夾成只剩 $s=2$：**退化 edge，不算 edge**。

**Pair (2)(N3)**
- 直線 $(s,\ 4-2s,\ 0)$。
- 方向：(1) 化為 $8-5s\le3$，即 $s\ge1$；(3) 化為 $-s-4\le-5$，即 $s\ge1$。所以 $s$ 從 1 往上走。
- 目標：$Z=2s+16-8s=16-6s$，遞減，**不是 improving**。
- 端點：N2 給出 $s\le2$，最先擋住；(4)、(5) 往上走時不會擋住。端點為 $(2,0,0)$。

**Pair (3)(N3)**
- 直線 $(s,\ 5-3s,\ 0)$。
- 方向：(1) 化為 $10-7s\le3$，即 $s\ge1$；(2) 化為 $5-s\le4$，即 $s\ge1$。所以 $s$ 從 1 往上走。
- 目標：$Z=2s+20-12s=20-10s$，遞減，**不是 improving**。
- 端點：N2 給出 $s\le\tfrac53$，最先擋住。端點為 $(\tfrac53,0,0)$。

### 結果整理

| Pair | 結果 | $Z$ 的走向 | 端點 |
|---|---|---|---|
| (1)(2) | edge | **遞增，improving** | $(\tfrac53,2,\tfrac23)$ |
| (1)(3) | edge | 遞減 | $(\tfrac43,1,\tfrac73)$ |
| (2)(3) | 退化，不是 edge | — | — |
| (1)(N3) | 退化，不是 edge | — | — |
| (2)(N3) | edge | 遞減 | $(2,0,0)$ |
| (3)(N3) | edge | 遞減 | $(\tfrac53,0,0)$ |

### 答

唯一的 improving edge：
$$\{(1+t,\ 2,\ t):\ 0\le t\le\tfrac23\}.$$
$Z$ 從 10 增加到 $\tfrac{32}3$。

### 驗證
- **edge 列舉**：Python 以向量方法列舉，結果相同：active 為 (1)(2)(3)(N3)，真正的 edge 有 4 條，只有 (1)(2) improving。
- **補充發現**：improving edge 的另一端 $(\tfrac53,2,\tfrac23)$ 正好是這個 LP 的最優解，$Z^*=\tfrac{32}3$（LP solver 確認）。

### 與詳解檔的差異
- 詳解檔把 $x\ge0$ 當成不存在，只檢查了 (1)(2)、(1)(3)、(2)(3) 三組。
- 它把 (2)(3) 當成一條無界射線 $(t,\ 5-3t,\ \tfrac{1-t}2)$，$t\ge1$。但 $t>1$ 時 $x_3<0$，違反原卷的 $x_3\ge0$。
- 它漏掉了 (2)(N3)、(3)(N3) 兩條真正的 edge。
- 兩者的最後結論碰巧相同。但若照詳解檔的做法作答，edge 的清單是錯的，可能被扣分。

### 常見失分
- 沒有發現 $x_3=0$ 也是 active，因此沒有察覺這是退化 CPF。
- 方向沒有同時檢查所有剩下的 active 約束。
- 把退化 edge 也列為 edge。

### 考卷作答版（精簡）
> Active at $\bar x$: (1),(2),(3) and $x_3\ge0$ (4 active, $n=3$ ⇒ degenerate; check 6 pairs).
> (1)(2): $(1+t,2,t)$; (3),$x_3\ge0$ ⇒ $t\ge0$; $Z=10+t$ ↑ **improving**; (4) ⇒ $t\le\tfrac23$.
> (1)(3): $(t,5-3t,7t-7)$; $t\ge1$; $Z=27-17t$ ↓.
> (2)(3): $(t,5-3t,\tfrac{1-t}2)$; (1) ⇒ $t\ge1$, $x_3\ge0$ ⇒ $t\le1$ ⇒ single point, not an edge.
> (1),$x_3$: $(2s-3,s,0)$; (2) ⇒ $s\le2$, (3) ⇒ $s\ge2$ ⇒ single point.
> (2),$x_3$: $(s,4-2s,0)$; $s\ge1$; $Z=16-6s$ ↓.
> (3),$x_3$: $(s,5-3s,0)$; $s\ge1$; $Z=20-10s$ ↓.
> ∴ the only improving edge is $\{(1+t,2,t):0\le t\le\tfrac23\}$.

**Cheatsheet 需要**：S4 的步驟、退化 CPF 的處理（$\binom{p}{n-1}$ 組、去重、夾成一點）、「先確認有沒有 $x\ge0$」。

---

## Question 3（25 分）

### 題目

$$\max\ Z=2x_1+x_2+x_3\quad\text{s.t.}\quad -x_1+2x_2=1,\quad x_1+x_2+x_3\ge2,\quad x_1-x_2+x_3=2,\quad x\ge0.$$

寫出 artificial problem，用 tabular simplex 判斷是否可行；若可行，進行 Phase 2 求最優解。

**考點**：轉成 SEF、artificial 的三條規則、Phase 1 與 Phase 2（L6；T6 Q3、Q4）。

**方法**：有 $=$ 和 $\ge$ 約束，沒有現成的可行基底，所以用 two-phase。

### Step 1：artificial problem

- 第 2 條減去 surplus $s_5$。
- 檢查每一列有沒有「只出現在這一列、且係數與 RHS 同號」的變數：
  - 第 1 列：沒有，加 $w_4$。
  - 第 2 列：$s_5$ 的係數 $-1$ 與 RHS 異號，加 $w_6$。
  - 第 3 列：沒有，加 $w_7$。

$$\min\ W=w_4+w_6+w_7$$
$$\text{s.t.}\quad -x_1+2x_2+w_4=1,\quad x_1+x_2+x_3-s_5+w_6=2,\quad x_1-x_2+x_3+w_7=2,\quad x_1,x_2,x_3,s_5,w_4,w_6,w_7\ge0.$$

（變數名稱與詳解檔相同。）

### Step 2：初始 W 列
把三列加總，消去基本變數 $w$：
$$W=5-x_1-2x_2-2x_3+s_5,\quad\text{即}\quad W+x_1+2x_2+2x_3-s_5=5.$$

這是 min 問題，**W 列為正的變數可以進入**。

### Phase 1

**初始表**

| BV | $x_1$ | $x_2$ | $x_3$ | $w_4$ | $s_5$ | $w_6$ | $w_7$ | RHS |
|---|---|---|---|---|---|---|---|---|
| W | 1 | 2 | 2 | 0 | −1 | 0 | 0 | 5 |
| $w_4$ | −1 | 2 | 0 | 1 | 0 | 0 | 0 | 1 |
| $w_6$ | 1 | 1 | 1 | 0 | −1 | 1 | 0 | 2 |
| $w_7$ | 1 | −1 | 1 | 0 | 0 | 0 | 1 | 2 |

**Iteration 1**
- 進入 $x_1$（Bland：W 列為正的變數中下標最小）。
- ratio：$w_6$ 列 $2/1$、$w_7$ 列 $2/1$，平手；$w_4$ 列係數為負，排除。依 Bland 選下標小的，$w_6$ 離開。
- 列運算：$R_W\leftarrow R_W-R_{w_6}$，$R_{w_4}\leftarrow R_{w_4}+R_{w_6}$，$R_{w_7}\leftarrow R_{w_7}-R_{w_6}$。

| BV | $x_1$ | $x_2$ | $x_3$ | $w_4$ | $s_5$ | $w_7$ | RHS |
|---|---|---|---|---|---|---|---|
| W | 0 | 1 | 1 | 0 | 0 | 0 | 3 |
| $w_4$ | 0 | 3 | 1 | 1 | −1 | 0 | 3 |
| $x_1$ | 1 | 1 | 1 | 0 | −1 | 0 | 2 |
| $w_7$ | 0 | −2 | 0 | 0 | 1 | 1 | 0 |

（$w_6$ 已離開基底，刪掉它的欄。注意 $w_7=0$，這個 BFS 已經是退化的。）

**Iteration 2**
- 進入 $x_2$。
- ratio：$w_4$ 列 $3/3=1$、$x_1$ 列 $2/1=2$；$w_7$ 列係數為負，排除。$w_4$ 離開。
- 列運算：$R_{w_4}\leftarrow\tfrac13R_{w_4}$，再以它消去其他列。

| BV | $x_1$ | $x_2$ | $x_3$ | $s_5$ | $w_7$ | RHS |
|---|---|---|---|---|---|---|
| W | 0 | 0 | 2/3 | 1/3 | 0 | 2 |
| $x_2$ | 0 | 1 | 1/3 | −1/3 | 0 | 1 |
| $x_1$ | 1 | 0 | 2/3 | −2/3 | 0 | 1 |
| $w_7$ | 0 | 0 | 2/3 | 1/3 | 1 | 2 |

**Iteration 3：這裡有兩條合法路徑**

W 列中 $x_3$ 與 $s_5$ 都為正，兩者都可以進入。

**路徑 A（老師詳解）：$s_5$ 進入**
- ratio：只有 $w_7$ 列的係數為正，$t=\tfrac{2}{1/3}=6$，$w_7$ 離開。
- 列運算：$R_{w_7}\times3$，再以它消去其他列。

| BV | $x_1$ | $x_2$ | $x_3$ | $s_5$ | RHS |
|---|---|---|---|---|---|
| W | 0 | 0 | 0 | 0 | 0 |
| $x_2$ | 0 | 1 | 1 | 0 | 3 |
| $x_1$ | 1 | 0 | 2 | 0 | 5 |
| $s_5$ | 0 | 0 | 2 | 1 | 6 |

**路徑 B（完全照 Bland）：$x_3$ 進入**
- ratio：$x_2$ 列 $3$、$x_1$ 列 $\tfrac32$、$w_7$ 列 $3$，$x_1$ 離開。
- 下一步 W 列只剩 $s_5$ 為正，$s_5$ 進入，$w_7$ 離開。
- Phase 1 結束時的基底為 $\{x_2,x_3,s_5\}$，BFS 為 $x_2=\tfrac12$、$x_3=\tfrac52$、$s_5=1$、$x_1=0$。

### Phase 1 結論
$W^*=0$，所以**原問題可行**，而且 artificial 都已離開基底。

### Phase 2（路徑 A）

從 Phase 1 的最終表讀出基本變數：
$$x_2=3-x_3,\qquad x_1=5-2x_3,\qquad s_5=6-2x_3.$$

代入原目標：
$$Z=2(5-2x_3)+(3-x_3)+x_3=13-4x_3,\quad\text{即}\quad Z+4x_3=13.$$

| BV | $x_1$ | $x_2$ | $x_3$ | $s_5$ | RHS |
|---|---|---|---|---|---|
| Z | 0 | 0 | 4 | 0 | 13 |
| $x_2$ | 0 | 1 | 1 | 0 | 3 |
| $x_1$ | 1 | 0 | 2 | 0 | 5 |
| $s_5$ | 0 | 0 | 2 | 1 | 6 |

Z 列沒有負數（max 問題），已經最優。

### Phase 2（路徑 B）

起始 Z 列為 $(-2,0,0,0\mid3)$，所以 $x_1$ 進入，$x_3$ 離開（ratio $\tfrac{5/2}{1/2}=5$）。pivot 之後得到與路徑 A 相同的最終表，Z 列為 $(0,0,4,0\mid13)$。

### 答
$$(x_1^*,x_2^*,x_3^*)=(5,3,0),\qquad Z^*=13\qquad(s_5=6).$$

### 驗證
- 代入原約束：$-5+6=1$ ✓；$5+3+0=8\ge2$ ✓；$5-3+0=2$ ✓。
- $Z=10+3=13$。
- LP solver 求得最優值 13，最優解 $(5,3,0)$。
- 兩條路徑都用 Fraction 精確算術重算過。

### 常見失分
- artificial problem 沒有完整寫出（漏寫目標或非負限制）。
- 初始 W 列沒有消去基本變數，或正負號弄錯。
- Phase 1 用 max 的進入規則（應該是 W 列為正者進入）。
- Phase 2 的 Z 列沒有消去基本變數。
- 忘了在 Phase 1 結束時說明「$W^*=0$ ⇒ feasible」。

### 考卷作答版要點
1. 寫出 artificial problem。
2. 寫出初始 W 列的推導。
3. 每次迭代：entering、ratio（排除的列標「—」）、leaving、列運算、新表。
4. 寫「$W^*=0$ ⇒ original LP is feasible; basis {…}」。
5. Phase 2：$Z$ 的代換推導與新表。
6. 寫「all z-row entries ≥ 0 ⇒ optimal」，再寫出 $x^*$ 與 $Z^*$。

**Cheatsheet 需要**：artificial 三條規則、W 列 = 各列相加、min 問題的進入規則、Phase 2 要消去基本變數、殘留 artificial 的處理。

---

## Question 4（25 分）

### 題目

$$\max\ z=3x_1+5x_2+3x_3\quad\text{s.t.}\quad x_1+2x_2+x_3\le8,\quad 2x_1+x_2+3x_3\le10,\quad x_1+x_2+x_3\le6,\quad x\ge0.$$

用 revised simplex 搭配 Bland's rule 求最優解。

**考點**：revised simplex 全流程、Bland 的進入與平手處理、$B^{-1}$ 更新（L7 p40–49；T7 Q2、Q4）。

**設定**
- 加 slack $s_4,s_5,s_6$，變數順序為 $(x_1,x_2,x_3,s_4,s_5,s_6)$。
- $A=[\,\cdot\mid I\,]$，$b=(8,10,6)$，$c=(3,5,3,0,0,0)$。
- 初始 $J_B=(s_4,s_5,s_6)$，$B^{-1}=I$。

### Iteration 1
- $x_B^*=(8,10,6)$，$c_B=(0,0,0)$，$y=(0,0,0)$。
- $\bar c_1=3$，$\bar c_2=5$，$\bar c_3=3$，全部為正。依 Bland，**$x_1$ 進入**（不是選最大的 $x_2$）。
- $d=B^{-1}a_1=(1,2,1)$。
- ratio：$8/1,\ 10/2,\ 6/1$，最小為 5，**$s_5$ 離開**，$t=5$。
- 更新 $x_B$：$s_4=8-5=3$，$x_1=5$，$s_6=6-5=1$。$J_B=(s_4,x_1,s_6)$。
- 更新 $B^{-1}$：$R_2\leftarrow\tfrac12R_2$，$R_1\leftarrow R_1-R_2$，$R_3\leftarrow R_3-R_2$：
$$B^{-1}=\begin{bmatrix}1&-\tfrac12&0\\0&\tfrac12&0\\0&-\tfrac12&1\end{bmatrix}.$$
- $z=15$。

### Iteration 2
- $c_B=(0,3,0)$，$y=c_B^TB^{-1}=(0,\tfrac32,0)$。
- $\bar c_2=5-\tfrac32=\tfrac72$，$\bar c_3=3-\tfrac92=-\tfrac32$，$\bar c_{s_5}=-\tfrac32$。只有 $x_2$ 為正，**$x_2$ 進入**。
- $d=B^{-1}a_2=(\tfrac32,\tfrac12,\tfrac12)$。
- ratio：$3/\tfrac32=2$，$5/\tfrac12=10$，$1/\tfrac12=2$。$s_4$ 與 $s_6$ 平手，依 Bland 選下標小的，**$s_4$ 離開**，$t=2$。
- 更新 $x_B$：$x_2=2$，$x_1=5-\tfrac12\cdot2=4$，$s_6=1-\tfrac12\cdot2=0$。新 BFS 是**退化的**。$J_B=(x_2,x_1,s_6)$。
- 更新 $B^{-1}$：$R_1\leftarrow\tfrac23R_1$，$R_2\leftarrow R_2-\tfrac12R_1$，$R_3\leftarrow R_3-\tfrac12R_1$（用的是縮放後的 $R_1$）：
$$B^{-1}=\begin{bmatrix}\tfrac23&-\tfrac13&0\\-\tfrac13&\tfrac23&0\\-\tfrac13&-\tfrac13&1\end{bmatrix}.$$
- $z=22$。檢查：$15+\tfrac72\cdot2=22$ ✓。

### Iteration 3
- $c_B=(5,3,0)$，$y=(\tfrac73,\tfrac13,0)$。
- $\bar c_3=3-(\tfrac73+1+\tfrac13)=-\tfrac13$，$\bar c_{s_4}=-\tfrac73$，$\bar c_{s_5}=-\tfrac13$。全部 $\le0$，**最優**。

### 答
- $J_B=(x_2,x_1,s_6)$。
- $(x_1^*,x_2^*,x_3^*)=(4,2,0)$，$s_6=0$。
- $z^*=22$。

### 驗證
- $B^{-1}B=I$：$B=[a_2\ a_1\ e_3]=\begin{bmatrix}2&1&0\\1&2&0\\1&1&1\end{bmatrix}$，與上面的 $B^{-1}$ 相乘得 $I$ ✓。
- 對偶：$y=(\tfrac73,\tfrac13,0)$ 對偶可行，$b^Ty=\tfrac{56}3+\tfrac{10}3=22=z^*$ ✓。
- LP solver 求得最優值 22。整個流程用 Fraction 重算，每一步都與詳解檔一致。

### 常見失分
- Iteration 1 照 largest coefficient 選 $x_2$，違反 Bland。
- Iteration 2 的平手沒有依下標處理。
- $c_B$ 的順序沒有跟著 $J_B$ 的位置。
- 更新 $B^{-1}$ 時，用原來的 $R_1$ 還是縮放後的 $R_1$ 混用。
- 退化的 $s_6=0$ 以為算錯了。

### 考卷作答版
每次迭代依序列出：
1. $J_B$、$x_B^*$、$c_B$、$B^{-1}$。
2. $y$。
3. 各 $\bar c$。
4. entering（並寫「by Bland」）。
5. $d$、ratios、leaving。
6. 更新後的 $x_B$ 與 $B^{-1}$（寫出列運算）。

最後一次迭代寫「all $\bar c\le0$ ⇒ optimal」，並寫出 $x^*$ 與 $z^*$。

**Cheatsheet 需要**：revised simplex 的公式卡（$y$、$\bar c$、$d$、$t$、$x_B$、$B^{-1}$ 更新）、Bland 的兩個規則、「不交換欄位」。

---

## 總結

| 題 | 主題 | 方法 | 答案 |
|---|---|---|---|
| Q1(a) | dual、weak duality、C.S. 檢驗 | S11、S13、S14 | $x^*$ 最優，$Z^*=\tfrac{98}9$，$y^*=(\tfrac29,0,2)$ |
| Q1(b) | 參數化 C.S. | S15 | $c_2\le c_1\le2c_2$，$c_3\le2c_2-c_1$ |
| Q2 | improving edges（退化 CPF） | S4 | 只有一條：$(1+t,2,t)$，$0\le t\le\tfrac23$ |
| Q3 | Two-phase tabular | S9 | 可行；$x^*=(5,3,0)$，$Z^*=13$ |
| Q4 | Revised simplex＋Bland | S10 | $x^*=(4,2,0)$，$z^*=22$ |
