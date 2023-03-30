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
아주 깔끔하게 적으려다보면 시간이 많이 걸리거나, 아예 안하게 되는 경우도 있어서, 조금 간단하게, 때로는 의식의 흐름대로 적어나가게 되는데, 그래도 쓰고 고치고 하다보면 잘 정리될 수도 있을 것 같습니다.

# 01 조건부확률과 Bayes 정리

**(1) sample Space**

확률에 대해 공부할 때 가장 먼저 배우는 것은 당연히 표본공간(sample space)입니다.
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

**(2) event**

확률은 보통 $P(A)$로 표시하는데, 여기에서 $A$는 사건(event)이라고 부릅니다.
이때, 사건은 $S$의 부분집합입니다. ($A\subset S$)

$$
\begin{align*}
P(A)
&=\text{the probability that the outcome belongs to $A$}\\
&=\text{Prob}(\text{outcome}\in A)
\end{align*}
$$

**(3) coditional probability**

두 사건 $A$, $B$에 대하여 사건 $A$가 발생했을 때
사건 $B$도 발생할 확률을 $P(B|A)$라고 쓰고,

$$P(B|A)=\frac{P(B\cap A)}{P(A)}$$

로 정의합니다.

이것은 마치, $A$를 sample space로 보는 것과 같습니다.
마찬가지로, 일반적인 확률 $P(A)$도 $P(A|S)$와 같이 해석할 수 있습니다.

**(4) the law of total probability**

$A_1$, $\cdots$, $A_n$가 $S$의 partition이면 ($i\ne j$일 때 $A_i\cap A_j=\varnothing$ 이고 $A_1\cup A_2\cup\cdots\cup A_n=S$)

$$P(A)=P(A_1\cap A)+\cdots+P(A_n\cap A)=\sum_{i=1}^nP(A_i\cap A)$$

입니다.
각각의 $i$에 대하여 $P(A_i\cap A)=P(A|A_i)P(A_i)$이므로

$$P(A)=\sum_{i=1}^nP(A|A_i)P(A_i)$$

입니다.
이후에 Bayes theorem에서 자세히 다루겠지만, $P(A|A_i)$와 같은 확률은 사전확률로 해석할 수 있습니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_1-1.png){: .img-100-center}

**(5) Bayesian theorem**

조건부확률의 식으로부터

$$P(B|A)=\frac{P(A|B)P(B)}{P(A)}$$

입니다.
$P(B|A)$를 직접적으로 구하기가 어려운데, partition $A_1$, $\cdots$, $A_n$이 존재하고, $P(A_i|B)$는 구하는 것이 상대적으로 용이한 경우에 Bayesian theorem이 자주 쓰입니다.
이때, $P(A|B)$는 사전확률(prior, 선행확률)이라고 불리며, $P(A)$는 the law of total probability에 의해 구하게 됩니다.

특히 $P(B|A)$에서 $A$가 observation data (input)에 대응되고 $B$가 original data (output)에 해당되는 경우가 대표적인 예입니다.
어떤 input이 주어졌을 때 어떤 output이 나올 확률은 보통 인과관계나 선후관계를 잘 따지면 계산할 수 있지만, 어떤 output이 나왔을 때 input이 그 값으로 주어졌을 확률, 즉 반대 경우는 해석하기 어렵고 계산하기 어렵습니다.
그런 경우에 $A$와 $B$의 위치를 바꾸어서, 계산하는 트릭이 Bayesian rule인 것 같습니다.

**ex. 1.7 binary symmetric channel**

데이터를 전송하는 어떤 기기가 있다고 하고, 그 기기가 transmitter와 receiver로 이루어져있다고 하겠습니다.
input data와 output data가 binary인 경우에 이 구조를 binary channel이라고 한다고 합니다.

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
$P(\cdot|\cdot)$의 두 $~\cdot~$에는 사건이, 그러니까 집합이 들어가야 하는데, 하나의 원소만 들어갔습니다.
$P(y_1|x_1)$라는 표현은 $P(\\{y_1\\}|\\{x_1\\})$로 해석하면 될 것 같습니다.
조금 더 정확하게는 $P(S_1\times\\{y_1\\}\|\\{x_1\\}\times S_2)$로 해석하면 될 것 같습니다.
하지만, 크게 혼동될 일이 없으니 $P(y_1|x_1)$로 써도 될 것 같습니다.)

만약 $P_{11}=P_{22}$이고 $P_{12}=P_{21}$이 성립하면 이 binary channel을 binary symmetric channel이라고 부릅니다.
(따라서 행렬이 symmetric한 것과는 다릅니다.)
당연히

$$
\begin{align*}
P_{11}+P_{21}=1\\
P_{12}+P_{22}=1
\end{align*}
$$

이 성립합니다.
강의에서는 세 종류의 계산을 해보는데, 첫번째 계산은 the law of total probability와 연관이 있고, 두번째와 세번째 계산은 Bayesian theorem과 연관이 있습니다.

**(1) error가 발생할 확률**

오류라고 판단할 수 있는 경우는 input이 $x_1$로 들어갔는데 output이 $y_2$로 나오는 경우와 그 반대의 경우(vice versa)입니다.
전자의 경우를 $\\{x_1\\}\times\\{y_2\\}$로 표현해야 정확하겠지만 이것을 그냥 $x_1\cap y_2$로 쓰면 (그러니까, $\left(\\{x_1\\}\times S_2\right)\cap\left( S_1\times\\{y_2\\}\right)$의 의미입니다.)

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

**(3) error가 발생했을 때, 입력값이 $x_1$일 확률**

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
문제에서 $P(x_i)$는 주어지지 않은 것처럼 보입니다.
그리고, 만약 이 channel이 symetric하면 위의 식은 조금 더 간단히 쓸 수 있을 것으로 보입니다.)

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_1-2.png){: .img-50-center}

**1.8 independent events**

두 개 혹은 여러 개의 사건에 대해서 독립/종속을 이야기할 수 있습니다.
강의에서는 두 개의 사건 $A$, $B$에 대한 독립(independece)만을 이야기합니다.
만약 두 사건 $A$, $B$가 서로 영향을 주지 않으면, 즉

$$P(B|A)=P(B)$$

이면, 혹은

$$P(A|B)=P(A)$$

이면, 두 사건 $A$, $B$가 서로 이라고 말합니다.
$P(A)\ne0$, $P(B)\ne0$인 경우에 이 독립조건은

$$P(A)P(B)=P(A\cap B)$$

와 동치입니다.

- 세 개 이상의 사건에 대한 독립을 말할 떄는 mutually independent라는 용어를 씁니다.
- 독립의 개념은 독립시행(복원시행, repeated restored trial)을 다룰 때 중요합니다.
- 독립(independence)과 배반(exclusiveness)의 개념을 혼동하지 말아야 합니다.
- $A$와 $B$가 독립이면 $A$와 $\overline B$($B$의 여사건, complement)도 독립입니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_1-3.png){: .img-50-center}

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

# 02 독립사건과 확률

**1.10 combinatorial analysis**

**1.10.1 permutation (순열)**

서로 다른 $n$개의 대상을 일렬로 나열하는 방법의 수는

$$n!=n\times(n-1)\times\cdots\times1$$

입니다.
$n!$은 $n$ factorial(팩토리얼)이라고 읽고, $0!=1$로 정의합니다.

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

이고 마지막 식을 $(\ast)$와 더하면

$$
\begin{equation}\tag{$**$}
nx(1+x)^{n-2}(1+nx)=\sum_{k=0}^nk^2\binom nkx^k
\end{equation}
$$

이산확률분포 $X$가 이항분포 $B(n,p)$를 따르면, $X$의 확률질량함수는

$$P(X=k)=\binom nkp^k(1-p)^{n-k}$$

입니다.
따라서 $X$의 평균은 $(\ast)$를 사용하여

$$
\begin{align*}
E(X)
&=\sum_{k=0}^nkP(X=k)\\
&=\sum_{k=0}^nk\binom nkp^k(1-p)^{n-k}\\
&=(1-p)^n\sum_{k=0}^nk\binom nk\left(\frac p{1-p}\right)^k\\
&\stackrel{(\ast)}=(1-p)^nn\cdot\frac p{1-p}\left(1+\frac p{1-p}\right)^{n-1}\\
&=np
\end{align*}
$$

으로 계산됩니다.
$X$의 분산은 조금 복잡한데 $(\ast\ast)$를 사용하여

$$
\begin{align*}
E(X)
&=E(X^2)-E(X)^2\\
&=\sum_{k=0}^nk^2P(X=k)-(np)^2\\
&=\sum_{k=0}^nk^2\binom nkp^k(1-p)^{n-k}-(np)^2\\
&=(1-p)^n\sum_{k=0}^nk^2\binom nk\left(\frac p{1-p}\right)^k-(np)^2\\
&\stackrel{(\ast\ast)}=(1-p)^n\frac{np}{1-p}\left(1+\frac p{1-p}\right)^{n-2}\left(1+\frac{np}{1-p}\right)-n^2p^2\\
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

입니다.
단, $|x|<1$ 입니다.

따라서

$$
f(x)=\frac1{(1-x)^2}
$$

입니다.
한편, 위의 결과를 다르게 얻을 수도 있는데

$$
g(x)=1+x+x^2+\cdots
$$

라고 하면 $g(x)=\frac1{1-x}$이고 $f(x)=g'(x)$이므로

$$
f(x)=\left(\frac1{1-x}\right)'=\frac1{(x-1)^2}
$$

인 것입니다.

**1.10.6 Sterling's formula**

$n$이 충분히 크면 $n!$는 다음 값과 거의 비슷합니다.

$$\sqrt{2\pi n}\left(\frac ne\right)^n$$

강의에는 이에 대한 증명이 나와있지 않은데 [이 자료](https://kconrad.math.uconn.edu/blurbs/analysis/stirling.pdf)(Keith Conrad의 자료)에 설명과 증명이 잘 되어 있는 것 같습니다.
여기에서의 증명은 Gaussian distribution을 통한 증명과, 어떤 함수열의 수렴을 통한 증명이 소개되고 있는 것 같습니다.
(언제 한 번 이것을 공부해서 포스트로 남기면 참 좋을텐데)

엄밀한 증명은 조금 어렵지만, 대략적으로 이 식의 의미를 파악하는 건 그렇게까지 어렵지 않은 것 같습니다.
어림하고자 하는 값 $n!$에 자연로그를 취하면

$$\log(n!)=\log1+\log2+\cdots+\log n$$

인데, 이것은 정적분

$$\int_1^n\log x\,dx$$

과 관련이 있는 값입니다.
폐구간 $1\le x\le n$를 길이가 1인 $n-1$개의 구간으로 나누면, 리만적분에서 흔히 하는 방식에 의해, 정적분의 값은 $n$개의 **큰** 직사각형들의 넓이의 합보다는 작고 $n$개의 (사실은 $n-1$개의) **작은** 직사각형들의 넓이의 합보다는 큽니다.
즉,

$$
\begin{align*}
\log1+\log2+\cdots+\log(n-1)&<\int_1^n\log x\,dx<\log2+\log3+\cdots+\log n\\[10pt]
\log((n-1)!)&<n\log n-n+1<\log(n!)\\[10pt]
n\log n-n+1&<\log(n!)<n\log n-n+1+\log n\\[10pt]
e^{n\log n-n+1}&<e^{\log(n!)}<e^{n\log n-n+1+\log n}\\[10pt]
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

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_2-1.png){: .img-50-center}

어떤 시스템(혹은 모듈)이 어떤 기간동안 얼마나 올바르게 고장나지 않고 잘 동작하는지를 나타내는 값을 reliability라고 합니다.
그것을 $R(t)$라고 적습니다.

**series connection(직렬연결)**

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_2-2.png){: .img-50-center}

여러 개의 독립적인 모듈 $C_1$, $\cdots$, $C_n$ 들이 직렬로 연결되어 있고(cascade) 각 모듈들의 reliabilty가 $R_1(t)$, $\cdots$, $R_n(t)$일 때, 이 시스템의 reliability는

$$\prod_{i=1}^nR_i(t)$$

입니다.

**parallel connection(병렬연결)**

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_2-3.png){: .img-50-center}

이번에는 이 모듈들이 병렬로 연결되어 있다면 이 시스템의 reliability는

$$1-\prod_{i=1}^n\left(1-R_i(t)\right)$$

입니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_2-4.png){: .img-50-center}

만약 위의 그림처럼 복잡한 시스템이라고 한다면, $C_3$가 동작하는지($R_x$) 동작하지 않는지($R_y$)에 따라 구분해서 얻어낼 수 있습니다.
전자의 경우에는 두 쌍의 병렬모듈들이 직렬로 연결된 것이고 후자의 경우에는 두 쌍의 직렬모듈들이 병렬로 연결된 것이라고 볼 수 있습니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_2-5.png){: .img-50-center}

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

# 03 확률변수의 정의

**Chapter 2. Random Variables(확률변수)**

**2.2 definiion of random variables**

언제나 확률변수의 개념을 정확히 이해하는 건 결코 쉬운 일은 아닌 것 같습니다.
매번 충분할 정도로 이해하고 넘어가려고 노력하는데도 불구하고 볼때마다 새로운 것 같습니다.
그래도 강의를 보며 다시 한 번 이해해봤습니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_3-1.png){: .img-50-center}

확률변수($X$)란, 어떤 시행의 근원사건 $w\in S$을 하나의 실수 $X(w)$로 대응시키는 함수를 말합니다.

A random variable is a function $X$ mapping each outcome of random experiment $w\in S$ to a real number $x=X(w)$.

즉 $X:S\to\mathbb R$인 $X$를 확률변수라고 합니다.

**ex.1 : tossing a coin**

동전을 하나 던져서 앞면이 나오면 1점을 얻고 뒷면이 나오면 $-1$점을 얻는 어떤 시행에서,

동전을 하나 던졌을 때 얻는 점수
{: .text-center}

를 확률변수 $X$로 정의할 수 있습니다.
이 시행에서 $S=\\{H,T\\}$이고, 확률변수 $X$는 $S$에서 $\mathbb R$로 가는 함수로서

$$
\begin{align*}
X(H)&=1\\
X(T)&=-1
\end{align*}
$$

확률변수를 사용하면 확률 $P(~\cdot~)$를 마치 숫자들의 함수로서 생각할 수 있게 됩니다.
그전까지 $P(A)$라는 표현에서 $A$는 사건(event)이라고 불렸고 표본공간 $S$의 부분집합을 의미했습니다.
그러니까 그전까지는 확률 $P(~\cdot~)$가 마치 '집합의 함수'처럼 동작했습니다.
그래서

$$P(\{H\})=\frac12,\quad P(\{T\})=\frac12,\quad P(\varnothing)=0,\quad P(S)=1$$

와 같은 표현들을 사용할 수 있었지만 직관적인 표현은 아니었습니다.

그런데 확률변수 $X$를 도입하고 나면 $P(~\cdot~)$를 숫자들의 함수처럼 생각할 수 있습니다.
$p(x)$ 혹은 $P(X=x)$라는 표현을 (이것들은 나중에 확률질량함수라는 이름을 가지게 되는데)

$$\tag{$\ast$}
\begin{aligned}
p(x)
&=P(X=x)\\
&=P\left(\{w\in S:X(w)=x\}\right)
\end{aligned}
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

이번에는 동전던지기에 관한 또다른 확률변수를 생각해봅니다.

동전을 두 번 던졌을 때 나온 앞면의 수
{: .text-center}

도 확률변수 $X$가 됩니다.
이때의 표본공간은 $S=\\{H,T\\}^2$인데, 강의에서는 cartesian product에서의 순서쌍의 표현을 생략하여, $S=\\{HH,HT,TH,TT\\}$로 쓰고 있습니다.
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
이때 $A_x$는 사건으로서, 확률변수 $X$가 $x$의 값을 가지는 경우, 즉 $X(w)=x$인 $w\in S$들의 집합입니다.
(따라서 이것은 $X$의 inverse image $X^{-1}(x)$이기도 합니다.)

$$A_x=\{w\in S:X(w)=x\}$$

이것은 아까 $(\ast)$에서 $p(x)$ 혹은 $P(X=x)$를 정의할 때 쓰인 집합입니다.
즉, $p(x)$ 혹은 $P(X=x)$를

$$p(x)=P(X=x)=P(A_x)$$

로 정의합니다.

지금까지, $P(~\cdot~)$에 들어가는 것이 사건(event, $S$의 부분집합)이었던 것을, 특정한 숫자로 들어갈 수 있게 바꾸었습니다.
여기에는 '숫자들의 집합'도 들어갈 수 있습니다.
예를 들어 $\\{X:a\lt X\le b\\}$와 같은 집합도 들어갈 수 있습니다.
보통 쓸 때는 $P(\\{X:a\lt X\le b\\})$로 쓰지 않고 $P(a\le X\le b)$로 표기하는데

$$
P(a<X\le b)=P\left(\{w\in S:a<X(w)\le b\}\right)
$$

로 정의합니다.
예를 들어 동전 두 개를 던지는 시행에서

$$P(X\le1)=P\left(\{HH,HT,TH\}\right)=\frac34$$

입니다.

**2.4 distribution functions**

확률변수 $X$와 실수 $x$에 대하여 cumulative distribution function(CDF, 누적확률)은 

$$F_X(x)=P\left(X\le x\right)$$

로 정의합니다.
위의 동전 두 개를 던지는 시행에서

$$F_X(1)=\frac34$$

였습니다.

따라서 CDF는
- nondecreasing 입니다 : if $x_1\lt x_2$, then $F_X(x_1)\le F_X(x_2)$
- 치역이 $[0,1]$입니다 : $0\le F_X(x)\le1$
- 두 점근선을 가집니다 : $\displaystyle\lim_{x\to\infty}F_X(x)=1$, $\displaystyle\lim_{x\to-\infty}F_X(x)=0$
- $P(a\lt X\le b)=F_X(b)-F_X(a)$
- $P(x>a)=1-F_X(a)$

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_3-3.png){: .img-50-center}

위의 $P(a\lt X\le b)$에서와 같이 부등호를 $\lt$로 할지 $\le$로 할지는 잘 구분해주어야 합니다.
다만, 연속확률변수의 경우에는 (아래 예제와 같은 예외가 발생하지 않는 한은) 둘 사이에 구분을 두지 않아도 됩니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_3-4.png){: .img-50-center}

위 그림과 같은 예제에서 CDF는

$$
F_X(x)=\begin{cases}
0&(x\lt0)\\
x+\frac12&(0\le x\le\frac12)\\
1&(x\gt\frac12)\\
\end{cases}
$$

와 같이 주어져 있는데

$$
\begin{align*}
P\left(X>\frac14\right)&=1-F_X\left(\frac14\right)=1-\frac34=\frac14\\
P(X>0)&=1-F_X(0)=1-\frac12=\frac12\\[10pt]
P(X\ge0)&=1\\[10pt]
P(X=0)&=1\\[10pt]
P\left(X\ge\frac14\right)&=\frac14
\end{align*}
$$

입니다.
아래의 세 개 계산은 notrivial합니다.
좌우극한을 가지고 계산하면

