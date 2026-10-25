# 02 概念與推導（主要複習教材）

每個主題依序寫：直覺 → 定義與符號 → 公式與適用條件 → 推導 → 範例 → 講義與老師補充 → 容易混淆的觀念 → 與其他章節的關聯。

**標記**
- 〔講義〕：老師的投影片原文。
- 〔手寫〕：課堂手寫筆記。
- 〔補充〕：本文件的解釋或推導，不是老師原文。

頁碼格式見 `01_OR_Knowledge_Map.md`。

**全文共用的記號**

| 記號 | 意義 |
|---|---|
| $n$ | 變數個數（在 L3 之後的 SEF 中，$n$ 指包含 slack 的總變數數） |
| $m$ | 函數約束個數 |
| $x_B,\ x_N$ | 基本變數、非基本變數 |
| $\bar c_{N_j}$ | 非基本變數 $x_{N_j}$ 的 reduced cost |
| $J_B$ | 基底（基本變數的集合） |
| $B,\ N$ | 基本、非基本係數矩陣 |
| $y$ | $c_B^TB^{-1}$，即對偶變數（shadow price） |

---

## 主題 1 建模（L1）

### 直覺
OR 的第一步是把文字敘述翻成數學：要決定什麼（變數）、要什麼最好（目標）、受什麼限制（約束）。翻譯得好，後面的演算法只是機械計算；翻譯錯了，演算法再完美也沒有意義。

### 定義與符號〔講義 L1 p19–32〕
一般模型：
$$\max/\min\ f(x)\quad\text{s.t.}\quad g_i(x)\le0,\ \ h_j(x)=0,\ \ x\in S.$$

| 名詞 | 定義 |
|---|---|
| decision variable | 要決定的量 |
| solution | 對所有變數給定一組值，不論是否可行 |
| feasible solution | 滿足所有約束的 solution |
| feasible region | 所有 feasible solution 構成的集合 |
| infeasible model | 沒有任何 feasible solution |
| optimal solution | 目標值最好的 feasible solution |
| optimal value | optimal solution 的目標值 |
| unbounded model | 存在 feasible solution，且目標值可以任意好 |
| LP | 目標函數與函數約束都是線性，set constraint 為非負限制（L1 p49） |

### LP 四假設〔講義 L1 p34–36〕

| 假設 | 意思 | 違反的例子 | 違反時的處理 |
|---|---|---|---|
| Proportionality | 每個活動的貢獻與其水準成正比 | 啟動成本、量大折扣、學習曲線 | 改用非線性規劃 |
| Additivity | 總貢獻等於各活動貢獻之和，沒有交叉項 | $3x_D+5x_W\pm x_Dx_W$ | 改用非線性規劃 |
| Divisibility | 變數可以是任意實數 | 冰箱不能生產 17.5 台 | 改用 integer programming |
| Certainty | 所有參數 $c_j,a_{ij},b_i$ 都是已知常數 | 停機時間不確定 | 做 sensitivity analysis |

### 建模四步〔講義 L1 p33〕
1. 找出決策與決策變數，**寫清楚單位**。
2. 找出目標與目標函數。
3. 找出所有約束，包含題目沒明說的（例如非負）。
4. 組合成完整模型。

### 範例〔講義 L1 p29–30〕Wyndor
- $x_D$、$x_W$：每週生產的門、窗批數。
- 模型：
$$\max\ Z=3x_D+5x_W\quad\text{s.t.}\quad x_D\le4,\ \ 2x_W\le12,\ \ 3x_D+2x_W\le18,\ \ x_D,x_W\ge0.$$
- 係數直接來自資料表：每一列約束對應一座工廠的工時，右邊是該工廠可用的時數。

### 容易混淆
- **unbounded 和可行域無界是兩件事**〔講義 L1 p25〕
  - $\max 1/x$，$0<x\le1$：可行域有界，但目標趨近無限大。
  - $\min x$，$x\ge0$：可行域無界，但最優值是 0。
- **只要有一條約束不滿足，就是 infeasible solution**（T1 Q5(c)）。
- **等式約束不能寫成不等式**：T1 Q3 的「每天固定 100 公升」是 $=$，不是 $\le$。

### 關聯
建模的輸出就是後面所有演算法的輸入。certainty 假設不成立，正是主題 14 sensitivity analysis 的動機。

---

## 主題 2 圖解法與模型狀態（L1 p49–69）

### 直覺
只有兩個變數時，可以直接把可行域畫出來。同一個目標值的點落在一條直線上（等值線），改變目標值就是把這條線平移。把線往「變好」的方向推，最後一個還碰得到可行域的點就是最優解。

### 方法〔講義 L1 p58〕
1. **畫可行域**：每條約束畫出邊界線（兩點決定一條線），代入原點判斷哪一側可行。
2. **畫等值線**：令目標等於任意一個值得到一條線，代入原點判斷往哪個方向是變好。
3. **平移**：沿變好的方向推到最後一個接觸點。

### 為什麼最優解會落在角落〔補充〕
- 目標 $c^Tx$ 是線性的，等值線彼此平行。
- 可行域是凸多邊形。
- 平移的直線最後離開可行域時，接觸到的不是一個頂點，就是整條邊。
- 若是整條邊，邊的兩個端點也都是最優解。

這就是講義的結論〔講義 L1 p50、L2 p9〕：若 LP 可行且有界，最好的 CPF 就是最優解；若有多個最優解，至少有兩個是 CPF。嚴格證明在主題 8 的 Fundamental Theorem。

### 三種特殊狀態〔講義 L1 p63–66〕

| 狀態 | 圖形特徵 | 講義例子 |
|---|---|---|
| infeasible | 各約束的可行側沒有交集 | Wyndor 加上 $3x_D+5x_W\ge50$ |
| multiple optima | 等值線與某條邊界平行 | $Z=3x_D+2x_W$，與 $3x_D+2x_W=18$ 平行 |
| unbounded | 可行域在變好的方向沒有盡頭 | $\min -4x_1+x_2$ |

### 範例〔講義 L1 p59–62〕
- **Example A**：$\max 5x_1+4x_2$，$6x_1+4x_2\le24$，$x_1+2x_2\le6$。
  - 頂點與目標值：$(0,0)\to0$；$(4,0)\to20$；$(3,1.5)\to21$；$(0,3)\to12$。
  - 最優解 $(3,1.5)$，$Z=21$。
- **Example B**：$\min 2x_1+3x_2$，$x_1+x_2\ge10$，$x_1\le6$，$x_2\le8$。
  - 頂點與目標值：$(2,8)\to28$；$(6,8)\to36$；$(6,4)\to24$。
  - 最優解 $(6,4)$，$Z=24$。

### 容易混淆
- **可行域無界時仍可能有最優解**：T1 Q12 是 min 問題，目標在所有無界方向都增加，所以仍有最小值。
- **redundant 約束不影響可行域**：T1 Q13 的 $x\le12$ 已被 $x+y\le10$ 蘊含。
- **可行域可能只剩一點**：T1 Q14 中，成對的 $\le$、$\ge$ 約束等價於兩條等式。

### 關聯
圖解法只適用於兩個變數，它的「角落 + 邊」概念在主題 3–4 推廣到 $n$ 維。

---

## 主題 3 CPF（L2 p16–33）

### 直覺
二維時，角落是兩條邊界線的交點；三維時，角落是三面牆的交點，就像房間的牆角是兩面牆加天花板（L2 p17）。推廣到 $n$ 維：$n$ 個彼此獨立的邊界在一點交會，那一點就是角落。

### 定義〔講義 L2 p21–25〕
把所有約束寫成不等式形式 $a_i^Tx\le b_i$，$i=1,\dots,m$。非負限制也算在內，寫成 $-x_j\le0$。

| 名詞 | 定義 |
|---|---|
| constraint boundary | $\{x:a_i^Tx=b_i\}$ |
| active at $\tilde x$ | $a_i^T\tilde x=b_i$ |
| CPF solution | $n$ 條 constraint boundary 交於一點，且該點可行 |
| defining equations | 決定 CPF 的 $n$ 條獨立 active 等式 |

### 判斷 CPF 的三步〔講義 L2 p24、p33〕
1. 檢查可行：每一條約束都成立。
2. 代入每一條約束，找出所有 active 約束。
3. 若 active 約束組成的方程組有**唯一解**，就是 CPF；否則不是。

### 為什麼需要 $n$ 條，而且要獨立〔補充〕
- $n$ 個未知數的線性方程組 $Mx=b_I$ 有唯一解，等價於 $\operatorname{rank}(M)=n$。
- 少於 $n$ 條時秩必定小於 $n$，所以有自由度，點可以沿某方向滑動，不是角落。
- 多於 $n$ 條但秩為 $n$ 時仍有唯一解：這是 **degenerate** 的 CPF〔講義 L2 p19、p32〕。

### 範例〔講義 L2 p26–32〕
Wyndor 二維：$x_D\le4$、$2x_W\le12$、$3x_D+2x_W\le18$、$x\ge0$。

| 點 | 判斷 | 原因 |
|---|---|---|
| $(2,6)$ | CPF | active：$2x_W=12$、$3x_D+2x_W=18$，唯一解 |
| $(4,6)$ | 不是 | $3(4)+2(6)=24>18$，不可行 |
| $(4,1)$ | 不是 | 只有 $x_D=4$ 一條 active，$x_W$ 仍自由 |

三維 Wyndor：$x_D+2x_T\le4$（P1）、$2x_W+6x_T\le12$（P2）、$3x_D+2x_W+9x_T\le18$（P3）、$x\ge0$。

| 點 | 判斷 | 原因 |
|---|---|---|
| $(4,3,0)$ | CPF | active：P1、P3、$x_T=0$ |
| $(2,2,0)$ | 不是 | 只有 $x_T=0$ 一條 active |
| $(0,0,2)$ | degenerate CPF | 5 條 active：P1、P2、P3、$x_D=0$、$x_W=0$ |

### 容易混淆（不是 CPF 的三種失敗方式）

| 失敗方式 | 例子 |
|---|---|
| 不可行 | T2 Q7 的 $(3,3,3)$：active 約束有唯一交點，但違反 $x_1+x_2+x_3\le5$ |
| active 太少 | L2 p28 的 $(4,1)$ |
| active 夠多但不獨立 | T2 Q1(b)：4 條 active 交出一條直線 |

### 關聯
主題 5 會證明：CPF 等價於 augmented form 的 BFS，active 約束對應到取值為 0 的變數。

---

## 主題 4 Edge、Improving Edge、Adjacent CPF（L2 p36–70）

