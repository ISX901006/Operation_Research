# 05 常見錯誤整理

依據：講義、Tutorial 詳解、期末考詳解（含詳解本身的錯誤）。

每條錯誤分四欄：
- **錯誤**：容易犯的錯。
- **原因**：為什麼會犯。
- **正確觀念**：正確的理解與出處。
- **避免方法**：作答時的檢查動作。

---

## A. 觀念理解錯誤

| # | 錯誤 | 原因 | 正確觀念 | 避免方法 |
|---|---|---|---|---|
| A1 | 可行域無界 ⇒ LP unbounded | 混淆「區域無界」與「目標無界」 | 兩者互不蘊含（L1 p25；T1 Q6、Q12） | 判定 unbounded 時，一定要給一條可行射線，並說明目標趨近無限大 |
| A2 | active 約束有 $n$ 條 ⇒ 一定是 CPF | 忽略「獨立」與「可行」兩個條件 | 可行，且 active 方程組有唯一解（L2 p24；T2 Q1(b)、Q7(b)） | S3 三步缺一不可 |
| A3 | 所有 $\bar c\le0$ 是最優的**必要**條件 | 把定理讀反 | 只是充分條件；退化時，最優 BFS 可能由一個帶有正 $\bar c$ 的基底決定（L4 p19、p22；T4 Q2） | 若遇到「BFS 沒變、$\bar c$ 仍有正值」，繼續做 pivot |
| A4 | Adjacent bases 有遞移性 | 直覺類比 | A~B、B~C，不能推出 A~C（T3 Q3(c)） | 逐一比對兩個基底差幾個變數 |
| A5 | 退化 BFS 只對應一個基底 | 以為基底與 BFS 一一對應 | 一個退化 BFS 可以有多個基底（T3 Q5 有 4 個） | 數一數 0 的個數是否超過 $n-m$ |
| A6 | 主問題與對偶目標值相等 ⇒ 兩者都最優 | 漏了可行性 | 必須兩者都可行，再加上目標值相等（T8 Q3 兩者都不可行，但目標值相等） | 先檢查兩邊可行，再比較目標值 |
| A7 | C.S. 是「恰好一個為 0」 | 誤解乘積等於 0 | 是「至少一個為 0」，可以兩個都是 0 | 由 $x_j^*=0$ 不能推出任何東西 |
| A8 | 主問題不可行 ⇒ 對偶一定 unbounded | 只記住了相容表的一格 | 對偶可能 unbounded，也可能不可行（T9 Q6(c)） | 照相容表逐格判斷 |
| A9 | Shadow price 在任何範圍都成立 | 忽略基底改變 | 只在 $x_B^*+B^{-1}\Delta b\ge0$ 的範圍內成立（T10 Q9(d)、Q10(c)(iii)） | 先算 $b$ 的有效範圍 |
| A10 | Phase 1 最優值 0 ⇒ artificial 都已離開基底 | 混淆「值為 0」與「不是基本變數」 | 可能有 artificial 以值 0 留在基底（L6 p38；T6 Q3；L8 p7） | Phase 1 結束時，檢查基底裡有沒有 $w$ |

---

## B. 公式使用錯誤