$$
\begin{align*}
P(X\ge0)
&=1-P(X\lt0)\\[10pt]
&=1-\lim_{x\to0+}P(X\le x)\\
&=1-\lim_{x\to0+}\left(x+\frac12\right)\\
&=1-0=1\\[10pt]
P(X=0)
&=P(X\le0)-P(X\lt0)\\
&=\frac12-0=1\\
P\left(X\ge\frac14\right)
&=1-P\left(X\lt\frac14\right)\\[10pt]
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

이산확률변수의 분포(distribution)는 확률질량함수의 그래프로서 나타내는데, 그것을 $xy$ 평면에 찍힌 여러 개의 점으로 표현하기보다는, 여러 개의 선분으로써 표현하는 경향이 있는 것 같습니다.

동전을 두 개 던지는 시행에서의
확률질량함수의 그래프와 CDF와 PMF의 그래프는 아래와 같습니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_3-5.png){: .img-100-center}

CDF의 그래프는 step function으로 나타나는 것을 볼 수 있습니다.

이산확률변수 $X$에 대하여 연속확률변수에서의 확률밀도함수 $f_X(x)$에 대응하는 개념을 설명하려면 dirac delta function과 같이 조금 복잡한 논의가 필요합니다.
다시 말해, 연속확률변수에서는

$$P(a\lt X\le b)=\int_a^bf_X(x)\,dx$$

와 같은 식을 만족시키는 함수 $f_X(x)$를 생각하게 되는데, 위의 $P_X(x)$의 그래프에서는 '그래프 아래의 면적'이라는 개념을 정의할 수 없으니까 애매합니다.
그럴 때에, 함수 $\delta$(dirac delta function)를 도입하는데, 이 함수는

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

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_3-6.gif){: .img-10-center}

따라서 이 함수 $\delta(x)$가

$$
P_X(x)=
\begin{cases}
1&(x=0)\\
0&(x\ne0)
\end{cases}
$$

와 같이 정의된 가장 기본적인 확률질량함수 $P_X(x)$에 대응되는 확률밀도함수라고 생각할 수 있습니다.
일반적인 확률질량함수에 대한 확률밀도함수는 이 $\delta(x)$를 적절히 shift한 것들을 가지고 일차결합하여 만들어낼 수 있습니다.
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
<div class="notice--danger">
dirac delta function은 엄밀히 말하면 함수가 아닌 generalized function이며, measure나 distribution을 통해 이해될 수 있다고 합니다.
</div>


# 04 이산확률변수와 연속확률변수

**2.6 continuous random variables**

앞서 강의에서 확률변수를 $X:S\to\mathbb R$인 함수로 정의했습니다.
어떤 확률변수가 이산확률변수인지 연속확률변수인지를 결정하는 것은 이 확률변수의 치역 $X(S)$과 관련있습니다.
$X(S)$가 countable이면 (혹은 at most countable, 그러니까, finite이거나 countably infinte) $X$를 이산확률변수라고 합니다.
이것은

확률변수 $X$가 가질 수 있는 값이 유한개(혹은 countable)이면 $X$를 이산확률변수라고 부릅니다.
{: .text-center}

와 같은 앞서의 정의를 다시 쓴 것입니다.

만약, 확률변수가 이산확률변수가 아니면 연속확률변수라고 부릅니다.
그러니까, 치역 $X(S)$가 uncountable인 경우를 말합니다.
말로 풀어 쓰면

확률변수 $X$가 가질 수 있는 값이 uncountable하게 많으면 $X$를 연속확률변수라고 부릅니다.
{: .text-center}

이산확률분포의 경우에 비해 연속확률분포의 경우에는 조금 어렵고 섬세한 이야기들이 많이 산적해있습니다.
예를 들어 0과 1 사이의 숫자를 임의로 뽑을 때 그 값을 $X$라고 하면, $X$는 연속확률변수입니다.
그런데 이런 경우에 $P(X=0.5)$을 어떻게 정의해야 할 지 애매합니다.

<div class="notice--danger">
답 : $P(X=0.5)=0$<br>

확률을 measure-theoretic하게 생각하면 $P$는 하나의 measure라고 볼 수 있고 이 경우에는 '집합의 길이'와 관련된 measure를 $P$로써 정의합니다.
그런데 원소가 하나인 집합에 대한 '길이'는 0이므로 $P(X=0.5)=0$입니다.<br>

조금 더 직관적으로 말할 수도 있을 것 같습니다.
$P(X=0.5)=a$로 두면 ($a>0$) 다른 모든 숫자 $0\le x\le1$에 대해서도 마찬가지로 $P(X=x)=a$가 성립한다고 말할 수 있을 겁니다.
그러면, 모든 $x$에 대하여 이 확률값들을 더했을 때 1이 되어야 합니다.
사실 이 덧셈이 잘 정의되는지도 의문이기는 하지만, 어쨌든 양수 $a$를 무한번 더해서 1이 된다는 것인데, 이건 말이 안됩니다.
따라서, 임의의 양의 실수 $a$에 대하여 $P(X=0.5)=a$일 수 없고, $P(X=0.5)=0$일 수밖에 없습니다.
</div>

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

(1) $f_X(x)\ge0$

(2) $\int_{-\infty}^\infty f_X(x)\,dx=1$

마찬가지로, 함수 $P_X(x)$가 어떤 이산확률변수의 PMF이기  위해서는 다음의 두 조건을 만족시켜야 합니다.

(1) $p_X(x_i)\ge0$

(2) $\sum_{k=1}^n p_X(x_i)=1$

PDF의 추가적인 성질들은 다음과 같습니다.

(3) $\int_a^bf_X(x)\,dx=P(a\lt X\le b)$

이것은, 지금까지 쓴 개념들을 동원해 쉽게 증명됩니다.

$$
\begin{align*}
P(a\lt X\le b)
&=F_X(b)-F_X(a)\\
&=\int_{-\infty}^bf_X(x)\,dx-\int_{-\infty}^af_X(x)\,dx\\
&=\int_a^bf_X(x)\,dx
\end{align*}
$$

(4) $P(X\lt a)=P(X\le a)$

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

$f_X(x)$가 (혹은 $P_X(x)$가) 상수함수이면 $X$가 uniform distribution을 따른다고 정의합니다.
아까, 0과 1 사이의 숫자를 임의로 골라 그 값을 $X$라고 할때, $X$는 uniform distribution을 따릅니다.
주사위를 하나 던져 눈을 보는 것도 일종의 uniform distribution에 해당합니다.

고등학교 과정의 '기하학적 확률'에서 확률을 넓이 혹은 길이에 의존해 계산하게 되는데 그러한 상황 또한 uniform distribution을 가정하고 있습니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_4-1.png){: .img-100-center}

강의의 마지막 부분에는 신호나 그림에서의 sampling과 quantization, binarization에 대해 언급됩니다. (아래 캡쳐)

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_4-2.png){: .img-100-center}

이에 대한 설명은 다음과 같습니다.

연속적인 아날로그 신호(continuous, analogue signal)를 특정한 주파수로 sampling하면 discrete signal을 얻을 수 있습니다.
이 discrete signal을 표현할 때에는 특정한 step size를 가정하여 level의 형태로 얻게 되는데 이 과정을 양자화(quantization)라고 부릅니다.
마지막으로 이 값들을 2진수로 바꾸어(binarization) 디지털 신호로 바꾸는 과정이 있습니다.
이 일련의 과정들은 아날로그로 주어진 데이터를 디지털의 형태로 바꾸는 작업입니다.
이때, 실제 신호와 level로 주어진 근사값들 사이의 차이를 quantization error라고 가정하는데, 많은 경우에 이 error를 uniform distribution을 따른다고 가정하고 모델링을 진행한다고 합니다.

<div class="notice--danger">
<b> 확률분포(probabilistic distribution) </b>
확률변수 $X$가 어디에 얼마나 분포되어있는지 하는 것을 그 확률변수의 분포(distribution)이라고 합니다.
이 분포를 직접적으로 표현하는 것이 PMF, PDF, CDF와 같은 분포함수들입니다.
그 중 이산확률변수에 대해서는 PMF를, 연속확률분포에 대해서는 PDF를 주로 분포함수로 취급하게 되는데 PMF와 PDF는 모든 종류의 확률변수에 대해 잘 정의되지 않습니다.

예를 들어, PDF로는 이산확률분포를 정하기가 힘들었습니다.
그래프의 면적이 1이 된다는 점을 만족시키기 위해서 dirac delta function 같은 것을 도입해야 했습니다.
또, PMF로는 연속확률분포를 정하는 데 어려움이 있었습니다.
각 점에 대한 PMF의 값이 0이 될 수밖에 없는데, 그건 그것대로 모순이었습니다.

하지만, CDF는 $X$가 이산확률변수이건 연속확률변수이건 상관없이 적절하게 잘 정의될 수 있습니다.
또한, 일단 CDF가 정해지고 나면 CDF의 식으로부터 PMF나 PDF의 식을 쉽게 구할 수 있다는 점도 있습니다.
그래서 그런지, 많은 경우에 CDF를 먼저 정의하고, 그 이후에 PMF나 PDF를 정의하는 것 같습니다.

 정할 수 없었습니다. (정하려면, PMF의 값들을 모두 0으로 만들어야 하는데)

dirac delta function은 엄밀히 말하면 함수가 아닌 generalized function이며, measure나 distribution을 통해 이해될 수 있다고 합니다.
</div>

# 05 확률변수의 평균과 분산

**Chapter 3. moments of random variables**

**arithemetic average(산술평균)**

$x_i$들의 산술평균은

$$\bar x=\frac{x_1+\cdots+x_N}N.$$

**different frequences**

서로다른 $x_i$들에 대하여 그 빈도 $w_i$가 주어져 있을 때의 평균(weighted average)은

$$\bar x=\frac{w_1x_1+\cdots+w_Nx_N}{w_1+\cdots+w_N}.$$

**3.1 expectation(mean)**

$$
\begin{align*}
E[X]&=\sum_{i=1}^nx_iP_X(x_i)             &&(\text{discrete})\\
E[X]&=\int_{-\infty}^\infty xf_X(x)\,dx &&(\text{continuous})
\end{align*}
$$

**ex 3.3 Poisson distribution**

$$
P_K(k)=\frac{\lambda^k}{k!}e^{-\lambda}\qquad(k=0,1,2,\cdots)
$$

$K$가 the number of event occurence in time interval이라고 하면, $K$는 위와 같은 분포를 따르는 경우가 많다고 합니다.

$P_K$가 PMF가 되기 위해서는 두 조건을 만족시켜야 하는데 첫번쨰 조건인 $P_K(k)\ge0$은 당연합니다.
두번째 조건인 $\sum_k P_K(k)=1$을 위해서는 $e^x$에 대한 Maclaurin series(혹은 지수함수의 추상적인 정의)를 사용할 수 있습니다;

$$e^x=\sum_{k=0}^\infty\frac{x^k}{k!}$$

여기에 $x=\lambda$를 대입하여

$$e^\lambda=\sum_{k=0}^\infty\frac{\lambda^k}{k!}$$

를 얻습니다.
이 식의 양변에 $e^{-\lambda}$를 곱하면

$$1=\sum_{k=0}^\infty\frac{\lambda^k}{k!}e^{-\lambda}=\sum_{k=1}^\infty P_K(k)$$
가 되어 두번째 조건을 만족시킵니다.
따라서 $P_K(k)$는 정말로 PMF가 됩니다.
강의에서는 일반적인 Taylor series에 대한 설명도 포함되어 있습니다.

이 Poisson distribution에 대한 평균을 구해보면

$$
\begin{align*}
E[X]
&=\sum_{k=0}^\infty kf_K(k)\\
&=\sum_{k=0}^\infty k\frac{\lambda^k}{k!}e^{-\lambda}\\
&=\sum_{k=1}^\infty k\frac{\lambda^k}{k!}e^{-\lambda}\\
&=\lambda\sum_{k=1}^\infty\frac{\lambda^{k-1}}{(k-1)!}e^{-\lambda}\\
&=\lambda\sum_{m=0}^\infty\frac{\lambda^m}{m!}e^{-\lambda}\\
&=\lambda
\end{align*}
$$

이 됩니다.

**ex 3.4 exponential distribution**

$$
\begin{align*}
f_X(x)=
\begin{cases}
\lambda e^{-\lambda x}  &x\ge0\\
0                       &x\lt0
\end{cases}
\end{align*}
$$

이번에도 $f_X$가 PDF가 되기 위해서는 두 가지 조건을 만족시켜야 하는데 첫번째 조건 $f_X(x)\ge0$은 당연합니다.
두 번째 조건인 $\int_{-\infty}^\infty f_X(x)\,dx=1$
을 확인해보면

$$
\begin{align*}
\int_{-\infty}^\infty f_X(x)\,dx
&=\lambda\int_0^\infty e^{-\lambda x}\,dx\\
&=\lambda\times\left[-\frac1\lambda e^{-\lambda x}\right]_0^\infty\\
&=\lambda\times\frac1\lambda\\
&=1
\end{align*}
$$

이 성립합니다.
한편, 평균을 구해보면

$$
\begin{align*}
E[X]
&=\int_{-\infty}^\infty xP_X(x)\,dx\\
&=\lambda\int_0^\infty xe^{-\lambda x}\,dx\\
&=\lambda\left(\left[-\frac1\lambda xe^{-\lambda x}\right]_0^\infty
+\int_0^\infty\frac1\lambda e^{-\lambda x}\,dx\right)\\
&=\lambda\left(0+\left[-\frac1{\lambda^2}e^{-\lambda x}\right]_0^\infty\right)\\
&=\frac1\lambda
\end{align*}
$$

입니다.

이와 같은 푸아송 분포와 지수분포는 특정한 값(parameter) $\lambda$에 의존합니다.
실제 자연현상이나 사회현상은 그 분포를 알 수 없는데, 우리는 특정한 확률모델을 전제하여 그 현상을 모델링해볼 수 있습니다.
이와 같은 과정을 parametric estimation (혹은 parametric probability density estimation) 이라고 부르는 것 같습니다.

**3.4 moments of random variables**

**nth order moments**

$$
\begin{align*}
E[X^n]&=\sum_i{x_i}^n P_X(x_i)\\
E[X^n]&=\int_{-\infty}^\infty x^n f_X(x)\,dx
\end{align*}
$$

**central moments**

$$
\begin{align*}
E[(X-\mu)^n]&=\sum_i(x_i-\mu)^nP_X(x_i)\\
E[(X-\mu)^n]&=\int_{-\infty}^\infty(x-\mu)^n f_X(x)\,dx
\end{align*}
$$

$n=1$이면

$$
\begin{align*}
E[(X-\mu)]
&=\sum_i(x_i-\mu)P_X(x_i)\\
&=\sum_ix_iP_X(x_i)-\mu\sum_iP_X(x_i)\\
&=\mu-\mu\times 1\\
&=0
\end{align*}
$$

입니다.
즉, 편차의 합은 항상 0입니다.

$n=2$이면

$$
\begin{align*}
E[(X-\mu)^2]
&=\sum_i(x_i-\mu)^2P_X(x_i)
\end{align*}
$$

인데 이 값을 분산(variance)이라고 부르고 ${\sigma_X}^2$으로 씁니다.

- 분산은 항상 0보다 크거나 같습니다.
- 모든 변량이 같으면 ($x_1=\cdots=x_n$) 분산이 0이고 그 역도 성립합니다.
- 분산이 작으면 변량들이 평균에 모여있고 분산이 크면 변량들이 넓게 분포되어 있습니다.
- $t$에 대한 함수 $g(t)=E[(X-t)^2]$를 생각하면 이 함수는 $t=\mu$에서 최솟값 ${\sigma_X}^2$를 가집니다.


**Proposition 3.3**

어떤 확률변수 $X$에 대한 함수 $g_1(X)$, $\cdots$, $g_n(X)$와 실수 $a_1$, $\cdots$, $a_n$에 대하여

$$
E[a_1g_1(X)+\cdots+a_ng_n(X)]=a_1E[g_1(X)]+\cdots+a_nE[g_n(X)]
$$

이 성립합니다.
정의에 넣어서 증명해보면 바로 증명됩니다.

이것은 $E$가 linear operator라는 뜻입니다.
즉, 모든 실함수(혹은 real measureable function)들의 집합을 $V$라고 하면, 이것은 (무한차원의) 벡터공간입니다.
이때, $E$는 $E:V\to\mathbb R$인 함수라고 생각할 수 있는데 이 $E$가 선형함수라는 뜻입니다. (더 구체적으로는, linear functional입니다.)

이 proposition으로부터 바로 얻을 수 있는 결과는

$$E[aX+b]=aE[X]+b$$

입니다.
또한

$$
\begin{align*}
{\sigma_X}^2
&=E[(X-\mu)^2]\\
&=E[X^2-2\mu X+\mu^2]\\
&=E[X^2]-2\mu E[X]+\mu^2\\
&=E[X^2]-2E[X]^2+E[X]^2\\
&=E[X^2]-E[X]^2
\end{align*}
$$

입니다.
이를 이용하여 Poisson distribution

$$P_K(k)=\frac{\lambda^k}{k!}e^{-\lambda}$$

에서의 분산을 구해보면

$$
\begin{align*}
E[K^2]
&=\sum_{k=0}^\infty k^2P_K(k)\\
&=\sum_{k=0}^\infty k^2\frac{\lambda^k}{k!}e^{-\lambda}\\
&=\sum_{k=0}^\infty k(k-1)\frac{\lambda^k}{k!}e^{-\lambda}
+\sum_{k=0}^\infty k\frac{\lambda^k}{k!}e^{-\lambda}\\
&=\sum_{k=2}^\infty k(k-1)\frac{\lambda^k}{k!}e^{-\lambda}+E[X]\\
&=\lambda^2\sum_{k=2}^\infty\frac{\lambda^{k-2}}{(k-2)!}e^{-\lambda}+E[X]\\
&=\lambda^2+\lambda
\end{align*}
$$

으로부터

$${\sigma_K}^2=E[K^2]-E[K]^2=(\lambda^2+\lambda)-\lambda^2=\lambda$$

입니다.
또한, exponential distribution

$$
\begin{align*}
f_X(x)=
\begin{cases}
\lambda e^{-\lambda x}  &x\ge0\\
0                       &x\lt0
\end{cases}
\end{align*}
$$

에서의 분산을 구해보면

$$
\begin{align*}
E[X^2]
&=\int_0^\infty x^2P_X(x)\,dx\\
&=\int_0^\infty x^2\lambda e^{-\lambda x}\,dx\\
&=\left[-x^2e^{-\lambda x}\right]_0^\infty+\int_0^\infty2xe^{-\lambda x}\,dx\\
&=0+\frac2\lambda\int_0^\infty x\lambda e^{-\lambda x}\,dx\\
&=\frac2\lambda\cdot E[X]=\frac2{\lambda^2}
\end{align*}
$$

이고

$${\sigma_X}^2=E[X^2]-E[X]^2=\frac1{\lambda^2}$$

입니다.

# 06 조건부 평균

**ex 3.13 geometric distribution**

Let $K$ be the number of trials until the first success.
For example, we may toss a die  repeatedly until the first $6$.

따라서 $K$는 이산확률변수이고, PMF는

$$P_K(k)=(1-p)^{k-1}p$$

로 주어집니다.
PMF의 두번째 조건을 (예의상) 확인해보면

$$
\sum_{k=1}^\infty P_K(k)=p+p(1-p)+p(1-p)^2+\cdots=\frac p{1-(1-p)}=1
$$

입니다.
다음으로 평균을 구해보면

