# 理论概述

考虑 $f(x)=a_nx^n+\cdots+a_1x+a_0,a_n\neq0$ 无重根. 设 $F=\mathbb Q[a_n,\cdots,a_0]$ 为 $f(x)$ 的系数域. 再设 $f(x)$ 根为 $\alpha_1.\cdots,\alpha_n$ 且 $\alpha_i\neq\alpha_j$. 取 $E=F[\alpha_1.\cdots,\alpha_n]$ 则 $E$ 为 $F$ 的分裂域, 即包含 $f(x)$ 所有根的最小域.

## e.g.

$f(x)=x^2-2$, 则 $\mathbb Q[\sqrt{2}]=\{a+b\sqrt{2}\mid a,b\in\mathbb Q\}$ 为 $f(x)$ 的分裂域. 

其中形如 $F[u]$ 的记法表示在域 $F$ 中添加 $u$ 使其称为域. 更通俗地, 我们仍以上述为例, 我们向 $\mathbb Q$ 中添加 $\sqrt 2$ 后得到了 $\mathbb Q\cup\{\sqrt 2\}$, 但它不是域. 为了让其对加减乘除封闭, 我们只好进行更一般的构造, 进而得到了形如 $a+b\sqrt{2}$ 这样的元素使其对四则运算封闭. 因此将 $\{a+b\sqrt{2}\mid a,b\in\mathbb Q\}$ 定义为 $\mathbb Q[\sqrt{2}]$, 表示向 $\mathbb Q$ 中添加 $\sqrt 2$ 形成的域. 我们把这个过程叫做**域扩张**.

为什么求解上述方程时会进行域扩张? 因为其根不在系数域内.

对于一般的二次方程 $ax^2+bx+c=0$, 由 Vieta 定理 $x_1+x_2=-\dfrac{b}{a},x_1x_2=\dfrac{c}{a}$. 其关于根的对称多项式构成了一个二元方程组, 但是为了解出 $x_1,x_2$, 我们需要构造出 $x_1-x_2$ 的形式才能进行下一步求解. 但是 $x_1-x_2$ 非对称, 而 $(x_1-x_2)^2=(x_1+x_2)^2-4x_1x_2$ 对称, 即 $x_1-x_2=\dfrac{\sqrt{b^2-4ac}}{a}$, 出现了根式! 这极大可能 $\sqrt{b^2-4ac}\notin\mathbb Q$. 因此只有在 $\mathbb Q[\sqrt{b^2-4ac}]$ 中我们才能找到 $ax^2+bx+c=0$ 的根. 这蕴含着扩域的思想.

下面我们考虑根的置换. 其原因类似上例, 要通过构造对称的 $(x_1-x_2)^2$ 进而找到不对称的 $x_1-x_2$, 进而破坏 Vieta 定理的对称性来求得 $x_1,x_2$.

考虑 $f(x)=a_nx^n+\cdots+a_1x+a_0\in K[x]$, 设其根为 $\alpha_1,\cdots,\alpha_n$, 则其分裂域为 $L=K[\alpha_1,\cdots,\alpha_n]$. 若存在映射 $\sigma$ 使 $\sigma(f(x))=0$ 的根仍为 $\alpha_1,\cdots,\alpha_n$, 易于验证 $\sigma$ 是 $L\rightarrow L$ 的域同构. 又 $f(x)\in K[x]$ 且又由 Vieta 定理 $\sigma(a_i)=a_i$, 故 $\sigma\mid_K=id$.

将所有这样的 $\sigma$ 找出, 定义集合 $G=Gal(L/K)=\{域同构\sigma:L\rightarrow L\ :\  \sigma\mid_K=id\}$. 事实上, $Gal(L/K)$ 对映射的复合构成群, 称为 Galois 群. 此时 $Gal(L/K)\cong S_n$.

