# 07 考試策略

本文件分成兩種內容，請分開看待：
- **〔事實〕**：可以直接從教材或原卷確認的內容。
- **〔建議〕**：根據去年考題與教材比重推出的準備方向。這不是對今年考題的預測。

---

## 1. 可確認的事實

### 1.1 考試規格〔事實，原卷封面〕
- 2 小時，4 題，每題 25 分，全部作答。
- 每題從新的一頁開始寫。
- 可帶**一張雙面 A4 參考紙，內容必須手寫**，不可黏貼或附加其他紙張。
- 可使用計算機，但必須「systematically」寫出步驟。

### 1.2 去年考點分布〔事實〕

| 題 | 分數 | 主題 | 講義 |
|---|---|---|---|
| Q1 | 25 | dual、weak duality 證明、C.S. 條件、C.S. 檢驗、參數化 C.S. | L8 Part 3–4、L9 Part 1 |
| Q2 | 25 | improving edges（題目給的點其實是退化 CPF） | L2 |
| Q3 | 25 | two-phase，tabular 形式 | L6 |
| Q4 | 25 | revised simplex 搭配 Bland's rule | L7 |

去年沒有出題的主題：
- 建模、圖解法（L1）
- basis / BFS 的判斷（L3）
- cycling（L5）
- 一般形式 dual、Primal-Dual 狀態、Farkas（L9 Part 2）
- sensitivity analysis（L9 Part 3、T10）
- PERT（L8 Part 8）

### 1.3 教材篇幅〔事實〕
- **講義頁數**：
  - L1 70、L2 72、L3 63、L4 81、L5 51、L6 59、L7 53。
  - L8 79，另有 L8' 46 頁重講 L8 後半。
  - L9 50。
- **Tutorial 題數**：
  - T1 14、T2 8、T3 8、T4 4、T5 4、T6 5、T7 5、T8 7、T9 8、T10 10。
  - T10 有 16 頁，是篇幅最長的一份。

---

## 2. 各章重要程度〔建議〕

| 等級 | 章節 | 依據 |
|---|---|---|
| ★★★ | L2 edges、L6 two-phase、L7 revised simplex、L8–L9 duality 與 C.S. | 去年四題各佔 25 分；而且都是有固定步驟的計算題 |
| ★★★ | Sensitivity（L9 Part 3、T10） | 去年沒考，但 T10 篇幅最大、題型最多，L9 也花了 18 頁鋪陳，這是今年的空白風險 |
| ★★ | L4–L5（reduced cost、MRT、tableau、Bland、退化） | 本身很少單獨出題，但 Q2–Q4 都要用到 |
| ★★ | 一般形式 dual、Primal-Dual Relation | T9 有 3 題，屬於 Q1 類型的延伸 |
| ★ | L3 basis / BFS 判斷、L1 建模與圖解 | 概念基礎；可能以小題形式出現 |
| ★ | 各定理的證明 | 去年考了 weak duality 證明；其他證明（optimality test、unbounded、artificial 定理、C.S. Lemma）建議記住架構 |

---

## 3. 必備技能清單〔建議〕

以下每一項都應該能**不看詳解、限時完成**。

1. **找 improving edges**（S4），包含退化 CPF 與沒有非負限制的題目。限時 25 分鐘。
2. **Two-phase tableau**（S9），包含：
   - 殘留 artificial 的處理
   - Phase 1 判定不可行
   - Phase 2 判定 unbounded
3. **Revised simplex**（S10），包含：
   - Bland's rule
   - 平手處理
   - 退化
   - 每次迭代都要更新 $B^{-1}$
4. **寫 dual**：SIF 與一般形式，包含 min 問題。
5. **證明 weak duality**，並寫出 C.S. 條件。
6. **C.S. 三步檢驗**，包含：
   - 結論為「不是最優」的情況
   - 目標係數為參數的版本
7. **Sensitivity 五種情況**：
   - 非基本變數的 $c$
   - 基本變數的 $c$
   - 右邊常數 $b$
   - 新增變數
   - 超出範圍後重新最佳化
8. **證明 unbounded 或 infeasible**：寫出可行點序列，或寫出 Phase 1 的最優值。

---

## 4. 公式：哪些要背、哪些可以推〔建議〕