$$
\begin{align*}
E[K]
&=\sum_{k=1}^\infty kP_k(k)\\
&=\sum_{k=1}^\infty k(1-p)^{k-1}p\\
&=p+2(1-p)p+3(1-p)^2+\cdots\\
(1-p)E[K]&=(1-p)p+2(1-p)^2p+3(1-p)^3p
\end{align*}
$$

두 식을 적당히 빼면

$$
pE[K]=p+(1-p)p+(1-p)^2p+\cdots=1
$$

이고 $E[K]=\frac1p$입니다.

(강의에서는 미분을 통해 구한 것 같습니다만, 위와 같이 멱급수의 공비를 곱하는 방식으로 구해봤습니다.
하지만 지금 구한 방법으로는 분산을 구하기가 힘들 것 같으니, 미분의 방법으로 처음부터 다시 풀어보면)

다시 평균을 구하기 위해 평균 식

$$E[K]=\sum_{k=1}^\infty k(1-p)^{k-1}p$$

을 보면 $\sum_k (1-p)^k$와 같은 함수형태를 미분하는 것이 요긴할 것으로 보입니다.
등비급수의 식에 의해

$$\sum_{k=1}^\infty(1-p)^k=\frac{1-p}{1-(1-p)}=\frac{1-p}p=\frac1p-1$$

이고, 양변을 미분한 뒤 마이너스를 붙이면

$$
\begin{equation}\tag{$*$}
\sum_{k=1}^\infty k(1-p)^{k-1}=\frac1{p^2}
\end{equation}
$$

입니다.
따라서

$$E[K]=\frac1{p^2}\times p = \frac1p$$

입니다.
$E[K^2]$의 식도 보면

$$E[K^2]=\sum_{k=1}^\infty k^2(1-p)^{k-1}p$$

인데, 이것은 식 ($\ast$)을 미분하면 비슷한 식을 얻을 수 있습니다.
($\ast$)을 미분한 뒤 마이너스를 붙이면

$$\sum_{k=1}^\infty k(k-1)(1-p)^{k-2}=\frac2{p^3}$$

이고, 따라서

$$
\begin{equation}\tag{$\ast\ast$}
\begin{aligned}
\sum_{k=1}^\infty k^2(1-p)^{k-2}
&=\frac2{p^3}+\sum_{k=1}^\infty k(1-p)^{k-2}\\
&=\frac2{p^3}+\frac1{p^2(1-p)}\\
&=\frac{2(1-p)+p}{p^3(1-p)}\\
&=\frac{2-p}{p^3(1-p)}
\end{aligned}
\end{equation}
$$

이고,

$$
E[K^2]=\sum_{k=1}^\infty k^2p(1-p)^{k-1}
=\frac{2-p}{p^3(1-p)}\times p(1-p)=\frac{2-p}{p^2}
$$

입니다.
따라서

$${\sigma_K}^2=E[K^2]-E[K]^2=\frac{2-p}{p^2}-\frac1{p^2}=\frac{1-p}{p^2}$$

입니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_6-1.png){: .img-100-center}

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_6-2.png){: .img-100-center}

이후에는 평균과 분산의 의미에 대한 설명이 있습니다(위 캡쳐).
computer vision에서의 얼굴인식문제를 아주 naive하게 생각할 때, 우리는 실제 카메라에 인식된 얼굴모양(실제값)이 우리가 정한 특정한 형태의 얼굴모양 (표준참값, 예측값, 추정값, 표준모델)과 얼마나 비슷한지를 판단할만한 판단근거가 필요합니다.

이때의 실제값과 표준참값은 각각 벡터로 생각할 수 있고, 따라서 표준적인 벡터사이의 거리(의 제곱)인 $L^2$ norm(의 제곱)을 생각하게 됩니다.
그것은 실제값과 표준참값을 뺀 다음 제곱하여 성분별로 더하는 것을 말합니다.
그리고 이 값(energy라고 통상 부르기도 하는 값)이 최소가 되도록 하는 표준참값을, '괜찮은 모델'이라고 둘 수 있을 것입니다.

그런데 $L^2$ norm의 제곱, 즉 sum of squared error(SSE)는 그 특성상 표준참값이 실제값들의 평균일 때에 최소가 되는 경향이 있습니다.
(사실 표준참값-실제값 예는 multivariate이고 뒤에 나오는 예시는 univariate이라서 적절한 설명인지 잘 이해가 안가긴 하지만)
그리고 이것은 아까 간단하게 언급한 적이 있습니다.

$$g(t)=\sum_{k=1}^n(t-x_k)^2$$

는 $t=\frac1n\sum_{k=1}^nx_k$일 때, 즉 $t$가 $x_k$들의 평균일 때 최소가 되는 것입니다.
(중학교 식으로 $ax^2+bx+c$의 최솟값을 구하는 식으로 해도 되고, 고등학교 식으로 미분을 사용해도 됩니다.)
여기에서는 discrete uniform distribution인 경우에 대해서만 증명한 셈이지만 일반적인 분포에 대해서도, 그리고 연속확률분포에 관해서도 마찬가지의 사실을 쉽게 증명할 수 있습니다.

반면

$$h(t)=\sum_{k=1}^n|t-x_k|$$

와 같은 값을 objective function으로 둘 수도 있을 것입니다.
이 경우에는 $t$가 $x_k$들의 중간값(median)일 때 $g(t)$가 최소임이 알려져있습니다.
이것은 그래프를 살짝 그려보기만 해도 알 수 있습니다. (아래 그림) 다만, 이 경우도 역시 discrete uniform distribution에 대한 논증인데, 일반적인 분포와 연속확률분포에 대해서는 다른 방식의 증명이 필요할 것입니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_6-3.png){: .img-100-center}

**3.5 conditional mean**

이산확률변수의 conditional mean(조건부 기댓값)을 정의하기 전에, 먼저 conditional PMF(조건부 확률질량함수)를 다음과 같이 정의합니다.

$$P_X(x|A)=P(X=x|A)$$

이때, $X=x$라는 표현이 마치 사건처럼 쓰여져있습니다.
이것은

$$P(\{w\in S:X(w)=x\}|A)$$

의 의미입니다.

<!-- 여기에서도 notation에 대한 이슈를 언급하지 않을 수가 없습니다.
$P(x_i|A)$라는 표현은 아직 정의된 적이 없는 표현입니다.
$P(\cdot|\cdot)$에서 두 개의 $~\cdot~$은 사건, 그러니까 $S$의 부분집합이 들어가야 합니다.
그런 점에서 $A$는 적절히 잘 들어갔으나, $x_i$는 도저히 사건이 아닙니다.
$P(x_i\cap A)$라는 표현 또한 마찬가지입니다. -->

<!-- 그런데, 앞서 확률변수의 의미($P$가 집합의 함수가 아니라 숫자의 함수라서 더 다루기가 편해졌다는 내용)에 대해 말할 때에 $p(x)$라는 표현을 쓴 적이 있습니다.
이것은

$$p(x)=P(X=x)=P(A_x)=P\left(\{w\in S:X(w)=x\}\right)$$

으로 정의되었던 것 같습니다.
여기서 $P(A_x)$라는 표현은 $A_x$가 사건이라는 점에서 제대로 된 표현입니다.
그러니까 위의 식을, (굉장히 원리주의적인 방식으로) 다시 표현하면

$$
\begin{align*}
E[X|A]
&=\sum_{x_i\in A}x_iP(A_{x_i}|A)\\
&=\sum_{x_i\in A}x_i\frac{P(A_{x_i}\cap A)}{P(A)}
\end{align*}
$$

와 같이 해석할 수 있을 것입니다.
notation 상의 문제가 없으니 앞으로는 $P(x_i|A)$, $P(x_i\cap A)$와 같은 표현을 마음껏 쓸 수 있을 것 같습니다. -->

<!-- (다만, $E[X|A]$라는 표현에 대해서는, 그 자체가 정의이기때문에 문제될 것이 없고, 직관적으로도 '사건 $A$가 발생했다는 조건 하에서의 $X$의 평균'이라는 의미이므로 전혀 문제될 것이 없지만, 아주 잘 와닿지는 않는 것 같습니다.) -->

그러면, 이산확률변수에서의 conditional expectation을

$$E[X|A]=\sum_{x_i\in A}x_iP_X(x_i)$$

로 정의할 수 있습니다.
(여기에서 $A\subset S$라면, $x_i\in A$는 $X^{-1}(\{x_i\})\subset A$로 해석해야 할 것입니다.)

이번에는 연속확률변수의 조건부 기댓값을 정의하겠습니다.
먼저 conditional CDF는

$$
F_X(x|A)=P(X\le x|A)
$$

로 정의됩니다.
conditional PDF는 PDF의 정의에서와 마찬가지로 미분을 통해 얻을 수 있습니다.

$$
\begin{align*}
f_X(x|A)
&=\lim_{\Delta x\to0+}\frac{P\left(x<X\le x+\Delta x|A\right)}{\Delta x}\\
&=\lim_{\Delta x\to0+}\frac{F_X(x+\Delta x|A)-F_X(x|A)}{\Delta x}\\
&=\frac d{dx}F_X(x|A)
\end{align*}
$$

입니다.
이를 통해 conditional expectation을

$$
E[X|A]=\int_{x\in A}xf_X(x|A)\,dx
$$

로 정의할 수 있습니다.
(마찬가지로 $x\in A$는 $X^{-1}(\{x\})\subset A$로 해석해야 할 것입니다.)

<!-- 이때, $f_X(x|A)$는 conditional probability density function, 줄여서 conditional density (혹은 conditional PDF) 입니다.
이것은 정의이며, 이 정의는 discrete case와 정확히 잘 대응되는 정의입니다.
그리고 이것은 conditional cumulative distribution function (혹은 conditional CDF)를 미분해서 얻어집니다.
이것 또한 정의이며, PDF와 CDF 사이의 관계와 같다는 점에서 일관된 정의입니다.
세번째 줄의 $P(X\le x|A)$라는 표현도 큰 문제는 없습니다.
$P\left(\\{w\in S:X(w)\le x\\}|A\right)$ 이므로 잘 정의됩니다. -->

**ex. 3.14**

사건 $A=\\{X\le a\\}$에 대하여 conditional CDF와 conditional PDF를 구해봅니다.
이때 $A$는

$$A=\{w\in S:X(w)\le a\}$$

라는 의미입니다.
이때 $X$의 CDF와 PDF는 이미 주어져 있다고 가정합니다.
그러니까, $F_X(x)$와 $f_X(x)$를 사용하여 $F_X(x|A)$와 $f_X(x|A)$를 구하는 것이 목적입니다.
conditional CDF $F_X(x|A)$ 를 먼저 계산하면

$$
\begin{align*}
F_X(x|A)
&=P\left(X\le x|X\le a\right)\\
&=\frac{P\left(X\le x\cap X\le a\right)}{P(x\le a)}
\end{align*}
$$

입니다.
두 경우가 있을 수 있는데, 만약 $x\gt a$이면,

$$F_X(x|A)=\frac{P(X\le a)}{P(X\le a)}=1$$

이 됩니다.
만약 $x\le a$이면

$$F_X(x|A)=\frac{P(X\le x)}{P(X\le a)}=\frac{F_X(x)}{F_X(a)}$$

가 됩니다.
<!-- 여기에서 분모인 $F_X(a)$ 값은 $x$와는 관계가 없는 상수입니다. -->
<!-- 우리 목적은 conditional CDF $F_X(x|A)$를 $F_X$와 $f_X$로 표현하는 것이므로 여기서 더 계산할 필요는 없습니다. -->
정리하면

$$
F_X(x|A)=
\begin{cases}
1&(x\gt a)\\
\frac{F_X(x)}{F_X(a)}&(x\le a)
\end{cases}
$$

입니다.
다음으로, condtional PDF $f_X(x|A)$를 구하면

$$
f_X(x|A)
=\frac d{dx}F_X(x|A)
=\begin{cases}
0&(x\gt a)\\
\frac{f_X(x)}{F_X(a)}&(x\le a)
\end{cases}
$$

입니다.

**ex. 3.15**

이번에는 PDF가

$$f_X(x)=\frac1{20},\quad 40\le x\le 60$$

로 주어지고, 사건 $A$가

$$A=\{X\le 55\}$$

인 경우를 보겠습니다.
conditionoal PDF는

$$
F_X(x|A)=P(X\le x|X\le 55)=\frac{x-40}{15}
$$

이고 conditionoal CDF는

$$
f_X(x|A)=\frac d{dx}F_X(x|A)=\frac1{15}
$$

입니다.
또한, condtional expectation은

$$
\begin{align*}
E[X|A]
&=\int_{x\in A}xf_X(x|A)\,dx\\
&=\int_{40}^{55}\frac1{15}x\,dx\\
&=\frac1{15}\frac12(55-40)(55+40)\\
&=\frac{95}2\\
&=47.5
\end{align*}
$$

입니다.
그냥 의미적으로 해석해보면, 원래 $X$는 40과 60 사이에 균일하게 분포되어 있었는데, 여기에 $X$가 55보다 작다는 조건 $A$를 준 것입니다.
그러면 이 조건 하에서 $X$는 40과 55 사이에 균일하게 분포되어 있습니다.
따라서 이 조건 하에서의 평균은 $\frac{40+55}2=47.5$가 되어야 합니다.

그런 것 치고는 위의 계산은 불필요하게 복잡한 것 같습니다.
저 위의 계산처럼 conditional density를 사용하지 않는 방법은.. 크게 없을 것 같습니다. conditional PDF로 바로 변환되는 것이 아니기 때문입니다.
굳이 다른 방법을 찾자면 부분적분을 사용해 conditional CDF를 사용할 수도 있을 것 같습니다.

# 07 여러가지 이산확률분포

**3.6 Chebysev inequality**

체비셰프의 부등식.
이름은 들어봤지만, 제대로 보는 것이 처음이라는 게 상당히 유감스럽습니다.
학부때 확률론을 계속해서 피해다녔더니, 이제서야 보게 되었습니다.

그런데, 아주 재미있는 부등식인 것 같습니다.
확률변수 $X$와 양의 실수 $a$에 대하여

$$
P\left(|X-E[X]|\ge a\right)\le\frac{\,{\sigma_X}^2}{a^2}
$$

입니다.
$X$가 평균으로부터 어느 정도의 간격($a$) 이상 떨어져있을 확률은 그 간격에 의존하는 어떤 값$\left(\frac{\,{\sigma_X}^2}{a^2}\right)$보다 작다는 뜻입니다.

예를 들어 $a=2\sigma_X$인 경우에 있어서의 Chebysev inequality는 $X$가 2-sigma 바깥에 있을 확률이 $\frac14$보다 작다는 것을 의미합니다.

이 부등식이 아주 tight한 것 같지는 않습니다.
만약, $X$가 정규분포를 따른다면, $a=2\sigma_X$에 대한 확률은

$$
\begin{align*}
P\left(|X-E[X]|\ge a\right)
&=P\left(|X-E[X]|\ge2\sigma_X\right)\\
&=P\left(|Z|\ge2\right)\\
&=2\left(1-P\left(0\le Z\le2\right)\right)\\
&=2(0.5-0.47725)\\
&=0.0455
\end{align*}
$$

