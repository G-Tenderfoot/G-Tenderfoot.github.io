---
comments: true
---
# 群与域扩张

这一节, 我们将逐步建立 $Gal(L/K)$ 的子群与 $K\subset E\subset L$ 中间域的对应关系.

## Lem 1 [Artin 引理]

设 $G\subseteq Aut(L)$ 为有限子群, 则 $L^G=\left\{x\in L\mid \sigma(x)=x,\forall\sigma\in G\right\}$ 是 $L$ 的一个子域且 $[L:L^G]\leqslant |G|$.

### Proof

1. 证明 $L^G$ 是 $L$ 的子域.首先 $0_L\cdot 1_L\in L^G$, 因此 $L^G\neq\varnothing$. $\forall a,b\in L^G$, 有 $\sigma(a)=a,\sigma(b)=b$. 则 $\forall\sigma\in G$, 有 $\sigma(a\pm b)=\sigma(a)\pm\sigma(b)=a\pm b$. $\sigma(ab)=\sigma(a)\sigma(b)=ab$. $\sigma(a^{-1})=\sigma(a)^{-1}=a^{-1}$.
2. 记 $G=\{\eta_1=id,\eta_2,\cdots,\eta_n\}$. 只需证 $\forall\alpha_1,\cdots,\alpha_m\in L$, $(m>n)$ 在 $L^G$ 上线性相关. 考虑 $\begin{pmatrix}\eta_1(\alpha_1) & \cdots &\eta_1(\alpha_m) \\\vdots & \ddots &\vdots\\ \eta_n(\alpha_1) & \cdots &\eta_n(\alpha_m)\end{pmatrix}$$\begin{pmatrix}x_1\\ \vdots\\ x_m\end{pmatrix}=0$. 由 $m>n$, 方程组在 $L$ 上有非零解. 令 $(a_1',\cdots,a_m')$ 是非零分量最少的非零解. 不妨设 $a_1'\neq 0$. 令 $(a_1')^{-1}\cdot (a_1',\cdots,a_m')$ $=(a_1=1,\cdots,a_m)$. 则 $(a_1,\cdots,a_m)$ 也是非零分量最少的解. 由 $\eta_i$ 的同构关系, 要证 $\forall\alpha_1,\cdots,\alpha_m\in L$, 在 $L^G$ 上线性相关, 即证 $\eta_i(\alpha_1),\cdots,\eta_i(\alpha_m)$ 在 $L^G$ 上线性相关. 即找到一组系数 $(a_1,\cdots,a_m)\in L^G$ 为上述方程的解. 目前已经找到这一组解, 下面我们证明它属于 $L^G$. 否则, 不妨设 $a_2\in L^G\ (a_1\neq 0)$. 则存在 $\eta_k\in G$ 使 $\eta_k(a_2)\neq a_1$. 注意到 $(x_1,\cdots,x_m)=(\eta_k(a_1),\cdots,\eta_k(a_m))$ 也是一组非零解, 因为 $\displaystyle\sum\limits_j\eta_i(\alpha_j)\cdot\eta_k(a_j)$ $=\displaystyle\sum\limits_j\eta_k(\eta_k^{-1}\eta_i(\alpha_j)a_j)$ $=\eta_k(\displaystyle\sum\limits_j\eta_k^{-1}\eta_i(\alpha_j)a_j)=\eta_k(0)=0$. 此时 $(a_1=1,\cdots,a_m)-(\eta_k(a_1),\cdots,\eta_k(a_m))$ 也是一组解. 它等于 $(0,a_2-\eta_k(a_2)\neq 0,\cdots,a_m-\eta_k(a_m)\neq 0)$. 这也是一组非零解, 但其非零分量个数小于 $(a_1,\cdots,a_m)$. 矛盾.

## Thm 6 (重要)

设 $K\subseteq L$ 是域扩张, 则下述等价:

1. $L$ 是可分多项式 $f(x)\in K[x]$ 的分裂域;
2. 存在有限子群 $G\subseteq Aut(L)$ 使 $L^G=K$;
3. $K\subseteq L$ 是 Galois 扩张.

### Proof

1 $\Rightarrow$ 2: 取 $G=Gal(L/K)$. 由 $f(x)$ 可分, 有 $|G|=[L:K]$ (由 **Cor 4**). 另一方面, $L$ 也是 $f(x)\in L^G[x]$ 的分裂域, 因此 $|Gal(L/L^G)|=[L:L^G]$. 而 $Gal(L/L^G)=\left\{域同构\varphi:L\rightarrow L\mid\varphi\mid_{L^G}=id\right\}$, $L^G=\{x\in L\mid\forall\sigma\in G,\sigma(x)=x\}$. 即对于 $\varphi\in G=Gal(L/K)$, 有 $\varphi\mid_{L^G}=id$, 与此同时, $\varphi\mid_K=id$. 因此有 $Gal(L/K)=Gal(L/L^G)$. 又因为 $[L:K]=[L:L^G]\cdot[L^G:K]$. 又 $[L:K]=[L:L^G]$, 故 $[L^G:K]=1$. 即 $L^G=K$.