| # | 錯誤 | 原因 | 正確觀念 | 避免方法 |
|---|---|---|---|---|
| B1 | Reduced cost 用 $c_j+ya_j$，或 $y=B^{-1}c_B$ | 公式記錯 | $y=c_B^TB^{-1}$（列向量），$\bar c_j=c_j-ya_j$ | 抽一個 slack 驗算：$\bar c_{s_i}=-y_i$ |
| B2 | Largest improvement 算成 $\bar c\times$ pivot element | 混淆 $t$ 與 pivot element | $\Delta z=\bar c_{N_k}\cdot t$（L5 p36 手寫；T5 Q3） | 先做 ratio test 得到 $t$ |
| B3 | 非基本變數的範圍寫成 $\Delta\ge-\bar c$ | 符號方向搞反 | max 問題：$\Delta\le-\bar c_{N_k}$，也就是 $c_{N_k}\le ya_{N_k}$（L9 p47） | 直接寫 $\bar c_{\text{new}}=c_{\text{new}}-ya\le0$ 再解 |
| B4 | 改基本變數的 $c$，只檢查一個 $\bar c$ | 套用了非基本變數的做法 | $y$ 會改變，所有非基本變數的 $\bar c$ 都要重算（T10 Q3、Q10(b)） | 先判斷這個變數是基本還是非基本 |
| B5 | 多個 $b$ 同時改，直接套用各自的範圍 | 範圍是一次只改一個時推出來的 | 要直接檢查整個向量 $x_B^*+B^{-1}\Delta b\ge0$（T10 Q7(d)） | 同時改多個時，一律重算向量 |
| B6 | 一般形式的 dual 符號對錯 | min 問題時沒有反轉規則 | 照對照表；主問題是 min 時方向全部相反（T9 Q5） | 寫完後用「自然配對」口訣檢查 |

---

## C. 方法選擇錯誤

| # | 錯誤 | 正確做法 |
|---|---|---|
| C1 | 題目要求 revised simplex，卻用 tableau 作答 | 依題目指定的方法作答，否則可能失分（FE Q4） |
| C2 | 有 $\ge$ 或 $=$ 約束，仍然從 slack 基底出發 | 改用 two-phase（FE Q3） |
| C3 | 題目要求「using complementary slackness」，卻用 simplex 解出最優解 | 依題目要求走三步檢驗（FE Q1(a)(iv)） |
| C4 | 找 improving edges 時先轉成 SEF、建 tableau | 照幾何方法做，保留 $n-1$ 條 active 約束（FE Q2）；tableau 不會自動列出退化 CPF 的所有 edges |

---

## D. 演算法執行錯誤

| # | 錯誤 | 原因 | 正確做法 | 避免方法 |
|---|---|---|---|---|
| D1 | Tableau 的 z-row 正負號搞反 | z-row 存的是 $-\bar c$ | max 問題選 z-row 為負的欄進入；min 問題選為正的欄（L5 p9；L6 p20） | 在答案卷上寫一行「max: enter if z-row < 0」 |
| D2 | MRT 把負數或 0 也算進去 | 忘了「只看正的係數」 | 只對 pivot 欄中 $>0$ 的列計算比值（L4 p32） | 被排除的列寫「—」並註明原因 |
| D3 | Pivot 時用已更新的列去消其他列 | 運算順序錯 | 一律用原 pivot 列（或已縮放的 pivot 列）作為基準（L5 p19；L7 p32） | 固定用一種寫法 |
| D4 | Bland 的平手比的是列位置 | 誤解規則 | 比的是變數下標（T5 Q3(c)：選 $x_4$，不是第 1 列的 $x_7$） | 寫出候選變數的名稱，再比較下標 |
| D5 | Revised simplex 把基底欄位重新排列 | 想讓 $B$ 看起來整齊 | 原地替換，位置不變（L7 p43） | $J_B$ 寫成有序列，例如 $(x_2,x_1,s_6)$ |
| D6 | Phase 2 的 z-row 直接用原 $c$，沒有消去基本變數 | 少了一步 | 先把目標用非基本變數表示，再填入 z-row（L6 p58） | 檢查每個基本變數在 z-row 的位置是不是 0 |
| D7 | 殘留 artificial 只敢用正的 pivot element | 套用了 ratio test 的習慣 | 任何非零係數都可以，這是退化 pivot（L6 p39；L8 p9） | 註明「degenerate pivot, $t=0$」 |
| D8 | 退化點只檢查 $n$ 組 edge | 以為 active 數一定等於 $n$ | 要檢查 $\binom{p}{n-1}$ 組，並去掉重複與退化的（T2 Q5；FE Q2） | 先數 active 的條數 |
| D9 | Edge 方向憑直覺決定 | 沒有代入剩下的 active 約束 | 由剩下的 active 約束決定（L2 p45） | 每組都寫出「(k) 化簡為 $t\ge\cdot$」 |