입니다([표준정규분포표](https://ko.wikipedia.org/wiki/%ED%91%9C%EC%A4%80%EC%A0%95%EA%B7%9C%EB%B6%84%ED%8F%AC%ED%91%9C)의 값을 활용했습니다.)
그러니까, Chevysev inequailty를 통해 얻는 확률의 upper bound는 0.25였는데, 실제 확률의 값은 0.0455입니다.
따라서 이 경우는 Chevysev inequality의 결과를 (당연히) 만족시키기는 합니다.
근데 그 결과라는 게 실제값보다는 너무 크다는 것입니다.
그런 의미에서 Chevysev inequality는 어떤 확률에 대한 일반적인 upper bound를 제시하는 것이라고 이해해야 할 것 같습니다.

연속확률변수에 대한 Chevysev inequality는, ${\sigma_X}^2$을 들여다보면 쉽게 증명됩니다.

$$
\begin{align*}
{\sigma_X}^2
&=\int_{-\infty}^\infty\left(x-E[X]\right)^2f_X(x)\,dx\\
&=\int_{|x-E[X]|\ge a}\left(x-E[X]\right)^2f_X(x)\,dx
+\int_{|x-E[X]|\lt a}\left(x-E[X]\right)^2f_X(x)\,dx\\
&\ge a^2\int_{|x-E[X]|\ge a}f_X(x)\,dx\\
&=a^2P\left(|x-E[X]|\ge a\right)
\end{align*}\\
$$

강의에서, 이산확률변수에 대한 증명은 조금 tricky할 수 있다고 했는데, 그래도 한 번 해보면

$$
\begin{align*}
{\sigma_X}^2
&=\sum_{i=1}^n\left(x_i-E[X]\right)^2P_X(x_i)\\
&=\sum_{|x_i-E[X]|\ge a}\left(x_i-E[X]\right)^2P_X(x_i)
+\sum_{|x_i-E[X]|\lt a}\left(x_i-E[X]\right)^2P_X(x_i)\\
&\ge a^2\sum_{|x_i-E[X]|\ge a}P_X(x_i)\\
&=a^2P\left(|x-E[X]|\ge a\right)
\end{align*}\\
$$

입니다.
(되는데?)
"expectation 값이 random variable이 아닐 수도 있다"는 말씀이 무슨 의미인지 잘 모르겠습니다.
[이 사람](https://zhengtianyu.wordpress.com/2014/01/04/proof-of-chebyshevs-inequality/)은 제가 한 것과 똑같은 증명을 적어놓았고, [wikipedia](https://en.wikipedia.org/wiki/Chebyshev%27s_inequality)에는 conditional expectation의 성질을 사용하여 (그러니까 summation이나 integral을 사용하지 않고) 증명했습니다.

**Chapter 4. special distributions**

**4.2 Bernoulli distribution**

'Bernoulli'는 '베르누이'라고 보통 쓰기도 하지만, 원래 발음은 '[베르눌리](https://www.youtube.com/watch?v=n6czlFpvaf4)'라고 읽는 것이 맞는 것 같습니다.
마찬가지로 Poisson은 '[푸아상](https://youtu.be/43eJq-pAOGA)'으로 발음하는 것이 맞는 것 같습니다.

강의에서는 *$X$가 binary인 경우*를 bernoulli distribution이라고 한다고 되어 있습니다.
앞서 말했듯 $X$는 $X:S\to\mathbb R$입니다.
여기서 binary라는 것은 $|S|=2$라는 의미인 것 같습니다.
물론 $|X(S)|=2$도 성립할 것입니다.
($|X(S)|=1$인 경우는 의미가 없으니까)
다시말해 sample space가

$$S=\{w_1,w_2\}$$

인 경우를 Bernoulli distribution이라고 합니다.
이때의 $X$의 값은 어떻게든 정해도 됩니다.
예를 들어

$$
\begin{cases}
X(w_1)=-2\\
X(w_2)=3
\end{cases}
$$

로 정의해도 이것은 Bernoulli distribution에 해당할 것 같습니다.
하지만, [통상](https://en.wikipedia.org/wiki/Bernoulli_distribution)

$$
\begin{cases}
X(w_1)=1\\
X(w_2)=0
\end{cases}
$$

인 경우를 가정합니다.

$P_X(X=1)=p$라고 하면 $P_X(X=0)=1-p$이고, 따라서 Bernoulli distribution은 오로지 하나의 값 $p$에 의해 결정되는 분포입니다.
기록을 위해 PMF를 다시 써보면

$$
P_X(x)=
\begin{cases}
p &(x=1)\\
1-p &(x=0)
\end{cases}
$$

인데 이것을 다음과 같이 한 줄로 쓸 수 있습니다.
(조금 쓸데없어보이기도 하고, 그냥 현학적인 표현인 것처럼 보이기도 하지만, 많은 경우에 Bernoulli distribution이 이와 같이 표현되니 알아두어도 나쁘지는 않을 것 같습니다.)
덧셈의 형태로

$$
P_X(x)=(1-p)(1-x)+px
$$

와 같이 쓸 수도 있고, 아니면 곱셈의 형태로

$$
P_X(x)=p^x(1-p)^{1-x}
$$

와 같이 쓸 수도 있습니다.

Beroulli 분포는 가장 간단한 형태의 분포이므로 (그보다 더 간단한 형태는 $P_X(x)$가 상수함수인 경우겠지만, 그 경우는 확률적으로 이야기하는 것 자체가 의미가 없습니다.) 평균과 분산도 아주 쉽게 계산됩니다.

$$
\begin{align*}
E[X]
&=0\times P_X(0)+1\times P_X(1)\\
&=0\times(1-p)+1\times p\\
&=p\\
{\sigma_X}^2
&=(0-E[X])^2\times P_X(0)+(1-E[X])^2\times P_X(1)\\
&=(0-p)^2\times(1-p)+(1-p)^2\times p\\
&=p(1-p)\left(p+(1-p)\right)\\
&=p(1-p)
\end{align*}
$$

**4.3 binomial distribution**

아까, $|S|=2$ 인 경우를 생각했었는데 이와 같은 시행을 Bernoulli trial이라고 부르는 것 같습니다.
[다음](https://en.wikipedia.org/wiki/Bernoulli_trial)은 위키피디아의 정의입니다.

A Bernoulli trial (or binomial trial) is a random experiment with exactly two possible outcomes, "success" and "failure", in which the probability of success is the same every time the experiment is conducted.

이런 Bernoulli trial을 $n$번 시행했을 때, sucess의 횟수 (혹은 $S=\\{s_1,s_2\\}의 관점에서는 $s_1$의 횟수)를 확률변수 $X$라고 정의할 때, 이때 $X$의 분포를 이항분포(binomial distribution)라고 합니다.

이항분포의 PMF는 당연히

$$P_X(x)=\binom nxp^x(1-p)^{n-x}\qquad(x=0,1,\cdots,n)$$

이고 이것은 다 더했을 때 1입니다;

$$
\begin{align*}
\sum_{x=1}^nP_X(x)
&=
\sum_{x=1}^n\binom nxp^x(1-p)^{n-x}\\
&=\left(p+(1-p)\right)^n\\
&=1
\end{align*}
$$

이항분포의 평균과 분산이 각각 $np$, $np(1-p)$이라는 것은 1.10.4에서 증명했습니다.
그 때에는 $(1+x)^n$을 미분하여 얻을 수 있는 성질로부터 증명했었습니다.
강의에서는 표준적인 방법 (combination의 성질)으로서 증명하고 있는데, 여기에는 생략하겠습니다.

**4.4 geometric distribution**

geometric distribution에 대해서는 이미 3.13에서 보았고, 평균과 분산도 계산했었습니다.

$$
\begin{align*}
P_K(k)&=(1-p)^{k-1}p\quad(k=1,2,\cdots)\\
E[K]&=\frac1p\\
{\sigma_X}^2&=\frac{1-p}{p^2}
\end{align*}
$$

geometric distribution을 Bernoulli trial의 입장에서 이것을 다시 해석해보면

the number of Bernoulli trial until the first success
{: .text-center}

입니다.
그러니까 앞서의 정의와 비슷한데 이번에는 완전히 정확하게 적혔습니다.

**forgetfulness(memorylessness)** 라는 개념은 geometric distribution에서 빈번히 생각될 수 있는 개념인 것 같습니다.
이것은 여러 번의 Bernoulli trial에서 앞서의 결과가 이후의 결과에 영향을 미치지 않는다는 뜻으로 [일종의 Markov property입니다](https://en.wikipedia.org/wiki/Memorylessness).

Consider $k$ additional trials until the first success, given $n$ trials fail. (강의의 칠판에 적힌 표현)

Consider the probability that a success is achieved at $k$ additional trials, given $n$ trials fail. (다시 적어본 표현)

그러니까, 어떤 Bernoulli trial을 여러 번 시행하는데 처음 $n$번은 모두 실패했다는 가정 하에 그 다음 $k$번째에 성공(그러니까, $1,\cdots,k-1$번째에는 모두 실패) 할 수 있는 확률을 계산해보려고 합니다.
그리고 이 확률이 (처음 $n$번이 모두 실패했다는 가정 없이) $k$번째에 성공할 수 있는 확률과 같은지를 보려고 합니다.

$$
\begin{align*}
P\left(X=n+k|X>n\right)
&=\frac{P\left((X=n+k)\cap(X>n)\right)}{P(X>n)}\\[10pt]
&=\frac{P\left(X=n+k\right)}{P(X>n)}\\[15pt]
&=\frac{(1-p)^{n+k-1}p}{\sum_{x\ge n+1}(1-p)^{x-1}p}\\[15pt]
&=\frac{(1-p)^{n+k-1}}{\sum_{x\ge n+1}(1-p)^{x-1}}\\[15pt]
&=\frac{(1-p)^{n+k-1}}{\frac{(1-p)^n}{1-(1-p)}}\\[15pt]
&=(1-p)^{k-1}p\\
&=P\left(X=k\right)
\end{align*}
$$

그리고 위의 계산결과에서 보듯, 정말로 그것이 성립합니다.
즉, 지금 하는 것은 독립시행이므로, 앞서의 결과가 이후의 시행에 영향을 미치지 않는 것이 당연한데, 그 사실을 다시 한 번 확인해보았습니다.

# 08 지수분포와 어랑분포

**4.7 Poisson distribution**

$$
\begin{align*}
P_K(k)&=\frac{\lambda^k}{k!}e^{-\lambda}\qquad(k=0,1,2,\cdots)\\
E[X]&=\lambda\\
{\sigma_K}^2&=\lambda
\end{align*}
$$

$K$ : the number of Bernoulli success in a time interal.

위의 간단한 정의는 칠판에 적힌 표현입니다.
([wikipedia](https://en.wikipedia.org/wiki/Poisson_distribution))에는 다음과 같이 적혀있습니다.

>The Poisson distribution is a discrete probability distribution that expresses the probability of a given number of events occurring in a fixed interval of time or space if these events occur with a known constant mean rate and independently of the time since the last event.
>
>For instance, a call center receives an average of 180 calls per hour, 24 hours a day. The calls are independent; receiving one does not change the probability of when the next one will arrive. The number of calls received during any minute has a Poisson probability distribution with mean 3: the most likely numbers are 2 and 3 but 1 and 4 are also likely and there is a small probability of it being as low as zero and a very small probability it could be 10.
>
>Another example is the number of decay events that occur from a radioactive source during a defined observation period.

Poisson 분포의 저 식이 도대체 무슨 의미가 있는지를 몰라서 여러가지로 알아보다가, 아주 재미있는 결과를 발견했습니다.
나중에 이 강의에서 다룰 지도 모르겠지만 먼저 적어보면, binomial PMF인

$$f_X(k)=\binom nkp^k(1-p)^{n-k}$$

에서 $n$을 무한대로 보내면, Poisson PMF의 모양이 된다는 것입니다.

$$
\lim_{n\to\infty}\binom nkp^k(1-p)^{n-k}=
\frac{\lambda^k}{k!}e^{-\lambda}
$$

단, $\lambda$는 $p=\frac\lambda n$으로 주어집니다.
이에 대한 [증명](https://math.stackexchange.com/q/3125971)은 어렵지 않은데


$$
\begin{align*}
\lim_{n\to\infty}\binom nkp^k(1-p)^{n-k}
=&\lim_{n\to\infty}\frac{n(n-1)(n-2)\cdots(n-k+1)}{k!}\left(\frac\lambda n\right)^k\left(1-\frac\lambda n\right)^{n-k}\\
=&\lim_{n\to\infty}\frac{n(n-1)(n-2)\cdots(n-k+1)}{n^k}\frac{\lambda^k}{k!}\left(1-\frac\lambda n\right)^{n-k}\\
=&\frac{\lambda^k}{k!}
\lim_{n\to\infty}\frac{n-1}n
\times\lim_{n\to\infty}\frac{n-2}n
\times\cdots
\times\lim_{n\to\infty}\frac{n-k+1}n
\times\lim_{n\to\infty}
\left(1-\frac\lambda n\right)^{n-k}\\
=&\frac{\lambda^k}{k!}\lim_{n\to\infty}\left(1-\frac\lambda n\right)^{n-k}\\
=&\frac{\lambda^k}{k!}
\lim_{n\to\infty}\left(1-\frac\lambda n\right)^n
\lim_{n\to\infty}\left(1-\frac\lambda n\right)^{-k}\\
=&\frac{\lambda^k}{k!}
\lim_{n\to\infty}\left(\left(1-\frac\lambda n\right)^{-\frac n\lambda}\right)^{-\lambda}\times1\\
=&\frac{\lambda^k}{k!}
\left(\lim_{n\to\infty}\left(1-\frac\lambda n\right)^{-\frac n\lambda}\right)^{-\lambda}\\
=&\frac{\lambda^k}{k!}e^{-\lambda}
\end{align*}
$$

이기 때문입니다.

추가적으로, [DeGroot, Probability and Statistics, 4ed](https://www.amazon.com/Probability-Statistics-4th-Morris-DeGroot/dp/0321500466)의 Example 5.4.1, 5.4.2를 읽어봤습니다.
설명이 잘 되어 있어서, 그 내용을 토대로 Poisson distribution의 의미를 적어보면 다음과 같습니다.

어떤 가게에 손님이 한 시간에 4.5명 꼴로 들어옵니다.
그럴 때에, 어느 날의 어느 시각으로부터 한 시간동안 들어온 손님의 수를 $X$라고 하면, $X$의 분포를 어떻게 이해하면 좋을지 생각해볼 수 있습니다.
답은 $\lambda=4.5$로 하는 Poisson distribution입니다.
이유는 다음과 같습니다.

위 문제를 풀기 위해 할 수 있는 자연스러운 방법은, 한 시간을 작은 시간단위로 쪼개는 것입니다.
예를 들어 1초 단위로 쪼개본다고 하겠습니다(1시간 = 3600초).
어느 날의 어느 시각(예를 들어 오후 1시)으로부터 한 시간동안이라고 하면 오후 2시까지입니다.
그 시간을
- 1시 00분 00초 ~ 1시 00분 01초 : $T_1$
- 1시 00분 01초 ~ 1시 00분 02초 : $T_2$

$\qquad\vdots$
- 1시 59분 59초 ~ 2시 00분 00초 : $T_{3600}$

의 3600개 시간간격으로 나눌 수 있는 것입니다.
한편, 1시간에 4.5명 꼴로 손님이 들어온다고 했으니까, 1초에 $4.5/3600=0.00125$명 꼴로 손님이 들어옵니다.
그러니까 각각의 $T_i$ 동안 0.00125명 꼴로 손님이 들어옵니다.
그러면, $T_i$ 동안 손님이 들어오는 횟수는 거의 0입니다. 어쩌다가 한 번 들어오는 것이고 두 명 이상 들어올 가능성은 거의 없습니다.
(실제로는 친구나 가족과 함께 방문할 수도 있으므로 현재로서는 이 가정이 좋은 가정은 아닐테지만, 어쨌든 수치상으로는 그렇습니다.)
그러니까 각각의 $T_i$에 대하여 손님이 들어오지 않거나(0명), 아니면 들어오거나(1명) 한다고 *가정*할 수 있습니다.
즉, 한 번의 시행에서 나오는 결과값이 0 아니면 1인 Bernoulli trial이고 이때 $p=0.00125$입니다.
그런데 이런 시행이 한 번 있는 것이 아니라 3600번 있습니다.
그리고 각각의 시행들이 독립적일테니까, 한 시간동안 들어온 손님의 수가 $x$인 확률이

$$
P(X=x)=\binom{3600}x(0.00125)^x(0.99875)^{3600-x}\tag{$\ast$}
$$

입니다.
즉, $X$는 $B(3600, 0.00125)$인 이항분포를 따릅니다.

그런데 한 시간을 1초 단위로 자른 것은, 그냥 1초가 익숙해서 그렇게 한 것이지 어떤 특별한 의미가 있는 것은 아닙니다.
예를 들어 0.1초로 자를 수도 있습니다.
그 경우에는 총 36000개의 시간간격이 존재할 것이고 $X$는 $B(36000,0.000125)$를 따를 것이며

$$
P(X=x)=\binom{36000}x(0.000125)^x(0.999875)^{36000-x}\tag{$\ast\ast$}
$$

이 될 것입니다.
그리고 이 때에는 아까의 *가정*(하나의 시간간격동안 2명 이상 들어오지 않는다는 가정)이 더 그럴듯하게 성립할 것이므로 $(\ast\ast)$의 분포는 $(\ast)$의 분포보다 더 괜찮은 (현상을 잘 반영하는) 분포일 것입니다.
심지어는, 아무리 친구 두 명이서 함께 가게를 방문한다고 하더라도, 두 명의 사람이 가게에 들어오는 시각에는 차이가 있을 것이므로 시간간격을 충분히 줄이면 이 *가정*은 항상 성립한다고 말할 수도 있을 것입니다.
그래서 3600, 36000이었던 값을 양의 무한대로 보내버리고, 아까의 계산결과를 적용하면

$$
P(X=x)
=\lim_{n\to\infty}
\binom nx\left(\frac{4.5}n\right)^x\left(1-\frac{4.5}n\right)^{n-x}
=\frac{4.5^x}{x!}e^{-4.5}
$$

이 되는데 이것은 $\lambda=4.5$인 Poisson PMF입니다.
$\square$

**4.8 exponential distribution**

$$
\begin{align*}
f_X(x)&=\lambda e^{-\lambda x}\qquad(x\ge0)\\
E[X]&=\frac1\lambda\\
{\sigma_K}^2&=\frac1{\lambda^2}
\end{align*}
$$

(Poisson distribution에서 그랬던 것처럼 이번에도 이 분포의 의미를 열심히 살펴보는 것은 의미있는 일일 것 같습니다.
하지만, 시간관계상 생략하고, 강의의 내용을 먼저 따라가려고 합니다.
나중에 한번 다 끝나고 나면, (Stirling's formula의 유도도 포함하여) 그때 다시 고민해보려 합니다.)

강의에서는 geometric distribution과 exponential distribution은 각각 선형대수에서의 difference equation/differential equation (차분방정식/미분방정식)과 연관이 있다고 설명합니다.

선형대수의 해당 개념들에 대해서는 [G. Strang, Linear Algebra and Its Applications, 4ed](https://a.co/d/5l0YO6H)의 5.3과 5.4에 그 설명이 잘 적혀있습니다. 5.3의 첫 절 정도만 읽어봤는데, 거기에서는 피보나치 수열의 일반식을 difference equation을 통해 얻어내고 있습니다.
그 과정에서 정사각행렬의 거듭제곱이 등장하는데, 이를 간단하게 하기 위해서 (당연히) 행렬의 대각화를 사용합니다.
(최근에 대각화에 대해 [정리]({{ site.url }}/mathematics/diagonalization/)해본 적이 있어서 이해하기가 편했습니다.)
그 결과로, 피보나치 수열의 일반식에는 어떤 숫자(=eigenvalues)의 거듭제곱이 수반됩니다 ;

$$
\begin{align*}
u_k&=c_1{\lambda_1}^kx_1+c_2{\lambda_2}^kx_2\\
F_k&=c_1{\lambda_1}^k+c_2{\lambda_2}^k
\end{align*}
$$

이러한 형태가 difference equation 말고도 differential equation(system of linear partial differential equations)에서도 나타나는 것은 주지의 사실입니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_8-1.png){: .img-100-center}

한편, 지난 강의에서 geometric distribution에서의 memorylessness에 대해 말했었는데, exponential distribution에서도 마찬가지로 memoryless property가 성립한다는 내용이 강의에 이어집니다.
확인할 내용은 다음과 같습니다.

expoential distribution은 어떤 시스템의 (혹은 어떤 상태의) 생존(survival, success)에 관한 문제와 관련있습니다.
어떤 시스템이 $t$라는 시점까지 생존했다는 가정 하에 그 이후 $s$만큼의 시간까지 생존할 확률을 계산할 건데, 그 확률이 ($t$라는 시점까지 생존했다는 가정 없이 그냥) $s$만큼의 시간만큼 생존할 확률과 같다는 것을 보려고 합니다.

계산에 앞서 expoential distribution에 대한 CDF를 먼저 계산해보면

$$
\begin{align*}
F_X(x)
&=\int_0^xf_X(\tilde x)\,d\tilde x\\
&=\int_0^x\lambda e^{-\lambda\tilde x}\,d\tilde x\\
&=1-e^{\lambda x}
\end{align*}
$$

입니다.
계산해보면

$$
\begin{align*}
P\left(X\le t+s|X>t\right)
&=\frac{P\left((X\le t+s)\cap(X>t)\right)}{P(X>t)}\\
&=\frac{P\left(t<X\le t+s\right)}{1-P(X\le t)}\\
&=\frac{F_X(t+s)-F_X(t)}{1-F_X(t)}\\
&=\frac{e^{\lambda t}-e^{\lambda(t+s)}}{e^{-\lambda t}}\\
&=1-e^{\lambda s}\\
&=F_X(s)\\
&=P(X\le s)
\end{align*}
$$

인 것입니다.

**relation between ED and PD**

여기에서 ED는 exponential distribution, PD는 poisson distribution입니다.
ED는 연속확률변수로서 '(생존)시간'과 관련이 있었고 PD는 이산확률변수로서 주어진 시간구간 동안의 '발생횟수'와 관련이 있었습니다.

For a Poisson distribution with $\lambda$ per unit time,

$$P_X(x) = \frac{\lambda^x}{x!}e^{-\lambda}.\qquad(x=0,1,2,\cdots)$$

Transforming 'unit time' to 'time interval $t$' yields
($1\to t$, $\lambda\to\lambda t$)

$$P_X(x) = \frac{\lambda^xt^x}{x!}e^{-\lambda t}.\qquad(x=0,1,2,\cdots)$$

한글로 다시 쓰면, 원래 PD식(첫번째 식)에서 $X$가 단위시간(길이가 1인 시간간격)동안 특정 사건이 발생한 횟수이었는데, 이번에는 길이가 $t$인 시간간격 동안 특정 사건이 발생할 횟수를 $X$로 정한 것입니다.
그리고 그 때의 PMF가 두번째 식처럼 나옵니다.

그러면, 길이가 $t$인 시간간격동안 한번도 사건이 발생하지 않을 확률 $P(\text{no event})$은

$$P(\text{no event})=P_X(0)=e^{-\lambda t}$$

이고 길이가 $t$인 시간간격동안 적어도 한 번 사건이 발생할 확률 $P(\text{at least one event})$는

$$P(\text{at least one event})=1-P_X(0)=1-e^{-\lambda t}$$

이것은 ED의 CDF에 $t$를 넣은 모양과 완전히 일치합니다.

그러니까, PD를 해석할 때 어떤 event를 상정했었습니다.
그 event의 예시를 '상점에서 손님이 들어오는 것'으로 해석했었지만, event가 어떤 종류의 것이었어도 상관없었습니다.
event의 의미를 '죽는 것', 그러니까 '생존에 실패하는 것'으로 둔다면, 그리고 PD의 단위시간간격을 '길이 $t$의 시간간격'으로 바꾼다면,

$$
\begin{align*}
P^{\text{poisson, $t$}}(X\ne0)
&=P^{\text{exponential}}(X\le t)\\
\text{$t$ 시간간격 안에 실패가 한 번도 발생하지 않을 확률}
&=\text{$t$ 시간 동안 생존할 확률}
\end{align*}
$$

인 것입니다.
여기서 좌변과 우변의 $X$는 서로 다른 종류의 확률변수입니다.
즉, 좌변의 $X$는 길이가 $t$인 시간간격 동안 '실패'가 발생할 횟수이고, 우변의 $X$는 생존시간, 즉 '실패'가 처음으로 발생한 시각을 뜻합니다.

다시 정리하면, 특정 시점에 일어날 수 있는 어떤 사건에 대하여

- 사건 사이의 시간간격은 exponential distribution을 따르고
- 일정한 시간간격 동안 사건이 일어난 횟수는 Poisson distribution을 따른다

고 할 수 있습니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_8-2.png){: .img-50-center}

그러니까, exponential distribution을 따르는 어떤 확률변수 $T$를 '사건 사이의 시간간격'이라고 해석하면, 특정 시간간격을 상정한 다음 그 시간간격 동안 해당 사건이 일어난 횟수를 확률변수 $X$라고 정할 때 $X$는 Poisson distribution을 따릅니다.

반대로, Poisson distribution을 따르는 어떤 확률변수 $X$를 '일정한 시간간격 동안 사건이 일어날 횟수'로 해석한다면, 그 사건이 일어나는 시간 간격을 확률변수 $T$로 정할 떄 $T$는 exponential distribution을 따릅니다.

**4.9 Erlang distribution**

Erlang distribution (of $k$) is a generalization of expoential distribution.

어떤 사건이 발생하는 간격은 exponetial distribution을 따른다고 했었습니다.
즉, 시각 $T_1$에 처음 사건이 발생하고 그 다음 사건이 시각 $T_2$에 두번째 사건이 발생했다면 $T_2-T_1$은 exponential distribution을 따릅니다.
다시 말해, exponential distribution은 한 개의 사건발생간격을 고려합니다.

$k=2$인 Erlang distribution은 두 개의 사건발생간격을 고려합니다.
시각 $T_1$에 처음 사건이 발생하고 그 다음 사건이 시각 $T_2$에 발생하며, 또 그 다음 사건이 시각 $T_3$에 발생하면, $T_3-T_1$이 따르르는 분포가 $k=2$인 Erlang distribution입니다.

(물론, $T_2-T_1$ 말고도 $T_3-T_2$, $T_4-T_3$도 exponential distribution을 따릅니다.
마찬가지로 $T_3-T_1$ 말고도 $T_4-T_2$, $T_5-T_3$도 $k=2$인 Erlang distribution을 따릅니다.)

그 연장선상에서 보면 $T_4-T_1$은 $k=3$인 Erlang distribution을, $T_5-T_1$은 $k=4$인 Erlang distribution을 따른다고 말할 수 있습니다.

이제 $k$-order Erlang distribution(혹은 Erlang-$k$ distribution)의 정의를 보면

$$
f_{X_k}(x)=\frac{\lambda^kx^{k-1}}{(k-1)!}e^{-\lambda x}\qquad x\ge0
\tag{$\ast$}
$$

**gamma function**

Erlang distribution의 계산을 돕기 위해 gamma function을 다음과 같이 정의합니다.

$$
\Gamma(k)=\int_0^\infty x^{k-1}e^{-x}\,dx\tag{$\ast\ast$}
$$

특별히 $k$가 자연수일 때 $\Gamma(k)$는 순열(팩토리얼)의 형태가 됩니다;

$$
\Gamma(k)=(k-1)!\qquad(k=1,2,\cdots)\tag{$\ast\ast\ast$}
$$

이것은 $k$에 대한 귀납법으로 쉽게 증명될 수 있습니다.
$k=1$이면

$$
\begin{align*}
\Gamma(1)
&=\int_0^\infty e^{-x}\,dx\\
&=\left[-e^{-x}\right]_0^\infty\\
&=1-0\\
&=0!
\end{align*}
$$

입니다.
$k-1$인 경우의 $(\ast\ast\ast)$이 성립한다고 가정하면, 즉, $\Gamma(k-1)=(k-2)!$을 가정하면 부분적분에 의해

$$
\begin{align*}
\Gamma(k)
&=\int_0^\infty x^{k-1}e^{-x}\,dx\\
&=\left[-x^{k-1}e^{-x}\right]_0^\infty+\int_0^\infty (k-1)x^{k-2}e^{-x}\,dx\\
&=(0-0)+(k-1)\Gamma(k-1)\\
&=(k-1)(k-2)!\\
&=(k-1)!
\end{align*}
$$

이 됩니다.
$\square$

gamma function의 정의 ($\ast\ast$)에서 $k$는 양의 정수(자연수)로 둘 수도 있고 양의 실수로 둘 수도 있습니다.
심지어는 실수부분이 양수인 복소수로 둘 수 있다고 합니다.
([출처 : wikipedia](https://en.wikipedia.org/wiki/Gamma_function))
그런 의미에서, gamma function은 팩토리얼의 개념을 일반화한 것이라고 볼 수 있습니다.
예를 들어,

$\frac12!$을 어떻게 정의할까?
{: .text-center}

하는 질문에 $\frac12!=\Gamma(\frac12)$ 로 정의해볼 수 있는 것입니다.

이제, Erlang distribution에 관한 $(\ast)$ 식이 정말로 PDF의 역할을 하는 지 살펴보기 위해 계산해보면

$$
\begin{align*}
\int_0^\infty f_{X_k}(x)\,dx
&=\int_0^\infty\frac{\lambda^kx^{k-1}}{(k-1)!}e^{-\lambda x}\,dx\\
&=\frac{\lambda^k}{(k-1)!}\int_0^\infty x^{k-1}e^{-\lambda x}\,dx\\
&=\frac{\lambda^k}{(k-1)!}\int_0^\infty
(\lambda x)^{k-1}\cdot\frac1{\lambda^{k-1}}e^{-\lambda x}\frac1{\lambda}\,d(\lambda x)\\
&=\frac1{(k-1)!}\int_0^\infty u^{k-1}e^{-u}\,du\\
&=\frac1{(k-1)!}\Gamma(k)\\
&=1
\end{align*}
$$

입니다.
평균을 계산해보면

$$
\begin{align*}
E[X]
&=\int_0^\infty x\cdot\frac{\lambda^kx^{k-1}}{(k-1)!}e^{-\lambda x}\,dx\\
&=\frac{\lambda^k}{(k-1)!}\underline{\int_0^\infty x^ke^{-\lambda x}\,dx}\\
&=\frac{\lambda^k}{(k-1)!}\left(
    \left[-\frac{x^{k-1}}\lambda e^{-\lambda x}\right]_0^\infty
    +\frac k{\lambda}\int_0^\infty x^{k-1}e^{-\lambda x}\,dx\right)\\
&=\frac{\lambda^k}{(k-1)!}\left(0+\frac k{\lambda^{k+1}}
\int_0^\infty(\lambda x)^{k-1}e^{-\lambda x}\,d(\lambda x)\right)\\
&=\frac{\lambda^k}{(k-1)!}\times\frac k{\lambda^{k+1}}
\int_0^\infty u^{k-1}e^{-u}\,du\\
&=\frac{\lambda^k}{(k-1)!}\times
\underline{\frac k{\lambda^{k+1}}\times\Gamma(k)}\\
&=\frac k{\lambda}
\end{align*}
$$

이고 분산을 계산하기 위해 $E[X^2]$를 계산해보면

$$
\begin{align*}
E[X^2]
&=\int_0^\infty x^2\cdot\frac{\lambda^kx^{k-1}}{(k-1)!}e^{-\lambda x}\,dx\\
&=\frac{\lambda^k}{(k-1)!}\int_0^\infty x^{k+1}e^{-\lambda x}\,dx\\
&=\frac{\lambda^k}{(k-1)!}\left(
    \left[-\frac{x^{k+1}}{\lambda}e^{-\lambda x}\right]_0^\infty
    +\frac{k+1}\lambda\int_0^\infty x^ke^{-\lambda x}\,dx\right)\\
&=\frac{\lambda^k}{(k-1)!}\times\frac{k+1}\lambda\times\frac k{\lambda^{k+1}}\times\Gamma(k)\\
&=\frac{k(k+1)}{\lambda^2}
\end{align*}
$$

입니다.
계산과정의 세번째 줄에서 네번째 줄로 넘어가는 것은 $E[X]$의 계산에서 밑줄친 두 값이 같다는 것을 활용한 것입니다.
분산을 계산하면

$${\sigma_{X_k}}^2=E[X^2]-E[X]^2=\frac k{\lambda^2}$$

이 됩니다.

이 결과들을 exponential distribution의 평균과 분산과의 관계와 연결지어 해석해보면 다음과 같습니다.
어떤 사건이 시각 $T_0$ $T_1$, $T_2$, $T_3$, $\cdots$, $T_k$에 일어난다고 가정할 때, $T_1-T_0$, $T_2-T_1$, $\cdots$, $T_k-T_{k-1}$은 모두 exponential distribution을 따른다고 했습니다.
반면, $T_2-T_0$, $T_3-T_1$, $\cdots$, $T_k-T_{k-2}$는 Erlang-$2$ distribution을 따릅니다.
마찬가지로, $T_3-T_0$, $T_4-T_1$, $\cdots$, $T_k-T_{k-3}$는 Erlang-$3$ distribution을 따릅니다.
그리고 $T_k-T_0$는 Erlang-$k$ distribution을 따른다고 했습니다.

그러면, exponential distribution을 따르는 두 확률분포를 더하면 그것은 Erlang-$2$ distribution을 따른다고 볼 수 있습니다;

$$(T_1-T_0)+(T_2-T_1)=T_2-T_0$$

그리고, exponential distribution을 따르는 $k$개의 확률분포를 더하면 그것은 Erlang-$k$ distribution을 따른다고 볼 수 있습니다;

$$(T_1-T_0)+(T_2-T_1)+\cdots+(T_k-T_{k-1})=T_k-T_0$$

만약, exponential distribution을 따르는 각각의 확률변수들을
 
$$
T_1-T_0=X^{(1)},\quad
T_2-T_1=X^{(2)},\quad
\cdots,\quad
T_k-T_{k-1}=X^{(k)}
$$

으로 표기하고 $X_k=T_k-T_0$이라고 하면,

$$X^{(1)}+X^{(2)}+\cdots+X^{(k)}=X_k$$

인 것입니다.
따라서

$$
\begin{align*}
E[X_k]
&=E\left[X^{(1)}+X^{(2)}+\cdots+X^{(k)}\right]\\
&\stackrel{\star}=E[X^{(1)}]+E[X^{(2)}]+\cdots+E[X^{(k)}]\\
&=\frac1\lambda+\frac1\lambda+\cdots+\frac1\lambda\\
&=\frac k\lambda.
\end{align*}
$$

라고 생각할 수 있습니다.
이것은 아까 계산한 Erlang-$k$ distribution의 평균과 정확히 일치합니다.
여기에서 $(\star)$의 과정은 직관적으로는 당연하지만, 엄밀하게는 아직 논할 수 없습니다.
그리고 '각 사건의 발생이 독립적이다'와 같은 가정이 있어야 저 과정이 정당화될 수 있을 것입니다.

강의에서는 나중에 convolution의 개념을 배우고 나서 저 $(\star)$ 과정을 제대로 설명할 수 있다고 말합니다.
그런데 정말로 그런 것이, 만약 $X^{(i)}$들이 0과 자연수의 값을 가진다고 가정하고(discrete) $X_2=T_2-T_0=X^{(1)}+X^{(2)}$의 PMF를 $X^{(1)}$의 PMF와 $X^{(2)}$의 PMF로 구하려고 한다면

$$
\begin{align*}
P_{X_2}(x)
&=P(X_2=x)\\
&=P(X^{(1)}+X^{(2)}=x)\\
&=P\left((X^{(1)}=0)\cap(X^{(2)}=x)\right)
+P\left((X^{(1)}=1)\cap(X^{(2)}=x-1)\right)
+\cdots
+P\left((X^{(1)}=x)\cap(X^{(2)}=0)\right)\\
&=\sum_{i=1}^xP\left((X^{(1)}=i)\cap(X^{(2)}=x-i)\right)\\
&=\sum_{i=1}^xP(X^{(1)}=i)\times P(X^{(2)}=x-i)\\
&=\sum_{i=1}^xP_{X^{(1)}}(i)\times P_{X^{(2)}}(x-i)\\
\end{align*}
$$

와 같은 꼴이 되어, $P_{X_2}$가 $P_{X^{(1)}}$와 $P_{X^{(1)}}$의 convolution 형태로 나타나기 떄문인 것 같습니다.
(exponential distribution과 Erlang distribution의 원래 정의에서처럼 PDF로 계산하는 경우에는 summation이 아닌 적분과 관련된 식으로 convolution 식이 나옵니다.)

분산에 대해서도 비슷한 해석을 할 수 있다고 하는데, 사실 강의에서의 설명은 잘 이해하지는 못했습니다.
하지만, 다음과 같이 해석하면 되지 않을까 싶습니다.
$X^{(1)}$, $X^{(2)}$, $\cdots$, $X^{(k)}$가 모두 평균 $\mu$를 가지고 분산 $\sigma^2$를 가지는 동일한 분포를 따를 때, 이것들의 산술평균인 $\overline X = \frac1k(X^{(1)}+\cdots+X^{(k)})$는 평균이 $\mu$이고 분산이 $\frac{\sigma^2}k$임이 알려져있습니다. (표본평균의 평균과 분산)
그러니까,

$$
\begin{align*}
\sigma_{X_k}
&=V[X_k]\\
&=V[X^{(1)}+X^{(2)}+\cdots X^{(k)}]\\
&=V[k\overline X]\\
&=k^2V[\overline X]\\
&=k^2\times\frac{\sigma^2}k\\
&=k\sigma^2\\
&=kV[X^{(1)}]\\
&=\frac{k}{\lambda^2}
\end{align*}
$$

이 되어 앞서 계산의 결과와 일치합니다.

마지막으로, $X_k$의 CDF를 계산해봅니다.
이 계산은 gamma function을 직접적으로 사용할 수 없습니다.
wikipedia 등에 따르면 위에서 정의한 gamma function에서 더 나아간
[incomplete gamma function](https://en.wikipedia.org/wiki/Incomplete_gamma_function)
과 같은 함수를 사용하면 $X_k$의 CDF를 계산하는 것이 더 쉬워지는 것으로 보이는데, 여기에서는 그냥 부분적분과 귀납법을 사용해 계산하겠습니다.
실제 강의에서도 부분적분을 연속적으로 사용하여 계산할 수 있다고 말씀하고 계십니다.

$$
\begin{align*}
F_{X_k}(x)
&=\int_0^xf_{X_k}(t)\,dt\\
&=\int_0^x\frac{\lambda^kt^{k-1}}{(k-1)!}e^{-\lambda t}\,dt\\
&=\frac{\lambda^k}{(k-1)!}\int_0^xt^{k-1}e^{-\lambda t}\,dt\\
&=\frac1{(k-1)!}\int_0^{\lambda x}(\lambda t)^{k-1}e^{-\lambda t}\,d(\lambda t)\\
&=\frac1{(k-1)!}\int_0^{\lambda x}u^{k-1}e^{-u}\,du\\
&\stackrel{\star\star}=1-\sum_{n=0}^{k-1}\frac{(\lambda x)^n}{n!}e^{-\lambda x}
\end{align*}
$$

$\star\star$를 수학적 귀납법으로 증명하겠습니다.
$k=1$인 경우는

$$
\begin{align*}
\text{LHS}
&=\frac1{0!}\int_0^{\lambda x}u^0e^{-u}\,du\\
&=\left[-e^{-u}\right]_0^{\lambda x}\\
&=1-e^{-\lambda x}\\
&=1-\sum_{n=0}^0\frac{(\lambda x)^n}{n!}e^{-\lambda x}\\
&=\text{RHS}
\end{align*}
$$

가 되어 성립합니다.
$k$의 경우를 성립한다고 가정하고 $k+1$인 경우를 고려하면

$$
\begin{align*}
\text{LHS}
&=\frac1{k!}\int_0^{\lambda x}u^ke^{-u}\,du\\
&=\frac1{k!}\left(\left[-u^ke^{-u}\right]_0^{\lambda x}
+k\int_0^{\lambda x}u^{k-1}e^{-u}\,du\right)\\
&=-\frac1{k!}(\lambda x)^ke^{-\lambda x}
+\frac1{(k-1)!}\int_0^{\lambda x}u^{k-1}e^{-u}\,du\\
&=-\frac{(\lambda x)^k}{k!}e^{-\lambda x}
+1-\sum_{n=0}^{k-1}\frac{(\lambda x)^n}{n!}e^{-\lambda x}\\
&=1-\sum_{n=0}^k\frac{(\lambda x)^n}{n!}e^{-\lambda x}\\
&=\text{RHS}
\end{align*}
$$

**4.10 uniform distribution**

uniform distribution에 대해서도 이미 다룬 바가 있지만, PMF와 PDF, 평균과 분산에 대해 다시 봅니다.

$X$가 uniform한 이산확률분포이고 $X$가 가질 수 있는 값이 $x_1$, $x_2$, $\cdots$, $x_n$이면 $P(X=x_1)=P(X=x_2)=\cdots=P(X=x_n)$인데, 따라서

$$
P_X(x_i)=\frac1n\qquad(i=1,2,\cdots,n)
$$

로 $X$의 PMF가 결정됩니다.
만약 $X$가 uniform한 연속확률분포이고 $X$가 가질 수 있는 값이 $a\le X\le b$이면

$$f_X(x)=c(a\le x\le b)$$

이고

$$\int_a^bf_X(x)\,dx=1$$

로부터

$$f_X(x)=\frac1{b-a}(a\le x\le b)$$

입니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_8-3.png){: .img-50-center}

이산확률분포의 경우 $E[X]=\frac1n(x_1+\cdots+x_n)$, ${\sigma_X}^2=\frac1n\left((x_i-E[X])^2\right)$이어서 사실 새로울 게 없습니다.
연속확률 변수의 경우의 평균과 분산은 $E[X]=\frac{a+b}2$, ${\sigma_X}^2=\frac{(a-b)^2}{12}$로 주어지는데, 직접 계산해보면

$$
\begin{align*}
E[X]
&=\int_a^bxf_X(x)\,dx\\
&=\frac 1{b-a}\int_a^bx\,dx\\
&=\frac{a+b}2\\
{\sigma_X}^2
&=\int_a^bx^2f_X(x)\,dx-E[X]^2\\
&=\frac 1{b-a}\int_a^bx^2\,dx-\left(\frac{a+b}2\right)^2\\
&=\frac{a^2+ab+b^2}3-\frac{a^2+2ab+b^2}4\\
&=\frac{a^2-2ab+b^2}{12}\\
&=\frac{(a-b)^2}{12}
\end{align*}
$$

입니다.
강의의 마지막에는 앞서 언급된 적이 있었던 digitization에서의 quantization에 대한 설명이 다시 나옵니다.
quantization에서의 level 사이의 간격을 $\Delta$라고 할 때, quantization error $e$는

$$-\frac\Delta2\lt e\le\frac\Delta2$$

와 같이 주어질텐데, 이때 $e$가 $[-\frac\Delta2,\frac\Delta2]$에서의 uniform distribution을 따른다고 가정한다는 것입니다.
그러면 $e$의 분산은

$$V[e]=\frac{\Delta^2}{12}$$

으로 나타나게 될 것입니다.
이때, error의 분산은 전력(power, 평균 에너지의 크기)로 해석할 수 있다고 합니다.
신호의 실제값들의 표준편차를 $\sigma_S$라고 하면,

$$
\log_{10}\left(\frac{\,{\sigma_S}^2}{\left(\frac\Delta{12}\right)^2}\right)
$$

은 [SNR](https://en.wikipedia.org/wiki/Signal-to-noise_ratio)([신호 대 잡음비](https://ko.wikipedia.org/wiki/%EC%8B%A0%ED%98%B8_%EB%8C%80_%EC%9E%A1%EC%9D%8C%EB%B9%84))의 값으로 정의할 수 있는데, 이 값은 db(데시벨)이라는 단위를 가지고 있다고 합니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_8-4.png){: .img-100-center}

# 09 정규분포

연속확률변수 $X$가 확률밀도함수

$$\tag{$\ast$}
f_X(x)=\frac1{\sqrt{2\pi}\sigma_X}e^{-\frac{(x-{\mu_X})^2}{2{\sigma_X}^2}}
\qquad(-\infty\lt x\lt\infty)
$$

를 가지면 $X$가 정규분포를 따른다고 하고 $X\sim N(\mu_X,{\sigma_X}^2)$라고 표시합니다.
이 PDF에 대하여 다음 세 사실이 성립합니다.

$$\tag{$\ast\ast$}
\begin{align*}
\int_{-\infty}^\infty f_X(x)\,dx&=1\\
E[X]&=\mu_X\\
V[X]&={\sigma_X}^2
\end{align*}
$$

이것을 직접 증명하는 것은 복잡하기 때문에, $\mu=0$이고 $\sigma=1$인 경우를 보려고 합니다.
다시 말해, 확률변수 $U$가 확률밀도함수

$$
f_U(u)=\frac1{\sqrt{2\pi}}e^{-\frac12u^2}
\qquad(-\infty\lt x\lt\infty)
$$

로 주어진 연속확률변수 $U$에 대하여

$$
\begin{align*}
\int_{-\infty}^\infty f_U(u)\,du&=1\\
E[U]&=0\\
V[U]&=1
\end{align*}
$$

를 증명하려고 합니다.
그리고 나서 $X=\sigma_X U+\mu_X$로 $X$를 정의하면
$X$의 확률밀도함수는 $(\ast)$를 만족시키고, $(\ast\ast)$의 세 성질이 성립합니다.

먼저 $U$의 확률밀도함수를 실수 전체에 대해 적분했을 때 1이 된다는 사실을 먼저 증명하기 위해

$$
A=\int_{-\infty}^\infty f_U(u)\,du
$$

로 두면, 극좌표계 변환에 의해

$$
\begin{align*}
A^2
&=\int_{-\infty}^\infty\frac1{\sqrt{2\pi}}e^{-\frac12u^2}\,du\times
\int_{-\infty}^\infty\frac1{\sqrt{2\pi}}e^{-\frac12v^2}\,dv\\
&=\frac1{2\pi}\iint e^{-\frac12(u^2+v^2)}\,du\,dv\\
&=\frac1{2\pi}\int_0^{2\pi}\int_{-\infty}^\infty
e^{-\frac12r^2}r\,dr\,d\theta\\
&=\frac1{2\pi}\int_0^{2\pi}d\theta\times
\int_{-\infty}^\infty
e^{-\frac12r^2}r\,dr\\
&=\frac1{2\pi}\times 2\pi\times\int_0^\infty
e^{-\frac12r^2}\,d\left(\frac12r^2\right)\\
&=\int_0^\infty e^{-R}\,dR\\
&=\left[-e^R\right]_0^\infty\\
&=1
\end{align*}
$$

입니다.
따라서 $A=1$입니다.

$U$의 평균을 계산하기 위해 똑같이 해보면

$$
\begin{align*}
E[U]^2
&=\int_{-\infty}^\infty\frac u{\sqrt{2\pi}}e^{-\frac12u^2}\,du\times
\int_{-\infty}^\infty\frac v{\sqrt{2\pi}}e^{-\frac12v^2}\,dv\\
&=\frac1{2\pi}\iint uve^{-\frac12(u^2+v^2)}\,du\,dv\\
&=\frac1{2\pi}\int_0^{2\pi}\int_{-\infty}^\infty
r^2\cos\theta\sin\theta e^{-\frac12r^2}r\,dr\,d\theta\\
&=\frac1{2\pi}\int_0^{2\pi}\cos\theta\sin\theta\,d\theta\times
\int_{-\infty}^\infty r^3e^{-\frac12r^2}r\,dr\\
&=\frac1{2\pi}\int_0^{2\pi}\frac12\sin(2\theta)\,d\theta
\times\int_0^\infty
\left(\frac12r^2\right)e^{-\frac12r^2}\,d\left(\frac12r^2\right)\times2\\
&=\frac1{2\pi}\times\left[-\frac14\cos(2\theta)\right]_0^{2\pi}\times
\int_0^\infty Re^{-R}\,dR\times2\\
&=\frac1{2\pi}\times0\times1\times2\\
&=0
\end{align*}
$$

입니다.
따라서 $E[U]=0$입니다.

마지막으로 $U$의 분산을 계산해보면

$$
\begin{align*}
V[U]
&=\int_{-\infty}^\infty\frac{(u-0)^2}{\sqrt{2\pi}}e^{-\frac12u^2}\,du\\
&=\int_{-\infty}^\infty\frac{u^2}{\sqrt{2\pi}}e^{-\frac12u^2}\,du
\end{align*}
$$

이고

$$
\begin{align*}
V[U]^2
&=\int_{-\infty}^\infty\frac{u^2}{\sqrt{2\pi}}e^{-\frac12u^2}\,du\times
\int_{-\infty}^\infty\frac{v^2}{\sqrt{2\pi}}e^{-\frac12v^2}\,dv\\
&=\frac1{2\pi}\iint u^2v^2e^{-\frac12(u^2+v^2)}\,du\,dv\\
&=\frac1{2\pi}\int_0^{2\pi}\int_{-\infty}^\infty
r^4\cos^2\theta\sin^2\theta e^{-\frac12r^2}r\,dr\,d\theta\\
&=\frac1{2\pi}\int_0^{2\pi}\cos^2\theta\sin^2\theta\,d\theta\times
\int_{-\infty}^\infty r^5e^{-\frac12r^2}r\,dr\\
&=\frac1{2\pi}\int_0^{2\pi}\frac14\sin^2(2\theta)\,d\theta
\times\int_0^\infty
\left(\frac12r^2\right)^2e^{-\frac12r^2}\,d\left(\frac12r^2\right)\times4\\
&=\frac1{2\pi}\int_0^{2\pi}\frac18(1-\cos(4\theta))\,d\theta\times
\int_0^\infty R^2e^{-R}\,dR\times4\\
&=\frac1{2\pi}\times\frac\pi4\times2\times4\\
&=1
\end{align*}
$$

따라서 $(\ast\ast)$의 세 성질이 성립합니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_9-1.png){: .img-100-center}

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_9-2.png){: .img-100-center}

강의에서는 연속확률변수들이 대개 정규분포를 따른다는 것이 언급되면서, 특히 어떤 신호의 signal이 정규분포를 따르는 경향이 있다는 사실도 소개됩니다.
single mode, symmetric, bellshaped등의 성질들에 대해서도 언급됩니다.

여기에서 mode란 PDF의 극대점을 의미한다고 설명되고 있습니다.
discrete case에서는 mode가 최빈값, 즉 PMF의 최대점을 의미합니다.

강의에서 위의 계산도 하는 것 같은데, $du\,dv=r\,dr\,d\theta$를 설명하기 위해 Jacobian matrix도 소개되고 있습니다.
다만 위에서 계산한 세 값 중 맨 위의 값만 계산하고 있습니다.

이외에도 표준졍규분포, 표준정규분포표에 대해서도 소개되고 있습니다.
이때 $\Phi$를 표준정규분포의 CDF로 정합니다 ;

$$\Phi(x)=F_Z(x)=P(Z\le x)=\int_{-\infty}^x\frac1{\sqrt{2\pi}}e^{-\frac{z^2}2}$$

**approximation of binomial distributions**

$X\sim B(n,p)$이고 $n$이 충분히 크면 $X\sim N(np,np(1-p))$ 입니다.

**error function**

$$\text{erf}(x)=\frac2{\sqrt\pi}\int_0^xe^{-y^2}\,dy.$$

$X\sim N(0,\frac12)$이면, 이 함수는 $\text{er}f(x)=P(-x\lt X\le x)$인 함수입니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_9-2.png){: .img-50-center}

**complementary error function**

$$\text{erfc}(x)=\frac2{\sqrt\pi}\int_x^\infty e^{-y^2}\,dy.$$

\text{erfc} 함수는 \text{erf} 함수와 complementary한 관계가 있습니다.
다시 말해서

$$\text{erf}(x)+\text{erfc}(x)=1$$

입니다.

또한, $X\sim N(0,\frac12)$, $Z\sim N(0,1)$, $\text{erf}(x)=P(-x\le X\le x)$, $\Phi(x)=P(Z\le x)$이므로

$$
\begin{align*}
\text{erf}(x)
&=2P(0\le X\le x)\\
&=2P\left(0\le Z\le\sqrt2x\right)\\
&=2\left(\Phi(\sqrt2x)-\frac12\right)\\
&=2\Phi(\sqrt2x)-1
\end{align*}
$$

이고, 반대로

$$\Phi(x)=\frac12+\frac12\text{erf}\left(\frac{x}{\sqrt2}\right)$$

입니다.

**Gaussian mixture model**

$X_1\sim N(\mu_1,{\sigma_1}^2)$, $X_2\sim N(\mu_2,{\sigma_2}^2)$일 때,새로운 확률변수 $\alpha X_1+\beta X_2$는 하나의 mode를 가지지 않고 두 개의 mode를 가질 수 있습니다.
일반적으로, 서로 다른 정규분포를 따르는 $n$개의 확률변수 $X_i$에 대하여 $X_i$들의 일차결합은 여러 개의 mode를 가질 수 있습니다(multimodal).
이 확률변수를 가지고 만들 수 있는 모델을 Gaussian mixture model이라고 하는 것 같습니다. [`sklearn`](https://scikit-learn.org/stable/modules/mixture.html)에서는 다음과 같은 설명을 하고 있습니다.

> A Gaussian mixture model is a probabilistic model that assumes all the data points are generated from a mixture of a finite number of Gaussian distributions with unknown parameters.
<!-- > One can think of mixture models as generalizing k-means clustering to incorporate information about the covariance structure of the data as well as the centers of the latent Gaussians. -->

**4.5 Pascal distribution (Negative binomial distribution)**

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_9-3.png){: .img-75-center}

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_9-4.png){: .img-50-center}

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_9-5.png){: .img-50-center}

# 10 다중변수 및 연합분포

이번 강의에서는 단일변수에 대한 분포가 아닌 다중변수에 대한 분포를 다룹니다.
단일변수에 대한 정의를 다시 떠올려보면, 원래 확률공간(probability space)이란, $(S,\Sigma,P)$이었습니다.
$S$는 sample space로 그냥 하나의 집합이었고 $\Sigma$는 $\sigma$-algebra로서 $S$의 부분집합(사건)들의 집합 중에서 특정한 성질을 만족시키는 것들이었으며 $P:\Sigma\to[0,1]$는 probability measure로서 전사건에 대한 값이 1인 finite measure입니다.
그러니까, $P(A)$라고 할 때, $A$는 $S$의 부분집합, 즉 '사건'입니다.
그런데, 집합에 대한 함수를 다루기보다는 숫자에 대한 함수를 다루기 위해 확률변수라는 걸 도입하게 됩니다.
확률변수란, $X:S\to\mathbb R$인 함수 $x=X(w)$로 정의됩니다.
이를 통해

$$P(X=x)=p(x)=P_X(x)$$

와 같은 표현을 ($P_X$는 확률질량함수, PMF)

$$P(X=x)=P\left(\{w\in S:X(w)=x\}\right)=P\left(X^{-1}(\{x\})\right)$$

로 정의하고

$$P(a\le X\le b)=\int_a^bf_X(x)\,dx$$

와 같은 표현을 ($f_X$는 확률밀도함수, PDF)

$$P(a\le X\le b)=P\left(\{w\in S:a\le X(w)\le b\}\right)=P\left(X^{-1}([a,b])\right)$$

로 정의하면 두 식 $P(X=x)$, $P(a\le X\le b)$은 잘 정의됩니다.
실제 강의에서는 $\sigma$-algebra라든지 probability measure에 대한 설명은 없이 진행됐습니다.

이번 강의에서는 두 확률변수 $X$, $Y$에 대하여

$$P(X=x, Y=y)$$

라든지

$$P(X\le x, Y\le y)$$

를 어떻게 정의할지 하는 문제를 다룹니다.

두 확률변수 $X:S_1\to\mathbb R$, $Y:S_2\to\mathbb R$를 고려한다고 해서 이 둘의 Cartesian product를 확률변수로 놓을 수는 없습니다.
$X\times Y:S_1\times S_2\to\mathbb R^2$을 $(X\times Y)(w_1,w_2)=(X(w_1),Y(w_2))$로 정의한다고 하면 이것은 공역이 $\mathbb R^2$이므로 확률변수라고 할 수 없기 때문입니다.
하지만, 순서쌍 $(X(w_1),Y(w_2))$에 대한 분포는 생각해볼 수 있습니다.

<!-- 다시 말해, 단일확률변수 $X$에 대한 distribution이라고 하면 그 확률변수 $X$에 대한 PMF나 PDF, CDF를 뜻하는 것으로 확률변수 자체보다는 확률변수의 값 $X(w)$에 의존해 결정될 수 있는 것들이었습니다.
두 확률변수 $X$, $Y$에 대한 distribution 역시 확률변수들의 값 $(X(w_1),Y(w_2))$에 의존해 결정될 수 있습니다. -->

위에 언급한 값들을

$$
\begin{align*}
P(X=x,Y=y)
&=P\left(\left\{(w_1,w_2)\in S_1\times S_2:X(w_1)=x,Y(w_2)=y\right\}\right)\\
&=P\left(X^{-1}(\{x\})\times Y^{-1}(\{y\})\right)\\
P(X\le x,Y\le y)
&=P\left(\left\{(w_1,w_2)\in S_1\times S_2:X(w_1)\le x,Y(w_2)\le y\right\}\right)\\
&=P\left(X^{-1}(-\infty,x]\times Y^{-1}(-\infty,y]\right)\\
\end{align*}
$$

로 정의하면 이것들은 잘 정의됩니다.
그러니까, $X^{-1}(\\{x\\})\times Y^{-1}(\\{y\\})\subset S_1\times S_2$이고, $X^{-1}(-\infty,x]\times Y^{-1}(-\infty,y]\subset S_1\times S_2$ 입니다.
사실은 각각의 집합들이 $S_1\times S_2$의 $\sigma$-algebra의 원소인지 하는 것도 봐야 더 정확하겠지만, 아래과 같은 [언급](math.stackexchange.com/q/22042)에 따르면 $S_1\times S_2$에 대한 $\sigma$-algebra를 $\Sigma_1\times\Sigma_2$로 generate해서 만들어내면 문제가 되지 않는 것 같습니다;

> The sigma-algebra on $E$ is generated by all products of the form $A_1\times\cdots\times A_n$, where $A_i$ is measurable in $E_i$ for each $i$.

이제 강의의 내용들을 따라서 써보겠습니다.

**Chapter 5. Multiple Random Variables**

**5.2 joint CDF of bivarirate random variables**

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_10-1.png){: .img-50-center}

예를 들어. 동전과 주사위를 각각 하나씩 던져서 나오는 결과를 본다고 하면,

$$
\begin{align*}
X(H)&=1\\
X(T)&=0
\end{align*}
$$

로 정의되는 확률변수 $X:\\{H,T\\}\to\mathbb R$와

$$
\begin{align*}
Y(1)&=1\\
Y(2)&=2\\
Y(3)&=3\\
Y(4)&=4\\
Y(5)&=5\\
Y(6)&=6
\end{align*}
$$

로 정의되는 확률변수 $Y:\\{1,2,3,4,5,6\\}\to\mathbb R$를 생각하게 됩니다.
이때, $X$, $Y$의 joint PMF는

$$
P(X=x,Y=y)=P\left(\{(w_1,w_2)\in S_1\times S_2:X(w_1)=x,Y(w_2)=y\}\right)
$$

로 정의할 수 있습니다.
(단, $S_1=\\{H,T\\}$, $S_2=\\{1,2,3,4,5,6\\}$)
예를 들어,

$$
\begin{align*}
P(X=0,Y=2)
&=P\left(\{(w_1,w_2)\in S_1\times S_2:X(w_1)=0,Y(w_2)=2\}\right)\\
&=P\left(\{(T,2)\}\right)\\
&=\frac1{12}
\end{align*}
$$

입니다.

방금 계산한 것은 joint distribution에서의 PMF에 해당하는 것입니다.
그런데 $X$와 $Y$ 중 하나라도 연속확률변수이면 PMF를 정의하는 건 어려운 문제가 됩니다.
반면, CDF는 연속확률변수나 이산확률변수 모두에 대해 잘 정의됩니다.
그러니, joint PMF와 joint PDF를 정의하기 전에 joint CDF의 정의를 먼저 보겠습니다.
joint CDF는

$$F_{XY}(x,y)=P(X\le x, Y\le y)$$

와 같이 정의됩니다. 그리고 다음 성질들을 만족시킵니다.

$$
\begin{align*}
(1)~
&0\le F_{XY}(x,y)\le 1\\
(2)~
&F_{XY}(x_1,y_1)\le F_{XY}(x_1,y_2)\qquad(x_1\lt x_2,\:\:y_1\lt y_2)\\
&F_{XY}(x_1,y_1)\le F_{XY}(x_2,y_1)\\
(3)~
&\lim_{\substack{x\to\infty \\y\to\infty}}F_{XY}(x,y)=1\\
(4)~
&\lim_{x\to-\infty}F_{XY}(x,y)=0\\
&\lim_{y\to-\infty}F_{XY}(x,y)=0\\
(5)~
&P(x_1\lt X\le x_2,Y\le y)=F_{XY}(x_2,y)-F_{XY}(x_1,y)\\
(6)~
&P(x_1\lt X\le x_2,y_1\lt Y\le y_2)
=F_{XY}(x_2,y_2)-F_{XY}(x_1,y_2)-F_{XY}(x_2,y_1)+F_{XY}(x_1,y_1)\\
\end{align*}
$$

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_10-2.png){: .img-50-center}

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_10-3.png){: .img-50-center}

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_10-4.png){: .img-50-center}

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_10-5.png){: .img-50-center}


**ex. 5.1**

$$
\begin{align*}
P(X\gt x,Y\gt y)
&=1-P(X\le x\text{ or }Y\le y)\\
&=1-\left(P(X\le x)+P(Y\le y)-P(X\le x, Y\le y)\right)\\
&=1-P(X\le x)-P(Y\le y)+P(X\le x, Y\le y)\\
&=1-F_X(x)-F_Y(y)+F_{XY}(x,y)\\
\end{align*}
$$

위 계산에서 한 변수에 대해서의 CDF인 $F_X(x)$가 등장했습니다.
이와 같이, 두 변수에 대한 확률분포에서 특별히 한 변수에 대한 분포를 생각할때, 그 분포를 marginal distribution이라고 합니다.
이때, marginal CDF와 joint CDF 사이에는 다음과 같은 관계가 성립합니다.

$$
\begin{align*}
F_X(a)&=\lim_{y\to\infty}F_{XY}(a,y)\\
F_Y(b)&=\lim_{x\to\infty}F_{XY}(x,b)
\end{align*}
$$

로 이해될 수 있습니다.

**5.3 discrete joint distributions**

이산확률변수 $X$, $Y$에 대하여 $X$와 $Y$의 joint distribution에 대한 PMF는

$$P_{XY}(x,y)=P(X=x,Y=y)$$

로 정의됩니다.
joint PMF는 다음 성질들을 만족시킵니다.

$$
\begin{align*}
(1)~
&0\le P_{XY}(x,y)\le1\\
(2)~
&\sum_x\sum_yP_X(x,y)=1\\
(3)~
&F_{XY}(x,y)=P(X\le x,Y\le y)=\sum_{\tilde x\le x}\sum_{\tilde y\le y}P_{XY}(\tilde x,\tilde y)\\
(4)~
&P_X(x)=\sum_y P_{XY}(x,y)\qquad(\text{marginalization})\\
&P_Y(y)=\sum_x P_{XY}(x,y)\\
(5)~
&P_{XY}(x,y)=P_X(x)P_Y(y)\qquad(X,Y:\text{independent})
\end{align*}
$$

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_10-6.png){: .img-50-center}

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_10-7.png){: .img-50-center}

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_10-8.png){: .img-50-center}

위의 성질들은 모두 당연해 보이므로 따로 증명하지 않겠습니다.
다만, (5)는 아직 이해할 수도 없고 증명할 수도 없습니다.
아직까지는 두 사건의 독립이라는 개념만 소개했지, 두 확률변수의 독립에 대해서는 정의한 바가 없기 때문입니다.
두 확률변수의 독립에 관해서는 12강에서 잠깐 소개하게 되는데(43분 경), 사실 이산확률변수와 연속확률변수에 대한 (5)번 항목은 두 확률변수가 독립인 것의 정의로 둘 수 있습니다.

**5.4 continuous joint distributions**

연속확률변수 $X$의 PDF는 CDF의 도함수로서 정의했었습니다.
$X$의 conditional PDF도 conditional CDF의 도함수로서 정의했습니다.
마찬가지로, 두 연속확률변수 $X$, $Y$에 대하여 $X$와 $Y$의 joint PDF를 정의하기 위해서는 일단 joint CDF를 먼저 정의해야 합니다.
joint CDF는

$F_{XY}(x,y)=P(X\le x,Y\le y)$

와 같이 정의됩니다.
연속확률변수 $X$에 대하여 $P(X=x)$의 값을 정하는 것의 의미가 없었습니다.
변수가 두 개일 때에도 $P(X=x,Y=y)$는 0으로 정할 수밖에 없고, 그건 큰 의미가 있지 않습니다.
그래서 joint PDF $f_{XY}(x,y)$를

$$
\begin{align*}
f_{XY}(x,y)
&=\lim_{\substack{\Delta x\to0+\\\Delta y\to0+}}\frac{P\left(x<X\le x+\Delta x,y<X\le y+\Delta y\right)}{\Delta x\Delta y}\\
&=\lim_{\substack{\Delta x\to0+\\\Delta y\to0+}}
\frac{F_{XY}(x+\Delta x,y+\Delta y)-F_{XY}(x+\Delta x,y)-F_{XY}(x,y+\Delta y)+F_{XY}(x,y)}{\Delta x\Delta y}\\
&=\lim_{\Delta x\to0+}\frac1{\Delta x}\lim_{\Delta y\to0+}
\frac{F_{XY}(x+\Delta x,y+\Delta y)-F_{XY}(x+\Delta x,y)-F_{XY}(x,y+\Delta y)+F_{XY}(x,y)}{\Delta y}\\
&=\lim_{\Delta x\to0+}\frac1{\Delta x}\left(
\lim_{\Delta y\to0+}\frac{F_{XY}(x+\Delta x,y+\Delta y)-F_{XY}(x+\Delta x,y)}{\Delta y}-
\lim_{\Delta y\to0+}\frac{F_{XY}(x,y+\Delta y)-F_{XY}(x,y)}{\Delta y}
\right)\\
&=\lim_{\Delta x\to0+}\frac1{\Delta x}\left(
\frac{F_{XY}}{\partial y}(x+\Delta x,y)
-\frac{F_{XY}}{\partial y}(x,y)\right)\\
&=\frac{\partial}{\partial x}\frac{\partial}{\partial y}F_{XY}(x,y)\\
&=\frac{\partial^2}{\partial x\partial y}F_{XY}(x,y)
\end{align*}
$$

로 정의합니다.
이 함수는 $F_{XY}$가 충분히 좋은 함수이면 (e.g. 연속함수) 잘 정의됩니다.

joint PDF는 다음 성질들을 만족시킵니다.

$$
\begin{align*}
(1)~
&f_{XY}(x,y)\ge0\\
(2)~
&\iint_{\mathbb R^2}f_{XY}(x,y)\,dx\,dy=1
=\lim_{\substack{x\to\infty\\y\to\infty}}F_{XY}(x,y)\\
(3)~
&\int_{y_1}^{y_2}\int_{x_1}^{x_2}f_{XY}(x,y)\,dx\,dy=P\left(x_1\lt X\le x_2,~~y_1\lt Y\le y_2\right)\\
&=F_{XY}(x_2,y_2)-F_{XY}(x_1,y_2)-F_{XY}(x_2,y_1)+F_{XY}(x_1,y_1)\\
(4)~
&f_X(x)=\int_{-\infty}^\infty f_{XY}(x,y)\,dy\qquad(\text{marginalization})\\
&f_Y(y)=\int_{-\infty}^\infty f_{XY}(x,y)\,dx\\
(5)~
&f_{XY}(x,y)=f_X(x)f_Y(y)\qquad(X,Y:\text{independent})
\end{align*}
$$

이번에도 (1)-(4)는 당연합니다.
그리고 (5)는 나중에 증명해보겠습니다.

# 11 연합확률밀도함수와 조건부확률밀도함수

**ex. 5.6**

두 확률변수에 대하여 joint PDF가

$$
f_{XY}(x,y)=2e^{-x-y}\qquad(0\le x\le y,\quad 0\le y)
$$

로 주어지는 경우에 대하여 앞서 강의에서의 성질들이 성립하는지 살펴보겠습니다.
이 함수의 정의역을 $R$로 두면

$$R=\{(x,y)\in\mathbb R^2:0\le x\le y, 0\le y\}$$

이고 이것은

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_11-1.png){: .img-75-center}

