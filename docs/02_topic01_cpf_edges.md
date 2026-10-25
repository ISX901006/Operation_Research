# 主題 1：幾何 Simplex — CPF、Edge、Improving Edge、Adjacent CPF

對應：L2（After 1.pdf）、Tutorial 2、期末考 Q2（25 分）
先備：線性方程組有唯一解的條件（係數矩陣可逆，即列向量線性獨立）

---

## Step 1：直覺

**要解決的問題**：LP 的可行區域有無限多個點，不可能一一比較。

**關鍵事實**〔講義 L2 p5–8〕：
1. 最優解一定出現在「角落」（corner point）。
2. 判斷一個角落是不是最優，只需要看從它出發的幾條「邊」（edge）：沒有任何一條邊能讓目標變好，它就是最優。
3. 若某條邊能讓目標變好、而且一直走都不會碰到邊界，LP 就是 unbounded。

**比喻**：你在一座多面體形狀的山上找最高點，而且天很黑。你不需要地圖，只要站在一個角落，摸摸每一條稜線往哪裡是上坡。有上坡就沿著它走到下一個角落；所有稜線都是下坡，你就在山頂。因為這座「山」是凸的，局部最高就是全域最高。

**輸入**：一個 LP（不等式形式）與一個候選點 $\bar x$。
**輸出**：$\bar x$ 是不是 CPF；它有哪些 edge；哪些 edge 是 improving；每條 edge 的另一端在哪裡（或為無界射線）；$\bar x$ 是否最優。

---

## Step 2：數學定義

設可行區域為不等式形式 $\{x\in\mathbb R^n: a_1^Tx\le b_1,\dots,a_m^Tx\le b_m\}$。
（非負限制 $x_j\ge0$ 也寫成 $-x_j\le0$，算在這 $m$ 條之中；$\ge$ 約束乘 $-1$ 轉成 $\le$。）

| 名詞 | 定義 | 白話 |
|---|---|---|
| Constraint boundary | $\{x: a_i^Tx=b_i\}$ | 約束「剛好等號」的那一片超平面 |
| Active constraint | $a_i^T\bar x=b_i$ | $\bar x$ 正好貼在這片牆上 |
| CPF solution | 可行，且 active 約束組成的方程組有**唯一解** $\bar x$ | 至少有 $n$ 片「彼此獨立」的牆在這點交會 |
| Defining equations | 決定 CPF 的 $n$ 條獨立 active 等式 | 釘住這個角落的 $n$ 根釘子 |
| Degenerate CPF | active 約束多於 $n$ 條 | 多出來的牆剛好也經過這個角落 |
| Edge | $n-1$ 條邊界交出一條直線，其中可行的那一段 | 兩個角落之間的稜線（或一端無限延伸的射線） |
| Improving edge | 沿著 edge 走，目標值變好 | 上坡的稜線 |
| Adjacent CPF | 兩個 CPF 是同一條 edge 的兩端 | 共用 $n-1$ 根釘子、只差一根 |

**判斷 CPF 的三個條件缺一不可**〔講義 L2 p22；Tutorial 2 Q7 Remark〕：

| 失敗方式 | 例子 |
|---|---|
| 不可行 | Tutorial 2 Q7 的 $(3,3,3)$：三條 active 有唯一交點，但違反 $x_1+x_2+x_3\le5$ |
| active 太少 | L2 p26 的 $(4,1)$：只有 1 條 active，$x_W$ 仍然自由 |
| active 夠多但不獨立 | Tutorial 2 Q1(b)：4 條 active，交集是一條線 |

---

## Step 3：推導

以下以 max 問題、**非退化** CPF（剛好 $n$ 條 active）為例。這段用向量寫，是〔補充〕的一般化說法；講義的做法（用某個變數當參數）是它的具體版本，考試照講義寫即可。

設 $\bar x$ 的 active 指標集為 $I$，$|I|=n$，且 $\{a_i\}_{i\in I}$ 線性獨立。

**(1) Edge 的方向。** 從 $I$ 中拿掉一條 $k$，保留其餘 $n-1$ 條等號：
$$a_i^Td=0,\quad i\in I\setminus\{k\}.$$
這是 $n-1$ 條獨立方程、$n$ 個未知數，解空間是一維的：$d$ 只差一個倍數。所以沿 $x(t)=\bar x+td$ 走，那 $n-1$ 條約束一直保持 active。這就是講義說「$n-1$ 條邊界交出一條直線」。

