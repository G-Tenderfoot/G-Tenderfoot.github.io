# 方程与扩域

下面, 我们以域扩张的定义入手来推导它.

## Def 1

$K$ 是一个域, $K$ 是 $L$ 的子域, 则称 $K\subset L$ 是一个域扩张.

## Def 2

设 $K\subset L$ 是一个域扩张, 则 $L$ 是一个 $K$- 线性空间. $[L:K]:= \dim_K L$ 为扩张次数.

## Def 3

设 $K\subset L$ 是域扩张. 若对于 $\alpha\in L$, 存在 $f(x)\in K[x]$ 使 $f(\alpha)=0$, 则称 $\alpha\in L$ 为 $K$ 上的代数元. 若 $\forall\alpha\in L$, $\alpha$ 为代数元, 则 $K\subset L$ 为代数扩张.

## Def 4

若 $[L:K]<+\infty$ 则称 $K\subset L$ 为有限扩张, 否则为无限扩张.

## Thm 1

设 $F\subseteq K\subseteq L$ 为域扩张. 若 $F\subseteq K$, $K\subseteq L$ 均为有限扩张, 那么 $F\subseteq L$ 也是有限扩张且 $[L:F]=[L:K]\cdot[K:F]$.

### Proof

设 $\alpha_1,\cdots,\alpha_m\in K$ 是 $F$ 上的一组基, $\beta_1,\cdots,\beta_n\in L$ 是 $K$ 上的一组基. $\forall x\in L$, $\exists\lambda_j\in K$ 使 $x=\displaystyle\sum\lambda_j\beta_j$. 而对于任意 $\lambda_j\in K$, 存在 $a_{ij}\in F$ 使 $\lambda_j=\displaystyle\sum a_{ij}\alpha_i$. 带入 $x$, 有 $x=\displaystyle\sum\displaystyle\sum a_{ij}\alpha_i\beta_j$. 即 $x$ 可由 $\alpha_i\beta_j$ 在 $F$ 上线性表出. 因此 $\dim_F L\leqslant m\cdot n$. 下证 $\alpha_i\beta_j$ 在 $F$ 上线性无关. 设 $h_{ij}\in F$ 使 $\displaystyle\sum\displaystyle\sum h_{ij}\alpha_i\beta_j=\displaystyle\sum\displaystyle\sum (h_{ij}\alpha_i)\beta_j=0$. 又由 $\beta_j$ 在 $K$ 上线性无关, 因此 $\displaystyle\sum h_{ij}\alpha_i=0$. 又因为 $\alpha_i$ 在 $F$ 上线性无关, $h_{ij}=0$. 因此 $\alpha_i\beta_j$ 是 $L$ 的一组基. 因此 $\dim_F L= m\cdot n$.

## Def 5 (极小多项式)

设 $K\subseteq L$, $\alpha\in L$ 是 $K$ 上的代数元.令 $\mu_\alpha(x)$ 是 $\left\{f(x)\in K[x]\mid f(\alpha)=0\right\}$ 中次数最小, 首一的多项式. 则称 $\mu_\alpha(x)$ 是 $\alpha$ 在 $K$ 上的极小多项式.

## Thm 2

设 $\alpha$ 是 $K$ 上的代数元. $\mu_\alpha(x)\in K[x]$ 是 $\alpha$ 的极小多项式, 则

1. $\mu_\alpha(x)$ 不可约;
2. 对任意 $f(x)\in K[x]$, 如果 $f(\alpha)=0$ 则 $\mu_\alpha(x)\mid f(x)$;
3. $[K[\alpha]:K]=\deg \mu_\alpha(x)$.

### Proof

