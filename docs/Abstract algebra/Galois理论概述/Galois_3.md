---
comments: true
---

# 等价关系与商群

接着, 我们对 $Gal(L/K)$ 进行研究, 讨论它满足什么条件时对应一个形如上述的根塔. 为此, 我们先进一步了解群的知识.

## Def 11

设 $G$ 是一个群, $H\subseteq G$ 是子群. $\forall x,y\in G$, 定义 $x\sim y \Leftrightarrow x^{-1}y\in H$. 可验证 $\sim$ 为等价关系. 记 $\overline{x}=\{y\in G\mid x^{-1}y\in H\}$ $=\{y\in G\mid x\sim y\}=xH$ 为 $x$ 所在等价类, 称为 $x$ 关于 $H$ 的左陪集, $x$ 为 左陪集 $xH$ 的代表元. 类似地, $x\sim y \Leftrightarrow xy^{-1}\in H$ 也定义了等价关系. $\overline{y}=\{x\in G\mid xy^{-1}\in H\}=Hy$ 称为 $y$ 关于 $H$ 的右陪集, $y$ 为右陪集 $Hy$ 的代表元.

## Thm 8

设 $G$ 是一个群, $H\subseteq G$ 是子群, 则 $G=\bigcup\limits_{x\in G}xH=\bigcup\limits_{y\in G}Hy$, 且 $xH,Hy$ 与 $H$ 之间有双射.

### Proof

考虑 $\varphi: H\rightarrow xH, h\mapsto xh$, 则 $\varphi$ 既单又满.

## Cor 7

设 $G$ 为有限群, 则 $|G|=|H|\cdot[G:H]_L=|H|\cdot[G:H]_R$. 其中 $[G:H]_L$ 是 $H$ 在 $G$ 中的左陪集个数, $[G:H]_R$ 是 $H$ 在 $G$ 中的右陪集个数.

## Def 12

$[G:H]=[G:H]_L=[G:H]_R$ 称为 $H$ 在 $G$ 中的指数.

## Cor 8 [Lagrange 定理]

设 $H$ 是有限群 $G$ 的子群, 则 $|H|\mid |G|$.

## Cor 9

设 $|G|<+\infty$, 则 $\forall g\in G$, $g^{ |G| }=e_G$. 特别地, 如果 $|G|$ 为素数则 $G$ 为循环群, 即非单位元都是生成元.

## Cor 10

设 $|G|<+\infty$, $K,H$ 为 $G$ 的子群且 $K\subseteq H\subseteq G$, 则 $[G:K]=[G:H]\cdot[H:K]$.

### Proof

$|G|=|K|[G:K]$, $|G|=|H|[G:H]$, $|H|=|K|[H:K]$, 因此 $|H|[G:H]=|K|[G:K]$, $|K|[H:K][G:H]=|K|[G:K]$, 即 $[G:K]=[G:H][H:K]$.

## Def 13 [正规子群]

子群 $H\subseteq G$ 称为正规子群如果 $\forall x\in G, xH=Hx$, 即 $xHx^{-1}=H$. 记为 $H\lhd G$. 此时左陪集与右陪集统称为 $H$ 的陪集.

## Thm 9

设 $H$ 为 $G$ 的子群, 令 $G/H=\{xH\mid x\in G\}$. 则 $G/H\times G/H\rightarrow G/H$, $(xH,yH)\mapsto (xy)H$ 是良定的当且仅当 $H\lhd G$. 若 $H\lhd G$ 则 $G/H$ 关于上述运算是群, 称为商群. 记 $p:G\rightarrow G/H, x\mapsto xH$ 且 $\ker p=H$.

### Proof

