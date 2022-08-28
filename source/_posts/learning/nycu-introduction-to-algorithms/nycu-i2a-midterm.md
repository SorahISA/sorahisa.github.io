---
title: 演算法概論－期中考
date: 2021-11-20 12:43:11
category:
  - [競程, 比賽心得]
  - [課業, 演算法概論]
tags:
---

好久沒發文了，電腦好像還有些東西沒設定好，沒辦法本機 deploy ;w;

<!-- more -->

---

## 準備階段

本來表定是 9:00 ~ 13:00 的，但是大家進教室之後就已經 9:00 了，還要測試環境，所以就延到 9:35 才開始。

先測一下 gcc 11.2 有支援什麼，發現不能直接 `#include <bits/extc++.h>`，會少東西，也不能宣告 `int _N`，他會說底線開頭的是預留字，但是可以宣告 `int _test` OwO。

在開始前約 10 分鐘，助教說今年的系統會跟以往的 Formosa OJ 不一樣，結果竟然是用 CMS！？而且還有計分板可以看，當下感覺好爽 >////<

{% note info %}
#### 想要 virtual 看看？

如果你想要找有這些題目可以做跟上傳的地方，你可以來 <a href="https://oj.nctu.edu.tw/groups/36/problems/">這裡</a> 上傳。

請注意你會需要先 apply 這個 group，而要等教授按確認可能會需要幾天的時間（教授基本上都不會在意有誰要加 group）。
{% endnote %}

---

## 考試開始

可以直接用測機時打的模板耶！

本來的策略是先看過所有題目跟 Subtask 再去想要用什麼順序去寫，結果...

### B - Spaghetti Tower Again (Spaghetti)

<span class="score_ac">分數：$100$</span> $(
$<span class="score_ac">$30$</span>$/
$<span class="score_ac">$70$</span>$)$
(02:38) 全場首 Submit、全場首殺

> 給你 $N$ 個正整數 $S_i$，接著詢問 $Q$ 次有多少數字在 $[l_i, r_i]$ 內。
> 
> 限制：
> 
> - $\hphantom{0}30\%$：$N \le 10\,000$、$Q \le 5000$。
> - $100\%$：$N \le 1\,000\,000$、$Q \le 500\,000$、$1 \le S_i \le 10^9$。

顯然就是 `upper_bound(ALL(S), r) - lower_bound(ALL(S), l)`，花了一分鐘把東西刻完之後發現題本上的範測複製不起來，只能載他的 .zip 或是手打，於是就乾脆不測範例直接丟，然後他就 AC 了。

接著就把剩下的幾題看完，挑出最水的（已經有人 AC 的）F 來做。

### F - Preventing Conflicts (Conflicts)

<span class="score_ac">分數：$100$</span> $(
$<span class="score_ac">$10$</span>$/
$<span class="score_ac">$90$</span>$)$
(06:50)

> 給你兩個長度為 $N$ 的整數陣列 $A$、$B$，請求出如果可以任意重新排列裡面的元素，變成 $A'$ 跟 $B'$，那 $\sum_{i=1}^{N}{A'_i B'_i}$ 的最小值可以是多少。
> 
> 限制：
> 
> - $\hphantom{0}10\%$：$N \le 10$。
> - $100\%$：$N \le 100\,000$、$|A_i|, |B_i| \le 10\,000$。

經典題，讓 $A$ 順序 $B$ 逆序，相乘就會最小。

因為剩下的題目感覺稍微有點麻煩，所以就先去開一眼就精神掉的 D。

### D - Get Together (Together)

<span class="score_ac">分數：$100$</span> $(
$<span class="score_ac">$25$</span>$/
$<span class="score_ac">$75$</span>$)$
(12:17) 首殺

> 給你 $N$ 個人在數線上的初始位置 $\ell_i$ 以及速度 $v_i$，每個人可以往任意方向用至多 $v_i$ 的速度移動，詢問使全部的人都到同一個位置上的最小時間。
> 精度誤差要 $\le 10^{-6}$。
> 
> 限制：
> 
> - $\hphantom{0}25\%$：$N \le 5000$、最佳解中，所有人會在整數點相遇。
> - $100\%$：$N \le 1\,000\,000$、$|\ell_i| \le 10^9$、$1 \le v_i \le 10^9$。

好好的對答案二分搜就能過了，作業裡有很多這樣的題目。

因為要對浮點數二分搜，所以要固定搜的次數才不會爆炸，我就直接設 $100$ 次ㄌwww。