와 같은 영역을 의미합니다.
먼저  (2)번 성질($\iint_R f_{XY}(x,y)\,dx\,dy=1$)을 보겠습니다.
이중적분의 순서에 따라 다음의 두 가지 방법으로 계산될 수 있습니다.

$$
\begin{align*}
\iint_R f_{XY}(x,y)\,dx\,dy
&\stackrel{(a)}=\int_0^\infty\int_0^yf_{XY}(x,y)\,dx\,dy\\
&=\int_0^\infty\int_0^y2e^{-x-y}\,dx\,dy\\
&=\int_0^\infty\left[-2e^{-x-y}\right]_{x=0}^{x=y}\,dy\\
&=\int_0^\infty2e^{-y}-2e^{-2y}\,dy\\
&=\left[e^{-2y}-2e^{-y}\right]_0^\infty\\
&=0-(1-2)\\
&=1\\
\iint_R f_{XY}(x,y)\,dx\,dy
&\stackrel{(b)}=\int_0^\infty\int_x^\infty f_{XY}(x,y)\,dx\,dy\\
&=\int_0^\infty\int_x^\infty2e^{-x-y}\,dy\,dx\\
&=\int_0^\infty\left[-2e^{-x-y}\right]_{y=x}^{y=\infty}\,dx\\
&=\int_0^\infty2e^{-2x}\,dx\\
&=\left[-e^{-2x}\right]_0^\infty\\
&=1
\end{align*}
$$