**(2) 方向的正負由被拿掉的那條決定。** 被拿掉的約束 $k$ 仍要成立：
$$a_k^Tx(t)=b_k+t\,a_k^Td\le b_k \iff t\,a_k^Td\le0.$$
因為 $a_k$ 與其他 $n-1$ 個向量獨立，$a_k^Td\ne0$。我們規定 $t\ge0$，就必須選 $d$ 使 $a_k^Td<0$，也就是「離開約束 $k$ 的牆，往可行的一側走」。講義的口訣「用剩下的 active 約束決定方向」就是這一步〔L2 p42 第 3 點〕。

**(3) 走多遠。** 其他 inactive 約束 $i\notin I$ 原本有 slack $b_i-a_i^T\bar x>0$。
- 若 $a_i^Td\le0$：$t$ 增加時這條約束只會更寬鬆，永遠擋不住。
- 若 $a_i^Td>0$：撞牆的時間是 $t_i=\dfrac{b_i-a_i^T\bar x}{a_i^Td}$。

所以
$$t_{\max}=\min\Big\{\frac{b_i-a_i^T\bar x}{a_i^Td}:\ i\notin I,\ a_i^Td>0\Big\},$$
另一端點 $\bar x+t_{\max}d$ 就是 adjacent CPF。若沒有任何 $a_i^Td>0$，這條 edge 是無界射線〔L2 p57〕。這個「取最小比值」和 L4 的 minimum ratio test 是同一件事。

**(4) 是否 improving。** 代入目標：
$$Z(t)=c^T\bar x+t\,(c^Td).$$
$Z$ 是 $t$ 的一次函數，斜率是 $c^Td$。max 問題 $c^Td>0$ 為 improving；min 問題 $c^Td<0$ 為 improving。講義說「代入化簡後看斜率正負」〔L2 p48〕就是這個。

**(5) 為什麼「沒有 improving edge」就是最優。**〔補充，講義以 Observation 2 陳述〕
非退化時，$n$ 個方向 $d^{(k)}$（每拿掉一條 $k$ 得一個）滿足 $a_k^Td^{(k)}<0$，且對其他 $i\in I$ 有 $a_i^Td^{(k)}=0$。任取可行點 $x$，令 $u=x-\bar x$。因為 $\{d^{(k)}\}$ 線性獨立，可寫成 $u=\sum_k\lambda_kd^{(k)}$。對每個 $k\in I$：
$$0\ge a_k^Tx-b_k=a_k^Tu=\lambda_k\,a_k^Td^{(k)},$$
又 $a_k^Td^{(k)}<0$，所以 $\lambda_k\ge0$。於是
$$c^Tx-c^T\bar x=\sum_k\lambda_k\,c^Td^{(k)}\le0$$
（每項 $\lambda_k\ge0$、$c^Td^{(k)}\le0$）。所以 $\bar x$ 最優。退化情形要改用 L4 的 reduced cost 論證。

**(6) 退化 CPF。** active 有 $p>n$ 條時，要檢查 $\binom{p}{n-1}$ 組。某些組合會發生：
- 交出來的線上，其餘 active 約束把 $t$ 夾成只能是 0：退化 edge，只是一個點，不算 edge〔Tutorial 2 Q5 Pair 3〕。
- 幾組不同的組合交出同一條線：只算一條 edge〔Tutorial 2 Q5 Pairs 4–6〕。

---

## Step 4：完整範例〔講義 L2 p59–64〕

$$\max\ Z=5x_1+4x_2+3x_3$$
$$\text{s.t. }\ \underbrace{2x_1+3x_2+x_3\le5}_{C1},\quad \underbrace{4x_1+x_2+2x_3\le11}_{C2},\quad \underbrace{3x_1+4x_2+2x_3\le8}_{C3},\quad x_1,x_2,x_3\ge0.$$

問：$\bar x=(2,0,1)$ 是不是 CPF？是不是最優？

**1. 題目給什麼、要求什麼**：一個三維 LP 和一個點。要判斷 CPF、找出所有 edges、判斷 improving、下結論。

**2. 為什麼用這個方法**：題目指定「從某個 CPF 出發的 edges」，而且只有一個點，用幾何 edge 法最直接，不需要建 tableau。

**3. 檢查可行與 active**

| 約束 | 代入 | 結果 |
|---|---|---|
| C1 | $4+0+1=5\le5$ | active |
| C2 | $8+0+2=10<11$ | inactive（slack 1） |
| C3 | $6+0+2=8\le8$ | active |
| $x_1\ge0$ | $2>0$ | inactive |
| $x_2\ge0$ | $0$ | active |
| $x_3\ge0$ | $1>0$ | inactive |

active 剛好 3 條：C1、C3、$x_2=0$。解方程組：$x_2=0$ 代入 $2x_1+x_3=5$ 與 $3x_1+2x_3=8$，得 $x_1=2$、$x_3=1$，唯一解。所以是非退化 CPF，$Z=13$。

