---
layout: single
title: "(강의정리) 확률 및 통계"
categories: mathematics
tags: [statistics]
use_math: true
publish: false
author_profile: false
---

이 포스트는 한양대학교 이상화 교수님의 [「확률 및 통계」 강의](http://www.kocw.net/home/search/kemView.do?kemId=1056974)에 대한 요약입니다.
이 강의는 총 21강으로 되어 있고 확률과 통계에 관한 전반적인 사항을 다루는 것 같습니다.
강의 내용을 아주 자세하게는 적지 않고 간략하게만 적어나갈 예정입니다.

# 1 조건부확률과 Bayes 정리

**1) sample Space**

확률에 대해 공부할 때 가장 먼저 배우는 것은 당연히 표본공간(sample space, 전공간)입니다.
고등학교 이후의 과정에서 확률은 항상 집합의 관점에서 이해됩니다.
표본공간 또한 집합으로, 보통 $S$로 적습니다.
표본공간이란 어떤 시행(trial)에 대하여

나타날 수 있는 가능한 모든 outcome들의 집합
{: .text-center}

을 말합니다.
예를 들어, 주사위를 하나 던지는 시행을 한다면

$$S=\{1,2,3,4,5,6\}$$

이고, 동전을 하나 던지는 시행을 한다면

$$S=\{H,T\}$$

입니다.

**2) event**

확률은 보통 $P(A)$로 표시하는데, 여기에서 $A$는 사건(event)이라고 부릅니다.
이때, 사건은 $S$의 부분집합입니다. ($A\subset S$)

$$
\begin{align*}
P(A)
&=\text{the probability that the outcome belongs to $A$}\\
&=\text{Prob}(\text{outcome}\in A)
\end{align*}
$$

**3) coditional probability**

두 사건 $A$, $B$에 대하여 사건 $A$가 발생했을 때
사건 $B$도 발생할 확률을 $P(B|A)$라고 쓰고,

$$P(B|A)=\frac{P(B\cap A)}{P(A)}$$

로 정의합니다.

이것은 마치, $A$를 sample space로 보는 것과 같습니다.
마찬가지로, 일반적인 확률 $P(A)$도 $P(A|S)$와 같이 해석할 수 있습니다.

**4) the law of total probability**

$A_1$, $\cdots$, $A_n$가 $S$의 partition이면 ($i\ne j$일 때 $A_i\cap A_j=\varnothing$이고 $A_1\cup A_2\cup\cdots\cup A_n=S$)

$$P(A)=P(A_1\cap A)+\cdots+P(A_n\cap A)=\sum_{i=1}^nP(A_i\cap A)$$

입니다.
각각의 $i$에 대하여 $P(A_i\cap A)=P(A|A_i)P(A_i)$이므로

$$P(A)=\sum_{i=1}^nP(A|A_i)P(A_i)$$

입니다.
이후에 Bayes theorem에서 자세히 다루겠지만, $P(A|A_i)$와 같은 확률은 사전확률로 해석할 수 있습니다.

![stats 1-1]({{site.url}}\images\2023-03-26-kocw_stats\stats_1-1.png){: .img-50-center}

**5) Bayesian theorem**

조건부확률의 식으로부터

$$P(B|A)=\frac{P(A|B)P(B)}{P(A)}$$

입니다.
$P(B|A)$를 직접적으로 구하기가 어려운데, $A$가 $A_1$, $\cdots$, $A_n$의 partition으로 표현될 수 있고, $P(A_i|B)$는 구하는 것이 상대적으로 용이한 경우에 Bayesian theorem이 자주 쓰입니다.
이때, $P(A|B)$는 사전확률(prior, 선행확률)이라고 불리며, $P(A)$는 the law of total probability에 의해 구하게 됩니다.

특히 $P(B|A)$에서 $A$가 observation data (input)에 대응되고 $B$가 original data (output)에 해당되는 경우가 대표적인 예입니다.
어떤 input이 주어졌을 때 어떤 output이 나올 확률은 보통 인과관계를 잘 따지면 계산할 수 있지만, 어떤 output이 나왔을 때 input이 그 값으로 주어졌을 확률, 즉 반대 경우는 해석하기 어렵고 계산하기 어렵습니다.
그런 경우에 $A$와 $B$의 위치를 바꾸어서, 계산하는 트릭이 Bayesian rule인 것 같습니다.

**ex. 1.7 binary symmetric channel**

데이터를 전송하는 어떤 기기가 있다고 하고, 그 기기가 transmitter와 receiver로 이루어져있다고 하겠습니다.
input data와 output data가 binary인 경우에 이 구조를 binary channel이라고 하는 것 같습니다.

$$
\begin{align*}
\text{input symbols}    &\in \{x_1,x_2\}&& \text{transmitter}\\
\text{output symbols}   &\in \{y_1,y_2\}&& \text{receiver}
\end{align*}
$$