### 直覺
站在一個角落，沿著稜線走：
- 稜線往上（目標變好），就走到下一個角落。
- 所有稜線都往下，這裡就是山頂（最優）。
- 若有一條往上的稜線永遠走不完，LP 就是 unbounded。

### 定義〔講義 L2 p38、p47、p56〕

| 名詞 | 定義 |
|---|---|
| edge | $n-1$ 條 constraint boundary 交出一條直線，該直線上可行的那一段 |
| improving edge | 沿著它走，目標值會變好 |
| adjacent CPF | 兩個 CPF 是同一條 edge 的兩端；等價於共用 $n-1$ 條 defining equations |

### 公式〔補充：向量寫法；講義寫法是選某個變數當參數〕
設 $\bar x$ 是非退化 CPF，active 指標集為 $I$，$|I|=n$。從 $I$ 中拿掉一條約束 $k$：

| 量 | 公式 | 說明 |
|---|---|---|
| 方向 $d$ | $a_i^Td=0$（$i\in I\setminus\{k\}$），且 $a_k^Td<0$ | 保持其餘 $n-1$ 條 active，往約束 $k$ 的可行側走 |
| 最遠步長 | $t_{\max}=\min\Big\{\dfrac{b_i-a_i^T\bar x}{a_i^Td}:\ i\notin I,\ a_i^Td>0\Big\}$ | 第一個撞到的 inactive 約束 |
| 目標沿 edge 的變化 | $Z(t)=c^T\bar x+t\,c^Td$ | 斜率為 $c^Td$ |

- **improving 的條件**：max 問題 $c^Td>0$；min 問題 $c^Td<0$。
- **找不到 $a_i^Td>0$ 的約束**：這條 edge 是無界射線。若它同時是 improving，LP 就是 unbounded（L2 p63–64）。

### 推導〔補充〕
1. **方向是唯一的。** $n-1$ 條線性獨立的齊次方程、$n$ 個未知數，解空間是一維，所以 $d$ 只差一個倍數。沿 $x(t)=\bar x+td$ 走時，這 $n-1$ 條約束一直保持 active。這就是「$n-1$ 條邊界交出一條直線」。
2. **方向的正負。** 被拿掉的約束仍要成立：
$$a_k^T(\bar x+td)=b_k+t\,a_k^Td\le b_k.$$
   因為 $a_k$ 與其他 $n-1$ 個 $a_i$ 獨立，$a_k^Td\neq0$。規定 $t\ge0$，就必須 $a_k^Td<0$。講義說「用剩下的 active 約束決定方向」〔L2 p45 第 3 點〕，指的就是這一步。
3. **步長。** 對 inactive 的約束 $i$，原本的 slack 為 $b_i-a_i^T\bar x>0$。
   - 若 $a_i^Td\le0$：$t$ 越大，這條約束越寬鬆，永遠擋不住。
   - 若 $a_i^Td>0$：在 $t_i=\dfrac{b_i-a_i^T\bar x}{a_i^Td}$ 時撞上邊界。
   - 取最小的 $t_i$，就得到最先撞上的牆。這和主題 6 的 minimum ratio test 是同一件事。
4. **斜率。** $Z(t)=c^T\bar x+t\,c^Td$ 是 $t$ 的一次函數，所以只要看斜率的正負，不必比較端點。
5. **沒有 improving edge 就是最優**（非退化情形）。
   - 拿掉每一條 $k\in I$ 各得一個方向 $d^{(k)}$，這 $n$ 個方向線性獨立。
   - 任取可行點 $x$，可寫成 $x-\bar x=\sum_k\lambda_kd^{(k)}$。
   - 對每個 $k\in I$：$a_k^T(x-\bar x)=a_k^Tx-b_k\le0$。而左式等於 $\lambda_ka_k^Td^{(k)}$（因為 $a_k^Td^{(j)}=0$，$j\ne k$），且 $a_k^Td^{(k)}<0$，所以 $\lambda_k\ge0$。
   - 因此 $c^Tx-c^T\bar x=\sum_k\lambda_k\,c^Td^{(k)}\le0$，即沒有可行點比 $\bar x$ 更好。
   - 退化情形要改用主題 6 的 reduced cost 證明。

### 講義的五步做法〔講義 L2 p60、p70〕
1. 用 $n-1$ 條 defining boundaries 寫出 edge 的參數式。
2. 把參數式代入其他所有約束並化簡。
3. 用剩下的 active 約束決定前進方向。
4. 沿前進方向，找出最先碰到的 inactive 邊界。
5. 那個交點就是 adjacent CPF。

### 範例〔講義 L2 p65–69〕
題目：$\max 5x_1+4x_2+3x_3$，約束為 $2x_1+3x_2+x_3\le5$（C1）、$4x_1+x_2+2x_3\le11$（C2）、$3x_1+4x_2+2x_3\le8$（C3）、$x\ge0$。檢查點 $(2,0,1)$。

- active：C1、C3、$x_2=0$，剛好 3 條，是非退化 CPF，$Z=13$。

| 保留 | 參數式 | 方向 | 端點 | $Z(t)$ | improving？ |
|---|---|---|---|---|---|
| C1、C3 | $(2-2t,\ t,\ 1+t)$ | $x_2\ge0\Rightarrow t\uparrow$ | $x_1\ge0$ 擋住：$(0,1,2)$ | $13-3t$ | 否 |
| C1、$x_2=0$ | $(s,\ 0,\ 5-2s)$ | C3 給出 $s\ge2$，$s\uparrow$ | $x_3\ge0$ 擋住：$(2.5,0,0)$ | $15-s$ | 否 |
| C3、$x_2=0$ | $(s,\ 0,\ \tfrac{8-3s}2)$ | C1 給出 $s\le2$，$s\downarrow$ | $x_1\ge0$ 擋住：$(0,0,4)$ | $12+\tfrac s2$ | 否 |

三條都不是 improving，所以 $(2,0,1)$ 是最優解，$Z^*=13$。

### 退化 CPF〔講義 L2 p44；T2 Q5〕
若 active 有 $p>n$ 條，要檢查 $\binom{p}{n-1}$ 組，會遇到兩種特殊情況：
- 有些組合的直線被其他 active 約束夾成單一點：這是退化 edge，不算（T2 Q5 Pair 3）。
- 有些組合交出同一條線：只算一條（T2 Q5 Pairs 4–6）。

### 容易混淆
- **方向不能憑直覺**，一定要代入剩下的 active 約束。
- **斜率為 0 不算 improving**（T2 Q5 Pairs 4–6）。
- **非負限制也是約束**：
  - 它可以是 active（決定 edge）。
  - 也可以是擋住 edge 的那面牆（T2 Q4 Pair 3、T2 Q5 全部）。
- **題目沒寫 $x\ge0$ 時不能自己加**：T2 Q2、Q3、Q6、Q8 沒有非負限制，edge 可以走到負值。

### 關聯
主題 5 把「保留 $n-1$ 條 active」翻成「讓一個非基本變數離開 0」；主題 6 把「斜率」翻成 reduced cost，「步長」翻成 minimum ratio test。

---

## 主題 5 SEF、Augmented Form、BFS（L3）

### 直覺
畫圖在高維行不通，要改用純代數。技巧是給每條不等式加一個 slack 變數，代表「離那面牆還有多遠」。這樣「貼在牆上」就變成「slack 等於 0」，角落就變成「有 $n$ 個變數等於 0，其餘變數由方程組唯一決定」。

### 定義〔講義 L3 p7–17、p31–35〕

| 名詞 | 定義 |
|---|---|
| SIF（standard inequality form） | 只有不等式約束，且所有變數 $\ge0$ |
| SEF（standard equality form） | $\max c^Tx$ s.t. $Ax=b,\ x\ge0$；唯一的不等式是非負限制 |
| augmented form | 把 SIF 的 $a^Tx\le b$ 寫成 $a^Tx+s=b$，$s\ge0$ |
| augmented solution | 原解加上 slack 值 $s=b-a^T\tilde x$ |
| basis $J_B$ | 一組 $m$ 個變數；其餘 $n-m$ 個設為 0 後，方程組有唯一解 |
| basic coefficient matrix $B$ | $A$ 中對應 $J_B$ 的那幾欄；$J_B$ 是 basis ⇔ $B$ 可逆 |
| basic solution | 由 basis 決定的那組解 |
| BFS | basic solution 且所有分量 $\ge0$ |
| feasible basis | 決定出 BFS 的 basis |
| adjacent bases | 兩個 basis 只差一個變數 |
| adjacent BFS | 由 adjacent feasible bases 決定的兩個 BFS |

### 定理〔講義 L3 p23、p46〕
- 一個 SIF 的解是 CPF ⇔ 它的 augmented solution 是 augmented form 的 BFS。
- 兩個 CPF 相鄰 ⇔ 它們的 augmented solution 是由 adjacent bases 決定的 BFS。

### 推導〔講義 L3 p24–26，optional；以下為整理〕
1. **active 對應到「變數為 0」。**
   - 函數約束 $i$ active ⇔ $s_i=b_i-a_i^T\tilde x=0$。
   - 非負約束 $x_j\ge0$ active ⇔ $x_j=0$。
2. **CPF 對應到 basis。**
   - CPF 有 $n$ 條獨立 active 約束，對應到 augmented form 中有 $n$ 個變數為 0（這裡的 $n$ 是原變數個數）。
   - 把這 $n$ 個變數設為 0 後，剩下 $m$ 個變數由 $m$ 條方程唯一決定，這正是 basis 的定義。
   - 可行性在兩種表示中是同一件事，所以 CPF 對應到 BFS。
3. **相鄰對應到只差一個變數。**
   - 兩個 CPF 共用 $n-1$ 條 active 約束 ⇔ 非基本變數集合共用 $n-1$ 個。
   - 非基本集合只差一個 ⇔ 基本集合也只差一個（L3 p49 的計數論證）。

### 判斷方法〔講義 L3 p42〕
- **一組變數是不是 basis**：把其他變數設為 0，檢查剩下的方程組是否有唯一解（可用 ERO 消去）。
- **一個解是不是 basic solution**：取包含所有非零變數的 $m$ 個變數組合逐一檢查；只要有一組是 basis，它就是 basic solution。

### 範例〔講義 L3 p36–41〕
系統：$x_1+2x_2-x_3=4$，$x_1+x_2+x_4=3$，$x_2-x_3=1$。