이때,

$$
\begin{align*}
f_X(x)
&=\int_x^\infty f_{XY}(x,y)\,dy\\
f_Y(x)
&=\int_0^y f_{XY}(x,y)\,dx\\
\end{align*}
$$

이므로, marginal PDF인 $f_X(x)$와 $f_Y(y)$는 (b)와 (a)의 계산 과정에서 구해진 셈입니다(4).
다시 말해,

$$
\begin{align*}
f_X(x)
&=2e^{-y}-2e^{-2y}\\
f_Y(x)
&=2e^{-2x}\\
\end{align*}
$$

입니다.
따라서

$$
f_{X,Y}(x,y)\ne f_X(x)f_Y(y)
$$

이고, $X$와 $Y$는 독립이 아닙니다(5).

**ex. 5.7?**

다음으로

$$
f_{XY}(x,y)=\frac1{\pi r^2}\qquad(x^2+y^2\le1)
$$

와 같이 joint PDF가 주어지는 경우입니다.
다시 말해, 단위원 내부에서 분포가 uniform distribution으로 주어지는 경우입니다.
이 함수의 정의역은

$$D=\{(x,y)\in\mathbb R^2:x^2+y^2\le1\}$$

이고 이것은

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_11-2.png){: .img-75-center}

와 같은 영역을 의미합니다.
이번에는 (2)번 성질이 당연합니다;