이상적인 상황은, $x_1$이 입력되었을 때 $y_1$이 잘 출력되는 경우와 $x_2$가 입력되었을 때 $y_2$가 잘 출력되는 경우입니다.
각각의 경우는 $P(y_1|x_1)$, $P(y_2|x_2)$이 큰 확률로 나타나는 경우에 해당합니다.
계산할 수 있는 네 개 확률을 각각

$$
\begin{align*}
P_{11} = P(y_1|x_1)\\
P_{12} = P(y_2|x_1)\\
P_{21} = P(y_1|x_2)\\
P_{22} = P(y_2|x_2)
\end{align*}
$$

로 표기하겠습니다.
(마치 행렬같습니다.)

(이때, 위의 표현식은 조금은 엄밀하지는 못한 표현식인 것 같습니다.
$P(\cdot|\cdot)$의 두 $\;\;\cdot\;\;$에는 사건이, 그러니까 집합이 들어가야 하는데, 하나의 원소만 들어갔습니다.
$P(y_1|x_1)$라는 표현은 $P(\\{y_1\\}|\\{x_1\\})$로 해석하면 될 것 같습니다.
조금 더 정확하게는 $P(S_1\times\\{y_1\\}\|\\{x_1\\}\times S_2)$로 해석하면 될 것 같습니다.
하지만, 크게 혼동될 일이 없으니 $P(y_1|x_1)$로 써도 될 것 같습니다.)

만약 $P_{11}=P_{22}$이고 $P_{12}=P_{21}$이 성립하면 이 binary channel을 binary symmetric channel이라고 부릅니다.
(따라서 행렬이 symmetric한 것과는 연관이 없습니다.)
당연히

$$
\begin{align*}
P_{11}+P_{21}=1\\
P_{12}+P_{22}=1
\end{align*}
$$

이 성립합니다.
강의에서는 세 종류의 계산을 해보는데, 첫번째 계산은 the law of total probability와 연관이 있고, 두번째와 세번째 계산은 Bayesian theorem과 연관이 있습니다.

**(1) $P(\text{error})$**

오류라고 판단할 수 있는 경우는 input이 $x_1$로 들어갔는데 output이 $y_2$로 나오는 경우와 그 반대의 경우입니다.
전자의 경우를 $\\{x_1\\}\times\\{y_2\\}$로 표현해야 정확하겠지만 이것을 그냥 $x_1\cap y_2$로 쓰면

$$
\begin{align*}
P(\text{error})
&=P\left((x_1\cap y_2)\cup(x_2\cap y_1)\right)\\
&=P(x_1\cap y_2)+P(x_2\cap y_1)\\
&=P(y_2|x_1)P(x_1)+P(y_1|x_2)P(x_2)\\
&=P_{12}P(x_1)+P_{21}P(x_2)
\end{align*}
$$

라고 할 수 있습니다.

**(2) When $y_2$ is received, what is the probability that $x_1$ is transmitted?**

$$
\begin{align*}
P(x_1|y_2)
&=\frac{P(y_2|x_1)P(x_1)}{P(y_2)}\\
&=\frac{P(y_2|x_1)P(x_1)}{P(y_2|x_1)P(x_1)+P(y_2|x_2)P(x_2)}\\
&=\frac{P_{12}P(x_1)}{P_{12}P(x_1)+P_{22}P(x_2)}
\end{align*}
$$

여기에서 $y_2$는 아까 말한 observation data (output)이고 $x_1$은 original data (input)입니다.

**(3) $P(x_1|\text{error})$**

$$
\begin{align*}
P(x_1|\text{error})
&=\frac{P(\text{error}|x_1)P(x_1)}{P(\text{error})}\\
&=\frac{P(\text{error}|x_1)P(x_1)}{P(\text{error}|x_1)P(x_1)+P(\text{error}|x_2)P(x_2)}\\
&=\frac{P(y_2|x_1)P(x_1)}{P(y_2|x_1)P(x_1)+P(y_1|x_2)P(x_2)}\\
&=\frac{P_{12}P(x_1)}{P_{12}P(x_1)+P_{21}P(x_2)}
\end{align*}
$$

(강의에서는 위 계산이 다 완성되지 않았고, 위의 계산은 나름대로 결과를 내본 것입니다.
문제에서 $P(x_i)$는 주어지지 않은 것처럼 보입니다.)

![stats 1-2]({{site.url}}\images\2023-03-26-kocw_stats\stats_1-2.png){: .img-50-center}

**1.8 independent events**

두 개 혹은 여러 개의 사건에 대해서 독립/종속을 이야기할 수 있습니다.
강의에서는 두 개의 사건 $A$, $B$에 대한 독립(independece)만을 이야기합니다.
만약 두 사건 $A$, $B$가 서로 영향을 주지 않으면, 즉

$$P(B|A)=P(B)$$

이면, 혹은

$$P(A|B)=P(A)$$

이면, 두 사건 $A$, $B$가 서로 독립이라고 말합니다.
$P(A)\ne0$, $P(B)\ne0$인 경우에 이 독립조건은

$$P(A)P(B)=P(A\cap B)$$

와 동치입니다.