2 $\Rightarrow$ 3: $[L:K]=[L:L^G]\leqslant |G| < +\infty$ (**Lem 1**), 故为有限扩张. $\forall\alpha\in L$, 令 $\mu_\alpha(x)\in K[x]$ 是 $\alpha$ 的极小多项式. 考虑 $\{\sigma(\alpha)\mid\forall\sigma\in G\}=\{\alpha=\alpha_1,\alpha_2,\cdots,\alpha_m\}$. 其中 $\alpha_i\neq\alpha_j,i\neq j$. 由 $\mu_\alpha(\alpha)=0$, 有 $\mu_\alpha(\sigma^{-1}\sigma(\alpha))=0$, 即 $\sigma(\mu_\alpha(\sigma^{-1}\sigma(\alpha)))=\mu_\alpha(\sigma(\alpha))=\sigma(0)=0$. 因此有 $\mu_\alpha(\sigma(\alpha))=0$, 即 $\mu_\alpha(\alpha_i)=0$. 因此在 $L[x]$ 中, $g(x)=(x-\alpha_1)\cdots(x-\alpha_m)\mid\mu_\alpha(x)$. 展开, $g(x)=x^m-\sum\alpha_ix^{m-1}+\cdots+(-1)^m\alpha_1\cdots\alpha_m$ (**Vieta 定理**). 而 $\forall\sigma\in G$, $\sigma(\sum\alpha_i)=\sum\sigma(\alpha_i)$, $\sigma(\sum\alpha_i\alpha_j)=\sum\sigma(\alpha_i)\sigma(\alpha_j)\cdots$. 因此 $g(x)\in L^G[x]=K[x]$. 此时 $\mu_\alpha(x)\mid g(x)$. 所以 $\mu_\alpha(x)=g(x)$. 从而可分, 正规.

3 $\Rightarrow$ 1: $K\subseteq L$ 有限, 即存在 $\beta_1,\cdots,\beta_s\in L$ 使 $L=K[\beta_1,\cdots,\beta_s]$. 令 $f(x)=\mu_{\beta_1}(x)\cdots\mu_{\beta_s}(x)$ 则 $f(x)$ 可分, $L$ 是可分多项式 $f(x)$ 的分裂域.

### Remark

2 $\Rightarrow$ 3 中, $\sigma(\sum\alpha_i)=\sum\alpha_i$, $\sigma(\sum\alpha_i\alpha_j)=\sum\alpha_i\alpha_j\cdots$. 其保持不变的原因是由 **Cor 5** 与对称多项式共同作用的. 由于 $\alpha_i$ 是 $\mu_\alpha(x)$ 的根, 由 **Cor 5**, $\sigma(\alpha_i)=\alpha_j$. 而又由对称多项式的性质, 原值不变.

## Thm 7 [Galois 对应] (重要)

$K\subseteq L$ 是 Galois 扩张. $G=Gal(L/K)$. 设 $\Gamma=\{H\subseteq G\mid H 是子群\}$. $\Sigma=\{E\mid K\subseteq E\subseteq L 是中间域\}$. 则 $\phi:\Gamma\rightarrow\Sigma$, $H\mapsto L^H$. $\psi:\Sigma\rightarrow\Gamma$, $E\mapsto Gal(L/E)$ 是双射且 $\phi,\psi$ 互为逆映射.

### Proof

只需证明 $\phi\cdot\psi=id_\Sigma,\psi\cdot\phi=id_\Gamma$, 即证 $H=Gal(L/L^H)$, $L^{Gal(L/E)}=E$. 

由 $L^H=\{x\in L\mid\forall\sigma\in H,\sigma(x)=x\}$, $Gal(L/L^H)=\{域同构\varphi:L\rightarrow L\mid\varphi\mid_{L^H}=id\}$. 则 $\forall\sigma\in H$, $\sigma\in Gal(L/L^H)$. 因此 $H\subseteq Gal(L/L^H)$. 因为 $K\subseteq L$ 是 Galois 扩张, 因此 $L$ 是某个可分多项式 $f(x)\in K[x]$ 的分裂域, 即 $L$ 是可分多项式 $f(x)\in L^H[x]$ 的分裂域. 由 **Cor 4**, $|Gal(L/L^H)|=[L:L^H]$. 由上述 $H\subseteq Gal(L/L^H)$, 有 $|H|\leqslant|Gal(L/L^H)|=[L:L^H]\leqslant |H|$ (**Lem 1**). 因此 $|H|=|Gal(L/L^H)|$, 进而 $H=Gal(L/L^H)$. 