**4. 三條 edge**（每次保留兩條 active）

**Edge 1：保留 C1、C3。** 令 $x_2=t$ 為參數。
$2x_1+x_3=5-3t$，$3x_1+2x_3=8-4t$。第一式乘 2 減第二式：$x_1=2-2t$，再得 $x_3=1+t$。
線：$(2-2t,\ t,\ 1+t)$。
- 方向：剩下的 active 是 $x_2\ge0$，即 $t\ge0$，$t$ 從 0 往上增加。
- 擋住的約束：$x_1=2-2t\ge0\Rightarrow t\le1$；C2：$4(2-2t)+t+2(1+t)=10-5t\le11$，$t$ 增加時恆成立；$x_3=1+t\ge0$ 恆成立。最先撞到的是 $x_1\ge0$，在 $t=1$，端點 $(0,1,2)$。
- 目標：$Z=5(2-2t)+4t+3(1+t)=13-3t$。$t$ 增加時 $Z$ 下降，**不是 improving**。

**Edge 2：保留 C1、$x_2=0$。** 令 $x_1=s$。$x_3=5-2s$，線：$(s,0,5-2s)$。
- 方向：剩下的 active 是 C3：$3s+2(5-2s)=10-s\le8\Rightarrow s\ge2$，$s$ 從 2 往上。
- 擋住的約束：$x_3\ge0\Rightarrow s\le2.5$；C2：$4s+2(5-2s)=10\le11$ 恆成立。端點 $(2.5,0,0)$。
- 目標：$Z=5s+3(5-2s)=15-s$，$s$ 增加時下降，**不是 improving**。

**Edge 3：保留 C3、$x_2=0$。** 令 $x_1=s$。$x_3=(8-3s)/2$，線：$(s,0,\tfrac{8-3s}{2})$。
- 方向：剩下的 active 是 C1：$2s+\tfrac{8-3s}{2}=4+\tfrac s2\le5\Rightarrow s\le2$，$s$ 從 2 往下。
- 擋住的約束：$x_1\ge0\Rightarrow s\ge0$；$x_3\ge0$ 在 $s$ 減少時恆成立；C2：$4s+(8-3s)=8+s\le11$ 恆成立。端點 $(0,0,4)$。
- 目標：$Z=5s+\tfrac32(8-3s)=12+\tfrac s2$。$s$ 減少時 $Z$ 下降，**不是 improving**。

**5. 結論**：三條 edge 都不是 improving，所以 $(2,0,1)$ 最優，$Z^*=13$。

**6. 驗證**：三個相鄰端點的目標值 $Z(0,1,2)=10$、$Z(2.5,0,0)=12.5$、$Z(0,0,4)=12$ 都小於 13，與斜率判斷一致。

**7. 方法的限制**：
- 只適合變數少的題目；變數多時 edges 的組合數爆炸，要改用 simplex。
- 退化 CPF 的組合數變多，而且會出現退化 edge。
- 「方向」一定要用剩下的 active 約束決定，不能只看參數「看起來」該往哪走。

---

## Step 5：連結老師的練習題

### Tutorial 2 Q4（非退化，有非負限制）

$\max 5x_1+2x_2+4x_3$，s.t. $x_1+2x_2+x_3\le9$，$2x_1+x_2+3x_3\le12$，$-x_1+x_2+2x_3\le3$，$x_1+x_3\le3$，$x\ge0$。點 $(2,3,1)$。

- **判斷**：active 為第 1、3、4 條，剛好 3 條，非退化，所以有 3 組。第 2 條：$4+3+3=10<12$，inactive；三條非負也都 inactive。
- **Pair 2（第 1 條與第 4 條）**：線 $(3-x_3,\ 3,\ x_3)$。剩下的第 3 條：$-(3-x_3)+3+2x_3=3x_3\le3\Rightarrow x_3\le1$，所以 $x_3$ 往下。$Z=5(3-x_3)+6+4x_3=21-x_3$，$x_3$ 減少時 $Z$ 增加，**improving**。再看誰擋住：$x_3\ge0$ 在 $x_3=0$ 擋住，端點 $(3,3,0)$。
- 另外兩組都不是 improving（詳解 Pair 1 的 $Z=13+7x_3$ 往下、Pair 3 的 $Z=27-7x_3$ 往上）。
- **易漏條件**：
  - (b) 找端點時，非負限制也是 inactive 約束，要一起檢查。Pair 3 就是被 $x_2\ge0$ 擋住。
  - 第 2 條雖然 inactive，在 Pair 3 上化簡成 $12-2x_3\le12$，永遠擋不住，要寫出來說明。