$$
\begin{align*}
\iint_D f_{XY}(x,y)\,dx\,dy
&=\iint_D\frac1{\pi r^2}\,dx\,dy\\
&=\frac1{\pi r^2}\iint_D\,dx\,dy\\
&=\frac1{\pi r^2}\times\pi r^2\\
&=1
\end{align*}
$$

이 계산은, 아까처럼 $dx\,dy$ 혹은 $dy\,dx$로 해도 잘 풀립니다.
또한 $r\,dr\,d\theta$로 풀어도 잘 계산됩니다.
marginal PDF를 계산해보면

$$
\begin{align*}
f_X(x)
&=\int_{-\sqrt{r^2-x^2}}^{\sqrt{r^2-x^2}}f_{XY}(x,y)\,dy\\
&=\int_{-\sqrt{r^2-x^2}}^{\sqrt{r^2-x^2}}\frac1{\pi r^2}\,dy\\
&=\frac{2\sqrt{r^2-x^2}}{\pi r^2}
\end{align*}
$$

이고, 마찬가지로

$$
f_Y(y)=\frac{2\sqrt{r^2-y^2}}{\pi r^2}
$$

입니다(4).
따라서

$$
f_{X,Y}(x,y)\ne f_X(x)f_Y(y)
$$

이고, 이번에도 $X$와 $Y$는 독립이 아닙니다(5).

**5.6 conditional distribution**

다음 개념인 conditional distribution으로 넘어가기 전에, 지금까지 학습한 개념들을 정리해보겠습니다.

$$
\begin{matrix}
\text{CDF(03)}&\text{PMF(03)}&\text{PDF(04)}&\text{exp.}(05)&\text{var.}(05)\\
\text{con. CDF(06)}&\text{con. PMF(06)}&\text{con. PDF(06)}&\text{con. exp.}(06)\\
\text{jnt. CDF(10)}&\text{jnt. PMF(10)}&\text{jnt. PDF(10)}\\
\end{matrix}
$$

여기에서 괄호 안의 숫자는 강의의 회차를 의미하고, exp.는 expectation, var.은 variance, con.은 conditional, jnt.는 joint를 의미합니다.

그러니까 conditional expectation에 대해서는 다루지 않았습니다.
joint expectation과 joint variance의 개념은 생각할 수 없습니다.
joint distribution에 대해서는 어떤 실수값을 가지는 확률변수를 생각할 수 없었기 때문입니다.
하지만, 여러 개의 확률변수들에 특정한 함수가 주어졌을 때의 expectation은 계산할 수 있습니다.
또 variance를 정의하는 대신 covariance를 계산하게 됩니다.

여하튼, 지금 단원에서 공부하는 것은 conditional distribution이지만, 06회차 강의에서 다루었던 일반적인 conditional distribution말고, 두 확률변수에 대해 생각할 때의 conditional distribution을 공부합니다.

$$
\begin{matrix}
\text{con2. CDF(11)}&\text{con2. PMF(11)}&\text{con2. PDF(11)}&\text{con2. exp.(11)}&\text{con2. var.(11)}
\end{matrix}
$$

이전 강의들에서

$$
\begin{align*}
P(A|B)
&=\frac{P(A\cap B)}{P(B)}
&&\text{(conditional probability with respect to events(01))}\\
P(X\le x|X\le a)
&=\frac{P\left((X\le x)\cap(X\le a)\right)}{P(X\le a)}
&&\text{(conditional probability with respect to a RV(06))}
\end{align*}
$$

와 같은 것들을 공부했습니다.

두 이산확률변수 $X$와 $Y$에 대하여 조건부 확률질량함수(conditional PMF)에 해당하는 함수 $P_{Y|X}$를

$$
\begin{align*}
P_{Y|X}(x,y)
&=P(Y=y|X=x)\\
&=\frac{P_{XY}(x,y)}{P_X(x)}
\end{align*}
$$

와 같이 정의합니다.

(설명을 자세히 적지 않고 캡쳐로 대체했지만) 이전 강의(10)에서 나왔던 예를 다시 살펴보겠습니다.
동전을 세 개 던질 때, $X$를

첫번째 동전이 앞면이면 1, 뒷면이면 0
{: .text-center}

으로 정하고 $Y$를

세 동전 중 앞면의 개수
{: .text-center}

로 정할 때 $X$, $Y$의 joint distribution이

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_11-3.png){: .img-75-center}

와 같이 나옴을 확인했었습니다.

이때,

$$
P_{Y|X}(1|0)=\frac{P_{XY}(0,1)}{P_X(0)}=\frac{\frac28}{\frac18+\frac28+\frac18}=\frac12
$$

입니다.

이번에는 $X$, $Y$가 연속확률변수인 경우를 살펴봅니다.
이전과 마찬가지로 CDF에서부터 출발합니다.
이때, conditional CDF는

$$
F_{Y|X}(y|x)=P(Y\le y|X=x)
$$

의 의미입니다.
($X$가 $x$로 주어져 있을 때, $Y$의 CDF입니다.)
그런데

$$
F_{Y|X}(y|x)=\frac{P(X=x,Y\le y)}{P(X=x)}
$$

와 같이 정의할 수는 없습니다.
왜냐하면 분모가 0이 될 가능성이 있기 때문입니다.
그러니까, 지금까지 CDF, (일반적인) conditional CDF, joint CDF가 별 문제 없이 정의되었던 것과는 조금 다릅니다.
위와 같은 정의 대신에, $y$를 포함하는 infinitesimal한 구간 $x\lt X\le x+\Delta x$를 고려하여

$$
F_{Y|X}(y|x)\approx\frac{P(x\lt X\le x+\Delta x,Y\le y)}{P(x\lt X\le x+\Delta x)}
$$

와 같이 생각할 수 있습니다.
그리고 우변에 $\Delta x\to0+$인 극한을 취해주어, 그 극한값을 $F_{Y|X}(y|x)$로 정해주는 것이 합리적입니다.
그러면

$$
\begin{align*}
F_{Y|X}(x,y)
&=\lim_{\Delta x\to0+}\frac{P(x\lt X\le x+\Delta x,Y\le y)}{P(x\lt X\le x+\Delta x)}\\
&=\lim_{\Delta x\to0+}\frac{P(x+\Delta x,Y\le y)-P(x,Y\le y)}{P(X\le x+\Delta x)-P(X\le x)}\\
&=\lim_{\Delta x\to0+}\frac{F_{XY}(x+\Delta x,y)-F_{XY}(x,y)}{F_X(x+\Delta x)-F_X(x)}\\
&=\frac{\lim_{\Delta x\to0+}\frac{F_{XY}(x+\Delta x,y)-F_{XY}(x,y)}{\Delta x}}{\lim_{\Delta x\to0+}\frac{F_X(x+\Delta x)-F_X(x)}{\Delta x}}\\
&=\frac{\frac\partial{\partial x}F_{XY}(x,y)}{\frac\partial{\partial x}F_{X}(x)}\\
\end{align*}
$$

입니다.
이제, conditional PDF를 정의할 수 있습니다.
이것은 conditional PDF를 $y$에 대해 편미분함으로써 얻어집니다;

$$
\begin{align*}
f_{Y|X}(x,y)
&=\frac\partial{\partial y}F_{Y|X}(x,y)\\
&=\frac\partial{\partial y}\left(\frac{\frac\partial{\partial x}F_{XY}(x,y)}{\frac\partial{\partial x}F_{X}(x)}\right)\\
&=\frac1{\frac\partial{\partial x}F_{X}(x)}\frac\partial{\partial y}\left(\frac\partial{\partial x}F_{XY}(x,y)\right)\\
&=\frac{\frac{\partial^2}{\partial y\partial x}F_{XY}(x,y)}{\frac\partial{\partial x}F_{X}(x)}\\
&=\frac{f_{XY}(x,y)}{f_X(x)}
\end{align*}
$$

마찬가지로 $X$와 $Y$의 위치를 바꾸면

$$f_{X|Y}(x,y)=\frac{f_{XY}(x,y)}{f_Y(y)}$$

입니다.

**conditional expectations and variances**

06회차 강의에서 (일반적인) conditional expectation은 (continuous case)

$$
E[X|\le a]=\int_{x\le a}xf_X(x|x\le a)\,dx
$$

와 같이 정의했었습니다.
예를 들어, 아래 그림과 같은 bimodal(쌍봉) 분포에서 $X\le a$라는 조건이 주어지면, 그렇지 않았을 때보다 평균이 왼쪽으로 이동하게 될 것입니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_11-4.png){: .img-75-center}

이번에 다루는 것은 (그러니까, 일반적인 conditional expectation이 아니라는 말은) $E[Y|A]$에서 $A$가 $X$에 대한 조건인 경우입니다 ; $E[Y|A_X]$

자세한 것은 다음 강의에서 이어갈 것 같습니다.


**독립과 종속**

강의에서 두 확률변수 $X$와 $Y$의 독립/종속에 대해서는 정의하지 않았던 것으로 보입니다.
연속확률변수 $X$, $Y$에 대해서는