- 세 개 이상의 사건에 대한 독립을 말할 떄는 mutually independent라는 용어를 씁니다.
- 독립의 개념은 독립시행(복원시행, repeated restored trial)을 다룰 때 중요합니다.
- 독립(independence)과 배반(exclusiveness)의 개념을 혼동하지 말아야 합니다.
- $A$와 $B$가 독립이면 $A$와 $\overline B$($B$의 여사건, complement)도 독립입니다.

![stats 1-3]({{site.url}}\images\2023-03-26-kocw_stats\stats_1-3.png){: .img-50-center}

**1.9 Combined Experiments**

For two experiments with sample spaces $S_1$ and $S_2$, the sample space of the combined experiments is the Cartesian product $S_1\times S_2$;

$$S_1\times S_2=\{(x,y):x\in S_1,y\in S_2\}$$

동전 세 개를 동시에 던지는 독립시행에서, 단일 시행에 대한 표본공간은

$$S=\{H,T\}$$

이지만, combined experiments에 대한 표본공간은

$$
\begin{align*}
S\times S\times S
&=\{H,T\}\times\{H,T\}\times\{H,T\}\\
&=\{(H,H,H),(H,H,T),(H,T,H),(H,T,T),(T,H,H),(T,H,T),(T,T,H),(T,T,T)\}
\end{align*}
$$

입니다.

# 2 독립사건과 확률

**1.10 combinatorial analysis**

**1.10.1 permutation (순열)**

서로 다른 $n$개의 대상을 일렬로 나열하는 방법의 수는

$$n!=n\times(n-1)\times\cdots1.$$

서로 다른 $n$개의 대상 중 $r$개를 일렬로 나열하는 방법의 수는

$$_nP_r=\frac{n!}{r!}=n(n-1)\cdots(n-r+1).$$

**1.10.2 group permutation (같은 것이 포함된 순열)**

세 종류의 대상 $A$, $B$, $C$가 각각 $a$개, $b$개, $c$개 있을 때($a+b+c=n$), 이 $n$개의 대상을 일렬로 나열하는 방법의 수는

$$\frac{n!}{a!b!c!}.$$

**1.10.3 circular permutation (원순열)**

서로 다른 $n$개의 대상을 원형으로 나열하는 방법의 수는

$$(n-1)!.$$

**1.10.4 combination (조합)**

서로 다른 $n$개의 대상들 중 $r$개를 선택하는 방법의 수는

$$\binom nk=_nC_r=\frac{_nP_r}{r!}=\frac{n!}{r!(n-r)!}.$$

**1.10.4 binomial theorem (이항정리)**

$$
\begin{align*}
(a+b)^n&=\sum_{k=0}^n\binom nka^kb^{n-k}\\
(1+x)^n&=f(x)=\sum_{k=0}^n\binom nkx^k\\
2^n&=f(1)=\sum_{k=0}^n\binom nk\\
0&=f(-1)=\sum_{k=0}^n(-1)^k\binom nk
\end{align*}
$$

$f(x)$를 조금 변형하면 이항분포에서의 평균과 분산 식을 계산하는 데 도움이 될 수 있습니다.

위 식의 $f(x)$를 한 번 미분하면

$$
\begin{align*}
n(1+x)^{n-1}=f'(x)=\sum_{k=0}^nk\binom nkx^{k-1}\\
\end{align*}
$$

에서

$$
\begin{equation}
nx(1+x)^{n-1}=\sum_{k=0}^nk\binom nkx^k\tag{$*$}
\end{equation}
$$

이고 $f(x)$를 두 번 미분하여 정리하면

$$
\begin{align*}
n(n-1)(1+x)^{n-2}&=f''(x)=\sum_{k=0}^nk(k-1)\binom nkx^{k-2}\\
n(n-1)x^2(1+x)^{n-2}&=\sum_{k=0}^nk(k-1)\binom nkx^k
\end{align*}
$$

이고 마지막 식을 $(*)$와 더하면

$$
\begin{equation}\tag{$**$}
nx(1+x)^{n-2}(1+nx)=\sum_{k=0}^nk^2\binom nkx^k
\end{equation}
$$

이산확률분포 $X$가 이항분포 $B(n,p)$를 따르면, $X$의 확률질량함수는

$$P(X=k)=\binom nkp^k(1-p)^{n-k}$$

입니다.
따라서 $X$의 평균은

$$
\begin{align*}
E(X)
&=\sum_{k=0}^nkP(X=k)\\
&=\sum_{k=0}^nk\binom nkp^k(1-p)^{n-k}\\
&=(1-p)^n\sum_{k=0}^nk\binom nk\left(\frac p{1-p}\right)^k\\
&=(1-p)^nn\cdot\frac p{1-p}\left(1+\frac p{1-p}\right)^{n-1}\\
&=np
\end{align*}
$$

으로 계산됩니다.
$X$의 분산은 조금 복잡한데