| 候選 | 結果 | 原因 |
|---|---|---|
| $\{x_1,x_2,x_4\}$ | feasible basis | 解出 $(2,1,0,0)$，全部 $\ge0$ |
| $\{x_1,x_2,x_3\}$ | 不是 basis | 方程組有一條多餘，沒有唯一解 |
| $\{x_1,x_3,x_4\}$ | basis 但不可行 | 解出 $x_3=-1<0$ |

二維 Wyndor 的 $(4,6)$：
- basis $\{x_D,x_W,s_3\}$ 解出 $s_3=-6$，是 basis 但不可行。
- 對應到幾何上的「角落但不可行」（corner-point infeasible）。

### 由 BFS 寫出 edges〔講義 L3 p55–59〕
1. 用 ERO 把基本變數寫成非基本變數的函數。
2. 每次讓一個非基本變數自由增加，其他非基本變數保持 0。

以 BFS $(4,3,0,0,6,0)$、basis $\{x_D,x_W,s_2\}$ 為例：
$$x_D=4-2x_L-s_1,\qquad x_W=3-1.5x_L+1.5s_1-0.5s_3,\qquad s_2=6-3x_L-3s_1+s_3.$$

以 $s_1$ 為自由變數：
- $x_D=4-s_1\ge0\Rightarrow s_1\le4$。
- $x_W=3+1.5s_1$ 隨 $s_1$ 增加，永遠不會變負，沒有限制。
- $s_2=6-3s_1\ge0\Rightarrow s_1\le2$。

取最小者，在 $s_1=2$ 停下，得到 $(2,6,0)$。

### 容易混淆
- **degenerate BFS 對應到不只一個 basis**：T3 Q5 的 $(2,0,4,0,0,0)$ 有 4 個 basis。
- **adjacent 沒有遞移性**：T3 Q3(c) 中，A 與 B 相鄰、B 與 C 相鄰，但 A 與 C 不相鄰。
- **basis 一定要用「唯一解」判斷**：T3 Q7(a) 中，$x_5$ 的欄等於 $x_1$ 欄加 $x_3$ 欄，三欄線性相依，所以不是 basis。

### 關聯
basis 是主題 6–9 所有演算法的「狀態」。主題 12 的 complementary basis 也建立在這裡的配對上。

---
## 主題 6 代數 Simplex（L4）

### 直覺
主題 4 找 improving edge 時，要把每條 edge 都畫出來、代入目標。主題 5 告訴我們：從一個 BFS 出發的 edge，就是「讓某個非基本變數從 0 開始增加」。所以只要把目標 $z$ 也寫成非基本變數的函數，$x_{N_j}$ 的係數就是沿那條 edge 的斜率。這個係數叫做 reduced cost。

### 定義與符號〔講義 L4 p12–13、p17、p31〕
在 basis $J_B$ 下，把目標和每個基本變數都寫成非基本變數的函數：
$$z=\bar v+\sum_j\bar c_{N_j}x_{N_j},\qquad x_{B_i}=\bar b_{B_i}-\sum_j\bar a_{B_i,N_j}x_{N_j}.$$

| 記號 | 意義 |
|---|---|
| 上橫線 | 「目前」的值：消去基本變數後的係數，會隨 basis 改變；原始資料 $a_{ij},b_i,c_j$ 不變 |
| $\bar c_{N_j}$ | reduced cost；基本變數的 reduced cost 定義為 0 |
| $\bar v$ | 目前 BFS 的目標值 |
| entering variable | 被選中從 0 開始增加的非基本變數 $x_{N_k}$ |
| leaving variable | 在 entering 增加時最先降到 0 的基本變數 $x_{B_r}$ |

### 公式與適用條件（max 問題、SEF、feasible basis）

| 用途 | 公式或判準 |
|---|---|
| improving edge | $\bar c_{N_j}>0$ |
| optimality test | 所有 $\bar c_{N_j}\le0$ ⇒ 目前 BFS 最優（充分條件，逆命題不成立） |
| optimal basis | feasible，且所有 $\bar c\le0$ |
| minimum ratio test | $t=\dfrac{\bar b_{B_r}}{\bar a_{B_r,N_k}}=\min\Big\{\dfrac{\bar b_{B_i}}{\bar a_{B_i,N_k}}:\ \bar a_{B_i,N_k}>0\Big\}$ |
| unbounded | $\bar c_{N_k}>0$，但它這一欄所有 $\bar a_{B_i,N_k}\le0$ |
| 目標增量 | $\Delta z=\bar c_{N_k}\cdot t$ |

**min 問題**〔手寫 L4 p14、p22〕：符號全部反過來。$\bar c<0$ 為 improving；所有 $\bar c\ge0$ 為最優。

### 推導

**(1) 為什麼 $\bar c_{N_j}$ 是沿 edge 的斜率**〔講義 L4 p14〕
沿著 $x_{N_j}$ 的 edge 走時，其他非基本變數都保持 0，所以 $z=\bar v+\bar c_{N_j}x_{N_j}$。$x_{N_j}$ 每增加 1 單位，$z$ 就改變 $\bar c_{N_j}$。

**(2) Optimality test 的證明**〔講義 L4 p20–21〕
- 設 $x^*$ 是由 $J_B$ 決定的 BFS，且所有 $\bar c_{N_j}\le0$。任取一個可行解 $\bar x$。
- $\bar x$ 滿足所有等式，而「$z=\bar v+\sum\bar c_{N_j}x_{N_j}$」是由等式推出來的，所以對 $\bar x$ 也成立：
$$\bar z=\bar v+\sum_j\bar c_{N_j}\bar x_{N_j}.$$
- $x^*$ 的非基本變數全為 0，所以 $z^*=\bar v$。
- $\bar x$ 可行，所以 $\bar x_{N_j}\ge0$；又 $\bar c_{N_j}\le0$，每一項都 $\le0$。因此 $\bar z\le\bar v=z^*$。
- $\bar x$ 是任意可行解，所以 $x^*$ 最優。∎

逆命題不成立〔講義 L4 p19〕：退化時，同一個最優 BFS 可能由某個「有正 reduced cost」的 basis 決定。〔手寫 L4 p19〕但一定存在另一個 basis 使所有 $\bar c\le0$。

**(3) Minimum ratio test**〔講義 L4 p30–32；手寫 L4 p33〕
- 讓 $x_{N_k}$ 增加、其他非基本變數保持 0，則 $x_{B_i}=\bar b_{B_i}-\bar a_{B_i,N_k}x_{N_k}$。
- 若 $\bar a_{B_i,N_k}\le0$：$x_{B_i}$ 不會減少，永遠 $\ge0$，不限制 $x_{N_k}$。
- 若 $\bar a_{B_i,N_k}>0$：$x_{B_i}$ 會減少，在 $x_{N_k}=\bar b_{B_i}/\bar a_{B_i,N_k}$ 時降到 0。
- 為了讓所有基本變數都保持 $\ge0$，只能增加到這些比值中最小的那一個；達到最小值的那個基本變數就是 leaving variable。

**(4) Unbounded 的證明**〔講義 L4 p43〕
- 設 $\bar c_{N_k}>0$，且所有 $\bar a_{B_i,N_k}\le0$。
- 對 $l=0,1,2,\dots$，令 $x_{N_k}=l$、其他非基本變數為 0、$x_{B_i}=\bar b_{B_i}-\bar a_{B_i,N_k}\,l\ge\bar b_{B_i}\ge0$。
- 每個點都可行，而目標 $z(l)=\bar v+\bar c_{N_k}\,l\to\infty$，所以 LP unbounded。∎

**(5) Pivot：換基底**〔講義 L4 p49〕
- 用 leaving variable 那一列解出 entering variable：
$$x_{N_k}=\frac{\bar b_{B_r}}{\bar a_{B_r,N_k}}-\frac{1}{\bar a_{B_r,N_k}}x_{B_r}-\sum_{j\ne k}\frac{\bar a_{B_r,N_j}}{\bar a_{B_r,N_k}}x_{N_j}.$$
- 把它代入其他所有列和 $z$，消去 $x_{N_k}$，就得到新 basis $(J_B\cup\{x_{N_k}\})\setminus\{x_{B_r}\}$ 下的系統。

**(6) 為什麼會終止**〔講義 L4 p50〕
- 每次迭代 $z$ 嚴格增加，或者在退化時不變。
- basis 只有有限多個。
- 所以只要不發生 cycling（見主題 7），一定會停在 optimal 或 unbounded。

### 五步演算法〔講義 L4 p51〕
1. **初始**：取一個 feasible basis，把 $z$ 和基本變數寫成非基本變數的函數。
2. **entering**：找 $\bar c>0$ 的非基本變數；沒有就停，目前解最優。
3. **leaving**：做 MRT；欄中沒有正係數就停，LP unbounded。
4. **pivot**：用 leaving 那一列解出 entering，代入其他列。
5. **重複**：回到第 2 步。

### 範例

**例 1：同一系統、兩個目標**〔講義 L4 p23–27〕
basis $\{x_1,x_2,x_4\}$ 決定 BFS $(0,2,0,6,0,0)$。

| 目標 | 化簡後 | 結論 |
|---|---|---|
| A：$z=3x_1+x_2+2x_3$ | $z=2-x_3-1.4x_5+0.8x_6$ | $\bar c_6=0.8>0$，$x_6$ 進入，還不是最優 |
| B：$z=x_1+4x_2+x_3$ | $z=8+0x_3-1.2x_5-0.1x_6$ | 所有 $\bar c\le0$，最優，$z=8$ |

**例 2：Wyndor 三維**〔講義 L4 p54–62〕
$\max 3x_D+5x_W+16x_L$，約束 $x_D+2x_L+s_1=4$、$2x_W+6x_L+s_2=12$、$3x_D+2x_W+9x_L+s_3=18$。

| 迭代 | 基底 | 目標式 | 動作 |
|---|---|---|---|
| 0 | $\{s_1,s_2,s_3\}$ | $z=3x_D+5x_W+16x_L$ | 選 $x_W$ 進入；ratio：$12/2=6$、$18/2=9$ → $s_2$ 離開 |
| 1 | $\{x_W,s_1,s_3\}$ | $z=30+3x_D+x_L-2.5s_2$ | 選 $x_D$ 進入；ratio：$4/1$、$6/3=2$ → $s_3$ 離開 |
| 2 | $\{s_1,x_W,x_D\}$ | $z=36-s_3-1.5s_2-2x_L$ | 所有 $\bar c\le0$，最優 $(2,6,0)$，$z=36$ |

〔手寫 L4 p55〕$x_L$ 的 reduced cost 最大（16），本來是最自然的選擇；這裡改選 $x_W$，是為了示範任何 $\bar c>0$ 的變數都可以進入。