$(xH,yH)=(xy)H$ 良定 $\Leftrightarrow$ $\forall xH=aH, yH=bH$ 有 $(xy)H=(ab)H$ $\Leftrightarrow$ $\forall x^{-1}a\in H, y^{-1}b\in H, (xy)^{-1}ab\in H$ $\Leftrightarrow$ $\forall x^{-1}a\in H, y^{-1}b\in H$, 有 $y^{-1}x^{-1}ab=y^{-1}x^{-1}ayy^{-1}b\in H$ $\Leftrightarrow$ $\forall x^{-1}a\in H, y^{-1}b\in H$, 有 $y^{-1}x^{-1}ay\in H$ $\Leftrightarrow$ $\forall x^{-1}a\in H, y^{-1}b\in H$, 有 $y^{-1}Hy\subseteq H$ $\Leftrightarrow$ $H\lhd G$. 其中 $e_{G/H}=H, (xH)^{-1}=x^{-1}H$.

## Def 14 [商同态]

上述 $p:G\rightarrow G/H$ 称为商映射 (商同态).

## Thm 10 [同态基本定理]

设 $f:G\rightarrow G'$ 为群同态, 则 $H=\ker f\lhd G$ 且存在唯一单同态 $\overline{f}:G/\ker f\rightarrow$ 使 $f=\overline{f}\cdot p$.

### Proof

$\forall x\in G, \forall h\in H$, 有 $f(h)=e_{G'}, f(xhx^{-1})=e_{G'}$. 即 $xhx^{-1}\in H$, 所以 $H\lhd G$. 

定义 $\overline{f}:G/H\rightarrow G', xH=\overline{x}\mapsto f(x)$. 则

1. $\overline{f}(x)$ 良定 $\Leftrightarrow$ $\forall xH=aH,f(x)=f(a)$. 由 $xH=aH$, $a=xh\Rightarrow x^{-1}a=h$ 即 $e_{G'}=f(h)=f(x^{-1}a)=f(x)^{-1}f(a)$.
2. $\forall x\in G$, $\overline{f}\cdot p(x)=\overline{f}(\overline{x})=f(x)$, 即 $\overline{f}\cdot p=f$.

### Remark

同态 $f$ 诱导了同构 $\overline{f}:G/\ker f\rightarrow f(G)$.

## Cor 11

设 $K\lhd G$, $\overline{G}=G/K$ 为商群则

1. 若 $H\subseteq G$ 为子群且 $K\subseteq H$ 则 $H/K$ 使 $G/K$ 的子群.
2. 若 $\overline{H}\subseteq\overline{G}=G/K$ 为子群, 则存在唯一 $H\subseteq G$ 且 $K\subseteq H$ 使 $\overline{H}=H/K$.
3. $\overline{H}\lhd\overline{G}\Leftrightarrow H\lhd G$.

### Proof

1. 由 $K\lhd G$, $K\lhd H$. 由 **Thm 9**, $H/K\subseteq G/K$ 为子群.
2. 设 $p:G\rightarrow\overline{G}=G/H$ 为商同态. 令 $H=p^{-1}(\overline{H})=\{x\in G\mid p(x)\in \overline{H}\}$. 则 $H$ 是 $G$ 的子群且 $K\subseteq H,p(H)=\overline{H}$. 存在性得证, 下证唯一性. 设 $H_1,H_2$ 为 $G$ 的子群且都包含 $K$, 使 $p(H_1)=p(H_2)=\overline{H}$. 下证如果 $p(H_1)\subseteq p(H_2)$ 那么 $H_1\subseteq H_2$. 任取 $h_1\in H_1$. 因为 $p(H_1)\subseteq p(H_2)$, 那么存在 $h_2\in H_2$ 使 $p(h_1)=p(h_2)$. 此时 $p(h_1h_2^{-1})=e_{G/K}$. 因此 $h_1h_2^{-1}\in K\subseteq H_2$, 即 $H_1\subseteq H_2$. 同理, 如果 $p(H_1)\supseteq p(H_2)$ 那么 $H_1\supseteq H_2$. 因此 $H_1=H_2$.
3. $H\lhd G$ $\Leftrightarrow$ $\forall x\in G, xHx^{-1}\subseteq H$ $\Leftrightarrow$ $\forall x\in G, p(xHx^{-1})\subseteq p(H)$ $\Leftrightarrow$ $\forall\overline{x}\in\overline{G}, \overline{xHx^{-1}}\subseteq\overline{H}$ $\Leftrightarrow$ $\overline{H}\lhd \overline{G}$.