$$
\begin{align*}
E(X)
&=E(X^2)-E(X)^2\\
&=\sum_{k=0}^nk^2P(X=k)-(np)^2\\
&=\sum_{k=0}^nk^2\binom nkp^k(1-p)^{n-k}-(np)^2\\
&=(1-p)^n\sum_{k=0}^nk^2\binom nk\left(\frac p{1-p}\right)^k-(np)^2\\
&=(1-p)^n\frac{np}{1-p}\left(1+\frac p{1-p}\right)^{n-2}\left(1+\frac{np}{1-p}\right)-n^2p^2\\
&=np(1-p)
\end{align*}
$$

입니다.
(잘 알려진 다른 증명보다 복잡한 것 같아서 유용한지는 잘 모르겠습니다.)

한편, 멱급수에 대해서도 재미있는 계산을 할 수 있습니다.

$$
f(x)=1+2x+3x^2+\cdots
$$

이면

$$
xf(x)=x+2x^2+3x^3+\cdots
$$

이고 두 식을 빼면

$$
(1-x)f(x)=1+x+x^2+\cdots=\frac1{1-x}
$$

입니다. (단, $|x|<1$)

따라서

$$
f(x)=\frac1{(1-x)^2}
$$

입니다.
한편, 위의 결과를 다르게 얻을 수도 있는데

$$
g(x)=1+x+x^2+\cdots
$$

라고 하면 $f(x)=g'(x)$이므로

$$
f(x)=\left(\frac1{1-x}\right)'=\frac1{(x-1)^2}
$$

인 것입니다.

**1.10.6 Sterling's formula**

$n$이 충분히 크면 $n!$는 다음 값과 거의 비슷합니다.

$$\sqrt{2\pi n}\left(\frac ne\right)^n$$

강의에는 이에 대한 증명이 나와있지 않은데 [이 자료](https://kconrad.math.uconn.edu/blurbs/analysis/stirling.pdf)(Keith Conrad의 자료)에 설명과 증명이 잘 되어 있는 것 같습니다.
여기에서의 증명은 Gaussian distribution을 통한 증명과, 어떤 함수열의 수렴을 통한 증명이 소개되고 있는 것 같습니다.

엄밀한 증명은 조금 어렵지만, 대략적으로 이 식의 의미를 파악하는 건 그렇게까지 어렵지 않은 것 같습니다.
어림하고자 하는 값 $n!$에 자연로그를 취하면

$$\log(n!)=\log1+\log2+\cdots+\log n$$

인데, 이것은 정적분

$$\int_1^n\log x\,dx$$

과 관련이 있는 값입니다.
폐구간 $1\le x\le n$를 길이가 1인 $n$개의 구간으로 나누면, 리만적분에서 흔히 하는 방식에 의해, 정적분의 값은 $n$개의 **큰** 직사각형들의 넓이의 합보다는 작고 $n$개의 (사실은 $n-1$개의) **작은** 직사각형들의 넓이의 합보다는 큽니다.
즉,

$$
\begin{align*}
\log1+\log2+\cdots+\log(n-1)&<\int_1^n\log x\,dx<\log2+\log3+\cdots+\log n\\
\log((n-1)!)&<n\log n-n+1<\log(n!)\\
n\log n-n+1&<\log(n!)<n\log n-n+1+\log n\\
e^{n\log n-n+1}&<e^{\log(n!)}<e^{n\log n-n+1+\log n}\\
e\left(\frac ne\right)^n&<n!<en\left(\frac ne\right)^n
\end{align*}
$$

입니다.
그러면 $n!$은 $\left(\frac ne\right)^n$이라는 값과 상당히 비슷한 값이어서

$$n!\approx\left(\frac ne\right)^n$$

라는 사실과

$$n!=g(n)\left(\frac ne\right)^n$$

와 같이 쓸 때 $e\lt g(n)\lt en$인 것도 알 수 있습니다.
그리고 실제 Sterling's formula에서의 $g(n)=\sqrt{2\pi n}$이 위의 범위에 있는 것도 확인할 수 있습니다.

**1. 11 Reliability**

![stats 2-1]({{site.url}}\images\2023-03-26-kocw_stats\stats_2-1.png){: .img-50-center}

어떤 시스템(혹은 모듈)이 어떤 기간동안 얼마나 올바르게 고장나지 않고 잘 동작하는지를 나타내는 값을 reliability라고 합니다.
그것을 $R(t)$라고 적습니다.

**series connection(직렬연결)**

![stats 2-2]({{site.url}}\images\2023-03-26-kocw_stats\stats_2-2.png){: .img-50-center}

여러 개의 독립적인 모듈 $C_1$, $\cdots$, $C_n$ 들이 직렬로 연결되어 있고(cascade) 각 모듈들의 reliabilty가 $R_1(t)$, $\cdots$, $R_n(t)$ 이 시스템의 reliability는

$$\prod_{i=1}^nR_i(t)$$

입니다.

**parallel connection(병렬연결)**

![stats 2-3]({{site.url}}\images\2023-03-26-kocw_stats\stats_2-3.png){: .img-50-center}

이번에는 이 모듈들이 병렬로 연결되어 있다면 이 시스템의 reliability는

$$1-\prod_{i=1}^n\left(1-R_i(t)\right)$$

입니다.

![stats 2-4]({{site.url}}\images\2023-03-26-kocw_stats\stats_2-4.png){: .img-50-center}

만약 위의 그림처럼 복잡한 시스템이라고 한다면, $C_3$가 동작하는지($R_x$) 동작하지 않는지($R_y$)에 따라 구분해서 얻어낼 수 있습니다.
전자의 경우에는 두 쌍의 병렬모듈들이 직렬로 연결된 것이고 후자의 경우에는 두 쌍의 직렬모듈들이 병렬로 연결된 것이라고 볼 수 있습니다.

![stats 2-5]({{site.url}}\images\2023-03-26-kocw_stats\stats_2-5.png){: .img-50-center}

따라서

$$
\begin{align*}
R
&=R_x+R_y\\
&=\left(1-(1-R_1)(1-R_2)\right)\left(1-(1-R_4)(1-R_5)\right)
+1-(1-R_1R_4)(1-R_2R_5)
\end{align*}
$$

입니다.

# 3 확률변수의 정의

**Chapter 2. Random Variables(확률변수)**

**2.2 definiion of random variables**

언제나 확률변수의 개념을 정확히 이해하는 건 쉬운 일은 아닌 것 같습니다.
한 번 볼 때마다 완벽히 이해한다고 생각하지만, 어찌된 것인지 볼때마다 새로운 것 같습니다.
그래도 다시 한 번 강의를 보며 다시 한 번 이해해봤습니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_3-1.png){: .img-50-center}