**例 3：Unbounded**〔講義 L4 p38–41〕
$\max 4x_1-x_2+8x_4$，basis $\{x_1,x_3\}$：
$$z=16+7x_2+4x_4,\qquad x_1=4+2x_2-x_4,\qquad x_3=15+5x_2-3x_4.$$
讓 $x_2$ 進入：$x_1$、$x_3$ 中 $x_2$ 的係數都是正的，兩者只增不減，沒有 leaving variable。所以 LP unbounded。

### 容易混淆
- **兩種表示法的符號不同。**
  - 代數式寫成 $x_{B_i}=\bar b-\bar a\,x_N$，MRT 要找 $\bar a>0$（即「代數式中係數為負」）。
  - 〔講義 L4 p39〕「a valid candidate needs a NEGATIVE coefficient」指的是代數式 $x_1=4+2x_2-\dots$ 裡的係數。
  - tableau 與代數式差一個負號，兩種說法不要混用。
- **任何 $\bar c>0$ 的變數都能進入**，不一定要選最大的（L4 p56）。
- **退化 pivot 時 $t=0$**：$z$ 不變，但 basis 換了（T4 Q2）。

### 關聯
主題 7 把這套代數寫成表格；主題 9 用 $B^{-1}$ 一次算出所有 $\bar c$；主題 12 證明 $-\bar c$ 正是對偶 slack。

---

## 主題 7 Tableau、Tie-Breaking、Cycling（L5）

### 直覺
每次迭代都重寫整個代數系統太容易出錯。tableau 只記係數、不寫變數名稱，pivot 就變成固定的列運算（Gauss–Jordan）。

### Tableau 結構〔講義 L5 p6–9〕

| 部分 | 內容 |
|---|---|
| z-row（第一列） | $z-\sum\bar c_{N_j}x_{N_j}=\bar v$，所以非基本欄存的是 $-\bar c_{N_j}$，RHS 存的是 $\bar v$ |
| constraint rows | 每列 $x_{B_i}+\sum\bar a_{B_i,N_j}x_{N_j}=\bar b_{B_i}$ |
| basic column | 只有一個 1、其餘為 0 的單位向量欄；所有 basic columns 合起來是單位矩陣 |

| 判斷 | 條件 |
|---|---|
| feasible tableau | 所有 RHS $\ge0$（z-row 的 RHS 不算） |
| optimal tableau（max） | feasible，且 z-row 所有項 $\ge0$ |
| optimal tableau（min） | feasible，且 z-row 所有項 $\le0$〔L5 p9 手寫；L6 p20〕 |

### Pivot 公式〔講義 L5 p19〕
設 entering 欄為 $k$、leaving 列為 $r$，pivot element 為 $\bar a_{B_r,N_k}$。

| 列 | 運算 |
|---|---|
| pivot row | $\text{row}_r\leftarrow\dfrac{1}{\bar a_{B_r,N_k}}\,\text{row}_r$ |
| z-row | $\text{z-row}\leftarrow\text{z-row}+\dfrac{\bar c_{N_k}}{\bar a_{B_r,N_k}}\,\text{row}_r$ |
| 其他列 $i\ne r$ | $\text{row}_i\leftarrow\text{row}_i-\dfrac{\bar a_{B_i,N_k}}{\bar a_{B_r,N_k}}\,\text{row}_r$ |

每條公式用的都是 **pivot 之前** 的 pivot row。

**推導**〔補充〕：pivot 的目標是讓第 $k$ 欄變成單位向量 $e_r$。
- 第 $r$ 列除以 pivot element，使該位置變成 1。
- 其他列減去適當倍數的第 $r$ 列，使第 $k$ 欄其他位置變成 0。z-row 該位置原本是 $-\bar c_{N_k}$，所以加上 $\bar c_{N_k}/\bar a_{B_r,N_k}$ 倍。
- ERO 不改變方程組的解集〔講義 L4 p70〕，所以新 tableau 描述的是同一個 LP，只是換成新的 basis。

### Tie-breaking 規則〔講義 L5 p33–38〕

| 規則 | 選法 | 優點 | 缺點 |
|---|---|---|---|
| Largest coefficient | reduced cost 最大者（z-row 最負者） | 直覺、容易執行 | 受約束的縮放（單位）影響 |
| Smallest subscript | 下標最小、$\bar c>0$ 者 | 最容易執行，方便分析 | 完全不管改善多少 |
| Largest improvement | $\bar c_{N_k}\cdot t$ 最大者 | 直接最佳化目標的增量，不受縮放影響 | 每個候選都要先做 MRT |

**Bland's rule**：進入與離開都用 smallest subscript 打破平手，保證不會 cycling〔講義 L5 p48〕。

〔手寫 L5 p36〕$t$ 就是 entering variable 的新值，所以增量 $\Delta z=\bar c_{N_k}\cdot t$。

**例**〔講義 L5 p37–38〕：基底 $\{x_1,x_5\}$，候選 $x_2$、$x_4$、$x_6$。

| 候選 | $\bar c$ | $t$ | $\Delta z$ |
|---|---|---|---|
| $x_2$ | 3 | $\min\{3/1,\ 2/4\}=1/2$ | 1.5 |
| $x_4$ | 4 | $3/8$ | 1.5 |
| $x_6$ | 1 | $\min\{3/1,\ 2/1\}=2$ | 2 |

- smallest subscript 選 $x_2$。
- largest coefficient 選 $x_4$。
- largest improvement 選 $x_6$：它的 $\bar c$ 最小，但改善最多。

### Degeneracy 與 cycling〔講義 L5 p41–47〕

| 名詞 | 定義 |
|---|---|
| cycling | 連續迭代的 feasible bases 重複出現；目標值與 BFS 都不變 |
| degenerate iteration | 目標值沒有改變的 pivot |
| degenerate basic solution | 至少有一個基本變數等於 0 |
| degenerate basis | 決定出 degenerate basic solution 的 basis |

**邏輯鏈**：cycling ⇒ degenerate iteration ⇒ degenerate basic solution ⇔ degenerate basis。

**推導**〔講義 L5 p42；手寫〕
- $\Delta z=t\cdot\bar c_{N_k}$，而 $\bar c_{N_k}>0$。
- 所以 $\Delta z=0$ ⇔ $t=0$ ⇔ $\bar b_{B_r}/\bar a_{B_r,N_k}=0$（因為 $\bar a_{B_r,N_k}>0$）⇔ $\bar b_{B_r}=0$。
- 也就是說，leaving variable 在目前的 BFS 中就已經等於 0，這個 basis 是退化的。

**有限終止定理**〔講義 L5 p47〕：simplex 若從未遇到 degenerate basis，必在有限步內停止。
- 證明：沒有退化 ⇒ 每次 $\Delta z>0$ ⇒ basis 不會重複 ⇒ basis 只有有限個 ⇒ 有限步停止。

**例**〔講義 L5 p44–46〕：Beale (1955) 的例子在 largest coefficient rule 下會循環。BFS 一直停在 $(0,0,0,0,0,0,1)$，$z=17$ 始終不變。

### 範例：Wyndor tableau〔講義 L5 p22–29〕
起始基底 $\{s_1,s_2,s_3\}$，z-row 為 $(-3,-5,-16,0,0,0\mid0)$。

| 迭代 | 進入 | ratio | 離開 | 新 z-row |
|---|---|---|---|---|
| 1 | $x_W$ | $12/2=6$、$18/2=9$ | $s_2$ | $(-3,0,-1,0,\tfrac52,0\mid30)$ |
| 2 | $x_D$ | $4/1=4$、$6/3=2$ | $s_3$ | $(0,0,2,0,\tfrac32,1\mid36)$ |

z-row 沒有負數，最優解 $(2,6,0)$，$z=36$。

### 容易混淆
- **z-row 存的是 $-\bar c$**：max 問題選「z-row 負數」進入，min 問題選「z-row 正數」進入。
- **同一張 tableau 在 max 與 min 下結論不同**（L5 p11–12）。
- **MRT 只看 pivot 欄中的正數**，0 和負數都排除。RHS 為 0、pivot 欄為正時，比值 $0/2=0$ 是合法的（T5 Q3(b)），這次 pivot 就是退化的。
- **每列一定要有一個基本變數的單位欄**：若某個基本欄不是單位向量，代表 pivot 算錯了〔講義 L6 p58〕。

### 關聯
主題 8 的 Phase 1 用同一套 tableau（但是 min 問題）；主題 9 證明 tableau 的每一欄都等於 $B^{-1}a_j$。

---
## 主題 8 Two-Phase Simplex（L6；L8 Part 1）

### 直覺
simplex 必須從一個 feasible basis 出發。若所有約束都是 $\le$ 且 $b\ge0$，slack 本身就是起點。但遇到 $\ge$、$=$ 或負的 RHS，就沒有現成的起點。

two-phase 的做法：
- **Phase 1**：先加「人工」變數，暫時讓起點存在；接著用 simplex 把人工變數全部壓到 0。壓得到 0 就得到原問題的可行基底；壓不到 0，原問題就不可行。
- **Phase 2**：從得到的可行基底出發，換回原本的目標函數繼續 simplex。

### 轉成 SEF〔講義 L6 p7–10、p55〕

| 原形式 | 轉換 |
|---|---|
| $a^Tx\le b$ | $a^Tx+s=b$，$s\ge0$（slack） |
| $a^Tx\ge b$ | $a^Tx-s=b$，$s\ge0$（surplus） |
| $x_j$ 沒有符號限制（free） | $x_j=x_j^+-x_j^-$，$x_j^\pm\ge0$ |

$a^+=\max(a,0)$、$a^-=\max(-a,0)$，所以 $a=a^+-a^-$〔講義 L6 p9〕。〔手寫〕例如 $a=5$ 時 $a^+=5$、$a^-=0$；$a=-7$ 時 $a^+=0$、$a^-=7$。

### 建 artificial problem 的三條規則〔講義 L6 p14〕
逐條檢查每一個等式約束：
1. 若有某個變數**只出現在這一條**約束中，可把它當成這條約束的 slack。
2. 若這個變數的係數與 RHS **同號**，就不需要加 artificial（必要時先把整列縮放，使其係數變成 $\pm1$〔L6 p17 把第 2 列乘 1/2〕）。
3. 否則加入一個新的非負 artificial variable，係數取 $\pm1$，符號與 RHS 相同。

新的目標：$\min\sum w_i$。

〔手寫 L6 p14〕目的是讓每條約束都有一個「係數與 RHS 同號」的 slack 型變數，這樣把它們當基底時，基本變數的值都 $\ge0$。

