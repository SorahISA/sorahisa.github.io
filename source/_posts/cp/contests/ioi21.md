---
title: IOI 2021 場外心得
date: 2021-07-05 21:12:55
category:
  - [競程, 比賽心得]
tags:
  - IOI
---

這是第一篇正式ㄉ文章ㄛ >////<，本來該是另一篇的，但是因為太懶了還沒有動工，這篇就變成第一個了 www。

<!-- more -->

---

前年的 IOI 2019 快結束的時候，看到 BB 搶下最後一題的首殺，拿到世界第 6 名，心情也不自覺的跟著變得激動雀躍，也讓我下定決心：只要還有認識的人在打，就一定要跟著看 scoreboard，甚至是同時打 Mirror（不知道為什麼 Yandex 沒開ㄌ），結果就變成線上了......

今年的 IOI 還是線上真的很可惜，少了那種在場外看著 scoreboard 跟著一起激動的感覺。當我想著自己一個人打會不會有點無聊的時候，正巧品庠來找我一起 virtual，就決定在 7/5 跟 7/7 的下午來打ㄌ！

---

## Day -2 ~ Day 0 --- 測試賽 & NHDK TPR

覺得自己需要稍微寫一下題目才不會燒雞，所以我就去找了測試賽的題目來打，但因為場外沒有今年的測試賽，所以我去 oj.uz 寫去年的測試題，發現有四分之三跟今年一樣ㄟ，賺到（X）。

反正也沒有限時，那就慢慢寫ㄅ。