1. 设 $\mu_\alpha(x)$ 在 $K[x]$ 中可约. 不妨设 $\mu_\alpha(x)=f_1(x)f_2(x)$. 其中 $\deg f_i(x)<\mu_\alpha(x)$. 则 $\mu_\alpha(\alpha)=f_1(\alpha)f_2(\alpha)=0$. 又由 $L$ 是整环, $f_1(\alpha)=0$ 或 $f_2(\alpha)=0$, 与 $\mu_\alpha(x)$ 次数最小矛盾.
2. 设 $f(x)=\mu_\alpha(x)g(x)+r(x)$, 则 $r(x)\equiv 0$ 或 $\deg r < \deg\mu_\alpha$. 由 $f(\alpha)=\mu_\alpha(\alpha)g(\alpha)+r(\alpha)=0$, $r(\alpha)\equiv 0$. 因此 $\mu_\alpha(x)\mid f(x)$.
3. 考虑取值映射 $\psi_\alpha:K[x]\rightarrow K[\alpha]$, $f(x)\mapsto f(\alpha)$. 则 $\psi_\alpha$ 是环同态. 因此 $\ker\psi_\alpha=\left\{f(x)\in K[x]\mid f(\alpha)=0\right\}=(\mu_\alpha(x))$ (即由 $\mu_\alpha(x)$ 生成的理想). 由环同态基本定理, $K[x]/(\mu_\alpha(x))\cong K[\alpha]$. 注意到 $1,\alpha,\cdots,\alpha^{n-1}$ 是 $K[\alpha]$ 的一组基, 否则这与 $\mu_\alpha(x)$ 次数最小性矛盾.

## Cor 1

设 $K\subseteq L$ 是域扩张, $\alpha,\beta\in L$ 是 $K$ 上的代数元, 则 $\alpha\pm\beta,\alpha\beta,\alpha\beta^{-1}$ 也是 $K$ 上的代数元. 特别地, $\left\{\alpha\in L\mid \alpha 是 K 上的代数元\right\}$ 是一个域.

## Def 6 (分裂域)

设 $K$ 是一个域. $f(x)\in K[x]$ 非零首一. $L\supseteq K$ 是扩域. $L$ 称 $f(x)$ 的分裂域,如果

1. 存在 $\alpha_1,\cdots,\alpha_m\in L$ 使 $f(x)=(x-\alpha_1)\cdots(x-\alpha_m)$;
2. $L=K[\alpha_1,\cdots,\alpha_m]$.

## Thm 3

设 $K$ 是一个域, $f(x)\in K[x]$ 非零首一, 则存在 $f(x)$ 的分裂域 $L\supseteq K$.

### Proof

对 $n=\deg f(x)$ 进行归纳. $n=1$ 时, $f(x)=x+a_0$, 取 $L=K$ 即可.

设 $\deg f < n$ 成立, 即对于任意域 $K$, $f(x)\in K[x], \deg f\leqslant n-1$ 都存在 $f(x)$ 的分裂域 $L$. 考虑 $f(x)\in K[x], \deg f= n$. 由 $K[x]$ 是 PID, $K[x]$ 是 UFD. 因此 $f(x)=f_1^{m_1}(x)\cdots f_k^{m_k}(x)$. 若 $\deg f_i=1$, 取 $K=L$ 即可. 否则不妨设 $\deg f_1\geqslant 2$ 不可约. 令 $K'=K[x]/(f_1(x))$, 则 $K'$ 是一个域, 且对于任意 $\overline{x}\in K'$, 取 $\alpha$ 是 $\overline{x}$ 的代表元, 有 $f_2(\alpha)\cdots f_k(\alpha)\neq 0$. 若 $f_1(\alpha)=0$, 则 $f(\alpha)=0$. 因此, 在 $K'[x]$ 中, $f(x)=(x-\alpha)g(x)$ ,$g(x)\in K'[x]$ 且 $\deg g=n-1$. 由归纳假设, 存在 $L\supseteq K'$ 使 $L$ 是 $g(x)$ 的分裂域. 即 $g(x)=(x-\alpha_1)\cdots(x-\alpha_{n-1})\in L[x]$. 故 $L=K'[\alpha_1,\cdots,\alpha_{n-1}]=K[\alpha,\alpha_1,\cdots,\alpha_{n-1}]$, $f(x)=(x-\alpha)(x-\alpha_1)\cdots(x-\alpha_{n-1})\in L[x]$. 即 $L$ 是 $f(x)$ 的分裂域.

## Thm 4 (重要)

设 $\eta:K\rightarrow\overline{K}$ 是域同构. 任意 $f(x)=a_nx^n+\cdots+a_x+a_0\in K[x]$, 令 $\overline{f}(x)=\overline{a_n}x^n+\cdots+\overline{a_1}x+\overline{a_0}\in\overline{K}[x]$. $\overline{a_i}=\eta(a_i)$. 记 $L,\overline{L}$ 分别为 $f(x),\overline{f}(x)$ 的分裂域. 令 $G_{\eta,K}=\left\{域同构 \varphi:L\rightarrow\overline{L}\mid\varphi\mid_K=\eta\right\}$. 则 $|G_{\eta,K}|\leqslant [L:K]$ 且等号成立当且仅当 $\overline{f}(x)$ 在 $\overline{L}$ 中无重根.