### 定理與推導

**(1) 原 LP 可行 ⇔ artificial problem 的最優值為 0**〔講義 L6 p26；T6 Q5 證明〕
- (⇒) 設 $\bar x\ge0$ 滿足 $A\bar x=b$。令 $w=0$，則 $(\bar x,0)$ 對 artificial problem 可行，目標值為 0。又因為 $w\ge0$，目標 $\sum w_i\ge0$，0 已是下界，所以最優值就是 0。
- (⇐) 最優解滿足 $\sum w_i=0$ 且每個 $w_i\ge0$，所以每個 $w_i=0$。代回約束，$x$ 部分正好滿足原問題的所有約束。
- 逆否命題：最優值 $>0$ ⇔ 原 LP 不可行。

**(2) Phase 1 結束時殘留的 artificial 一定等於 0**〔講義 L6 p31〕
- 最優值 $0=\sum w_i$，每項非負，所以每個 $w_i=0$，包括仍在基底中的那個。

**(3) 殘留的 artificial 為什麼可以換掉**〔講義 L6 p32；L8 p10〕
- 殘留的 $w$ 雖然是基本變數，但值為 0，所以它的非負約束是 active 的，和非基本變數一樣。
- 因此可以拿它和某個非基本變數交換，只要新的組合仍是 basis，也就是 pivot element 不為 0。
- **作法**：在 $w$ 那一列找任一個係數 $\ne0$ 的非基本原變數（正負都可以），以它為 pivot。
- 因為 RHS 是 0，這是退化 pivot：$t=0$，所有變數的值都不變。
- revised 版本：該列係數 $\bar a_{B_r,N_j}=(B^{-1}\text{ 的第 }r\text{ 列})\cdot a_{N_j}$。

**(4) Fundamental Theorem of LP**〔講義 L6 p52–54〕
- 若 LP 可行且不是 unbounded，則它有最優解；若 LP 是 SEF，則有一個最優解是 BFS。
- 證明：任何 LP 都能轉成 SEF。Phase 1（用 Bland）會在有限步內判定不可行，或給出一個 BFS。Phase 2（用 Bland）會在有限步內判定 unbounded，或給出最優 BFS。兩階段的每種結局都恰好對應定理的一種情況。

### Phase 1 的 z-row〔講義 L6 p18–20；FE Q3〕
- 目標 $W=\sum w_i$。$w_i$ 是基本變數，要先把 $W$ 寫成非基本變數的函數：$W=\sum(\text{各 artificial 列})$。
- 實作上，**z-row 的係數 = 含 artificial 的各列係數相加**（artificial 欄設為 0），RHS = 這些列的 RHS 相加。
- 這是 min 問題：z-row 為**正**的變數進入；z-row 全部 $\le0$ 就是最優。

### 範例〔講義 L6 p43–49〕
$\max 2x_1-7x_2+4x_3+3x_4+x_5$，約束：
- $-x_1+5x_2-x_4=9$
- $x_1+x_2-2x_3+2x_5=3$
- $4x_1-x_3=-1$

**建 artificial problem**
| 列 | 判斷 | 處理 |
|---|---|---|
| 第 1 列 | $x_4$ 只出現一次，但係數 $-1$ 與 RHS $9$ 異號 | 加 $w_2$ |
| 第 2 列 | 乘 $\tfrac12$ 後 $x_5$ 係數為 $+1$，與 RHS 同號 | 當 slack，不用加 |
| 第 3 列 | 先乘 $-1$ 變成 $-4x_1+x_3=1$，沒有可用的 slack | 加 $w_1$ |

**Phase 1**（z-row 正數進入）
- 初始 z-row：$(-5,5,1,-1,0\mid10)$。
- $x_2$ 進入：ratio 為 $w_2$ 列 $9/5$、$x_5$ 列 $3$ → $w_2$ 離開。
- $x_3$ 進入：只有 $w_1$ 列可用 → $w_1$ 離開。
- Phase 1 最優值 0，基底 $\{x_2,x_5,x_3\}$。

**Phase 2**
- 代回原目標後 z-row 為 $(-20,0,0,-\tfrac32,0\mid-7)$。
- 選 $x_1$ 進入：它這一欄的係數 $-\tfrac15$、$-\tfrac{17}5$、$-4$ 全部為負，沒有 leaving variable。
- 所以 LP **unbounded**。
- 直接驗證：令 $x_1=t$，可得 $x_2=\tfrac95+\tfrac t5$、$x_3=1+4t$、$x_5=\tfrac85+\tfrac{17t}5$，目標 $z(t)=20t-7\to\infty$。

### 容易混淆
- **artificial 的係數符號跟 RHS 走，不是一律 $+1$**（L6 p17 的 $w_1$ 係數是 $-1$）。也可以先把整列乘 $-1$ 使 RHS 變正，兩種做法等價。
- **Phase 1 是 min 問題**：進入條件與 max 相反。
- **Phase 2 的起始 z-row 不能直接抄**：要用原目標，並把基本變數消掉〔講義 L6 p58 第 1 點〕。
- **artificial 一旦離開基底就可以刪掉它的欄**（L6 p31；FE Q3 詳解也這樣做）。
- **清除殘留 artificial 時 pivot element 可以是負的**：這是為了換掉基底的記帳 pivot，不是改善目標（L6 p39）。

### 關聯
主題 9 用 revised 的形式做同一件事（L8 Part 1）。Strong duality 的證明（主題 12）要用到「two-phase revised simplex 一定會停」這件事。

---

## 主題 9 Revised Simplex（L7）

### 直覺
tableau 每次都要更新整張 $(m+1)\times(n+1)$ 的表，但其實只有 entering 那一欄和 RHS 會用到。所有需要的量都可以從 $B^{-1}$ 和原始資料 $A,b,c$ 算出來，所以只要維護 $B^{-1}$ 就夠了。

### 符號〔講義 L7 p5–10〕
- 把 $Ax=b$ 依基本、非基本拆開：$Bx_B+Nx_N=b$。
- 目標同樣拆開：$c^Tx=c_B^Tx_B+c_N^Tx_N$。
- $a_j$ 表示 $A$ 中 $x_j$ 那一欄。

### 公式〔講義 L7 p13–14、p23、p30、p35〕

| 量 | 公式 |
|---|---|
| 目前的 BFS | $x_B^*=B^{-1}b$ |
| 單純形乘數（simplex multipliers） | $y=c_B^TB^{-1}$（列向量） |
| reduced cost | $\bar c_{N_j}=c_{N_j}-y\,a_{N_j}$ |
| entering 欄 | $d=B^{-1}a_{N_k}$ |
| ratio test | $t=\min\{x^*_{B_i}/d_{B_i}:\ d_{B_i}>0\}$；若沒有 $d_{B_i}>0$，LP unbounded |
| BFS 更新 | $x^*_{B_i}\leftarrow x^*_{B_i}-d_{B_i}\,t$（$i\ne r$）；$x_{N_k}\leftarrow t$，放在第 $r$ 個位置 |
| $B^{-1}$ 更新 | $\text{row}_i\leftarrow\text{row}_i-\dfrac{d_{B_i}}{d_{B_r}}\text{row}_r$（$i\ne r$）；$\text{row}_r\leftarrow\dfrac1{d_{B_r}}\text{row}_r$ |

### 推導
**(1) $x_B$ 與 reduced cost**〔講義 L7 p13–14〕
- $B$ 可逆，所以 $x_B=B^{-1}b-B^{-1}Nx_N$。
- 代入目標：
$$z=c_B^TB^{-1}b+\big(c_N^T-c_B^TB^{-1}N\big)x_N.$$
- 所以 $\bar v=c_B^TB^{-1}b$，而 $\bar c_{N_j}=c_{N_j}-c_B^TB^{-1}a_{N_j}=c_{N_j}-ya_{N_j}$。

**(2) $d$ 就是 entering 欄**〔講義 L7 p22–24〕
- 只讓 $x_{N_k}$ 增加時，$x_B=x_B^*-B^{-1}a_{N_k}\,x_{N_k}=x_B^*-d\,x_{N_k}$。
- 所以 $d$ 的角色和 tableau 中 entering 欄的 $\bar a_{\cdot,N_k}$ 完全相同〔手寫 L7 p22–24〕，ratio test 自然得出。

**(3) $B^{-1}$ 的更新**〔講義 L7 p29–30；T7 Q5〕
- 新基底把 $B$ 的第 $r$ 欄換成 $a_{N_k}$，得到 $B_{\text{new}}$。
- 此時 $B^{-1}B_{\text{new}}$ 除了第 $r$ 欄變成 $d$ 之外都是單位矩陣（因為 $B^{-1}a_{N_k}=d$）。
- 用上表的列運算把 $d$ 變回 $e_r$，就得到單位矩陣。列運算等於左乘基本矩陣：$E_m\cdots E_1B^{-1}B_{\text{new}}=I$，所以 $E_m\cdots E_1B^{-1}=B_{\text{new}}^{-1}$。
- 結論：對 $B^{-1}$ 本身做同樣的列運算，就得到 $B_{\text{new}}^{-1}$。

**(4) 驗證關係**〔講義 L7 p36〕：$\Delta z=\bar c_{N_k}\cdot t$。在 L7 例子中，$3\times2=6$，目標從 30 變成 36。

### 演算法〔講義 L7 p37、p40–45〕
1. 已知 $J_B$、$B^{-1}$、$x_B^*$。
2. 計算 $y=c_B^TB^{-1}$ 與每個非基本變數的 $\bar c_{N_j}$。max 問題全部 $\le0$ 就是最優；min 問題全部 $\ge0$ 就是最優。
3. 選 entering $x_{N_k}$，計算 $d=B^{-1}a_{N_k}$，做 ratio test。
4. 更新 $J_B$：把 leaving variable **原地**換成 entering variable，不要調換欄的位置〔講義 L7 p43 "Do NOT exchange column positions!!"〕。接著更新 $x_B^*$ 與 $B^{-1}$。
5. 回到第 2 步。

### 求 $B^{-1}$〔講義 L7 p16–17〕
對 $[B\mid I]$ 做列運算，直到左邊變成 $I$，右邊就是 $B^{-1}$。