확률변수($X$)란, 어떤 시행의 근원사건 $w\in S$을 하나의 실수 $X(w)$로 대응시키는 함수를 말합니다.

A random variable is a function $X$ mapping each outcome of random experiment $w\in S$ to a real number $x=X(w)$.

즉 $X:S\to\mathbb R$인 $X$를 확률변수라고 합니다.

**ex.1 : tossing a coin**

동전을 하나 던져서 앞면이 나오면 1점을 얻고 뒷면이 나오면 $-1$점을 얻는 어떤 시행에서,

동전을 하나 던졌을 때 얻는 점수
{: .text-center}

를 확률변수 $X$로 정의할 수 있습니다.
이 시행에서 $S=\{H,T\}$이고, 확률변수 $X$는 $S$에서 $\mathbb R$로 가는 함수로서

$$
\begin{align*}
X(H)&=1\\
X(T)&=-1
\end{align*}
$$

확률변수를 사용하면 확률 $P(\:\cdot\:)$를 마치 숫자들의 함수로서 생각할 수 있게 됩니다.
그전까지 $P(A)$라는 표현에서 $A$는 사건(event)이라고 불렸고 표본공간 $S$의 부분집합을 의미했습니다.
그러니까 그전까지는 확률 $P(\:\cdot\:)$가 마치 '집합의 함수'처럼 동작했습니다.
그래서

$$P(\{H\})=\frac12,\quad P(\{T\})=\frac12,\quad P(\varnothing)=0,\quad P(S)=1$$

와 같은 표현들을 사용할 수 있었지만 직관적인 표현은 아니었습니다.

그런데 확률변수 $X$를 도입하고 나면 $P(\:\cdot\:)$를 숫자들의 함수처럼 생각할 수 있습니다.
$p(x)$ 혹은 $P(X=x)$라는 표현을 (이것들은 나중에 확률질량함수라는 이름을 가지게 되는데)

$$
\begin{equation}\tag{$*$}
\begin{aligned}
p(x)
&=P(X=x)\\
&=P\left(\{w\in S:X(w)=x\}\right)
\end{aligned}
\end{equation}
$$

와 같이 정의하면

$$
\begin{align*}
p(1)&=P(X=1)=\frac12\\
p(-1)&=P(X=-1)=\frac12
\end{align*}
$$

와 같이 쓸 수 있습니다.
$P$는 집합을 숫자로 대응시키는, 조금 복잡한 느낌이었지만 $p$는 숫자를 숫자로 대응시키고 있어서 다루고 이해하기가 편합니다.


**ex.2 : tossing two coins**

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_3-2.png){: .img-50-center}

동전을 두 개 던졌을 때 나온 앞면의 수
{: .text-center}

도 확률변수 $X$가 됩니다.
이때의 표본공간은 $S=\{H,T\}^2$인데, 강의에서는 cartesian product에서의 순서쌍의 표현을 생략하여, $S=\{HH,HT,TH,TT\}$로 쓰고 있습니다.
확률변수 $X$는

$$
\begin{align*}
X(HH)&=2\\
X(HT)&=1\\
X(TH)&=1\\
X(TT)&=0
\end{align*}
$$

로 정의되고 기존의 확률의 정의로는

$$
\begin{align*}
P(\{HH\})&=\frac14\\
P(\{HT,TH\})&=\frac12\\
P(\varnothing)&=0\\
P(S)&=1
\end{align*}
$$

와 같은 표현을 사용할 수 있었습니다.

그런데 이것을

