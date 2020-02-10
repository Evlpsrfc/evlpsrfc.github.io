---
title: 数论中的欧拉函数
date: 2020-01-31 19:10:57
tags: 算法
mathjax: true
---

在数论中，对于一正整数 $n$ ，**欧拉函数** $\varphi(n)$ 定义为 $1,2,\cdots,n$ 中与 $n$ 互质的数字的个数。

例如，$\varphi(12)=4$ ，因为 $1,5,7,11$ 和 $12$ 互质。

<!-- more -->

## 前言

本文的前置知识包括数论、群论的基础内容。

本文讨论的函数都是算术函数，也就是定义域为正整数、陪域为复数的函数。

缺少欧拉函数是积性函数这一性质的证明。

## 表达式

首先，若 $n=p^k$ ，$p$ 是素数，$k\geqslant1$，由于 $1,2,\cdots,p^k$ 中与 $p^k$ 互质的数为不含有 $p$ 因子的数，即除了 $p,2p,3p\cdots,p^{k}$ 以外的数，因此 $\varphi(n)=\varphi(p^k)=p^k-p^{k-1}$ 。

其次，欧拉函数是**积性函数**，即，若 $m,n$ 互质，则 $\varphi(mn)=\varphi(m)\varphi(n)$ 。

因此，利用算术基本定理，若 $n=p_1^{k_1}\cdots p_r^{k_r}$ ，则

$$
\begin{aligned}
\varphi(n)&=\varphi\left(\prod_{i=1}^r p_i^{k_i}\right)=\prod_{i=1}^r\varphi\left(p_i^{k_i}\right)=\prod_{i=1}^r\left(p_i^{k_i}-p_i^{k_i-1}\right)\\
&=\prod_{i=1}^rp_i^{k_i}\left(1-\frac{1}{p_i}\right)=n\prod_{i=1}^r\left(1-\frac{1}{p_i}\right)=n\prod_{p\mid n}\left(1-\frac1p\right)
\end{aligned}
$$
事实上，我们还可以这样考虑：

设 $n=p_1^{k_1}\cdots p_r^{k_r}$ ，定义集合 $A=\{1,2,\cdots,n\}$ 为全集，集合 $A_i$ 的元素为 $1\sim n$ 中被 $p_i$ 整除的数，集合 $S$ 的元素为 $1\sim n$ 中与 $n$ 互质的数，也就是不被任何 $p_i$ 整除的数，因此有
$$
S=A-\bigcup_{i=1}^{r}A_i\Rightarrow |S|=|A|-\left|\bigcup_{i=1}^{r}A_i\right|
\Rightarrow\varphi(n)=n-\left|\bigcup_{i=1}^{r}A_i\right|
$$
而我们知道以下两个事实：
$$
|A_i|=\frac{n}{p_i},|A_i\cap A_j|=\frac{n}{p_ip_j}
$$
那么根据容斥原理，
$$
\left|\bigcup_{i=1}^{r}A_i\right|=\sum_{i=1}^{r}|A_i|-\sum_{1\leqslant i<j\leqslant r}|A_i\cap A_j|+\cdots=\sum_{i}\frac{n}{p_i}-\sum_{i,j}\frac{n}{p_ip_j}+\cdots
$$
因此有
$$
\varphi(n)=n-\sum_{i}\frac{n}{p_{i}}+\sum_{i,j}\frac{n}{p_ip_j}-\cdots\tag{$\ast$}
$$

## 性质

引入**莫比乌斯函数** $\mu$：
$$
\mu(n)=\begin{cases}
1 & \text{若 $n=1$}\\
(-1)^k & \text{若 $n$ 无平方数因数，且 $n=p_1p_2\cdots p_k$}\\
0 & \text{若 $n$ 有大于 $1$ 的平方数因数}
\end{cases}
$$
由 $\mu$ 的定义容易看出它也是个积性函数。