### 範例〔講義 L7 p46–49〕
資料：
$$A=\begin{bmatrix}4&3&8&1&0&0\\4&1&12&0&1&0\\4&-1&3&0&0&1\end{bmatrix},\quad b=(12,8,8),\quad c=(2,1,2,0,0,0).$$
- 起始 $J_B=\{s_4,s_5,s_6\}$，$B^{-1}=I$。
- reduced cost：$\bar c_1=2$、$\bar c_2=1$、$\bar c_3=2$。$x_1$ 與 $x_3$ 平手，依 smallest subscript 選 $x_1$。
- $d=(4,4,4)$，ratio 為 $12/4=3$、$8/4=2$、$8/4=2$。$s_5$、$s_6$ 平手，選下標較小的 $s_5$ 離開。
- 以第 2 列 pivot：$B^{-1}_{\text{new}}=\begin{bmatrix}1&-1&0\\0&\tfrac14&0\\0&-1&1\end{bmatrix}$，$x_B^*=(4,2,0)$，基底 $\{s_4,x_1,s_6\}$。

### 容易混淆
- **$y$ 是列向量**，$y\,a_j$ 是內積。
- **$c_B$ 的順序必須和 $J_B$ 的順序一致**，也就是和 $B$ 的欄順序一致。
- **$B^{-1}$ 更新用的是 pivot 前的第 $r$ 列**。若先把第 $r$ 列縮放，其他列要改用縮放後的列與 $d_{B_i}$ 相乘（FE Q4 詳解 iteration 2 就是先縮放第 1 列）。兩種寫法結果相同，不要混著用。
- **min 問題**：最優條件是所有 $\bar c\ge0$，進入條件是 $\bar c<0$（L8 p6、p12）。

### 關聯
- $y=c_B^TB^{-1}$ 就是對偶解（主題 12）和 shadow price（主題 14）。
- 主題 14 的 sensitivity 全部用這裡的公式計算。

---

## 主題 10 代數最優證明、Weak Duality、Dual LP（L8 p16–33）

### 直覺
要證明某個解最優，不必比較所有角落。只要把約束乘上非負倍數後相加，使左邊正好等於目標函數，右邊的數字就是目標的上界。如果這個上界剛好等於候選解的目標值，候選解就是最優的。

「找最好（最小）的上界」本身又是一個 LP，這就是 dual。

### 推導：從組合約束到 dual〔講義 L8 p17–21〕
以 SIF $\max c^Tx$ s.t. $Ax\le b$、$x\ge0$ 為例。
- 給第 $i$ 條函數約束一個乘數 $y_i\ge0$，給第 $j$ 條非負約束 $-x_j\le0$ 一個乘數 $v_j\ge0$。相加得到：
$$\sum_j\Big(\sum_iy_ia_{ij}-v_j\Big)x_j\le\sum_iy_ib_i.$$
- 要求左邊恰好等於 $c^Tx$：對每個 $j$，$\sum_iy_ia_{ij}-v_j=c_j$。
- 「$v_j\ge0$ 且 $\sum_iy_ia_{ij}-v_j=c_j$」等價於「$\sum_iy_ia_{ij}\ge c_j$」（$v_j$ 就是這條不等式的 slack），所以 $v$ 可以消去。
- 於是 $b^Ty$ 就是所有可行 $x$ 的目標上界。最小化這個上界，就得到 dual：
$$\text{(D)}\quad\min\ b^Ty\quad\text{s.t.}\quad A^Ty\ge c,\ \ y\ge0.$$

### Weak Duality 與證明〔講義 L8 p25–27〕
若 $\bar x$ 對 (P) 可行、$\bar y$ 對 (D) 可行，則 $c^T\bar x\le b^T\bar y$。

證明：
1. 每條主問題約束乘上 $\bar y_i\ge0$，不等號方向不變：$\bar y_ib_i\ge\bar y_i\sum_ja_{ij}\bar x_j$。
2. 對 $i$ 加總，並把雙重和改成依 $j$ 分組：
$$\sum_i\bar y_ib_i\ \ge\ \sum_j\Big(\sum_i\bar y_ia_{ij}\Big)\bar x_j.$$
3. 每條對偶約束乘上 $\bar x_j\ge0$：$\Big(\sum_i\bar y_ia_{ij}\Big)\bar x_j\ge c_j\bar x_j$。
4. 對 $j$ 加總：$\sum_j\Big(\sum_i\bar y_ia_{ij}\Big)\bar x_j\ge\sum_jc_j\bar x_j$。
5. 第 2 步與第 4 步相接，得 $b^T\bar y\ge c^T\bar x$。∎

**推論**
- 若可行的 $\bar x$、$\bar y$ 滿足 $c^T\bar x=b^T\bar y$，兩者都是最優（T8 Q2(b)）。
- 若 (P) unbounded，則 (D) 不可行（T8 Q2(c)）。

### 寫 dual 的六條規則（SIF）〔講義 L8 p30〕
1. dual 是 min 問題。
2. dual 目標係數 = 主問題的 RHS。
3. dual 的約束全部是 $\ge$。
4. dual 約束的 RHS = 主問題的目標係數。
5. dual 的係數矩陣 = 主問題係數矩陣的轉置。
6. dual 變數全部非負。

〔手寫 L8 p30〕每個主變數 $x_j$ 對應一條對偶約束 $a_{1j}y_1+\dots+a_{mj}y_m\ge c_j$；每條主約束 $i$ 對應一個對偶變數 $y_i$。

### 範例〔講義 L8 p16–18、p24〕
- 主問題：$\max x_1+3x_2+5x_3$，s.t. $x_1+x_2+2x_3\le3$、$5x_1+2x_2+x_3\le7$、$x\ge0$。候選解 $x^*=(0,3,0)$，目標值 9。
- 取乘數 $(y_1,y_2,v_1,v_2,v_3)=(3,0,2,0,1)$，組合後得 $x_1+3x_2+5x_3\le9$ 對所有可行 $x$ 成立。
- $x^*$ 達到 9，所以是最優。
- 對應的 dual：$\min 3y_1+7y_2$，s.t. $y_1+5y_2\ge1$、$y_1+2y_2\ge3$、$2y_1+y_2\ge5$、$y\ge0$。

### 容易混淆
- **weak duality 證明的順序**：先用主問題可行性（乘 $y\ge0$），再用對偶可行性（乘 $x\ge0$）。FE Q1(a)(ii) 的詳解順序相反，先用對偶可行性；兩種順序都對，但每一步都要寫明用了哪個條件。
- **六條規則只適用於 SIF**（max、$\le$、$x\ge0$）。其他形式要用主題 13 的規則。

### 關聯
主題 11 從 weak duality 的「不等式鏈」推出 complementary slackness。

---
## 主題 11 Complementary Slackness（L8 p36–42；L9 p6–13）

### 直覺
weak duality 的證明是一串不等式：$c^T\bar x\le(\cdots)\le b^T\bar y$。若兩端相等，中間每個「$\le$」都必須是等號。每個等號又是「一堆非負項加起來等於 0」，所以每一項都是 0。逐項寫出來，就是：

- 主問題約束有 slack（不緊），對應的對偶變數必須是 0。
- 對偶約束有 slack（不緊），對應的主變數必須是 0。

〔補充〕比喻：用不到的資源（有 slack）影子價格是 0；在現行價格下虧本的產品（對偶約束有 slack），就不生產。

### 符號
- 主問題 slack：$\bar s_i=b_i-\sum_ja_{ij}\bar x_j$。
- 對偶 slack：$\bar v_j=\sum_i\bar y_ia_{ij}-c_j$。

### 關鍵恆等式〔講義 L8 p40〕
$$b^T\bar y-c^T\bar x=\sum_{i=1}^m\bar y_i\Big(b_i-\sum_ja_{ij}\bar x_j\Big)+\sum_{j=1}^n\Big(\sum_i\bar y_ia_{ij}-c_j\Big)\bar x_j.$$

**推導**：把右邊展開，
$$\sum_ib_i\bar y_i-\sum_i\sum_ja_{ij}\bar y_i\bar x_j+\sum_j\sum_ia_{ij}\bar y_i\bar x_j-\sum_jc_j\bar x_j.$$
中間兩個雙重和的項完全相同、只是加總順序不同，互相抵消，剩下的就是左邊。∎

### C.S. Lemma〔講義 L8 p39–42〕
設 $\bar x$ 對 (P) 可行、$\bar y$ 對 (D) 可行。則
$$b^T\bar y=c^T\bar x\iff\begin{cases}\bar y_i\,\bar s_i=0,&i=1,\dots,m\\[2pt]\bar v_j\,\bar x_j=0,&j=1,\dots,n\end{cases}$$

**證明**
1. 可行性保證恆等式右邊每一項都 $\ge0$：$\bar y_i\ge0$、$\bar s_i\ge0$、$\bar v_j\ge0$、$\bar x_j\ge0$。
2. 所以 $b^T\bar y-c^T\bar x\ge0$，這正是 weak duality。
3. 一串非負數的和為 0，若且唯若每一項都是 0。∎

**最優形式**：對可行的 $\bar x,\bar y$，兩者都最優 ⇔ C.S. 條件成立。
- (⇐) 由 Lemma 得 $c^T\bar x=b^T\bar y$，再由 weak duality 推出兩者都最優。
- (⇒) 需要 strong duality（主題 12）。
- 〔講義 L8 p42〕strong duality 的證明只用到 (⇐)，所以沒有循環論證。

### C.S. Theorem〔講義 L9 p6–8〕
可行的 $x^*$ 是最優解 ⇔ 存在對偶可行的 $y^*$，與 $x^*$ 一起滿足 C.S. 條件。
- (⇐) 就是 Lemma 的最優形式。
- (⇒) 由 strong duality，(D) 有最優解 $y^*$ 且 $b^Ty^*=c^Tx^*$；再由 Lemma，C.S. 條件成立。

### 三步檢驗法〔講義 L9 p9〕
1. **主問題可行**：$x^*$ 不可行就直接結束，它不可能是最優解。
2. **用 C.S. 解出 $y^*$**：
   - $x_j^*>0\Rightarrow$ 第 $j$ 條對偶約束取等號。
   - $s_i^*>0\Rightarrow y_i^*=0$。
   - 解這組方程。〔手寫 L9 p9〕順便列出 slack 為正的主約束。
3. **檢查對偶可行**：$y^*\ge0$，且所有沒用到的對偶約束都成立。成立則 $x^*$ 最優；不成立則 $x^*$ 不是最優。

**為什麼一次失敗就能下結論**〔講義 L9 p13〕：若第 2 步解出的 $y^*$ 是唯一的，它不可行就代表沒有任何對偶可行解能和 $x^*$ 滿足 C.S.。若第 2 步的方程組不能唯一決定 $y^*$，就要檢查是否存在某個對偶可行解〔補充〕。