$$
\begin{align*}
p(0)&=P(X=0)=\frac14\\
p(1)&=P(X=1)=\frac12\\
p(2)&=P(X=2)=\frac14
\end{align*}
$$

로 생각하게 되면 $p$는 다루기 쉬운 실함수가 됩니다.

관습적으로 확률변수 자체는 대문자 기호 $X$, $Y$, $Z$ 등으로, 확률변수가 가지는 특정한 값은 $x$, $y$, $z$ 등으로 나타냅니다.

**2.3 events defined by RV**

강의에서는 $A_x$를 도입해서 설명하고 있습니다.
이떄 $A_x$는 사건으로서, 확률변수 $X$가 $x$의 값을 가지는 경우, 즉 $X(w)=x$인 $w\in S$들의 집합입니다.
(따라서 이것은 $X$의 inverse image $X^{-1}(x)$이기도 합니다.)

$$A_x=\{w\in S:X(w)=x\}$$

이것은 아까 $(*)$에서 $p(x)$ 혹은 $P(X=x)$를 정의할 때 쓰인 집합입니다.
즉, $p(x)$ 혹은 $P(X=x)$를

$$p(x)=P(X=x)=P(A_x)$$

로 정의합니다.

지금까지, $P(\:\cdot\:)$에 들어가는 것이 사건(event, $S$의 부분집합)이었던 것을, 특정한 숫자로 들어갈 수 있게 바꾸었습니다.
여기에는 '숫자들의 집합'도 들어갈 수 있습니다.
예를 들어 $\{X:a\lt X\le b\}$와 같은 집합도 들어갈 수 있습니다.
보통 쓸 때는 $P(\{X:a\lt X\le b\})$로 쓰지 않고 $P(a\le X\le b)$로 표기하는데

$$
P(a<X\le b)=P\left(\{w\in S:a<X(w)\le b\}\right)
$$

로 정의합니다.
예를 들어 동전 두 개를 던지는 시행에서

$$P(X\le1)=P\left(\{HH,HT,TH\}\right)=\frac34$$

입니다.

**2.4 distribution functions**

For a random variable $X$ and a real value $x$,
the *cumulative distribution function*(CDF, 누적확률)은 

$$F_X(x)=P\left(X\le x\right)$$

로 정의합니다.
위의 동전 두 개를 던지는 시행에서

$$F_X(1)=\frac34$$

였습니다.

따라서 CDF는
- nondecreasing 입니다 : if $x_1\lt x_2$, then $F_x(x_1)\le F_X(x_2)$
- 치역이 $[0,1]$입니다 : $0\le F_X(x)\le1$
- 두 점근선을 가집니다 : $\displaystyle\lim_{x\to\infty}F_X(x)=1$, $\displaystyle\lim_{x\to-\infty}F_X(x)=0$
- $P(a\lt X\lt b)=F_X(b)-F_X(a)$
- $P(x>a)=1-F_x(a)$

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_3-3.png){: .img-50-center}

위의 $P(a\lt X\le b)$에서와 같이 부등호를 $\lt$로 할지 $\le$로 할지는 잘 구분해주어야 합니다.
다만, 연속확률변수의 경우에는 (아래 예제와 같은 예외가 발생하지 않는 한은) 둘 사이에 구분을 두지 않아도 됩니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_3-4.png){: .img-50-center}

위 그림과 같은 예제에서 CDF는

$$
F_X(x)=\begin{cases}
0&(x\lt0)\\
x+\frac12&(0\le x\lt\frac12)\\
1&(x\gt\frac12)\\
\end{cases}
$$

와 같이 주어져 있는데

$$
\begin{align*}
P\left(X>\frac14\right)&=1-F_X\left(\frac14\right)=1-\frac34=\frac14\\
P(X>0)&=1-F_X(0)=1-\frac12=\frac12\\
P(X\ge0)&=1\\
P(X=0)&=1\\
P\left(X\ge\frac14\right)&=\frac14
\end{align*}
$$

입니다.
아래의 세 개 계산은 notrivial합니다.
좌우극한을 가지고 계산하면

$$
\begin{align*}
P(X\ge0)
&=1-P(X\lt0)\\
&=1-\lim_{x\to0+}P(X\le x)\\
&=1-\lim_{x\to0+}\left(x+\frac12\right)\\
&=1-0=1\\
P(X=0)
&=P(X\le0)-P(X\lt0)\\
&=\frac12-0=1\\
P\left(X\ge\frac14\right)
&=1-P\left(X\lt\frac14\right)\\
&=1-\lim_{x\to\frac14+}P(X\le x)\\
&=1-\lim_{x\to\frac14+}\left(x+\frac12\right)\\
&=1-\frac34=\frac14
\end{align*}
$$

이고, 강의에 따르면 조금 직관적으로도 이해할 수 있는 것 같습니다.

**2.5 discrete random variables(이산확률변수)**

확률변수 $X$가 가질 수 있는 값이 유한개이면 (혹은 countable개이면) $X$를 이산확률변수라고 부릅니다.