### Proof

对 $[L:K]$ 进行归纳.

$[L:K]=1$ 时, $L=K$, 因此 $f(x)$ 在 $K[x]$ 中是一次因子的乘积. $\overline{f}(x)$ 在 $\overline{K}[x]$ 中也是一次因子乘积. 因此 $\overline{L}=\overline{K}$, 故 $G_{\eta,K}=\{\eta\}$. 因此 $|G_{\eta,K}|=1\leqslant [L:K]=1$.

$[L:K]>1$ 时, 设小于 $[L:K]$ 的情形成立. 此时 $f(x)$ 至少有一个不可约因子 $f_1(x)\in K[x]$ 且 $\deg f_1\geqslant 2$. 取 $\alpha_1\in L$ 使 $f_1(\alpha_1)=0$. 记 $\mu_{\alpha_1}(x)\in K[x]$ 是 $\alpha_1$ 的极小多项式. 令 $L_1=K[x]/(\mu_{\alpha_1}(x))=K[\alpha_1]$ (由 **Thm 2** 3. 的证明过程. 事实上,这里把同构的域看作同一个域, 这是无关紧要的). 则 $[L_1:K]=\deg \mu_{\alpha_1}\geqslant 2$. 令 $H_\eta(L,\overline{L})=\left\{单同态\phi:L_1\rightarrow\overline{L}\mid\phi\mid_K=\eta\right\}$. 

我们断言 $H_\eta(L,\overline{L})=\{\eta_1,\cdots,\eta_m\}$, 其中 $m$ 是 $\overline{\mu_{\alpha_1}}(x)$ 在 $\overline{L}$ 中不同根的个数. 

倘若断言成立, 则 $|H_\eta|\leqslant\deg \mu_{\alpha_1}=[L_1:K]$ 且等号成立当且仅当 $\overline{\mu_{\alpha_1}}(x)$ 在 $\overline{L}$ 中无重根. 由 $[L_1:K]\geqslant 2$ 得 $[L:L_1]<[L:K]$. 令 $\overline{L_1}=\eta_i(L_1)$ 则 $f(x)\in L_1[x]$, $\overline{f}(x)\in\overline{L_1}[x]$. 则 $L,\overline{L}$ 可看成 $f(x)\in L_1[x],\overline{f}(x)\in\overline{L_1}[x]$ 的分裂域. 又归纳假设 $|G_{\eta,L_1}|\leqslant [L:L_1]$ 且等号成立当且仅当 $\overline{f_1}(x)$ 在 $\overline{L}$ 中无重根. 

最后证明断言: $\forall \phi\in H_\eta$, $\phi(\alpha_1)$ 是 $\overline{\mu_{\alpha_1}}(x)$ 的根且 $\phi$ 由 $\phi(\alpha_1)$ 唯一确定.

记 $\mu_{\alpha_1}(x)=b_kx^k+\cdots+b_1x+b_0$. 则 $0=b_k\alpha_1^k+\cdots+b_1\alpha_1+b_0\in L_1$. 因此 $0=\phi(b_k\alpha_1^k+\cdots+b_1\alpha_1+b_0)$ $=\overline{b_k}\phi(\alpha_1)^k+\cdots+\overline{b_1}\phi(\alpha_1)+\overline{b_0}$. 因此 $\phi(\alpha_1)$ 是 $\overline{\mu_{\alpha_1}}(x)$ 的根. 因此 $|H_\eta(L,\overline{L})|\leqslant m$. 故只需证明若 $\beta\in\overline{L}$ 是 $\overline{\mu_{\alpha_1}}(x)$ 的根, 则存在单同态 $\phi:L_1\rightarrow\overline{L},\alpha_1\mapsto\beta$.