### 範例〔講義 L9 p10–13〕
$\max 2x_1+4x_2+3x_3$，s.t. $x_1+2x_2+4x_3\le4$、$2x_1+x_2+x_3\le8$、$x\ge0$；候選解 $x^*=(2,1,0)$。

1. **可行性**：第 1 條為 $4=4$（緊）；第 2 條為 $5<8$（有 slack）。
2. **解 $y^*$**：
   - 第 2 條有 slack，所以 $y_2=0$。
   - $x_1>0$：$y_1+2y_2=2$；$x_2>0$：$2y_1+y_2=4$。
   - 得 $y^*=(2,0)$。
3. **對偶可行**：$y^*\ge0$；第 3 條對偶約束 $4y_1+y_2=8\ge3$ 成立。所以 $x^*$ 最優，最優值 $=b^Ty^*=8$。

**變化題**：若 $c_3$ 改成 9，第 3 條對偶約束變成 $8\ge9$，不成立，所以 $x^*$ 不是最優〔講義 L9 p13〕。

### 範例〔講義 L8 p36–38〕
$x^*=(0,3,0)$、$y=(3,0)$ 的 C.S. 檢查：

| 主約束 | 是否緊 | 對應 $y$ |
|---|---|---|
| $x_1+x_2+2x_3=3$ | 緊 | $y_1=3>0$ |
| $5x_1+2x_2+x_3=6<7$ | 有 slack | $y_2=0$ |

| 對偶約束 | 是否緊 | 對應 $x$ |
|---|---|---|
| $y_1+5y_2=3>1$ | 有 slack | $x_1^*=0$ |
| $y_1+2y_2=3$ | 緊 | $x_2^*>0$ |
| $2y_1+y_2=6>5$ | 有 slack | $x_3^*=0$ |

### 容易混淆
- **C.S. 只說「至少一個為 0」**，不是「恰好一個為 0」。兩者可以同時為 0（退化）。
- **$x_j^*=0$ 不能推出任何結論**，它不要求對偶約束取等號。
- **方程組不夠決定 $y$ 時**（例如 $x^*$ 的正分量太少），要加上對偶可行性一起判斷。FE Q1(b) 就是要找出 $y$ 存在的條件。

### 關聯
- 主題 12 用 C.S. 直接構造對偶解（complementary basic solution）。
- 主題 14 的 shadow price 用 C.S. 解釋：沒用完的資源，價格為 0。

---

## 主題 12 Complementary Basic Solution 與 Strong Duality（L8 p45–70）

### 直覺
simplex 每走到一個主問題基底，C.S. 就能在對偶那邊找到一個「配對」的基底。兩者的目標值永遠相等。主問題的 reduced cost 全部 $\le0$（最優）時，對偶解剛好也可行，兩邊同時最優。

### 配對〔講義 L8 p47〕
augmented 主問題：$Ax+s=b$。augmented dual：$A^Ty-v=c$。

| 主問題變數 | 配對的對偶變數 |
|---|---|
| $x_j$ | $v_j$（第 $j$ 條對偶約束的 surplus） |
| $s_i$ | $y_i$ |

### 定義〔講義 L8 p48、p55〕
- 主問題基底 $J_B=\{x_{j_1},\dots,x_{j_k},s_{i_1},\dots,s_{i_l}\}$。
- **complementary basis** $K_N$：與主問題**非基本**變數配對的對偶變數集合。
- **complementary basic solution**：由 $K_N$ 決定的對偶基本解。
- 〔手寫 L8' p15〕$J_B$ 是主問題基底，$K_N$ 是對偶基底。

### 定理 (I)〔講義 L8 p48–54〕
$K_N$ 一定是 augmented dual 的基底，而且它決定的 $(y^*,v^*)$ 與主問題的 $(x^*,s^*)$ 自動滿足 C.S.

**證明要點**
- **$K_N$ 是基底**（L8 p50–52）：
  - 對偶中不在 $K_N$ 的變數設為 0。
  - 這些變數正是與主問題基本變數配對的 $v_{j_1},\dots,y_{i_1},\dots$，所以剩下的方程組就是 $B^Ty=c_B$。
  - $B$ 可逆 ⇒ $B^T$ 可逆 ⇒ 有唯一解。
- **滿足 C.S.**（L8 p53–54）：
  - 每個指標 $j$ 不是在主問題基底中（此時 $v_j=0$，因為它不在 $K_N$），就是在主問題非基底中（此時 $x_j=0$）。
  - 所以 $x_j^*v_j^*=0$；同理 $s_i^*y_i^*=0$。

### 定理 (II)〔講義 L8 p58–62〕
complementary basic solution 滿足 $y^{*T}=c_B^TB^{-1}$，而且：
- 非基本 $x_j$ 的 reduced cost $=-v_j^*$。
- 非基本 $s_i$ 的 reduced cost $=-y_i^*$。

**推導**
1. $K_N$ 的方程組是 $B^Ty=c_B$，所以 $y^{*T}=c_B^TB^{-1}$，正是 revised simplex 的 $y$。
2. 非基本 $x_j$：$\bar c_j=c_j-y^*a_j$。而對偶約束 $a_j^Ty^*-v_j^*=c_j$ 給出 $c_j-a_j^Ty^*=-v_j^*$。
3. 非基本 $s_i$：它的欄是 $e_i$，係數 $c_{s_i}=0$，所以 $\bar c_{s_i}=0-y^*e_i=-y_i^*$。∎

**重要推論**〔講義 L8 p62–63〕
- 主問題最優（所有 $\bar c\le0$）⇔ $v^*\ge0$ 且 $y^*\ge0$ ⇔ complementary basis 對偶可行。
- 也就是說，revised simplex 的最優性檢驗，其實一直在檢查對偶可行性。

**定理 (II) 對任何基底都成立**，不只最優基底。T8 Q3 的基底主、對偶都不可行，但兩邊目標值仍相等。

### Strong Duality〔講義 L8 p66–69〕
若 SIF 的 (P) 有最優解 $x^*$，則 (D) 也有最優解 $y^*$，而且兩者最優值相等。

**證明**
1. (P) 有最優解 ⇒ two-phase revised simplex（用 Bland）會停在某個可行基底 $J_B$，且所有 $\bar c\le0$。
2. $(x^*,s^*)$ 是 $J_B$ 的 BFS，對 (P) 可行，而且由 optimality test 知道它最優。
3. 令 $(y^*,v^*)$ 為 complementary basic solution。由定理 (II)，$\bar c\le0\iff(y^*,v^*)\ge0$，所以它對偶可行。
4. 由定理 (I)，$(x^*,y^*)$ 滿足 C.S.
5. 由 C.S. Lemma：兩者都可行、又滿足 C.S.，所以兩者都最優，且 $c^Tx^*=b^Ty^*$。∎

矩陣版本見 T8 Q6：$b^Ty=(Bx_B^*)^Ty=x_B^{*T}B^Ty=x_B^{*T}c_B$。

### 範例〔講義 L8 p45–46、p58–59〕
主問題基底 $\{x_2,s_2\}$，$x^*=(0,3,0)$，$s=(0,1)$。
- 非基本 $\{x_1,x_3,s_1\}$，所以 $K_N=\{v_1,v_3,y_1\}$。
- 解出 $y_1=3$、$v_1=2$、$v_3=1$，其餘為 0。
- reduced cost：$\bar c_1=-2$、$\bar c_3=-1$、$\bar c_{s_1}=-3$，全部 $\le0$，所以主問題最優、對偶可行。

### 容易混淆
- **$K_N$ 配對的是主問題的「非基本」變數**，不是基本變數。
- **對偶 slack $v_j$ 是 surplus**：$A^Ty-v=c$，所以 $v=A^Ty-c$。
- **兩邊目標值相等不代表兩邊都最優**，還需要兩邊都可行（T8 Q3）。

### 關聯
- $y=c_B^TB^{-1}$ 在主題 14 被解釋為 shadow price。
- Strong duality 是主題 13 Primal-Dual Relation Theorem 第 (1) 條的基礎。

---

## 主題 13 一般形式 Dual、Primal-Dual Relation、Farkas（L9 p16–30）

### 直覺
實際的 LP 不一定是 SIF。可以先把它轉成 SIF、寫出 dual、再把轉換倒回來，最後得到一張對照表。考試時直接查表就好。

### 推導〔講義 L9 p17–21；手寫 L9 p17–21〕
從一個包含各種情況的代表例出發：
$$\max\ c_1x_1+c_2x_2+c_3x_3\quad\text{s.t.}\quad(\le b_1),\ (\ge b_2),\ (=b_3),\quad x_1\text{ free},\ x_2\ge0,\ x_3\le0.$$

1. **轉成 SIF**
   - $\ge$ 的約束乘 $-1$。
   - $=$ 的約束拆成 $\le$ 與 $-(\cdot)\le-b_3$ 兩條。
   - $x_1=x_1^+-x_1^-$。
   - $x_3'=-x_3\ge0$。
2. **寫出 SIF 的 dual (D1)**：四個變數 $y_1,y_2,y_3,y_4\ge0$。
3. **倒回轉換**
   - 令 $y_2'=-y_2\le0$（因為原約束是 $\ge$）。
   - 令 $y_3'=y_3-y_4$，這是 free 的（因為原約束是 $=$）。
   - $x_1^+$、$x_1^-$ 產生的兩條對偶約束合併成一條等式（因為 $x_1$ 是 free）。
   - $x_3'$ 對應的對偶約束乘 $-1$ 後變成 $\le$（因為 $x_3\le0$）。
4. **結果**
$$\min\ b_1y_1+b_2y_2'+b_3y_3'\quad\text{s.t.}\quad(=c_1),\ (\ge c_2),\ (\le c_3),\quad y_1\ge0,\ y_2'\le0,\ y_3'\text{ free}.$$

### 對照表（主問題為 max）〔講義 L9 p21–22；T9 Q2〕

| 主問題約束 $i$ | 對偶變數 $y_i$ | 主問題變數 $x_j$ | 對偶約束 $j$ |
|---|---|---|---|
| $\le b_i$ | $y_i\ge0$ | $x_j\ge0$ | $\ge c_j$ |
| $\ge b_i$ | $y_i\le0$ | $x_j\le0$ | $\le c_j$ |
| $=b_i$ | $y_i$ free | $x_j$ free | $=c_j$ |

**主問題為 min**（T9 Q5）：dual 是 max 問題，對照全部反過來。
- 主約束 $\ge\to y\ge0$；$\le\to y\le0$；$=\to$ free。
- 主變數 $x\ge0\to\le c_j$；$x\le0\to\ge c_j$；free $\to=c_j$。