---

## E. 計算與符號錯誤

| # | 錯誤 | 避免方法 |
|---|---|---|
| E1 | 分數算錯 | 每次迭代後驗算 $B^{-1}B=I$（取一欄就夠），或檢查 tableau 中每個基本欄是不是單位向量 |
| E2 | 寫 dual 時沒有轉置 | 第 $j$ 條對偶約束用的是主問題的第 $j$ **欄** |
| E3 | $c_B$ 的順序與 $J_B$ 不一致 | 寫 $c_B$ 時逐一標上對應的變數名稱 |
| E4 | 最後的最優值算錯 | 用 $c^Tx^*$ 與 $b^Ty^*$ 兩種方式計算，兩者應相等 |

---

## F. 忽略限制條件或假設

| # | 錯誤 | 案例 | 正確做法 |
|---|---|---|---|
| F1 | 題目有 $x\ge0$ 卻漏看 | **FE Q2 的詳解檔**：原卷寫 $x_1,x_2,x_3,\ge0$（多了一個逗號），詳解檔誤以為沒有非負限制，結果只檢查 3 組，把一條違反 $x_3\ge0$ 的射線當成 edge，並漏掉兩條真正的 edge | 先抄下完整的約束清單，再逐條檢查 |
| F2 | 題目沒有 $x\ge0$，卻自己加上 | T2 Q1、Q2、Q6、Q7、Q8 | 只用題目給的約束 |
| F3 | 等式約束寫成不等式 | T1 Q3 | 「恰好」、「固定」要寫 $=$ |
| F4 | 把 surplus 寫成 $+s$ | — | $\ge$ 約束是 $a^Tx-s=b$ |
| F5 | Artificial 的符號沒有跟 RHS 一致 | L6 p17 的 $w_1$ | artificial 係數取 $\pm1$，與 RHS 同號；也可以先把整列乘 $-1$ |

---

## G. 最優解判斷錯誤

| # | 錯誤 | 正確觀念 |
|---|---|---|
| G1 | 斜率 0 的 edge 算成 improving | 必須嚴格變好（T2 Q5） |
| G2 | 只檢查 C.S. 中取等號的那幾條對偶約束 | 其他對偶約束也要檢查是否成立，這是對偶可行性（T9 Q1：$4y_1-2y_3\ge3$） |
| G3 | 沒有發現多重最優解 | 若某個非基本變數 $\bar c=0$，或等值線與某條邊平行，就有替代最優解（T1 Q9；T10 Q8(c)） |
| G4 | 用 MRT 判定 unbounded，但 entering 變數的 $\bar c$ 不是正的 | unbounded 的條件是「$\bar c>0$ 且整欄 $\le0$」，兩者都要（L4 p42 手寫「must have positive reduced cost」） |

---

## H. 考試作答不完整

| # | 缺漏 | 應補上的內容 |
|---|---|---|
| H1 | 只寫答案，沒有過程 | 原卷規定「write down systematically the steps」；每次迭代都要寫出 entering、ratio、leaving、新的表或 $B^{-1}$ |
| H2 | 宣稱 unbounded 卻沒有證明 | 寫出可行點序列 $\bar x(k)$，並說明目標趨近無限大（T4 Q4(c)；T5 Q1、Q2） |
| H3 | 宣稱 infeasible 卻沒有證明 | 寫出 Phase 1 最優值 $>0$，或寫出矛盾的約束組合，或給 Farkas 證書 |
| H4 | 沒有寫 artificial problem 的完整模型 | FE Q3 的第一句就要求「write down the artificial problem」，這一步有分數 |
| H5 | C.S. 判斷沒有寫結論句 | 加上「By the Complementary Slackness Theorem, $x^*$ is (not) optimal」 |
| H6 | 用了 Bland 卻沒有說明 | 在平手處寫明「tie: $s_4,s_6$；by Bland, $s_4$ leaves」 |
| H7 | 最後沒有回到原變數 | 寫出 $(x_1,\dots,x_n)$ 與目標值；slack 的值可以另外附上 |