이 때에는 확률질량함수(probability mass function) $P_X(x)$를 다음과 같이 정의합니다.

$$P_X(x)=P(X=x)$$

동전을 두 개 던지는 시행에서

$$
\begin{align*}
P_X(0)=\frac14\\
P_X(1)=\frac12\\
P_X(2)=\frac14
\end{align*}
$$

CDF와의 관계는 다음과 같습니다.

$$F_X(x)=\sum_{x_i\le x}P_X(x_i)$$

이산확률변수의 분포(distribution)는 확률질량함수의 그래프로서 나타내는데, 그것을 $xy$ 평면에 찍힌 여러 개의 점으로 표현하기보다는, 선분으로써 표현하는 경향이 있는 것 같습니다.

동전을 두 개 던지는 시행에서의
확률질량함수의 그래프와 CDF의 그래프는 아래와 같습니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_3-5.png){: .img-100-center}

이때, CDF의 그래프는 step function으로 나타납니다.

연속확률변수에서 확률밀도함수 $f_X(x)$에 대응하는 개념을 설명하려면 dirac delta function과 같이 조금 복잡한 논의가 필요합니다.
다시 말해, 연속확률변수에서는

$$P(a\le X\lt b)=\int_a^bf_X(x)\,dx$$

와 같은 식을 만족시키는 함수 $f_X(x)$를 생각하게 되는데, 위의 $P_X(x)$의 그래프에서는 '그래프 아래의 면적'이라는 개념을 정의할 수 없으니까 애매합니다.
그럴 때에, 함수 $\delta$(dirac delta function)를

$$
\delta(x)\approx
\begin{cases}
+\infty&(x=0)\\
0&(x\ne0)
\end{cases}
$$

와 같이 이해합니다.
[(출처)](https://en.wikipedia.org/wiki/Dirac_delta_function)
이 함수는 $x\ne0$인 곳에서는 함숫값이 0이고 $x=0$인 곳에서만 함숫값이 $\infty$인 불연속함수처럼 적혀있는데, 실제로는 연속함수처럼 생각합니다.
또, 실수 전체의 범위에서 적분했을 때의 값이 $1$인 것으로 가정합니다.

$$
\int_{-\infty}^{\infty}\delta(x)\,dx=1
$$

따라서 이 함수 $\delta(x)$가

$$
P_X(x)=
\begin{cases}
1&(x=0)\\
0&(x\ne0)
\end{cases}
$$

와 같이 정의된 가장 기본적인 확률질량함수 $P_X(x)$에 대응되는 확률밀도함수라고 생각할 수 있습니다.
일반적인 확률질량함수는 이 $\delta(x)$를 적절히 shift한 것들을 가지고 일차결합하여 만들어낼 수 있습니다.
즉

$$
P_X(x)=
\begin{cases}
p_1&(x=x_1)\\
&\vdots\\
p_n&(x=x_n)
\end{cases}
$$

인 확률질량함수 $P_X(x)$에 대해서는 (단, $p_1+\cdots+p_n=1$)

$$f_X(x)=\sum_{k=1}^np_k\delta(x-x_k)$$

가 확률밀도함수의 역할을 할 수 있습니다.

예를 들어 동전을 두 번 던지는 시행에 대해서는

$$f_X(x)=\frac14\delta(x)+\frac12\delta(x-1)+\frac14\delta(x-2)$$

로 정할 수 있습니다.

<!-- 실제 강의에서는 dirac delta function에 대해서는 언급하지 않고 $\delta(x)$를 '델타의 수'라고 부르고 있습니다. -->
dirac delta function은 엄밀히 말하면 함수가 아닌 generalized function이며, measure를 통해 이해될 수 있다고 합니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_3-6.gif){: .img-100-center}

# 4 이산확률변수와 연속확률변수

**2.6 continuous random variables**

앞서 강의에서 확률변수를 $X:S\to\mathbb R$인 함수로 정의했습니다.
어떤 확률변수가 이산확률변수인지 연속확률변수인지를 결정하는 것은 이 확률변수의 치역 $X(S)$과 관련있습니다.
$X(S)$가 countable이면 (혹은 at most countable, 그러니까, finite이거나 countably infinte) $X$를 이산확률변수라고 합니다.
이것은

확률변수 $X$가 가질 수 있는 값이 유한개(혹은 countable)이면 $X$를 이산확률변수라고 부릅니다.
{: .text-center}

와 같은 앞서의 정의에 대응됩니다.

만약, 확률변수가 이산확률변수가 아니면 연속확률변수라고 부릅니다.
그러니까, 치역 $X(S)$가 uncountable인 경우 (uncountably infinte)를 말합니다.
말로 풀어 쓰면

확률변수 $X$가 가질 수 있는 값이 uncountable하게 많으면 $X$를 연속확률변수라고 부릅니다.
{: .text-center}

이산확률분포의 경우에 비해 연속확률분포의 경우에는 조금 어렵고 섬세한 이야기들이 많이 산적해있습니다.
예를 들어 0과 1 사이의 숫자를 임의로 뽑을 때 그 값을 $X$라고 하면, $X$는 연속확률변수입니다.
그런데 이런 경우에 $P(X=\frac12)$을 어떻게 정의해야 할 지 애매합니다.