我们可以用 $\mu(n)$ 将 $(\ast)$ 式改写为
$$
\varphi(n)=n-\sum_{i}\frac{n}{p_{i}}+\sum_{i,j}\frac{n}{p_ip_j}-\cdots=\sum_{d\mid n}\mu(d)\frac{n}{d}\tag{1}
$$
考虑到 $(1)$ 式的形式，我们再引入**迪利克雷卷积**，对于函数 $f,g$ ，其迪利克雷卷积定义为
$$
(f\ast g)(n)=\sum_{d\mid n}f(d)g\left(\frac nd\right)
$$
容易看出，迪利克雷卷积满足交换律、结合律和分配律。

将 $(1)$ 式用迪利克雷卷积表示，即为：
$$
\varphi=\mu\ast\operatorname{Id}\tag{2}
$$
其中 $\operatorname{Id}$ 为**恒等函数**，对于任意的 $n$ ，有 $\operatorname{Id}(n)=n$ 。

记模 $n$ 加法群为 $\mathbb{Z}/n\mathbb{Z}$ 。我们考虑 $\mathbb{Z}/n\mathbb{Z}$ 中生成元的个数。由于 $1$ 一定是生成元，因此数 $a$ 是生成元，当且仅当存在一整数 $b$ ，使得 $ab\equiv1\pmod n$ 。由裴蜀定理，$\gcd(a,n)=1$ 。因此 $a$ 是生成元当且仅当 $a$ 和 $n$ 互质。

因此 $\mathbb{Z}/n\mathbb{Z}$ 中生成元的个数即为 $\varphi(n)$ 。设 $\mathbb{Z}/d\mathbb{Z}$ 是 $\mathbb{Z}/n\mathbb{Z}$ 的一个子群，由**拉格朗日定理**，$d\mid n$ 。由于不同的子群具有不同的生成元，则不同子群之间无交。因此有
$$
\sum_{d\mid n}\varphi(d)=n\tag{3}
$$
定义常函数 $I(n)\equiv1$ ，则 $(3)$ 式可用迪利克雷卷积表示为
$$
\varphi\ast I=\operatorname{Id}\tag{4}
$$
迪利克雷卷积可看成二元运算，容易看出，该运算的幺元为**单位函数** $\epsilon$ ：
$$
\epsilon(n)=\begin{cases}
1 & \text{若 $n=1$}\\
0 & \text{其他情况}
\end{cases}
$$
则对于任意算术函数 $f$ 有
$$
f=f\ast\epsilon=\epsilon\ast f
$$
定义算数函数 $f$ 的**逆函数** $f^{-1}$ 为满足 $f\ast f^{-1}=\epsilon$ 的函数。

对比 $(2)$ 式和 $(4)$ 式，可得 $\mu$ 的逆函数为 $I$，即
$$
\mu\ast I=\epsilon
$$
将 $(2)$ 式和 $(4)$ 式的关系作推广，假设对于函数 $f(n)$ 和 $F(n)$ 有如下关系式：
$$
F(n)=\sum_{d\mid n}f(d)
$$
则有
$$
f(n)=\sum_{d\mid n}F(d)\mu\left(\frac{n}{d}\right)
$$
这就是所谓的**莫比乌斯反演公式**。

## 应用

一、求 $1\sim n!$ 中有多少个整数 $x$ ，满足 $x$ 的所有素因子都大于 $m$ ，其中 $m\leqslant n$ 。

 $x$ 的所有素因子都大于 $m$ ，等价于 $\gcd(x,m!)=1$ 。因此本题等价于求 $\sum_{x=1}^{n!}[\gcd(x,m!)=1]$ 。

由辗转相除法，$\gcd(x,m!)=\gcd(x\bmod m!,m!)$ 。由于 $m\leqslant n$ ，因此 $m!\mid n!$ 。因此答案即为 $\varphi(m!)\frac{n!}{m!}$ 。

二、求满足 $\gcd(a,b)=\gcd(a+x,b)$ 且 $0\leqslant x<b$ 的 $x$ 数量。