| 類別 | 內容 | 建議 |
|---|---|---|
| 必寫上參考紙 | revised simplex 的六條公式（$x_B^*=B^{-1}b$、$y=c_B^TB^{-1}$、$\bar c_j=c_j-ya_j$、$d=B^{-1}a_{N_k}$、$t=\min\{x^*_{B_i}/d_i:\ d_i>0\}$、$B^{-1}$ 的更新規則） | 抄在參考紙上；考前仍要能默寫 |
| 必寫上參考紙 | 一般形式 dual 的對照表；Primal-Dual 狀態相容表 | 容易記反，抄上去 |
| 必寫上參考紙 | Sensitivity 五種情況的條件與最優值變化 | 抄上去 |
| 可從定義推出 | C.S. 條件（從 weak duality 的不等式鏈推得） | 只需記住「slack × 對應變數 = 0」 |
| 可從定義推出 | tableau 的 pivot 規則（Gauss–Jordan 消去） | 記住目標：讓 pivot 欄變成單位向量 |
| 可從定義推出 | edge 的方向（由剩下的 active 約束決定） | 記住原理 |
| 要記架構的證明 | weak duality 的 5 步；optimality test；unbounded 序列；artificial 定理；C.S. Lemma 的恆等式 | 參考紙上寫一行架構即可 |

---

## 5. 解題順序與時間分配〔建議〕

**總時間 120 分鐘，四題等分。**

| 時段 | 分鐘 | 做什麼 |
|---|---|---|
| 開場 | 3 | 掃過四題，標出類型與題目要求的方法（例如「revised」「tabular」「using C.S.」） |
| 第一輪 | 約 25 × 4 | 依自己的熟練度排序，最熟的先做 |
| 收尾 | 約 10 | 驗算最優值（$c^Tx^*=b^Ty^*$）、代回約束、補上結論句 |

**排序建議**
- 計算型的題（two-phase、revised simplex）步驟固定，可以穩定拿分，先做。
- 證明型、參數型的子題容易卡住，放在中後段。

**卡住的處理**
- 同一個子題卡超過 8 分鐘，就先跳過。
- 跳過時把已經想到的關鍵等式寫下來，爭取部分分數。

**單題內部的時間（以 25 分鐘為例）**

| 題型 | 建議分配 |
|---|---|
| Revised simplex | 每次迭代約 6–7 分鐘；三次迭代加上設定約 22 分鐘 |
| Two-phase | Phase 1 三次迭代約 15 分鐘，Phase 2 約 7 分鐘 |
| Improving edges，4 條 active | 每組約 3 分鐘 × 6 組，加上整理約 22 分鐘 |
| Dual 綜合題 | (i)(iii) 約 5 分鐘，(ii) 約 5 分鐘，(iv) 約 7 分鐘，(b) 約 8 分鐘 |

---

## 6. 考前複習清單〔建議〕

### 考前一週
- [ ] 讀完 `02_Concepts_and_Derivations.md`，能用自己的話說出每個主題的直覺。
- [ ] 每個 S 模板（`03`）至少獨立做一題。
- [ ] 限時重做去年的期末考（不看 `06`），寫完再對答案。
- [ ] 把 `05_Common_Mistakes.md` 中自己犯過的錯標記出來。
- [ ] 依 `08`、`09` 的內容，**手寫**參考紙（Canva 版只能當底稿，不能帶進考場）。

### 考前一天
- [ ] 默寫 revised simplex 的公式、dual 對照表、sensitivity 五種情況。
- [ ] 重做 T2 Q5、T6 Q3、T7 Q4、T9 Q1、T10 Q3、T10 Q7。
- [ ] 檢查參考紙：只有一張、雙面、全部手寫、沒有黏貼。

### 考場上
- [ ] 每題開頭先寫：max 或 min？有沒有 $x\ge0$？題目指定什麼方法？
- [ ] 每次迭代都寫出 entering、ratio、leaving。
- [ ] 每題最後寫結論句與目標值。

---

## 7. 最值得反覆練習的題目〔建議〕

| 優先 | 題目 | 原因 |
|---|---|---|
| 1 | FE Q1–Q4（以 `06` 的修正版為準） | 去年原題 |
| 2 | T2 Q5（退化 CPF 的 6 組 edges） | 與 FE Q2 結構完全相同 |
| 3 | T6 Q3（殘留 artificial）、T6 Q4（完整 two-phase） | FE Q3 的兩個變化 |
| 4 | T7 Q4、T7 Q2 | revised simplex 的標準流程 |
| 5 | T9 Q1、T9 Q4 | C.S. 檢驗的「最優」與「不是最優」兩種結論 |
| 6 | T10 Q3、T10 Q4 | 基本變數係數的範圍與超出範圍，最容易出錯 |
| 7 | T10 Q7、T10 Q10 | $b$ 的範圍與 shadow price 的綜合應用 |
| 8 | T9 Q2、T9 Q5 | 一般形式 dual |
| 9 | T5 Q3 | 三種 tie-breaking 規則 |
| 10 | T4 Q2、T5 Q4 | 退化 pivot |

**練習方式**
1. 第一次看詳解，理解每一步的理由。
2. 第二次遮住詳解，自己寫出完整步驟。
3. 第三次改掉題目中的一個數字或一條約束再做（例如 FE Q2 拿掉 $x\ge0$、T10 Q3 改成 $c_1$），檢查是否真正理解。