$$f_{XY}(x,y)=f_X(x)=f_Y(y)$$

인 것이 독립조건에 해당한다는 언급이 잠깐 있었던 것 같습니다.
이것이 성질 또는 정리일지, 정의인지 몰랐는데, 그냥 이걸 정의로 채택하겠습니다.

그럼 이산확률변수 $X$, $Y$에 대해서는

$$P_{XY}(x,y)=P_X(x)=P_Y(y)$$

인 것을 독립조건으로 두어야 할 것입니다.

참고로 [DeGroot, Probability and Statistics, 4ed](https://www.amazon.com/Probability-Statistics-4th-Morris-DeGroot/dp/0321500466)에서는 Definition 3.7.5에 정의되어 있고, 내용은 다음과 같습니다.
두 확률변수 $X$, $Y$에 대하여, $A$, $B$가 각각 실수집합의 부분집합일때(정확하게는 real measurable set이라고 해야 할 것 같습니다.)

$$P(X\in A,Y\in B)=P(X\in A)P(Y\in B)$$

이면 $X$와 $Y$가 독립이라고 말합니다.
이것은 정확한 의미로 쓰면

$$P\left(X^{-1}(A)\times Y^{-1}(B)\right)=P\left(X^{-1}(A)\times S_2\right)P\left(S_1\times Y^{-1}(B)\right)$$

로 받아들이면 될 것 같습니다.
만약 $A=\\{x\\}$, $B=\\{y\\}$이면, 이것은 이산확률변수에 대해서의 독립조건과 일치합니다.
또, $A=[x_1,x_2]$, $B=[y_1,y_2]$로 두면 이것이 연속확률변수에서의 독립조건과 동치라는 것을 증명할 수 있을 것 같습니다.

# 12 조건부 평균과 공분산

이번 강의에서 다루는 것은, 드디어 $E[Y|X]$ 입니다.
이전에 이것의 정확한 의미를 파악하지 못해 고생했었습니다.

강의의 가장 초반부에 $E[Y|X]$의 의미는 사실은 $E[Y|X=x]$의 의미라는 언급이 있습니다.
사실 $E[Y|X]$는 그 자체로는 아직 정의된 적이 없는 어떤 개념입니다.
conditional expectation에서 condition에 어떤 '확률변수'가 들어가있습니다.
지금까지 condition에 들어갈 수 있었던 것은 $S$의 부분집합(사건), 확률변수가 포함된 조건(e.g. $X=x$, $X\le x$)이었지 확률변수 그 자체는 아니었던 것입니다.
하지만, $E[Y|X=x]$라고 하면 의미가 생깁니다.
이것은 $X=x$인 조건 하에서의 $Y$의 기댓값을 의미합니다.

더 나아가 이해해야 할 것은 [$E[Y|X]$가 확률변수](https://math.stackexchange.com/q/1946058)라는 사실입니다.
$E[Y|X=x]$는 $Y$의 기댓값이기 때문에 $Y$라든지 $y$라든지 하는 값에 의존하지 않습니다.
이것은 오로지 $x$에 의존하는 값입니다.
다시 말해, $x$에 대한 함수입니다;

$$E[Y|X=x]=g(x)$$

그러면 $E[Y|X]$를

$$E[Y|X]=g(X)$$

로 정의하면 이 값은 하나의 확률변수로 생각할 수 있는 것입니다.
예를 들어, $X$가 확률변수이면 $X$에 대한 함수 $X^2+X$도 확률변수인 것처럼, $X$가 확률변수이기 떄문에 $g(X)$도 확률변수인 것입니다.
더 깊이 말하면, $X$와 $Y$가 각각 $X:S_1\to\mathbb R$이고 $Y:S_2\to\mathbb R$인 확률변수들이라고 할 때, 새로운 확률변수

$$E[Y|X]:S_1\to\mathbb R$$

을

$$E[Y|X](w)=E[Y|X=X(w)]$$

로 정의하면 이것은 잘 정의된 확률변수이고, 위에서 말한 의미와도 부합합니다.

사실, 강의에서는 $E[Y|X]$의 의미에 대해서는 설명하지 않는 것으로 보이고, 조금은 notation abusing을 하는 것으로 보입니다.

이제 강의를 따라서 $E[Y|X=x]$의 정의를 적어보겠습니다.
아래 식에서 첫번째 등호가 정의이고, 이후의 식들은 이전에 언급한 사실들을 적용한 것입니다.

$$
\begin{align*}
E[Y|X]
&=\int_\mathbb Ryf_{Y|X}(x,y)\,dy\\
&=\int_\mathbb Ry\frac{f_{XY}(x,y)}{f_X(x)}\,dy\\
&=g(y)
\end{align*}
$$

둘째 줄의 적분을 계산할 때 $x$가 사라지므로, 적분값을 $y$에 대한 함수로서 놓을 수 있습니다. 따라서 (아까 언급한 것처럼) 마지막 등호가 성립합니다.

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_12-1.png){: .img-100-center}

위의 그림은, 강의의 예시를 구체화해서 적어본 것입니다.
좌표평면 위에 $(0,0)$, $(2,0)$, $(1,1)$을 꼭짓점으로 하는 삼각형의 내부에 점 $P$가 위치한다고 할 때, $P$의 $x$좌표와 $y$좌표를 각각 $X$, $Y$라고 하겠습니다.
$P$가 삼각형 내부에 균일한 정도의 가능성으로 존재할 때 (uniform distribution) $X$, $Y$의 joint PDF는

$$f_{XY}(x,y)=1\qquad(0\le y\le x, y\le 2-x)$$

입니다.
이때, $E[X|Y=y]$와 $E[Y|X=x]$를 계산해보려 합니다.
계산을 하기 전에 직관적으로 살펴보면, $y$의 값이 어떤 값이건 상관없이 $(0\lt y\lt 1)$ $X$가 위치하는 구간은 $1$을 중심으로 하는 구간입니다.
또한, $X$가 여전히 uniform distribution을 따를 것이므로, [$X$의 평균은 1일 수밖에 없습니다.](https://math.stackexchange.com/q/4669361)
따라서 $E[X|Y=y]=1$입니다.
반대로 $x$ 값이 고정되어 있다고 생각하겠습니다.
이번에는 $x$가 $0\le x\le1$인 경우와 $1\le x\le2$인 경우의 상황이 다릅니다.
$0\le x\le1$이면, $Y$는 $0$부터 $x$ 사이를 움직이고, 따라서 그 평균은 $\frac12x$가 될 것이니다.
$1\le x\le2$이면, $Y$는 $0$부터 $2-x$ 사이를 움직이고, 따라서 그 평균은 $\frac12(2-x)$가 될 것입니다.

계산해보면

$$
\begin{align*}
E[X|Y=y]
&=\int_y^{2-y}xf_{X|Y}(x,y)\,dx\\
&=\int_y^{2-y}x\frac{f_{XY}(x,y)}{f_Y(y)}\,dx\\
&=\int_y^{2-y}x\frac{f_{XY}(x,y)}{\int_y^{2-y}f_{XY}(x,y)\,dx}\,dx\\
&=\int_y^{2-y}x\frac1{\int_y^{2-y}\,dx}\,dx\\
&=\int_y^{2-y}x\frac1{2-2y}\,dx\\
&=\frac1{2-2y}\int_y^{2-y}x\,dx\\
&=\frac1{2-2y}\times\frac12\left((2-y)^2-y^2\right)\\
&=1
\end{align*}
$$

이고

$0\le x\le 1$일 때의 $E[Y|X=x]$는

$$
\begin{align*}
E[Y|X=x]
&=\int_0^xyf_{Y|X}(x,y)\,dy\\
&=\int_0^xy\frac{f_{XY}(x,y)}{f_X(x)}\,dy\\
&=\int_0^xy\frac{f_{XY}(x,y)}{\int_0^xf_{XY}(x,y)\,dy}\,dy\\
&=\int_0^xy\frac1{\int_0^x\,dy}\,dy\\
&=\int_0^xy\frac1x\,dy\\
&=\frac1x\int_0^xy\,dy\\
&=\frac12x
\end{align*}
$$

이고, $1\le x\le 2$일 때의 $E[Y|X=x]$는

$$
\begin{align*}
E[Y|X=x]
&=\int_0^{2-x}yf_{Y|X}(x,y)\,dy\\
&=\int_0^{2-x}y\frac{f_{XY}(x,y)}{f_X(x)}\,dy\\
&=\int_0^{2-x}y\frac{f_{XY}(x,y)}{\int_0^{2-x}f_{XY}(x,y)\,dy}\,dy\\
&=\int_0^{2-x}y\frac1{\int_0^{2-x}\,dy}\,dy\\
&=\int_0^{2-x}y\frac1{2-x}\,dy\\
&=\frac1{2-x}\int_0^{2-x}y\,dy\\
&=\frac12(2-x)
\end{align*}
$$

입니다.

**ex.5.10**

두 연속확률변수 $X$, $Y$에 대한 PDF가 다음과 같이 주어졌다고 가정하겠습니다.

$$f_{XY}(x,y)=\frac1ye^{-\frac xy}e^{-y}\qquad(0\le y\le x, y\le 2-x)$$

정말로 PDF가 맞는지 (예의상) 계산해보면

$$
\begin{align*}
\int_0^\infty\int_0^\infty f_{XY}(x,y)\,dx\,dy
&=\int_0^\infty\frac{e^{-y}}y\int_0^\infty e^{-\frac xy}\,dx\,dy\\
&=\int_0^\infty\frac{e^{-y}}y\left[-ye^{-\frac xy}\right]_{x=0}^{x=\infty}\,dy\\
&=\int_0^\infty e^{-y}\,dy\\
&=1
\end{align*}
$$

입니다.
conditional expectation $E[X|Y=y]$을 계산하기 전에, 그 과정에 쓰이는 $f_Y(y)$를 먼저 계산해보면

$$
\begin{align*}
f_Y(y)
&=\int_0^\infty f_{XY}(x,y)\,dx\\
&=\int_0^\infty\frac1ye^{-\frac xy}e^{-y}\,dx\\
&=\frac{e^{-y}}y\left[-ye^{-\frac xy}\right]_{x=0}^{x=\infty}\\
&=e^{-y}
\end{align*}
$$

입니다.
이제 계산을 해보면

$$
\begin{align*}
E[X|Y=y]
&=\int_0^\infty xf_{XY}(x,y)\,dx\\
&=\int_0^\infty x\frac{f_{X|Y}(x,y)}{f_Y(y)}\,dx\\
&=\int_0^\infty x\times\frac{\frac1ye^{-\frac xy}e^{-y}}{e^{-y}}\,dx\\
&=\int_0^\infty\left(\frac xy\right)e^{-\frac xy}\,dx\\
&=y\int_0^\infty\left(\frac xy\right)e^{-\frac xy}\,d\left(\frac xy\right)\\
&=y\left[te^{-t}-e^{-t}\right]_{t=0}^{t=\infty}\\
&=y
\end{align*}
$$

입니다.
중간 계산과정에서 $\int te^{-t}\,dt=-te^{-t}-e^{-t}$를 활용했습니다.

이번에는, 확률변수 $X$에 대하여 $g(X)$의 확률을 구하는 식을 소개합니다.
이번 강의의 맨 처음에 언급한 것이지만, $X$가 어떤 분포를 가지는 확률변수이면, $g(X)$ 또한 새로운 분포를 따르는 확률변수이며, 그 떄의 PMF 혹은 PDF는 일치합니다.
따라서 $g(x)$의 평균을

$$
\begin{align*}
E\left[g(X)\right]&=\int_{-\infty}^\infty g(x)f_X(x)\,dx
&&\text{(continuous)}\\
E\left[g(X)\right]&=\sum_{i=1}^ng(x_i)P_X(x_i)
&&\text{(discrete)}\\
\end{align*}
$$

와 같이 정의할 수 있습니다.
마찬가지로, 다변수 함수 $g(X,Y)$에 대해서도

$$\tag{$\ast$}
\begin{aligned}
E\left[g(X,Y)\right]&=\int_{\mathbb R^2} g(x,y)f_{XY}(x,y)\,dx
&&\text{(continuous)}\\
E\left[g(X,Y)\right]&=\sum_{i=1}^m\sum_{j=1}^ng(x_i,y_j)P_X(x_i,y_j)
&&\text{(discrete)}\\
\end{aligned}
$$

입니다.
또한,
두 확률변수 $X$, $Y$에 대하여, 두 함수 $g_1(X,Y)$, $g_2(X,Y)$가 존재할 때, 두 실수 $\alpha$, $\beta$에 대하여

$$E\left[\alpha g_1(X,Y)+\beta g_2(X,Y)\right]
=\alpha E\left[g_1(X,Y)\right]+\beta E\left[g_2(X,Y)\right]\tag{$\ast\ast$}$$

입니다.
즉, $E$는 다변수 함수에 대해서도 linear operator입니다.
왜냐하면

$$
\begin{align*}
E\left[g_1(X,Y)+g_2(X,Y)\right]
&=\iint_{\mathbb R^2}\left(g_1(X,Y)+g_2(X,Y)\right)f_{XY}(x,y)\,dx\,dy\\
&=\iint_{\mathbb R^2}\left(g_1(X,Y)\right)f_{XY}(x,y)\,dx\,dy
+\iint_{\mathbb R^2}\left(g_2(X,Y)\right)f_{XY}(x,y)\,dx\,dy\\
&=E\left[g_1(X,Y)\right]+E\left[g_2(X,Y)\right]
\end{align*}
$$

이고,

$$
\begin{align*}
E\left[\alpha g(X,Y)\right]
&=\iint_{\mathbb R^2}\alpha g(X,Y)f_{XY}(x,y)\,dx\,dy\\
&=\alpha\iint_{\mathbb R^2}g(X,Y)f_{XY}(x,y)\,dx\,dy\\
&=\alpha E\left[g(X,Y)\right]
\end{align*}
$$

이기 때문입니다.

이와 같은 사실들은 구구절절 다 소개되지는 않았지만, 암시적으로 언급되고 있는 것 같습니다.

**ex.5.11** $E\left[E[X|Y]\right]=E[X]$

이번 성질을 이해하려면, 초반에 언급한

$E[X|Y]$는 확률변수이다.
{: .text-center}

라는 것을 확실히 알아야 합니다.
좌변에서 $E[X|Y]$에 대해 기댓값 연산을 취하고 있는데, 그럴 수 있는 것이 $E[X|Y]$가 그 자체로 확률변수이기 때문입니다.
앞서 언급한대로 $E[X|Y=y]$는 $y$의 함수입니다 ;

$$E[X|Y=y]=g(y)$$

그런 관점에서 보면 $E\left[E[X|Y]\right]$는 $g(Y)$에 대한 평균을 계산하고 있는 것입니다.
계산해보면

$$
\begin{align*}
E\left[E[X|Y]\right]
&=E\left[g(Y)\right]\\
&=\int_{\mathbb R}g(Y)f_Y(y)\,dy\\
&=\int_{\mathbb R}\left(\int_{\mathbb R}xf_{X|Y}(x,y)\,dx\right)f_Y(y)\,dy\\
&=\iint_{\mathbb R^2}xf_{X|Y}(x,y)f_Y(y)\,dx\,dy\\
&=\iint_{\mathbb R^2}xf_{XY}(x,y)\,dx\,dy\\
&=\int_{\mathbb R}x\int_{\mathbb R}f_{XY}(x,y)\,dy\,dx\\
&=\int_{\mathbb R}xf_X(x)\,dx\\
&=E[X]
\end{align*}
$$

입니다.

이것에 대한 discrete 버전의 증명은

$$
\begin{align*}
E\left[E[X|Y]\right]
&=E\left[g(Y)\right]\\
&=\sum_{j=1}^ng(y_j)P_Y(y_i)\\
&=\sum_{j=1}^n\left(E[X|Y=y_i]\right)P_Y(y_i)\\
&=\sum_{j=1}^n\left(\sum_{i=1}^mx_iP_{X|Y}(x,y)\right)P_Y(y_i)\\
&=\sum_{j=1}^n\sum_{i=1}^mx_iP_{X|Y}(x,y)P_Y(y_i)\\
&=\sum_{j=1}^n\sum_{i=1}^mx_iP_{XY}(x,y)\\
&=\sum_{i=1}^mx_i\sum_{j=1}^nP_{XY}(x,y)\\
&=\sum_{i=1}^mx_iP_X(x)\\
&=E[X]
\end{align*}
$$

입니다.
여기에서 세번째 줄과 마지막 줄의 값을 같다고 두면

$$E[X]=\sum_{j=1}^n\left(E[X|Y=y_i]\right)P_Y(y_i)$$

이것은 the law of total probability인

$$P[A]=\sum_{j=1}^nP(A|A_i)P(A_i)$$

와 구조가 거의 똑같다는 점이 설명되고 있습니다.

**5.7 covariance and correlation coefficient**

$X$와 $Y$가 확률변수이고, $E[X]=\mu_X$, $E[Y]=\mu_Y$이면, $X$와 $Y$ 사이의 공분산(covariance)을

$$\text{cov}(X,Y)=\sigma_{XY}=E\left[(X-\mu_X)(Y-\mu_Y)\right]$$

로 정의합니다.
물론, $(\ast)$에 의해

$$
\text{cov}(X,Y)=\iint_{\mathbb R^2}(x-\mu_X)(y-\mu_Y)f_{XY}(x,y)\,dx\,dy
$$

$(\ast\ast)$를 사용해 이것을 정리하면

$$\tag{$\ast\ast\ast$}
\begin{aligned}
\text{cov}(X,Y)
&=E\left[XY-\mu_YX-\mu_XY+\mu_X\mu_Y)\right]\\
&\stackrel{\ast\ast}{=}E[XY]-\mu_YE[X]-\mu_XE[Y]+\mu_X\mu_Y\\
&=E[XY]-E[X]E[Y]
\end{aligned}
$$

입니다.

만약 $\text{cov}(X,Y)\ne0$이면, $X$와 $Y$는 상관성이 있다(correlated)고 말하고, $\text{cov}(X,Y)=0$이면, $X$와 $Y$는 상관성이 없다(uncorrelated)고 말합니다.
이때, 독립성은 uncorrelatedness를 보장합니다 ;

$X$, $Y$가 서로 독립이면, $X$와 $Y$는 상관성이 없습니다.
{. :text-center}

왜냐하면, $X$와 $Y$가 독립이라고 가정할 때,

$$
\begin{align*}
E[XY]
&=\iint_{\mathbb R^2}xyP_{XY}(x,y)\,dx\,dy\\
&=\iint_{\mathbb R^2}xyP_X(x)P_Y(y)\,dx\,dy\\
&=\int_{\mathbb R}xP_X(x)\,dx\times\int_{\mathbb R}yP_Y(y)\,dy\\
&=E[X]E[Y]
\end{align*}
$$

가 되어 식 $(\ast\ast\ast)$의 우변이 0이 되기 때문입니다.

하지만, uncorrelatedness가 독립성을 보장하지는 않습니다.
그 [반례](https://stats.stackexchange.com/q/85384)로, $X$가 $[-1,1]$의 uniform distribution이고 $Y=X^2$이면, $X$와 $Y$는 uncorrelated하지만 독립조건이 깨집니다.
$X$의 분포는

$$f_X(x)=\frac12\qquad(-1\le x\le1)$$

로 주어집니다.