(답 : 확률을 measure-theoretic하게 생각하면 $P$는 하나의 measure라고 볼 수 있고 이 경우에는 '집합의 길이'와 관련된 measure를 $P$로써 정의합니다.
그런데 원소가 하나인 집합에 대한 '길이'는 0이므로 $P(X=\frac12)=0$입니다.)

즉, 이산확률변수에서의 '확률질량함수'가 잘 작동하지 않고, 따라서 다른 방식으로 연속확률분포를 이해할 필요가 있습니다.

It is not possible to define a probability value for each $x$.

$X$가 특정한 값 $x$를 가질 때의 확률은 무조건 0인데 비해

$$P(X=x)=0$$

$X$가 어떤 구간 안에 위치할 확률은 많은 경우에 계산할 수 있습니다.
예를 들어, 0과 1 사이의 숫자를 임의로 뽑을 때, 그 수가 0.1과 0.3사이의 값을 가질 확률은 0.2이라고 생각할 수 있습니다.

$$P(0.1\lt X\lt 0.3)=0.2$$

그러니까, 특정한 점 $X=x$에 대한 확률을 정의하는 대신 $x$를 포함하는 infinitesimal한 구간을 생각하고 그 구간에 대한 확률값을 그 구간의 길이로 나눈 값을 고려할 수 있습니다.
그리고 그 값은 $F_X$가 미분가능할 경우 $F_X$의 도함수와 정확히 일치합니다.

$$
\begin{align*}
f_X(x)
&=\lim_{\Delta x\to0+}\frac{P\left(x<X\le x+\Delta x\right)}{\Delta x}\\
&=\lim_{\Delta x\to0+}\frac{F_X(x+\Delta x)-F_X(x)}{\Delta x}\\
&=F_X'(x)
\end{align*}
$$

이 함수 $f_X(x)$를 확률밀도함수(probability density function)이라고 부릅니다.
위의 식은 CDF가 주어졌을 때 PDF를 구하는 방법이기도 합니다.
그 반대의 경우는 $f_X=F_X'$와 $\lim_{x\to-\infty}F_X(x)=0$로부터

$$F_X(x)=\int_{-\infty}^xf_X(\tilde x)\,d\tilde x$$

와 같이 쓸 수 있습니다.

CDF는 일반적으로 미분가능하지 않을 수도 있지만, 이 강의에서는 CDF가 미분가능한 경우만 다룬다고 합니다.
CDF가 미분가능하지도 않고, 심지어 불연속인 극단적인 경우는 2.3에서 봤었습니다.

함수 $f_X(x)$가 어떤 연속확률변수의 PDF이기 위해서는 다음 두 조건을 만족시켜야 합니다.

1. $f_X(x)\ge0$
2. $\int_{-\infty}^\infty f_X(x)\,dx=1$

마찬가지로, 함수 $P_X(x)$가 어떤 이산확률변수의 PMF이기  위해서는 다음의 두 조건을 만족시켜야 합니다.

1. $p_X(x_i)\ge0$
2. $\sum_{k=1}^n p_X(x_i)=1$

PDF의 추가적인 성질들은 다음과 같습니다.

3. $\int_a^bf_X(x)\,dx=P(a\lt X\le b)$

이것은, 지금까지 쓴 개념들을 동원해 쉽게 증명됩니다.

$$
\begin{align*}
P(a\lt X\le b)
&=F_X(b)-F_X(a)\\
&=\int_{-\infty}^bf_X(x)\,dx-\int_{-\infty}^af_X(x)\,dx\\
&=\int_a^bf_X(x)\,dx
\end{align*}
$$

4. $P(X\lt a)=P(X\le a)$

이것은, 한 점에서의 확률이 항상 0이라는 사실로부터 바로 설명될 수 있습니다.
위의 4번에 쓴 식은 가능한 여러 식들 중 하나를 대표적으로 쓴 것입니다.
일반적으로 $\le$와 $\lt$는 적절히 바꿔가면서 사용될 수 있습니다.

**ex 2.11**

$0\lt x\lt 2$에 대하여 $f_X(x)=A(2x-x^2)$이 PDF가 되려면

$$
1
=A\int_0^22x-x^2\,dx
=\frac43A
$$

으로부터 $A=\frac34$입니다.

**ex 2.15 uniform distribution**

$f_X(x)$가 상수함수이면 $X$가 uniform distribution을 따른다고 합니다.
아까, 0과 1 사이의 숫자를 임의로 골라 그 값을 $X$라고 할때, $X$는 uniform distribution을 따릅니다.
주사위를 하나 던져 눈을 보는 것도 일종의 uniform distribution에 해당합니다.

고등학교 과정의 '기하학적 확률'에서 확률을 넓이 혹은 길이에 의존해 계산하게 되는데 그러한 상황 또한 uniform distribution을 가정하고 있습니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_4-1.png){: .img-100-center}