- **答案呈現**：每組依序寫「線的參數式 → 方向（來自哪條 active）→ $Z(t)$ → 是否 improving → 擋住的約束與端點」。

### Tutorial 2 Q5（退化 CPF）

點 $(3,4,1)$ 有 4 條 active，所以要檢查 $\binom42=6$ 組。

- Pair 3：剩下兩條 active 化簡成 $x_3\le1$ 與 $x_3\ge1$ 同時成立，$x_3$ 被固定在 1。這組是退化 edge，不算 edge。
- Pairs 4–6：三組交出同一條線 $(2+x_3,3+x_3,x_3)$，只算一條 edge。上面 $Z=-5$ 為常數，**不是 improving**（斜率 0 也不算）。
- 真正的 edge 只有 3 條，其中只有 Pair 2 是 improving。
- 這是考試的陷阱類型：拿到點先數 active。多於 $n$ 條就要預期出現重複的線與退化 edge。

### Tutorial 2 Q6（min 問題）

方向判斷與 max 相同，只有 improving 的定義相反：$Z$ 沿方向**下降**才算 improving。

---

## Step 6：解題模板（找 improving edges / 相鄰 CPF）

**辨識特徵**：題目給一個點（通常說它是 CPF），問「all (improving) edges emanating from」或「the CPF at the end of every edge」。

**步驟**：

1. **整理約束**：列出所有約束，**包含非負限制**（先確認題目有沒有寫 $x\ge0$）。
2. **代入點**：逐條代入，標 active / inactive，同時確認可行。
3. **數 active 數量 $p$**：
   - $p<n$：不是 CPF。
   - $p=n$ 且獨立：非退化 CPF，共 $n$ 組 edge。
   - $p>n$：退化 CPF，要列 $\binom{p}{n-1}$ 組，最後去掉重複與退化的。
4. **每一組**（保留 $n-1$ 條等號）：
   1. 解出直線，選一個變數當參數 $t$，其餘用 $t$ 表示。
   2. **方向**：把直線代入剩下的 active 約束，得到 $t\ge t_0$ 或 $t\le t_0$。
   3. **目標**：代入 $Z$，化成 $Z(t)=\alpha+\beta t$。
   4. **判斷**：參數往方向走時，max 要 $Z$ 增加，min 要 $Z$ 減少，才算 improving。斜率 0 不算。
   5. **端點**（題目有問時）：把直線代入每條 inactive 約束，只保留在前進方向會撞到的，取最近的一條。沒有任何一條擋住，就是無界射線。
5. **結論**：列出 improving edges。若沒有，寫「no improving edge ⇒ $\bar x$ is optimal」。

**檢查**：
- 端點代回所有約束要可行。
- 端點的 active 約束應該包含這組的 $n-1$ 條，再加上擋住的那條。
- 端點的 $Z$ 與 $Z(t_{\max})$ 一致。

**常見錯誤**：
- 忘了非負限制，或題目沒寫非負卻自己加上。
- 用直覺決定方向，沒有代入剩下的 active 約束。
- 端點只檢查函數約束，漏掉 $x_j\ge0$。
- 退化點只檢查 $n$ 組。
- 把斜率 0 當成 improving。

---

## Step 7：理解檢查

請先作答，我再批改。

**問題 1（概念與適用條件）**
在 $\mathbb R^3$ 中，某個可行點 $\bar x$：
- (a) 只有 2 條 active 約束。它可能是 CPF 嗎？為什麼？
- (b) 有 4 條 active 約束。它一定是 CPF 嗎？如果是 CPF，和只有 3 條 active 的 CPF 有什麼差別？

**問題 2（方法與邏輯）**
在某個 max 問題中，你已經從一個非退化 CPF 找出一條 edge：$x(t)=(1+t,\ 2-t,\ 3)$。
- (a) 你怎麼知道 $t$ 應該往正方向還是負方向走？要用哪一條約束？
- (b) 把直線代入所有 inactive 約束後，發現每一條都化成「$t\ge$ 某個負數」，而 $t$ 是往正方向走。這代表什麼？此時若 $Z(t)=7+2t$，你能對整個 LP 下什麼結論？

**問題 3（小型計算）**

$$\max\ Z=x_1+2x_2+x_3$$
$$\text{s.t. }\ x_1+x_2+x_3\le4,\quad x_2\le2,\quad x_1\le3,\quad x_1,x_2,x_3\ge0.$$

對 $\bar x=(2,2,0)$：
- (a) 列出 active 約束，判斷它是不是 CPF。
- (b) 求出所有 edges 的參數式、前進方向與 $Z(t)$。
- (c) 判斷哪些是 improving edges，並求每條 edge 另一端的 CPF。
- (d) $\bar x$ 是不是最優？最優解唯一嗎？