由辗转相除法，本题即为求解满足 $\gcd(a,b)=\gcd\left((a+x)\bmod b,b\right)$ 的 $x$ 数量，即满足 $\gcd(a,b)=\gcd(x',b)$ 的 $x'$ 数量。其中 $0\leqslant x'<b$ 。

设 $\gcd(a,b)=\gcd(x',b)=d$ ，则 $\gcd(x'/d,b/d)=1$ 。因此最终的答案即为 $\varphi\left(b/d\right)$ 。

三、求 $\displaystyle f(n)=\sum_{i=1}^n\gcd(i,n)$ 。

设 $\gcd(i,n)=d$ ，则 $\gcd(i/d,n/d)=1$ 。满足 $\gcd(i,n)=d$ 的 $i$ 的个数即为满足 $\gcd(i/d,n/d)=1$ 的 $i$ 的个数，也就是 $\varphi(n/d)$ 。因此最终的答案即为
$$
f(n)=\sum_{d\mid n}d\cdot\varphi\left(\frac{n}{d}\right)
$$
若 $n$ 太大，不能预处理所有的 $\varphi(i)$ ，则需要做以下分解：
$$
f(p^k)=\sum_{i=0}^kp^i\cdot\varphi\left(p^{k-i}\right)=\sum_{i=0}^{k-1}p^i\cdot p^{k-i-1}(p-1)+p^k=p^{k-1}(kp+p-k)\\f(n)=f\left(\prod_{i=1}^rp^{k_i}\right)=\prod_{i=1}^rf(p^{k_i})=\prod_{i=1}^r\left(p_i^{k_i-1}(k_ip_i+p_i-k_i)\right)
$$
四、求 $\displaystyle \sum_{i=1}^{n}\sum_{j=1}^{m}[\gcd(i,j)=k]$ 。
$$
\begin{split}&\sum_{i=1}^{n}\sum_{j=1}^{m}[\gcd(i,j)=k]=\sum_{i=1}^{\lfloor n/k\rfloor}\sum_{j=1}^{\lfloor m/k\rfloor}[\gcd(i,j)=1]\\=&\sum_{i=1}^{\lfloor n/k\rfloor}\sum_{j=1}^{\lfloor m/k\rfloor}\sum_{d\mid\gcd(i,j)}\mu(d)=\sum_{d=1}^{\lfloor \min(n,m)/k\rfloor}\mu(d)\sum_{i=1}^{\lfloor n/k\rfloor}[d\mid i]\sum_{j=1}^{\lfloor m/k\rfloor}[d\mid j]\\=&\sum_{d=1}^{\lfloor \min(n,m)/k\rfloor}\mu(d)\left\lfloor\frac{n}{kd}\right\rfloor\left\lfloor\frac{m}{kd}\right\rfloor\end{split}
$$
下面用分块计算即可。

>  注：**数论分块**
>
>  对于含有 $\lfloor n/i\rfloor$ 的求和式，对于每个 $i$ ，找到最大的 $j$ 使得 $\lfloor n/i\rfloor=\lfloor n/j\rfloor$ ，则每次以 $[i,j]$ 为一块求和即可。$j$ 的求法如下：
>  $$
>  \left\lfloor\frac{n}{i}\right\rfloor\leqslant\frac{n}{i}\Leftrightarrow\left\lfloor\frac{n}{\left\lfloor\frac{n}{i}\right\rfloor}\right\rfloor\geqslant\left\lfloor\frac{n}{\frac ni}\right\rfloor=\lfloor i\rfloor=i\Leftrightarrow i\leqslant\left\lfloor\frac{n}{\left\lfloor\frac{n}{i}\right\rfloor}\right\rfloor\\\Rightarrow j=\left\lfloor\frac{n}{\left\lfloor\frac{n}{i}\right\rfloor}\right\rfloor
>  $$

五、求 $\displaystyle \sum_{i=1}^n\sum_{j=1}^m\frac{\varphi(ij)}{\varphi(i)\varphi(j)}$ 。
$$
\frac{\varphi(ij)}{\varphi(i)\varphi(j)}=\frac{\displaystyle ij\prod_{p\mid ij}\left(1-\frac 1p\right)}{\displaystyle i\prod_{p\mid i}\left(1-\frac 1p\right)j\prod_{p\mid j}\left(1-\frac 1p\right)}=\frac{1}{\displaystyle \prod_{p\mid\gcd(i,j)}\left(1-\frac 1p\right)}=\frac{\gcd(i,j)}{\varphi(\gcd(i,j))}
$$
因此原式可化简为
$$
\begin{aligned}&\sum_{i=1}^n\sum_{j=1}^m\frac{\varphi(ij)}{\varphi(i)\varphi(j)}=\sum_{i=1}^n\sum_{j=1}^m\frac{\gcd(i,j)}{\varphi(\gcd(i,j))}\\=&\sum_{k=1}^{\min(n,m)}\frac{k}{\varphi(k)}\sum_{i=1}^n\sum_{j=1}^m[\gcd(i,j)=k]\\=&\sum_{k=1}^{\min(n,m)}\frac{k}{\varphi(k)}\sum_{d=1}^{\lfloor \min(n,m)/k\rfloor}\mu(d)\left\lfloor\frac{n}{kd}\right\rfloor\left\lfloor\frac{m}{kd}\right\rfloor\end{aligned}
$$

下面只需预处理 $k/\varphi(k)$ ，$\mu(d)$ 即可。若时间限制较紧，预处理 $k/\varphi(k)$ 时需要先预处理出逆元。

> 注：**线性预处理逆元**
>
> 设 $\operatorname{inv}(i)$ 表示 $i$ 模 $p$ 的逆元，若 $p=ki+j$ ，其中 $k$ 是整数，$j<i$ ，则有 $ki+j\equiv0\pmod p$ 。两边同乘 $i^{-1}j^{-1}$ ，有 $kj^{-1}+i^{-1}\equiv0\pmod p$ 。
>
> 因此 $i^{-1}\equiv-kj^{-1}\pmod p$ 。其中，$k=\lfloor p/i\rfloor$ ，$j=p\bmod i$ 。则
> $$
> \operatorname{inv}(i)=-\lfloor p/i\rfloor\operatorname{inv}(p\bmod i)
> $$
> 代码实现如下：
>
> ```c++
> const int N = 1e5 + 5;
> int inv[N];
> void init(){
>     inv[1] = 1;
>     for (int i = 2; i < N; ++i)
>         inv[i] = (MOD -  MOD / i) * inv[MOD % i] % MOD;
> }
> ```

## 代码实现

借助欧拉筛预处理 $\varphi(n)$ 和 $\mu(n)$ 的方法：

```c++
const int N = 1e5 + 5;
vector<int> pri;
bool npr[N];
int phi[N];
short int mu[N];
void euler(){ // O(n)
    memset(npr, false, sizeof(npr));
    mu[1] = 1;
    for (int i = 2; i < N; ++i){
        if (!npr[i]){
            pri.emplace_back(i);
            phi[i] = i - 1;
            mu[i] = -1;
        }
        for (int p: pri){
            int k = i * p;
            if (k >= N) break;
            npr[k] = true;
            if (i % p == 0){
                phi[k] = phi[i] * p;
                mu[k] = 0;
                break;
            }
            phi[k] = phi[i] * (p - 1);
            mu[k] = -mu[i];
        }
    }
}
```

不用筛法预处理 $\varphi(n)$ 和 $\mu(n)$ 的方法：

```c++
const int N = 1e5 + 5;
int phi[N];
void get_phi() { // O(nloglogn)
    for (int i = 2; i < N; ++i) if (!phi[i])
        for (int j = i; j < N; j += i){
            if (!phi[j]) phi[j] = 1;
            phi[j] -= phi[j] / i;
        }
}
short int mu[N];
void get_mu() { // O(nlogn)
    mu[1] = 1;
    for (int i = 1; i < N; ++i)
        for (int j = i + i; j < N; j += i)
            mu[j] -= mu[i];
}
```

