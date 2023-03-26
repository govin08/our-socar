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
이 강의는 총 14강으로 되어 있고 확률과 통계에 관한 전반적인 사항을 다루는 것 같습니다.
그 내용을 아주 자세하게는 적지 않고 간략하게만 적어나갈 예정입니다.

# 1 조건부확률과 Bayes 정리

**1) sample Space**

확률에 대해 공부할 때 가장 먼저 배우는 것은 당연히 표본공간(sample space, 전공간)입니다.
고등학교 이후의 과정에서 확률은 항상 집합의 관점에서 이해됩니다.
표본공간 또한 집합으로, 보통 $S$로 적습니다.
이것은 어떤 시행(trial)에 대하여 나타날 수 있는 *가능한 모든 outcome들의 집합*을 말합니다.
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

두 사건 $A$, $B$에 대하여 사건 $A$가 발생했을 때, 사건 $B$도 발생할 확률을 $P(B|A)$라고 하고,

$$P(B|A)=\frac{P(B\cap A)}{P(A)}$$

로 정의합니다.

이것은 마치, $A$를 sample space로 보는 것과 같습니다.
마찬가지로 일반적인 확률 $P(A)$도 $P(A|S)$와 같이 해석할 수 있습니다.

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

**ex. 1.7> binary symmetric channel**

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
$P(\cdot|\cdot)$의 두 $\:\:\cdot\:\:$에는 사건이, 그러니까 집합이 들어가야 하는데, 하나의 원소만 들어갔습니다.
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

**1) $P(\text{error})$**

오류라고 판단할 수 있는 경우는 input이 $x_1$로 들어갔는데 output이 $y_2$로 나오는 경우와 그 반대의 경우입니다.
전자의 경우를 $\{x_1\}\times\{y_2\}$로 표현해야 정확하겠지만 이것을 그냥 $x_1\cap y_2$로 쓰면

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

**2) When $y_2$ is received, what is the probability that $x_1$ is transmitted?**

$$
\begin{align*}
P(x_1|y_2)
&=\frac{P(y_2|x_1)P(x_1)}{P(y_2)}\\
&=\frac{P(y_2|x_1)P(x_1)}{P(y_2|x_1)P(x_1)+P(y_2|x_2)P(x_2)}\\
&=\frac{P_{12}P(x_1)}{P_{12}P(x_1)+P_{22}P(x_2)}
\end{align*}
$$

여기에서 $y_2$는 아까 말한 observation data (output)이고 $x_1$은 original data (input)입니다.

**3) $P(x_1|\text{error})$**

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
nx(1+x)^{n-1}=\sum_{k=0}^nk\binom nkx^k\tag{*}
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
\begin{equation}\tag{**}
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

여러 개의 독립적인 모듈 $C_1$, $\cdots$, $C_n$ 들이 직렬로 연결되어 있고(cascade) 각 모듈들의 reliabilty가 $R_1(t)$, $\cdots$, 이 시스템의 reliability는

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