- [Judge](https://oj.uz/problems/source/532)

### A - Handcrafted Gift ([gift](https://oj.uz/problem/view/IOI20_gift))

<span class="score_ac">分數：$100$</span> $(
$<span class="score_ac">$10$</span>$/
$<span class="score_ac">$15$</span>$/
$<span class="score_ac">$20$</span>$/
$<span class="score_ac">$25$</span>$/
$<span class="score_ac">$30$</span>$)$

{% note info no-icon %}
有一個長度 $n$ 的字串，每個字元是 `R` 或 `B`，你有 $r$ 個任務，第 $i$ 個任務要使 $[a_i, b_i]$ 恰有 $x_i$ 種顏色，詢問有沒有合法的構造，有的話輸出任意一組。

- $n, r \le 500\,000$。
- $x_i \in \{1, 2\}$。
{% endnote %}

[AC Solution](https://oj.uz/submission/440315)

水題，把 $x = 1$ 的區間都 merge 起來剩下 RB 交錯放就好ㄌ。

### B - Painting Squares ([squares](https://oj.uz/problem/view/IOI20_squares))

<span class="score_ac">分數：$100$</span> $(
$<span class="score_ac">$10$</span>$/
$<span class="score_ac">$15$</span>$/
$<span class="score_ac">$20$</span>$/
$<span class="score_ac">$55$</span>$)$

{% note info no-icon %}
你需要完成兩個程式，第一個程式會給 jury 一個長度 $n$ 的 01 陣列 $a$ 和一個正整數 $k$，jury 會給你的第二個程式 $q$ 段長度為 $k$ 的 subarray $c = [a_x, a_{x+1}, \ldots, a_{x+k-1}]$，你需要回傳這些 subarray 們在 $a$ 的位置。

- $n, q \le 1000$。
- 給分方法：$k \le 10$ 滿分。
{% endnote %}

[AC Solution](https://oj.uz/submission/441104) #
[Random String](https://oj.uz/submission/440962)

看到一眼就知道是要構造 de Bruijn sequence 的題目，但是忘記怎麼構造，所以先 random 生了一堆 01 字串來看看可以把 $k$ 壓到多少（BioInformatics 後遺症 www）。放了大約一小時最好的結果就是 $k = 15$，就丟上去了。

想了幾個小時之後可恥的去看了 Wiki 寫了 inverse Burrows Wheeler transform 過了。

有個小插曲是我中途交的所有 $k \in [15, 20]$ 的解也都拿到滿分，所以我就丟了一ㄍ issue 給他們，~~不知道會不會被回 owo~~ 現在已經修好ㄌ >////<。

### C - Finding Routers ([routers](https://oj.uz/problem/view/IOI20_routers))

<span class="score_ac">分數：$100$</span> $(
$<span class="score_ac">$16$</span>$/
$<span class="score_ac">$21$</span>$/
$<span class="score_ac">$23$</span>$/
$<span class="score_ac">$40$</span>$)$

{% note info no-icon %}
數線上 $[\,0, \ell\,]$ 的位置放有 $n$ 座基地台，已知 $p_0 = 0, \quad p_i < p_{i+1}$ 且 $p_i \equiv 0 \pmod{2}$，你可以詢問他最多 $q$ 次離位置 $x$ 最近的基地台在哪裡（相同距離就選左邊的），最後要回傳所有基地台的位置。

- $\ell = 100\,000$。
- $n = 1000$。
- 給分方法：$q \le 7500$ 滿分。
{% endnote %}

[AC Solution](https://oj.uz/submission/440944) #
[Binary Search](https://oj.uz/submission/440817)

詢問得到的陣列會長 $[\,0, \ldots, 1, \ldots, i, \ldots, n-1\,]$ 這樣子，每個數字都會出現至少一次且值非嚴格遞增。可以二分搜出每個 $p_c = x$ 且 $p_{c+1} = x+1$ 的位置並得到 $c$ 就是 $x$ 跟 $x+1$ 的中點。這樣 query 的次數會是 $\mathcal{O}(n \lg \ell) \approx 20\,000$ 次，拿到 <span class="score_70">$72.85$ 分</span>。

不過，每一段的長度平均是 $\frac{\ell}{n} = 100$，如果可以先花幾次把陣列分塊，大概就只需要再 $\mathcal{O}(n \lg \frac{\ell}{n}) \approx 7000$ 次詢問。自然而然的就會想到用 CDQ 分治來做，實作也很簡單。

{% note success %}
<details>
<summary>範例 code</summary>
```cpp
void cdq(int nL, int nR, int pL, int pR) {
    if (nL > nR or pL > pR) return;
    if (pL == pR) return chmax(last_place[use_detector(pL)], pL), void();
    int pM = pL + pR >> 1, nM = use_detector(pM);
    chmax(last_place[nM], pM);
    cdq(nL, nM-1, pL, pM-1), cdq(nM, nR, pM+1, pR);
}
```
</details>
{% endnote %}

實際上自己 random 的一些測資，大約會 query $7200 \sim 7300$ 次。

### D - Jelly Flavours ([jelly](https://oj.uz/problem/view/IOI20_jelly))

<span class="score_ac">分數：$100$</span> $(
$<span class="score_ac">$11$</span>$/
$<span class="score_ac">$24$</span>$/
$<span class="score_ac" >$9$</span>$/
$<span class="score_ac">$10$</span>$/
$<span class="score_ac">$14$</span>$/
$<span class="score_ac">$32$</span>$)$

{% note info no-icon %}
有 $n$ 本相異的書，第 $i$ 本書在商店 A 跟商店 B 分別賣 $a_i$ 跟 $b_i$ 元。你現在沒帶錢，但有 A 商店的 $x$ 元折價券跟 B 商店的 $y$ 元折價券，請求出你最多可以買幾本相異的書。

- $n \le 2000$。
- $0 \le x, y \le 10\,000$。
- $0 \le a_i, b_i \le 10\,000$。
{% endnote %}

[AC Solution](https://oj.uz/submission/440487)

每個物品只有 3 種狀態：不選、選 Store A、選 Store B。Subtask 3 提供了很重要的想法，如果先對 $a_i$ 排序，之後會發現存在一個位置 $p$ 使在區間 $[\,0, p)$ 的物品都會在 Store A 或 Store B 買；在區間 $[\,p, N)$ 的物品都會在 Store B 買或是不會買。

{% note info %}
<details>
<summary><h4>簡單的證明</h4></summary>
以 A、B、X 代表在 Store A 買、在 Store B 買、不買的狀態。如果存在一個 A 在 X 後面 $[A, B, A, {\color{red}X}, B, {\color{red}A}, X, B, X]$，那把 A 跟 X 交換一定更好。
</details>
{% endnote %}

剩下就是 DP 了。你需要計算在一個前綴如何用 A 取代掉 B 來使剩下的 B 盡量小，這邊是一個簡單的背包問題，然後後綴就直接暴力計算 B 從小到大 B 可以買幾個。維護前綴是 $\mathcal{O}(x)$；維護後綴是 $\mathcal{O}(n \lg n)$。

總複雜度是 $\mathcal{O}(nx + n^2 \lg n)$。

### NHDK Ten Point Round #7 (Div. 1)

- [Contest link](https://codeforces.com/group/H0qY3QmnOW/contest/316436)

7/4 晚上又一次覺得沒事做，想說來找一場感覺不會太難的比賽來打，就選到了 NHDK 辦ㄉ TPR ㄌ。

題目基本上都蠻簡單的（？，花了兩個小時慢慢把他寫完，就去睡覺ㄌ。

---

## Day 1

- [Judge](https://oj.uz/problems/source/576)
- [Screencast](https://youtu.be/GVPBfpvT6V0)

開始之前先把兩天的題目都印好，因為開始之後就沒辦法跑出去印ㄌ。

### A - 分發糖果 / Distributing Candies ([candies](https://oj.uz/problem/view/IOI21_candies))

<span class="score_10">分數：$11$</span> $(
$<span class="score_ac" >$3$</span>$/
$<span class="score_ac" >$8$</span>$/
$<span class="score_na">$27$</span>$/
$<span class="score_na">$29$</span>$/
$<span class="score_na">$33$</span>$)$

{% note info no-icon %}
給定一長度為 $n$ 的陣列 $c$ 跟 $q$ 次操作，你需要對一個長度為 $n$ 且初始值為 $0$ 的陣列 $a$ 執行操作：

1. $\forall i \in [l_j, r_j], \quad a_i = \min\{c_i, a_i + v_j\}$（放糖果進盒子）；
2. $\forall i \in [l_j, r_j], \quad a_i = \max\{0,   a_i - v_j\}$（從盒子拿糖果）。

最後需要輸出 $a$。

- $n, q \le 200\,000$。
- $1 \le c_i \le 10^9$。
- $1 \le v_j \le 10^9$。
{% endnote %}

[$\mathcal{O}(nq)$ brute force](https://oj.uz/submission/441424) #
[$v_j > 0$](https://oj.uz/submission/441429) #
[$(l_i, r_i) = (0, n-1)$](https://oj.uz/submission/441562)

看到題目的第一眼覺得是[吉如一線段樹](https://codeforces.com/blog/entry/57319)裸題（至少 Subtask 3（盒子容量都相同）是裸題），因為回想起第一次在 IOIC 刻他花了大約 6 小時，而且這題看起來要維護最大、次大、最小、次小，所以把這題放在最後想。

Subtask 1（$n, q \le 2000$）是暴力，本來以為 Subtask 2（只有加值）要用線段樹，後來發現差分就好了 owo。拿到 <span class="score_10">$11$ 分</span>之後，覺得好像對 Subtask 4（每次操作都是全域）有點想法，發現了一些性質：

首先，可以把整個陣列排序，然後你會發現：

1. 每個盒子剩下的空位（$c_i - a_i$）非嚴格遞增；
2. 每次 $\texttt{Add}(l_j, r_j, v_j)$ 操作完會有且僅有一段前綴是滿的（$\exists\,p \Rightarrow (i \in [\,0, p) \Longleftrightarrow a_i = c_i)$）；
3. 每次 $\texttt{Sub}(l_j, r_j, v_j)$ 操作完會有且僅有一段前綴是空的（$\exists\,p \Rightarrow (i \in [\,0, p) \Longleftrightarrow a_i = 0)$）。

接下來的要做的事會長這樣：

1. 找到操作後全空（或全滿）的前綴 $[\,0, p)$；
2. 給 $[\,0, p)$ 那段區間一個代表全空（或全滿）的 tag；
3. 更新前綴 $[\,0, p)$ 跟後面的交界處（$a_{p-1}$ 跟 $a_p$）的差值。

{% note success %}
<details>
<summary>範例 code</summary>
```cpp
for (int i = 1; i <= Q; ++i) {
    int lo = 0, hi = N, mi;
    if (V[i] > 0) {
        /// nothing or full ///
        if (CheckVal(N, i-1) + V[i] >= C[N].X) {
            RangeModify(0, N, -1, i); continue;
        }
        while (lo < hi) {
            mi = lo + hi >> 1;
            if (CheckVal(mi, i-1) + V[i] >= C[mi].X) lo = mi + 1; /// [0, mi] is full
            else hi = mi;                                         /// [mi, N] is not full
        }
        /// [0, lo) is full ///
        PointModify(lo, CheckVal(lo, i-1) - CheckVal(lo-1, i-1));
        RangeModify(0, lo-1, -1, i);
    }
    else {
        /// nothing or empty ///
        ...
    }
}
```
</details>
{% endnote %}

要找一個位置當下的值，就紀錄「上次變空（或變滿）是什麼時候」，再看那時候到現在的每次操作的 $v_j$ 的和就好了。

{% note success %}
<details>
<summary>範例 code</summary>
```cpp
int CheckVal(int idx, int qID) {
    /// push tags from root to idx ///
    ...
    /// pre_V[qID+1] - pre_V[last_change] ///
    if (seg[idx].last_type == "Empty") {
        return pre_V[qID] - pre_V[seg[idx].last_change];
    }
    if (seg[idx].last_type == "Full") {
        return pre_V[qID] - pre_V[seg[idx].last_change] + C[idx].X;
    }
}
```
</details>
{% endnote %}

求答案就是最後再問一輪就好ㄌ。

{% note success %}
<details>
<summary>範例 code</summary>
```cpp
for (int i = 1; i <= N; ++i) ans[C[i].Y] = CheckVal(i, Q);
return ans;
```
</details>
{% endnote %}

最慘的是因為這題實作的部份想太久，最後來不及 de 完 bug，在[結束後 6 分鐘](https://youtu.be/GVPBfpvT6V0?t=18360)才拿到 <span class="score_20">$29$ 分</span>，虧豹 QwQ。

### B - 鑰匙 / Keys ([keys](https://oj.uz/problem/view/IOI21_keys))

<span class="score_30">分數：$37$</span> $(
$<span class="score_ac" >$9$</span>$/
$<span class="score_ac">$11$</span>$/
$<span class="score_ac">$17$</span>$/
$<span class="score_na">$30$</span>$/
$<span class="score_na">$33$</span>$)$

{% note info no-icon %}
有一座地牢，$n$ 個房間每間都有一把不盡相異的鑰匙 $r_i$，且 $m$ 條雙向通道 $(u_j, v_j)$ 每條都有一顆需要鑰匙 $c_j$ 才能開的鎖（不會消耗鑰匙），你要輸出從哪些房間出發可以到達的房間數量最少。

- $n, m \le 300\,000$。
- $0 \le r_i, c_j < n$。
{% endnote %}

[$\mathcal{O}(nm)$ DFS](https://oj.uz/submission/441446)

前 3 個 Subtask 都有 $n, m \le 2000$，用 $n$ 次 DFS 就拿到了，因為之前在 [TPOJ #6 pE](https://drive.google.com/file/d/1G5kHW5mN6tPeCqVI_QxrnF3GaT0U_CHT) 看過一樣的題目，所以就很順利的拿到這 <span class="score_30">$37$ 分</span>。

接下來想了很久，對後面的其他 Subtask 怎麼做都毫無頭緒。

### C - 噴泉公園 / Fountain Parks ([parks](https://oj.uz/problem/view/IOI21_parks))

<span class="score_50">分數：$55$</span> $(
$<span class="score_ac" >$5$</span>$/
$<span class="score_ac">$10$</span>$/
$<span class="score_na">$15$</span>$/
$<span class="score_ac">$20$</span>$/
$<span class="score_ac">$20$</span>$/
$<span class="score_na">$30$</span>$)$

{% note info no-icon %}
有 $n$ 座噴泉，第 $i$ 座噴泉在 $(x_i, y_i)$，座標兩兩相異且必為偶數，你需要判斷可不可行並規劃一種道路構建跟長椅擺放方式使

- 每條道路長度皆為 $2$ 且連接兩座噴泉；
- 所有噴泉必須被道路們連通；
- 每條道路都有一張相鄰的長椅面向他（長椅的座標需為奇數）；
- 兩張長椅不能被放在同個位置。

<!-- -->

- $n \le 200\,000$。
- $2 \le x_i, y_i \le 200\,000$。
{% endnote %}

[$2 \le x_i \le 4$](https://oj.uz/submission/441398) #
[No $2 \times 2$ square](https://oj.uz/submission/441994)

因為這題看起來最有趣就第一個做ㄌ。前兩個 Subtask 都有 $2 \le x_i \le 4$，就算把所有可以連的邊都連起來也只會像下面那樣，一定有解。

<img src="Z7wVLiu.png" style="width: auto; max-width: 150px">

接下來感覺 Subtask 4（只有一種蓋道路的方式）好像可做，不過感覺跟 Subtask 5（沒有任四個噴泉形成 $2 \times 2$ 的方格）蠻像，都不會有像下面兩條<span style="color:orange">橘線</span>或<span style="color:blue">藍線</span>的情況，於是就想出一個跟 $\bmod 4$ 相關的作法：

<img src="r26XQWf.png" style="width: auto; max-width: 120px">

先隨便建一棵樹，對所有的<span style="color:red">平行 $y$ 軸的邊（紅邊）</span>把 <span style="color:blue">$x + y \equiv 2 \pmod{4}$ 的椅子（藍椅）</span>指給他；對所有<span style="color:lime">平行 $x$ 軸的邊（綠邊）</span>把 <span style="color:#FFBF00">$x + y \equiv 0 \pmod{4}$ 的椅子（黃椅）</span>指給他。

<img src="oDF75lk.png" style="width: auto; max-width: 400px">

因為不會有上面平行相鄰的狀況，所以不用擔心一張椅子被指到兩條平行的邊。

{% note success %}
<details>
<summary>範例 code</summary>
```cpp
for (int i = 0; i < M; ++i) {
    if (X[u[i]] == X[v[i]]) {
        int midY = (Y[u[i]] + Y[v[i]]) >> 1;
        if ((X[u[i]] + 1 + midY) % 4 == 2) a[i] = X[u[i]] + 1;
        else a[i] = X[u[i]] - 1;
        b[i] = midY;
    }
}

for (int i = 0; i < M; ++i) {
    if (Y[u[i]] == Y[v[i]]) {
        int midX = (X[u[i]] + X[v[i]]) >> 1;
        if ((Y[u[i]] + 1 + midX) % 4 == 0) b[i] = Y[u[i]] + 1;
        else b[i] = Y[u[i]] - 1;
        a[i] = midX;
    }
}
```
</details>
{% endnote %}

有這 <span style="score_40">$40$ 分</span>讓我放心了許多，可是感覺有很多人會的 Subtask 3（$2 \le x_i \le 6$）一直沒有想法，燒雞的以為是位元 DP owo。

### 小結

- Day 1 總分：<span class="score_10">$11$</span>${}+{}$<span class="score_30">$37$</span>${}+{}$<span class="score_50">$55$</span>${}={}$<span class="score_30">$103$ 分</span>
- Day 1 排名：<span class="medal_cu">$106$</span>$/351$

因為在 IOI 當下也有看 scoreboard，所以清楚的記得有三位選手拿到 <span class="score_30">$38$</span>${}+{}$<span class="score_30">$37$</span>${}+{}$<span class="score_70">$70$</span>${}={}$<span class="score_40">$145$ 分</span>，本來想說拿到 gift 的 <span class="score_20">$29$ 分</span>可以補上不太會寫的大資結，結果耍廢到什麼都沒有 QwQ。

開場打好模板，看了約半小時的題目，就開始寫水分ㄌ。我的策略是先給一題一個小時的時間寫，如果可以拿到精神分數就先換題。

在 C 跟 A 拿到水分之後意外有了 C Subtask 4+5 的想法，多花了一點時間把他寫完，再把 B 的水分拿掉之後總共的時間也才過一半而已，不過有了之前 vir JOISC 的經驗，我知道這之後我就會開始思考力下降，就算吃ㄌ一條巧克力也不會變好。果然，思考了一個小時，實作又花了一個半小時，剛剛好在結束之後作完。

希望明天的 Day 2 可以打好一點 owo，至少可以到銀牌線上ㄅ >////<。

---

## Day 2

- [Judge](https://oj.uz/problems/source/577)
- [Screencast](https://youtu.be/62C07VDg_1g)

### A - DNA 突變 / Mutating DNA ([dna](https://oj.uz/problem/view/IOI21_dna))

<span class="score_ac">分數：$100$</span> $(
$<span class="score_ac">$21$</span>$/
$<span class="score_ac">$22$</span>$/
$<span class="score_ac">$13$</span>$/
$<span class="score_ac">$28$</span>$/
$<span class="score_ac">$16$</span>$)$

{% note info no-icon %}
給定兩個長度 $n$ 且只包含 `A`、`T`、`C` 的字串 $a, b$，接下來會有 $q$ 次詢問，每次給一段區間 $[x, y]$，你需要計算 $a[x..y]$ 最少需要經過幾次「交換兩個字元的位置」來變成 $b[x..y]$。

- $n, q \le 100\,000$。
- $0 \le x \le y \le n-1$。
{% endnote %}

[AC Solution](https://oj.uz/submission/442137)

今年最水 IOI 題，一開始看錯題以為是「交換兩個**相鄰**字元的位置」，結果交上去 WA 才發現根本不需要那麼麻煩 QAQ。

發現之後就把他水掉了，大概只有 Div2B ~ Div2C 左右的難度吧，但是這時已經經過兩個小時了，慘。

### B - 地牢遊戲 / Dungeons Game ([dungeons](https://oj.uz/problem/view/IOI21_dungeons))

<span class="score_50">分數：$50$</span> $(
$<span class="score_ac">$11$</span>$/
$<span class="score_ac">$26$</span>$/
$<span class="score_ac">$13$</span>$/
$<span class="score_na">$12$</span>$/
$<span class="score_na">$27$</span>$/
$<span class="score_na">$11$</span>$)$

{% note info no-icon %}
有 $(n+1)$ 座地牢，其中編號 $i$ $(0 \le i \le n-1)$ 的地牢有一位力量為 $s_i$ 的對手，假設英雄現在在地牢 $x$ 並擁有 $z$ 的力量：

- 如果 $x = n$，遊戲結束；
- 如果 $z \ge s_x$，則 $z \leftarrow z + s_x$ 且 $x \leftarrow w_x$（$w_x > x$）；
- 如果 $z < s_x$，則 $z \leftarrow z + p_x$ 且 $x \leftarrow l_x$。

你需要進行 $q$ 次模擬，每次給你英雄的初始位置 $x$ 跟初始力量 $z$，請求出當遊戲結束時英雄的力量。

- $n \le 400\,000$。
- $q \le 50\,000$。
- $1 \le s_i, p_i, z \le 10^7$。
- $0 \le w_i, l_i \le n$。
- $0 \le x < n$。
{% endnote %}

[AC Solution](https://oj.uz/submission/442807) #
[$n \le 50\,000$](https://oj.uz/submission/442812) #
[Doubling on $s_i = p_i$](https://oj.uz/submission/442814) #
[$\#\{x : x \in s\} = 1$](https://oj.uz/submission/442835) #
[$\#\{x : x \in s\} \le 5$](https://oj.uz/submission/442827) #
[$\mathcal{O}(q(n + C))$ brute force](https://oj.uz/submission/442142)

在寫這題之前先想到 Subtask 2（$s_i = p_i$）有個有趣的性質可以倍增，那就是如果英雄某一場打輸了，那他的力量至少會變成兩倍，所以就做 $\mathcal{O}(\lg n)$ 次「最多可以連勝到哪裡」就會到終點了，複雜度大約是 $\mathcal{O}(\lg n \lg C)$。把暴力寫完之後也把倍增寫掉了，這時才發現倍增的作法可以一次過前兩筆 Subtask www。

接著還剩下約 70 分鐘，接下來只能想 Subtask 3（$\#\{x : x \in s\} = 1$）了，因為 Subtask 3 $\subsetneq$ Subtask 4 $\subsetneq$ Subtask 5 $\subsetneq$ Subtask 6。有了剛剛 Subtask 2 的倍增想法，這邊就變的很好想了，只要同樣用倍增維護「力量 $< s_0$ 走 $2^i$ 步會到哪裡」跟「力量 $\ge s_0$ 走 $2^i$ 步會到哪裡」就能 AC 了，應該也很好寫......

結果我因為開的陣列層數剛剛好只有 $\lceil{\lg(50\,000)}\rceil = 16$ 層，最後一層是代表可以一次走 $2^{15} = 32\,768$ 步的值，結果在某些測資會爛掉，花了 10 分鐘寫完卻花了一小時 debug，最後還是真的找不出 bug 於是就倍增做完亂暴力，意外的在 4:56:56 拿到這唬爛來的 <span class="score_10">$13$ 分</span>。真是不知道該感到笑還是該哭呢 OwO。

話說，這題是前國手何達睿學長出的ㄛ >////<，最後面有他的心得文喵。

### C - 位元移位暫存器 / Bit Shift Registers ([registers](https://oj.uz/problem/view/IOI21_registers))

<span class="score_10">分數：$10$</span> $(
$<span class="score_ac">$10$</span>$/
$<span class="score_na">$11$</span>$/
$<span class="score_na">$12$</span>$/
$<span class="score_na">$25$</span>$/
$<span class="score_na">$13$</span>$/
$<span class="score_na">$29$</span>$)$

{% note info no-icon %}
你有 $100$ 個容量 $2000$ bits 的 register $r_0 \sim r_{m-1}$，你可以進行以下操作：

- $\texttt{move}(t, y)$：$r_t = r_y$；
- $\texttt{store}(t, v)$：$r_t = v$；
- $\texttt{and}(t, x, y)$：$r_t = r_x \land r_y$；
- $\texttt{or}(t, x, y)$：$r_t = r_x \lor r_y$；
- $\texttt{xor}(t, x, y)$：$r_t = r_x \oplus r_y$；
- $\texttt{not}(t, x)$：$r_t = \neg r_x$；
- $\texttt{left}(t, x, p)$：$r_t = r_x \ll p$；
- $\texttt{right}(t, x, p)$：$r_t = r_x \gg p$；
- $\texttt{add}(t, x, y)$：$r_t = r_x + r_y$。

一開始有 $n$ 個 $k$-bit 整數 $c_0 \sim c_{n-1}$ 依序儲存在 $r_0$，其他所有 bits 皆為 $0$，你可以進行最多 $q$ 次操作使：

- $s = 0$：$r_0$ 在 $[\,0, k)$ 區間的 bits 需要是 $\min\limits_{0 \le i \le n-1}\{c_i\}$；
- $s = 1$：$r_0$ 在 $[\,i \cdot k, (i+1) \cdot k)$ 區間的 bits 需要是 $c$ 裡面第 $i$ 小的數字。

其他不在要求區間裡的 bit 可以是任意值。

- 限制（$s = 0$）：$n \le 100$、$k \le 10$、$q = 150$。
- 限制（$s = 1$）：$n \le 100$、$k \le 10$、$q = 4000$。
{% endnote %}

[$s = 0$、$n = 2$、$k \le 2$、$q = 1000$](https://oj.uz/submission/442197)

光是題目敘述就有整整 6 頁，而且他的左移和右移的方向跟 grader 輸出的方向又讓我頭昏腦脹，很久才理解要怎麼實作出東西來。

根據我在「數位電路設計」~~學習~~耍廢的經驗，對兩個 $2$-bit 的數字 $a, b$，有以下式子：

$$\min\{a, b\}_1 = a_1 \cdot (\overline{a_1} \cdot \overline{a_0} + b_1 \cdot b_0 + \overline{a_1} \cdot b_1) + b_1 \cdot \overline{(\overline{a_1} \cdot \overline{a_0} + b_1 \cdot b_0 + \overline{a_1} \cdot b_1)} \notag$$

$$\min\{a, b\}_0 = a_0 \cdot (\overline{a_1} \cdot \overline{a_0} + b_1 \cdot b_0 + \overline{a_1} \cdot b_1) + b_0 \cdot \overline{(\overline{a_1} \cdot \overline{a_0} + b_1 \cdot b_0 + \overline{a_1} \cdot b_1)} \notag$$

我就花了一個多小時在把這個寫出來，結果還用了 $26$ 次操作，只有拿到 <span class="score_10">$10$ 分</span>，然後我就放棄了。

### 小結

- Day 2 總分：<span class="score_ac">$100$</span>${}+{}$<span class="score_50">$50$</span>${}+{}$<span class="score_10">$10$</span>${}={}$<span class="score_50">$160$ 分</span>
- Day 2 排名：<span class="medal_cu">$105$</span>$/351$

多虧有印出題目，不然電腦先卡了大約 20 分鐘應該就會先死去ㄌ www。

策略跟 Day 1 是一樣的，但是因為 dna 跟 register 都太特別了，導致今天根本沒能按照計畫進行。

嘛，題目應該要多讀幾次的，最好可以把自己的理解寫出來再對比一次，不然在「看錯題目」這種小錯誤上花整整一小時還是很燒雞ㄉ，還有有時候遇到真的超級麻煩的題目應該先不要管他，~~只要祈禱大家都拿不到分數就好了~~。

今天整體狀況比較平靜，多虧 dna 超水，讓我沒有遇到「會做卻沒時間做」的狀況（也有我直接把 register 當成實作題的原因啦），Day 2 花在~~寫 code~~ debug 的時間就比 Day 1 多出不少呢，能跟 Day 1 有著幾乎相同的名次也很令我意外吶。

---

## 總結

- 總分：<span class="score_10">$11$</span>${}+{}$<span class="score_30">$37$</span>${}+{}$<span class="score_50">$55$</span>${}+{}$<span class="score_ac">$100$</span>${}+{}$<span class="score_50">$50$</span>${}+{}$<span class="score_10">$10$</span>${}={}$<span class="score_40">$263$ 分</span>
- 排名：<span class="medal_cu">$104$</span>$/351$
- 牌線：<span class="medal_au">$373$</span>$/$<span class="medal_ag">$289$</span>$/$<span class="medal_cu">$203$</span>

如你所見，Day 1、Day 2、總排名呈等差數列，而且有越來越好的趨勢 www。如果 Day 1 再多 6 分鐘就有壓線銀牌ㄌ QwQ。

目前覺得最大的缺陷是沒有調整好自己的心態，對分數沒有執著，有點把這種 virtual 當成在玩的感覺（？

現在，平常在打 ICPC 的時候也是這樣，甚至連正式比賽都有點提不起勁。如果沒辦法對得獎、對分數有執著，基本上就只能當個休閒選手了吧......

希望這個暑假可以讓我重新拿回學習新東西的熱情ㄅ >////<。

---

- [現任國手 WiwiHo 的比賽心得](https://www.wiwiho.me/2021/07/01/ioi2021/)
- [前國手何達睿學長的 dungeons 出題心得](https://hackmd.io/@E3-nUNPsRmy1gPXmWIt8jQ/r1yMcVOhu)