下面考虑 $f(x)=ax^3+bx^2+cx+d=0\in K[x]$. 由 Vieta 定理, $\left\{\begin{matrix}
x_1+x_2+x_3=-\dfrac b a\\ 
x_1x_2+x_2x_3+x_3x_1=\dfrac c a\\ 
x_1x_2x_3=-\dfrac d a
\end{matrix}\right.$.
其中 $x_1+x_2+x_3$ 的置换群为 $S_3$.

为了解这个方程组, 我们不妨首先找到 $x_1+x_2-x_3$ 来破坏其对称性. 那么是否存在一个域使 $x_1+x_2-x_3$ 在其中有意义?答案是有, 为 $K[\sqrt{B},\sqrt[3]{A+\sqrt B}]$, 其中 $A=\dfrac{27}{2}\cdot\dfrac{b^2-3ac}{3a^2}$, $B=\left(\dfrac{27}{2}\cdot\dfrac{3b^3-9abc+27a^2d}{27a^3}\right)^2+27\left(\dfrac{2b^3-9abc+27a^2d}{27a^3}\right)^3$.

现在联立 $\left\{\begin{matrix}
x_1+x_2+x_3\\ 
x_1+x_2-x_3
\end{matrix}\right.$, 两式相加得到 $2x_1+2x_2$. 因此使其不变的置换为 $\left\{id,\begin{pmatrix}
1 & 2 & 3\\ 
2 & 1 & 3
\end{pmatrix} \right\}\subset S_3$. 同理, 再增加不对称多项式 $x_1-x_2+x_3$ 与上述联立, 此时不变的置换只有 $\{id\}$.

因此得到 $\left\{ id\right\}\subset\left\{id,\begin{pmatrix}
1 & 2 & 3\\ 
2 & 1 & 3
\end{pmatrix}\right\}\subset S_3$. 这便是我们逐步破坏对称性得到的子群列. 同时, 为了使各个不对称多项式有意义, 我们构造出了扩域列 $K_2\supseteq K_1\supseteq K$. 又因为 $Gal(L/K)\cong S_n$, 因此形式化地得到 $Gal(L/K_2)\subseteq Gal(L/K_1)\subseteq Gal(L/K)$ 这个子群列.

由上述推导, 三次方程可用开方的方式求解 $\iff$ $Gal(L/K_2)=\{id\}$.

推广到 $n$ 次的形式. 设 $f(x)=a_nx^n_\cdots+a_1x+a_0\in K_1[x]$. 则其可根式求解 $\iff$ $Gal(L/K_n)=\{id\}$. 这便是 Galois 理论核心的一部分.

下面给出方程可用根式求解的严谨定义.

## Def

设 $f(x)\in K[x]$ 是 $n$ 次多项式, $L=K[z_1,\cdots,z_n]$ 是其分裂域. 若存在域扩张塔 $K=K_1\subset\cdots\subset K_{r+1}=L$ 使 $K_{i+1}=K_i[\alpha_i]$, 其中 $\alpha_i$ 的极小多项式 $\mu_{\alpha_i}(x)=x^{n_i}-a_i\in K_i[x]$ (即所谓的单扩张). 则称 $f(x)$ 在 $K$ 上可解. 上述的域扩张塔称为 $L$ 在 $K$ 上的一个根塔.

这样的定义并不突兀. 首先对于 $K_1\subset K_2$, 即在 $K_1$ 中找到一个元素 $a_1$ 并将其开 $n_1$ 次方得到 $\alpha_1=\sqrt[n_1]{a_1}$, 然后使 $K_2=K_1[\sqrt[n_1]{a_1}]$. 以此类推下去. 这就是为何 $\mu_{\alpha_i}(x)=x^{n_i}-a_i$ 的原因.

与此同时, 注意到每次域的扩张都伴随着 $Gal(L/K_i)$ 的 "缩小".

不妨大胆猜测, 根塔 $K=K_1\subset\cdots\subset K_{r+1}=L$ 与子群链 $Gal(L/K)=G_1\supset\cdots\supset G_{r+1}=\{id\}$ 存在一个一一对应的关系. 因此要研究是否存在这样的根塔, 只需研究其子群链即可.

下面提出问题, 由其一一对应关系, 当 $Gal(L/K)$ 及其子群满足什么关系时, 会出现形如上述的根塔, 即 $Gal(L/K)$ 及其子群满足什么条件时, 方程可根式求解?

我们给出群可解的定义.

## Def

设 $G$ 是有限群, 考虑正规列 $\{1\}=G_{s+1}\lhd\cdots\lhd G_1=G$ 使得 $G_i/G_{i+1}$ 为交换群.

Galois 证明了这样的正规子群列与正规域扩张有一一对应的关系. 因此, 我们得到了 $f(x)$ 可解 $\iff$ $f(x)$ 的 Galois 群 $G_f$ 可解. 即把方程可根式解的问题等价为群是否可解.