下证 $L^{Gal(L/E)}=E$. 令 $H=Gal(L/E)$ 则 $K\subseteq E\subseteq L^H\subseteq L$, $Gal(L/L^H)=H$. 类似地, $E\subseteq L,L^H\subseteq L$ 都是 Galois 扩张. 因此 $|Gal(L/E)|=|H|=[L:E]$, $|Gal(L/L^H)|=|H|=[L:L^H]$. 因此 $[L:E]=[L:L^H]$, 而 $[L:E]=[L:L^H]\cdot[L^H:E]$. 所以 $[L^H:E]=1$ 即 $L^H=E$.

### Remark

对于 $\phi\cdot\psi$, 有 $E\mapsto Gal(L/E)\mapsto L^{Gal(L/E)}$. 为了证明它是 $id_\Sigma$, 我们需要证明 $L^{Gal(L/E)}=E$. 记 $H=Gal(L/E)$. 根据第一部分证明, 我们有 $H=Gal(L/L^H)$, 且由其是 Galois 扩张, 因此 $|H|=|Gal(L/E)|=[L:E]$,$|H|=|Gal(L/L^H)|=[L:L^H]$. 因此 $[L^H:E]=1$ 即 $L^H=E$.

在这个过程中, 我们用到了一个事实: 若 $f(x)\in K[x], K\subseteq L$ 是 Galois 扩张, 那么对于 $K\subseteq E\subseteq L, f(x)\in E[x]$, $E\subseteq L$ 也是 Galois 扩张.

## Cor 6 [本原元素定理]

设 $K\subseteq L$ 是有限, 可分扩张, $|K|=+\infty$. 则存在 $\alpha\in L$ 使 $L=K[\alpha]$.

### Proof

$K\subseteq L$ 是有限扩张, 即存在 $\beta_1,\cdots,\beta_s\in L$ 使 $L=K[\beta_1,\cdots,\beta_s]$. $K\subseteq L$ 可分, 因此 $\mu_{\beta_i}(x)\in K[x]$ 可分. 令 $f(x)=\mu_{\beta_1}(x)\cdots\mu_{\beta_s}(x)\in K[x]$. 设 $\overline{L}$ 是可分多项式 $f(x)\in K[x]$ 的分裂域, 则 $K\subseteq L$ 是 Galois 扩张. 由 **Thm 7**, $K\subseteq\overline{L}$ 的中间域只有有限个. 因此 $K\subseteq L$ 的中间域也只有有限个. 下面对 $s$ 进行归纳.

$s=1$ 时, 成立.

$s=2$ 时, 即 $L=K[\beta_1,\beta_2]$. 考虑 $L_a=K[\beta_1+a\beta_2], a\in K$. 则对于 $\forall a\in K$, 有 $K\subseteq L_a\subseteq L$. 由 $|K|=+\infty$, 存在 $a_1\neq a_2$ 使 $K[\beta_1+a_1\beta_2]=K[\beta_1+a_2\beta_2]$, 即 $L_{a_1}=L_{a_2}$. 记 $\alpha=\beta_1+a_1\beta_2$ 则 $\beta_1+a_1\beta_2\in K[\alpha]$, $\beta_1+a_2\beta_2\in K[\alpha]$. 因此 $\beta_1,\beta_2\in K[\alpha]$, 即 $K[\alpha]=K[\beta_1,\beta_2]$.

$s\geqslant 3$ 时, 由归纳, 存在 $\alpha\in L$ 使 $K[\beta_1,\cdots,\beta_{s-1}]=K[\alpha]$. 此时 $K[\beta_1,\cdots,\beta_s]=K[\alpha,\beta_2]$. 由 $s=2$ 的情形, 存在 $\widetilde{\alpha}\in L$ 使 $K[\alpha,\beta_2]=K[\widetilde{\alpha}]$.

## Def 10 [方程可解]

设 $f(x)\in K[x]$ 是 $n$ 次多项式. $L=K[\alpha_1,\cdots,\alpha_n]$ 是其分裂域. 如果存在域扩张塔 $K=K_1\subseteq\cdots\subseteq K_r=L$ 使 $K_{i+1}=K_i[\beta_i]$, 其中 $\beta_i$ 在 $K_i$ 上的极小多项式 $\mu_{\beta_i}(x)$ 形如 $x^{n_i}-b_i\in K_i[x]$ 则称 $f(x)$ 可解. 上述域扩张塔称为根塔. 由 **Thm 7**, 其对应一个子群链 $G=Gal(L/K)\supseteq\cdots\supseteq Gal(L/K_r)=\{e\}$.