考虑取值映射 $\psi_{\alpha_1}: K[x]\rightarrow L, h(x)\mapsto h(\alpha_1)$ 是满同态. 则有 $K[x]/\ker\psi_{\alpha_1}\cong L_1$. 又因为 $\ker\psi_{\alpha_1}=(\mu_{\alpha_1}(x))$, 故 $K[x]/(\mu_{\alpha_1}(x))\xrightarrow[\backsim]{\overline{\psi_{\alpha_1}}}L_1$. 考虑 $\eta_\beta :K[x]\rightarrow \overline{L},h(x)\mapsto\overline{h}(\beta)$. 由 $K[x]$ 是 PID, $\ker \eta_\beta=(h_0(x))$. 另一方面, 由 $\eta_\beta(\mu_{\alpha_1}(x))=0$ 有 $\mu_{\alpha_1}(x)\in\ker\eta_\beta$. 故 $h_0(x)\mid \mu_{\alpha_1}(x)$. 故 $h_0(x)\backsim\mu_{\alpha_1}(x)$. 因此 $\overline{\eta_\beta}:K[x]/(\mu_{\alpha_1}(x))\rightarrow\overline{L}$ 是单射. 令 $\phi=\overline{\eta_\beta}\cdot\overline{\eta_\alpha}^{\ -1}:L_1\rightarrow\overline{L}$ 是单同态且满足条件.

### Remark 1

对于 $[L:K]>1$, 我们先找到使归纳假设成立的情况, 即 "温柔地" 向 $K$ 中添加一个元 $\alpha_1$, 使其成为 $L_1=K[\alpha_1]$. 进而构造出了类似题中 $G_{\eta,K}$ 的 $H_\eta$. 对于 $H_\eta$, 设其满足题中要求, 即若 $\overline{\mu_{\alpha_1}}(x)$ 在 $\overline{L}$ 中不同根个数为 $m$, 则 $[L_1=K[\alpha_1]:K]=\deg \mu_{\alpha_1}\leqslant m$. 为此, 令 $|H_\eta|=m$, 即令 $H_\eta=\{\eta_1,\cdots,\eta_m\}$ 即可完成证明.

那么我们只需证明 $H_\eta$ 满足形如 $\{\eta_1,\cdots,\eta_m\}$ 的形式即可, 即只需证明若 $\beta\in\overline{L}$ 是 $\overline{\mu_{\alpha_1}}(x)$ 的根, 则存在单同态 $\phi:L_1\rightarrow\overline{L},\alpha_1\mapsto\beta$.

### Remark 2

事实上, 可以通俗地把 $|G_{\eta,K}|$ 看成不同根的个数, $[L:K]$ 看成多项式的次数. 这样题中 $|G_{\eta,K}|\leqslant [L:K]$ 且等号成立当且仅当 $\overline{f}(x)$ 在 $\overline{L}$ 中无重根这一结果就很自然.

### Remark 3

注意, $|G_{\eta,K}|$ 总是 $>0$ 的, 这也就意味着无论什么情况, 只要满足题中条件, 我们总能找到域同构 $\varphi:L\rightarrow\overline{L}$ 使得 $\varphi\mid_K=\eta$.

## Cor 2 (重要)

设 $L$ 是 $f(x)\in K[x]$ 的一个分裂域. 令 $G=Gal(L/K)=\left\{域同构\varphi:L\rightarrow L\mid\varphi\mid_K=id\right\}$ 则 $|G|\leqslant [L:K]$, 且等号成立当且仅当 $f(x)$ 在 $L$ 无重根.

### Proof

在 **Thm 4** 中令 $K=\overline{K},\eta=id$ 即可.

## Thm 5

$L$ 是 $f(x)\in K[x]$ 的分裂域, 则 $f(x)$ 在 $L$ 上无重根 $\iff$ $(f(x),f'(x))=1$.

### Proof

$\Leftarrow:$ 则 $f(x)$ 与 $f'(x)$ 在 $L$ 中无公共根. 因此无重根. 否则如果 $\alpha\in L$ 是 $f(x)$ 的 $k$ 重根, $k>1$, 则 $f(x)=(x-\alpha)^kf_1(x)$, $f'(x)=k(x-\alpha)^{k-1}f_1(x)+(x-\alpha)^kf'_1(x)$. 从而 $\alpha$ 是 $f(x)$ 与 $f'(x)$ 的公共根, 矛盾.

$\Rightarrow:$ 设 $f(x)=(x-\alpha_1)\cdots(x-\alpha_n)$, 其中 $\alpha_i\neq\alpha_j$. 则 $f'(x)=\displaystyle\sum\dfrac{f(x)}{x-\alpha_i}$, 此时 $(x-\alpha_i)\nmid f'(x)$. 因此 $(f(x),f'(x))=1$.

