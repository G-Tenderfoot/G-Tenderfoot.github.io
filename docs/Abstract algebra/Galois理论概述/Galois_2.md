# 群与域扩张

这一节, 我们将逐步建立 $Gal(L/K)$ 的子群与 $K\subset E\subset L$ 中间域的对应关系.

## Lem 1 [Artin 引理]

设 $G\subseteq Aut(L)$ 为有限子群, 则 $L^G=\left\{x\in L\mid \sigma(x)=x,\forall\sigma\in G\right\}$ 是 $L$ 的一个子域且 $[L:L^G]\leqslant |G|$.

### Proof

1. 证明 $L^G$ 是 $L$ 的子域.首先 $0_L\cdot 1_L\in L^G$, 因此 $L^G\neq\varnothing$. $\forall a,b\in L^G$, 有 $\sigma(a)=a,\sigma(b)=b$. 则 $\forall\sigma\in G$, 有 $\sigma(a\pm b)=\sigma(a)\pm\sigma(b)=a\pm b$. $\sigma(ab)=\sigma(a)\sigma(b)=ab$. $\sigma(a^{-1})=\sigma(a)^{-1}=a^{-1}$.