小插曲：因為慢慢的 C++20 中毒，所以我用了 `std::midpoint` 去求 $\frac{\ell+r}{2}$，交上去就吃了一發 CE。

剩下的題目就是：裸作業題 A、裸作業題 E、（把我打爆的）經典題 C，因為昨天看東區有一題是有帶權的 C，所以我就以為 C 會是防破台題，先丟一邊再說。

### A - Yet Another Good Sequence (Sequence)

<span class="score_ac">分數：$100$</span> $(
$<span class="score_ac">$60$</span>$/
$<span class="score_ac">$40$</span>$)$
(19:01)

> 就是 <a href="https://oj.nctu.edu.tw/problems/1367/">作業</a> 的簡化版，你只能做 $+1$ 的操作，不能 $-1$。
>
> ![](https://i.imgur.com/LzT3CcF.png)
> 
> 限制：
> 
> - $\hphantom{0}60\%$：$N \le 100\,000$。
> - $100\%$：$N \le 2\,000\,000$、$|a_i| \le 10^9$。

作業的版本還需要把左右 merge 起來，或是使用 `nth_element`，考試的簡化版直接往左右兩邊遞迴，回傳一個 $(答案, 最大值)$ 的 pair 就能更新ㄌ。

### E - Awkwardness Continued (Awkwardness)

<span class="score_ac">分數：$100$</span> $(
$<span class="score_ac">$60$</span>$/
$<span class="score_ac">$40$</span>$)$
(26:45) 首殺

> 給你一棵 $N$ 個點的樹的合法前序跟中序表達，你要求出他的後序表達。
> 
> 限制：
> 
> - $\hphantom{0}60\%$：$N \le 10\,000$。
> - $100\%$：$N \le 2\,000\,000$、保證有解。

跟 <a href="https://oj.nctu.edu.tw/problems/1366/">作業</a> 一樣，而且求的是前序，更直觀了。

{% note info %}
<details>
<summary>範例 code</summary>
```cpp
int tok = 0;
vector<int> pre(N), in(N), inv_in(N), post;
void recur(int l, int r) {
    if (l > r) return;
    int rt = pre[tok++], p = inv_in[rt];
    recur(l, p-1), recur(p+1, r);
    post.emplace_back(rt);
}
```
</details>
{% endnote %}

小插曲：因為已經 C++20 中毒，所以我用了 `for (int tok = 0; int &x : in) cin >> x, inv_in[--x] = tok++;` 又吃了一次 CE。

### C - AMD Stocks (Stocks)

<span class="score_ac">分數：$100$</span> $(
$<span class="score_ac">$20$</span>$/
$<span class="score_ac">$80$</span>$)$
(41:36)

> 給你 $N$ 個區間 $[s_i, e_i]$，你要從中選出盡量多個區間使不存在任意位置被超過 $K$ 個區間覆蓋。
> 
> 限制：
> 
> - $\hphantom{0}20\%$：$K = 1$。
> - $100\%$：$1 \le K \le N \le 200\,000$、$1 \le s_i \le e_i \le 10^9$。

因為東區的題目，昨天剛好在討論這題帶權的做法，於是當下以為他很難。然後想了幾分鐘之後突然意識到昨天就討論過不帶權的作法ㄌ，只要 greedy 就能過。

當時沒有仔細的討論細節，所以當下我就直接跟著感覺走，刻了一棵區間加值查詢全域 max 的線段樹，所幸沒有太大的 bug，只有忘記端點離散化之後有 $2N$ 個數字而吃了一次 WA。

## 結語

就這樣，經過了考試約莫 $\frac{1}{6}$ 的時間，成功破台了耶！本來聽說老師想把平均控制在 $40$ 分（$40\%$ 的意思）左右，又有整整四個小時可以寫，所以以為他會比競程一的期中考難，結果很失望（？

昨天在做怪怪的測機的時候，林栢瑋說我們應該要寫一個小時就出來不然不算分，這樣才好玩，沒想到真的可以在一個小時內破台 www。

出來之後意識到其實 C 已經寫過很多次了，去年競程也有這題，PCCA 團練也有這題，但是我每次都還是直接暴力砸線段樹下去做 ._.，其實只要維護一個 `multiset` 就好了。

：「他一定能在 $35$ 分鐘破台。」<br/>
：「喔他寫線段樹喔，那沒救。」

88888888

希望期末考能夠有個夠難的防破台題，或是至少出一點有趣的題目（？
    