**口訣**〔補充〕
- 「自然」的組合對「自然」的組合：max 問題的 $\le$ 與 $x\ge0$、min 問題的 $\ge$ 與 $x\ge0$，都對應到 $y\ge0$ 或 $\ge$ 型約束。
- 「不自然」的對「反號」。
- 等式對 free。

### Primal-Dual Relation Theorem〔講義 L9 p23–26〕
1. (P) 有最優解 ⇔ (D) 有最優解，而且最優值相等。
2. (P) 不可行 ⇒ (D) 不可行或 unbounded。
3. (P) unbounded ⇒ (D) 不可行。

| P \ D | D 有最優解 | D 不可行 | D unbounded |
|---|---|---|---|
| P 有最優解 | ✓ | × | × |
| P 不可行 | × | ✓ | ✓ |
| P unbounded | × | ✓ | × |

**證明要點**〔講義 L9 p25–26〕
- (1)：strong duality，加上「dual 的 dual 是原問題」的對稱性。
- (3)：weak duality。若 (D) 有可行的 $\bar y$，則 (P) 的目標被 $b^T\bar y$ 從上方限制住，不可能 unbounded。
- (2)：(D) 若有最優解，由 (1) 得 (P) 也有最優解，與 (P) 不可行矛盾。所以 (D) 只能不可行或 unbounded。

〔手寫 L9 p24〕例：若發現 (D) unbounded，則 (P) 一定不可行。

### Farkas 型可行性判準〔講義 L9 p27–30；T9 Q7〕
- **講義版本**：$Ax\le b,\ x\ge0$ 無解 ⇔ 存在 $l\ge0$ 使 $A^Tl\ge0$ 且 $b^Tl<0$。
- **T9 Q7 版本**：$Ax=b,\ x\ge0$ 無解 ⇔ 存在 $y$（free）使 $A^Ty\ge0$ 且 $b^Ty<0$。

**證明**（講義版本）
- (⇐) 若某個 $x$ 可行，則 $0\le x^T(A^Tl)=(Ax)^Tl\le b^Tl<0$，矛盾。
- (⇒) 考慮 (P) $\max 0^Tx$ s.t. $Ax\le b,\ x\ge0$，以及它的 (D) $\min b^Ty$ s.t. $A^Ty\ge0,\ y\ge0$。
  - $y=0$ 永遠是 (D) 的可行解，所以 (D) 不是不可行。
  - (P) 不可行時，由定理第 (2) 條，(D) 只能 unbounded。
  - 因為 $b^T0=0$，unbounded 代表存在可行的 $l$ 使 $b^Tl<0$。∎

### 容易混淆
- **主問題為 min 時，對照方向全部相反**。
- **一般形式下 C.S. 仍成立**，但等式約束的 slack 恆為 0（T9 Q5(d)）。
- **兩邊都不可行是可能的**（T9 Q6(c)）。

---

## 主題 14 Sensitivity Analysis（L9 p33–50；T9、T10）

### 直覺
求出最優解後要問：資料（價格、產能）有估計誤差時，同一個最優基底還能用多久？

基底 $J_B$ 最優需要兩個條件：
1. **primal feasible**：$B^{-1}b\ge0$。
2. **dual feasible**：所有 $\bar c\le0$。

所以要看參數變動會影響哪一個條件：

| 改變的參數 | 改變了什麼 | 要重新檢查 |
|---|---|---|
| 目標係數 $c$ | 只影響 $\bar c$ | dual feasibility |
| 右邊常數 $b$ | 只影響 $x_B^*=B^{-1}b$ | primal feasibility |

### 四種情況〔講義 L9 p41–47；T10 Q9 證明〕

| 改變 | 不變的量 | 會改變的量 | 最優條件 | 最優值 |
|---|---|---|---|---|
| 非基本 $c_{N_k}\to c_{N_k}+\Delta$ | $B$、$x_B^*$、$c_B$、$y$、其他 $\bar c$ | 只有 $\bar c_{N_k}^{\text{new}}=\bar c_{N_k}+\Delta$ | $\Delta\le-\bar c_{N_k}$，即 $c_{N_k}\le c_{N_k}-\bar c_{N_k}$ | 不變（$x^*_{N_k}=0$） |
| 基本 $c_{B_r}\to c_{B_r}+\Delta$ | $B$、$x_B^*$ | $y$ 改變，**所有**非基本變數的 $\bar c$ 都要重算 | 每個 $\bar c_{N_j}(\Delta)\le0$，各解一個不等式後取交集 | $z^*+\Delta\,x^*_{B_r}$ |
| 右邊常數 $b\to b+\Delta b$ | $B^{-1}$、$y$、所有 $\bar c$ | $x_B=x_B^*+B^{-1}\Delta b$ | $x_B^*+B^{-1}\Delta b\ge0$ | $z^*+y^T\Delta b$ |
| 新增變數 $x_0$（欄 $a_0$、係數 $c_0$） | 原基底 | 多一個非基本變數 | $\bar c_0=c_0-ya_0\le0$ | 不變 |

### 推導（T10 Q9）
- **(a) 非基本 $c$**：$B$、$b$ 不變，所以 $x_B^*$ 不變；$c_B$ 不變，所以 $y$ 不變。除了 $x_{N_k}$ 之外，每個 $\bar c_{N_j}=c_{N_j}-ya_{N_j}$ 都不變。$\bar c_{N_k}$ 變成 $(c_{N_k}+\Delta)-ya_{N_k}=\bar c_{N_k}+\Delta$。最優值 $c_B^Tx_B^*$ 不含 $c_{N_k}$，所以不變。
- **(b) 基本 $c$**：$x_B^*$ 不變。最優值變成 $(c_B+\Delta e_r)^Tx_B^*=z^*+\Delta x^*_{B_r}$。
- **(c) 右邊常數**：$y$ 與 $\bar c$ 不變，所以仍是 dual feasible。新的基本解為 $B^{-1}(b+\Delta b)$。最優值 $c_B^TB^{-1}(b+\Delta b)=y^Tb+y^T\Delta b=z^*+y^T\Delta b$。
- **(d) 超出範圍**：若 $x_B^*+B^{-1}\Delta b$ 有負的分量，$J_B$ 就不再可行，$z^*+y^T\Delta b$ 只是一個不可行點的目標值，不能拿來預測。

### Shadow price
- $y_i$ 是第 $i$ 個資源每多 1 單位時，最優值增加的量。
- 只在「$J_B$ 仍然可行」的 $b_i$ 範圍內有效（T10 Q10(c)）。
- 鬆的約束（slack 為基本變數）的 $y_i=0$，這就是 C.S.（T10 Q7(a)）。

### Reduced cost 的經濟意義（T9 Q8(c)）
$\bar c_j=c_j-ya_j$：每生產 1 單位 $x_j$ 的利潤，減去它用掉的資源以影子價格計算的價值。

### 超出範圍後怎麼做（T10 Q2、Q4、Q8、Q10(d)）
- 從原 $J_B$ 出發，用新的 $c$ 繼續做 revised simplex。
- 通常只需要再一兩次迭代。

### 範例 1：非基本係數〔講義 L9 p42–47〕
- $J_B=\{x_1,s_5,s_6\}$，$y=(2,0,0)$，$\bar c_2=-1$。
- 範圍：$c_2\le1+1$，即 $c_2\in(-\infty,2]$。

### 範例 2：Leopard Airlines〔講義 L9 p34–40、p48–49〕
- 最優解 $x^*=(260,260,40,250,250,50,100,85)$，收入 \$2,241,500。
- 需求約束的 shadow price：SG-TK 400、TK-SG 350、LA-SG 4000，其他 0。
  - 所以廣告應優先投在 LA-SG：每增加 1 位需求，價值 \$4,000。
- 航段的 shadow price：$y_{FL3}=4200$、$y_{FL2a}=1500$、$y_{FL2b}=600$。
  - 一個套票（SG-LA + LA-TK-SG）的最低價為 $4200+1500+600=\$6{,}300$；25 套為 \$157,500。
- SG-TK-LA 的 $x_3=40>0$，是基本變數，所以改它的價格屬於「基本 $c$」的情況，不能用非基本的方法。
- 新產品 $x_9$（使用 FL1a 與 FL2a）：$\bar c_9=p_9-(600+1500)$，所以 $p_9>2100$ 才值得推出。

### 範例 3：T10 Q10 麵包店
- $\max 60x_1+60x_2+40x_3$，最優解 $(8,6,0)$，利潤 840，$y=(0,15,15)$。
- 蛋糕利潤 $c_1\in[30,90]$ 時方案不變。
- 餅乾盒利潤 $c_3\le60$ 時仍不生產。
- 勞力時數 $b_2\in[12,\tfrac{180}7]$ 時 shadow price 15 有效。
  - 加班每小時 12 元，比 15 便宜，值得買到 $\tfrac{40}7$ 小時。
  - 若增加 6 小時，超出範圍，預測的 930 不對，實際最優值為 925.71（已用 Python 驗證）。
- 起司蛋糕：$\bar c_0=50-45=5>0$，值得生產。重新最佳化後為 $(0,2,0)$ 加上 16 個起司蛋糕，利潤 920。

### 容易混淆
- **先判斷變數是基本還是非基本**，兩種情況的算法完全不同。
- **$b$ 的範圍只適用於一次改一個 $b_i$**；同時改多個要直接檢查 $x_B^*+B^{-1}\Delta b\ge0$（T10 Q7(d)）。
- **非基本變數的 $\bar c=0$ 代表有替代最優解**（T10 Q8(c)）。

---

## 主題 15 應用：PERT/CPM（L8 p73–79）

### 模型
- $x_i$：milestone $i$ 的最早開始時間。
- 目標：$\min x_I-x_A$（專案總時間）。
- 約束：每個活動 $(u\to v)$ 的工期為 $d$，則 $x_v-x_u\ge d$。

### Dual
- 主問題是 min、約束為 $\ge$，所以 dual 是 max 問題。
- 每個活動對應一個 $y_k$；目標係數是工期，約束形成從 A 到 I 的路徑流量守恆。
- 解出來 $y_k=1$ 的活動構成**最長路徑**，也就是 critical path。

### 結果
- 主問題：$x_A=0,\ x_B=3,\ x_C=7,\ x_D=10,\ x_E=12,\ x_F=14,\ x_G=15,\ x_H=22,\ x_I=27$，總時間 27 天。
- Critical path：DIG→FOUND→WALLS→RAFTERS→ROOF→FINISH（$3+4+5+3+7+5=27$）。
- 其他活動的 $y_k=0$，因為它們的主問題約束不緊，這正是 C.S.
