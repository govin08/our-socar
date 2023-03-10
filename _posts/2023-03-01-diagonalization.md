---
layout: single
title: "행렬의 직교대각화"
#description: "행렬의 직교대각화(orthogonal/unitary diagonalization of matrices)에 대해 요약해본 글입니다."
categories: mathematics
tags: [linear algebra]
use_math: true
publish: false
author_profile: false
---

<!-- https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/
info / 파랑 / 정의
success / 연두 / 정리
warning / 주황 / 증명 -->


2020년 3월, 대학원의 두번째 학기에 행렬의 직교대각화(orthogonal diagonalization)에 대해 고민했습니다.
해당 내용은 수학과 기준 학부 2학년 2학기에 배워야 하는 내용이지만, 그리고 해당 시기의 〈선형대수2〉 과목은 A+을 받기는 했지만, 완벽하게 직교대각화에 대해 이해하지는 못했습니다.
개별적인 행렬의 직교대각화는 할 줄 알았고, eigenvalue-eigenvector가 뭔지 알았지만,
 - **real symmetric 행렬은 왜 orthogonally diagonalizable한지**

마찬가지로
 - **complex Hermitian 행렬은 왜 unitarily diagonalizable한지**
 
 이해하지 못했습니다.

그리하여, 한 번 시간을 잡고 위의 두 내용에 대해 고민해본 적이 있습니다.
많은 자료들을 뒤졌지만 정작 제가 궁금해하는 저 위의 사실에 대하여 AtoZ로 알려주는 자료는 찾지 못했습니다.
그래서, 해당 내용을 직접 TeX으로 정리해 본 적이 있습니다.
[링크]({{ site.url }}/assets/pdf/orthogonally_diagonalizable.pdf){: .btn .btn--primary}

해당 파일은 영어로 작성해본 것인데, 이번 포스트에서는 이것을 한글로 적으면서 내용도 풀어서 다시 정리해보고자 합니다.
사실, 어느 정도 선형대수에 대한 지식이 있다면, 간결하게 적어놓은 원래 파일이 더 잘읽힐 수 있습니다.

이 포스트는 기본적으로 한글을 사용하지만, 사용된 수학용어들은 대부분 영어로 적었습니다.
해당 용어가 처음등장할 때에 한해서만 한글 표현을 병기해보았습니다.
다만, 고등학교 수준의 수학용어는 그냥 한국어 용어로 썼습니다.

# 1 정의

## 1.1 행렬

이 포스트에서 다루는 행렬들은 모두 entry(성분)들이 실수 혹은 복소수인 행렬들만을 다룹니다.
즉, 여기에서 행렬(matrix)이란, 실수 혹은 복소수를 직사각형 모양으로 배열해 괄호로 묶어 놓은 것을 말합니다.
예를 들어
<!-- (특정한 행렬은 $P$, $Q$, $R$, $S$, $T$, $U$ 등으로 쓰고 일반적인 행렬은 $A$, $B$, $C$ 등으로 적겠습니다.) -->
,

$$P=\begin{bmatrix}1&2\\0&1\end{bmatrix},\qquad Q=\begin{bmatrix}0&1&0\\1&0&0\end{bmatrix}$$

는 행렬입니다.
이때, $P$는 2개의 행과 2개의 열로 이루어진 행렬이어서 '$2\times 2$ 행렬'이라고 부르고 $Q$는 2개의 행과 3개의 열로 이루어진 행렬이어서 '$2\times3$ 행렬'이라고 부릅니다.

행이 하나인 행렬과 열이 하나인 행렬도 행렬로 취급합니다.
이것들은 각각 '행벡터', '열벡터' 라는 이름으로도 불립니다.
예를 들어

$$R=\begin{bmatrix}2&4\end{bmatrix},\qquad S=\begin{bmatrix}1\\-1\\0\end{bmatrix}$$

이면 $R$는 $1\times2$ 행렬이기도 하지만 2차원의 행벡터라고도 불리고, $S$는 $3\times1$ 행렬이기도 하지만 3차원의 열벡터라고도 불립니다.

선형대수를 말할 때 늘 그렇듯이, 이 포스트에서도 벡터는 열벡터로 표시합니다.
그러니까, 고등학교 수학에서는 $v=(2,1)$을 2차원 벡터(평면 벡터), $w=(1,0,3)$을 3차원 벡터로 생각했었습니다.
그런데 선형대수에서는 보통 이것들을 열벡터로 쓰고

$$
v=\begin{bmatrix}2\\1\end{bmatrix},\qquad w=\begin{bmatrix}1\\0\\3
$$

와 같이 나타내게 됩니다.

행렬을 대문자 알파벳으로 표시한다면, 이 행렬의 entry는 소문자 알파벳과 두 개의 아래첨자로 표시합니다.
이때 첫번째 아래첨자는 행 번호를, 두번째 아래첨자는 열 번호를 각각 의미합니다.
예를 들어,
위의 $P$의 정의에서

$$p_{11}=1,\quad p_{12}=2,\quad p_{21}=0,\quad p_{22}=1$$

입니다.
어떤 행렬의 모양을 나타낼 때, 두 개의 아래첨자가 있는 소문자 알파벳의 양옆에 소괄호를 붙이고, 거기에 다시 행렬의 모양을 특정해 표시하기도 합니다.
예를 들어

$$T=(e_ij)_{2\times2}$$

이면, 이것은 이 행렬이 $2\times2$ 행렬이라는 뜻이고, 그 성분들이 $t_{ij}$로 표시된다는 뜻입니다.
만약 $t_{ij}=i+j-1$이면

$$T=\begin{bmatrix}1&2\\2&3\end{bmatrix}$$

이 될 것입니다.

어떤 행렬의 행의 개수와 열의 개수가 같으면 그 행렬을 정사각행렬(정방행렬, square matrix)이라고 부릅니다.
예를 들어, $P$, $T$는 정사각행렬이지만 $Q$, $R$, $S$는 정사각행렬이 아닙니다.

## 1.2 행렬의 연산

### 이항연산
두 행렬의 모양이 같으면 두 행렬을 더할 수 있습니다.
두 행렬을 더할 때에는 성분별로 더하면 됩니다.
예를 들어, $A$와 $E$는 모양이 서로 같으므로 서로 더할 수 있고, 그 결과가

$$P+T=\begin{bmatrix}1&2\\0&1\end{bmatrix}+\begin{bmatrix}1&2\\2&3\end{bmatrix}=\begin{bmatrix}1+1&2+2\\0+2&1+3\end{bmatrix}=\begin{bmatrix}2&4\\2&4\end{bmatrix}$$

로 나타나지만, $P$와 $Q$는 모양이 서로 다르므로 더할 수 없습니다.

두 행렬에 대해서 첫번째 행렬의 열의 수와 두번째 행렬의 행의 수가 같으면 두 행렬을 곱할 수 있습니다.
그러니까, $A$가 $m\times n$ 행렬이고, $B$가 $n\times l$ 행렬이면, 두 행렬 $A$, $B$의 곱 $AB$를 생각할 수 있습니다.
$AB=C$이라고 하면,

$$c_{ij}=\sum_{k=1}^na_{ik}b_{kj}$$

입니다.

예를 들어, $P$와 $Q$는 각각 $2\times2$, $2\times3$ 행렬이고 따라서 두 행렬을 곱할 수 있습니다.
($m=2$, $n=2$, $k=3$)
그 결과는

$$
\begin{align*}
PQ
&=\begin{bmatrix}1&2\\0&1\end{bmatrix}\begin{bmatrix}0&1&0\\1&0&0\end{bmatrix}\\
&=\begin{bmatrix}
1\times0+2\times1&1\times1+2\times0&1\times0+2\times0\\
0\times0+1\times1&0\times1+1\times0&0\times0+1\times0
\end{bmatrix}\\
&=\begin{bmatrix}
2&1&0\\
1&0&0
\end{bmatrix}
\end{align*}
$$
입니다.

마찬가지로,

$$
\begin{align*}
PT&=\begin{bmatrix}1&2\\0&1\end{bmatrix}\begin{bmatrix}1&2\\2&3\end{bmatrix}=\begin{bmatrix}5&8\\2&3\end{bmatrix}\\
QS&=\begin{bmatrix}0&1&0\\1&0&0\end{bmatrix}\begin{bmatrix}1\\-1\\0\end{bmatrix}=\begin{bmatrix}-1\\1\end{bmatrix}\\
RP&=\begin{bmatrix}2&4\end{bmatrix}\begin{bmatrix}1&2\\0&1\end{bmatrix}=\begin{bmatrix}2&8\end{bmatrix}\\
P^2&=\begin{bmatrix}1&2\\0&1\end{bmatrix}^2=\begin{bmatrix}1&2\\0&1\end{bmatrix}\begin{bmatrix}1&2\\0&1\end{bmatrix}
=\begin{bmatrix}1&4\\0&1\end{bmatrix}
\end{align*}
$$

와 같이 계산할 수 있습니다.
이상은 행렬이 두 개 주어졌을 때 만들 수 있는 이항연산입니다.

### 단항연산
행렬 하나에 대해서도 연산을 정의할 수 있는데, 대표적인 것이 transpose(전치)와 conjugate transpose(켤레전치)입니다.

행렬 $A$에 대하여, $A$의 transpose는 $A^T$와 같이 표시하는데, 이것은 $A$의 행번호와 열번호를 뒤집어놓은 것입니다.
예를 들면,

$$
\begin{align*}
P^T&=\begin{bmatrix}1&2\\0&1\end{bmatrix}^T=\begin{bmatrix}1&0\\2&1\end{bmatrix}\\
Q^T&=\begin{bmatrix}0&1&0\\1&0&0\end{bmatrix}^T=\begin{bmatrix}0&1\\1&0\\0&0\end{bmatrix}\\
R^T&=\begin{bmatrix}2&4\end{bmatrix}^T=\begin{bmatrix}2\\4\end{bmatrix}
\end{align*}
$$

등입니다.

행렬 $A$의 conjugate transpose는 $A^H$와 같이 표시하는데, 이것은 $A$를 transpose하고, 각 entry들에 conjuagtion(켤레 연산)을 취한 것입니다.
즉,

$$
A^H=\overline{A^T}
$$

입니다.
그런데, 사실 transpose를 먼저 하나, 각 entry에 conjuagtion을 취하나 같으므로

$$
A^H = \bar A^T
$$

와 같이 정의해도 정확히 같은 정의가 됩니다.
이때, 어떤 복소수에 conjuagtion을 취하는 것은 이 복소수의 허수부분의 부호를 바꾸어 켤레복소수를 얻어내는 것을 말합니다.
즉 $2+3i$의 켤레복소수는 $2-3i$인데, 이것을

$$
\overline{2+3i}=2-3i
$$

로 표현합니다.
마찬가지로,

$$
\begin{align*}
\overline{2-3i}&=2+3i\\
\overline{i}&=-i\\
\overline{3}&=3\\
\overline{\frac{i-2}3}&=\frac{-i-2}3\\
\end{align*}
$$

입니다.
특히, 실수의 켤레 복소수가 자기 자신이 된다는 것은 중요합니다.
즉

**정리 1** \\
$z$가 실수이면, $\bar z=z$이고, 그 역도 성립합니다.
{: .notice--success}

어떤 행렬에 conjuagtion을 취하는 것은 그 행렬의 각 entry에 conjuagtion을 취하는 것입니다.
예를 들어

$$U=\begin{bmatrix}0&2-3i\\2+3i&3\end{bmatrix}$$

이면

$$
\begin{align*}
\overline U
&=\begin{bmatrix}0&\overline{2-3i}\\\overline{2+3i}&\overline3\end{bmatrix}\\
&=\begin{bmatrix}0&2+3i\\2-3i&3\end{bmatrix}
\end{align*}
$$

인 것입니다.
한편, 정리 1을 응용하면 다음과 같이 쓸 수도 있습니다.

**정리 2** \\
$A$가 실수로 이루어진 행렬이면, $\bar A=A$이고, 그 역도 성립합니다.
{: .notice--success}

## 1.3 symmetric / Hermitian

이제 드디어 symmetric, Hermitian이라는 말이 나옵니다.

### symmetric 행렬

symmetric 행렬 (symmetric matrix, 대칭 행렬)이란, 행렬의 대각선을 기준으로 양옆이 대칭인 행렬을 말합니다.
예를 들어 행렬

$$T=\begin{bmatrix}1&2\\2&3\end{bmatrix}$$

의 대각선은 1, 3을 잇는 직선인데, 이 행렬은 이 직선을 기준으로 양옆이 대칭입니다.
따라서 $T$는 symmetric 행렬입니다.
반면, 행렬

$$P=\begin{bmatrix}1&2\\0&1\end{bmatrix},\qquad Q=\begin{bmatrix}0&1&0\\1&0&0\end{bmatrix}$$

는 대각선을 기준으로 대칭이 아니므로 $P$, $Q$는 symmetric 행렬이 아닙니다.
$Q$와 같은 $2\times 3$ 행렬은 어떻게 해도 symmetric하지 않습니다.
즉, symmetric 행렬이 되기 위한 필요조건은, 그 행렬이 정사각행렬인 것입니다.

행렬의 symmetricity는 transpose를 사용하면 쉽게 정의할 수도 있습니다.

**정의 3**\\
행렬 $A$에 대하여 $A^T=A$이면 $A$를 symmetric 행렬이라고 부릅니다.
{: .notice--info}

### Hermitian 행렬

한편, Hermitian 행렬(Hermitian matrix, 에르미트 행렬)이란, 대각선을 기준으로 양옆이 서로 켤레관계인 행렬을 말합니다.
이것을 conjugate transpose로 표현하면 다음과 같이 간단하게 정의할 수 있습니다.

**정의 4**\\
행렬 $A$에 대하여 $A^H=A$이면 $A$를 Hermitian 행렬이라고 부릅니다.
{: .notice--info}

symmetric 행렬에서와 마찬가지로, 어떤 행렬이 Hermitian이기 위해서는 일단 정사각행렬이어야 합니다.
$P$, $Q$, $R$, $S$, $T$, $U$ 중에서 정사각행렬인 것은

$$
\begin{align*}
P=\begin{bmatrix}1&2\\0&1\end{bmatrix}\\
T=\begin{bmatrix}1&2\\2&3\end{bmatrix}\\
U=\begin{bmatrix}0&2-3i\\2+3i&3\end{bmatrix}
\end{align*}
$$

입니다.
이 중 $T$는 Hermitian 행렬입니다(transpose의 $T$와 행렬 이름의 $T$가 혼동되지 않게 잘 보아야 합니다.);

$$
T^H=\bar T^T=T^T=T
$$

반면, $P$는 Hermitian 행렬이 아닙니다;

$$
P^H=\bar P^T=P^T\neq P.
$$

(그러니까, $T$는 symmetric 행렬이면서 Hermitian 행렬입니다.
반면에 $P$는 symmetric 행렬도 못 되고, Hermitian 행렬도 못 됩니다.)
즉, 실수로 이루어진 행렬에서는 conjugation은 아무 역할을 하지 못하기 때문에 (정리 2) symmetricity와 Hermitianity의 개념이 서로 일치합니다.
다시 말해, 모든 real symmetric 행렬 (실수로 이루어진 행렬들 중 symmetric 행렬)은 Hermitian 행렬인 것입니다.

마지막으로, $U$도 Hermitian 행렬입니다.

$$
\begin{align*}
U^H
&=\begin{bmatrix}0&2-3i\\2+3i&3\end{bmatrix}^H=\begin{bmatrix}0&2+3i\\2-3i&3\end{bmatrix}^T=U
\end{align*}
$$

## 1.4 inner product / norm

고등학교 수학에 따르면, 2차원 벡터 $v$, $w$가 다음과 같이 주어져 있을 때,

$$
v=\begin{bmatrix}v_1\\v_2\end{bmatrix},\quad w=\begin{bmatrix}w_1\\w_2\end{bmatrix}
$$

두 벡터의 내적 $v\cdot w$은

$$
v\cdot w=v_1w_1+v_2w_2
$$

로 정의됩니다.
이때, 벡터 $v$의 길이는

$$\sqrt{v_1\,^2+v_2\,^2}$$

으로 나타낼 수 있었습니다.
고등학교 수학에서는 3차원까지 다룹니다.
3차원 벡터 $v$, $w$가 

$$
v=\begin{bmatrix}v_1\\v_2\\v_3\end{bmatrix},\quad w=\begin{bmatrix}w_1\\w_2\\w_3\end{bmatrix}
$$

와 같이 주어질 때, 두 벡터의 내적은

$$
v\cdot w=v_1w_1+v_2w_2+v_3w_3
$$

이고, $v$의 길이는

$$\sqrt{v_1\,^2+v_2\,^2+v_3\,^2}$$

입니다.

이것을 일반적인 $n$차원으로 확장하면, 두 벡터

$$
v=\begin{bmatrix}v_1\\v_2\\v_3\\\vdots\\v_n\end{bmatrix},\quad w=\begin{bmatrix}w_1\\w_2\\w_3\\\vdots\\w_n\end{bmatrix}
$$

에 대하여 $v$와 $w$의 내적은

$$
v\cdot w=\sum_{k=1}^nv_kw_k
$$

이고, $v$의 길이는

$$
\sqrt{\sum_{k=1}^n{v_k}^2}
$$

입니다.

이것이, $n$차원 벡터의 내적(inner product)과 놈(norm)에 해당합니다.
더 정리해서 말하기 전에, 열벡터로서 표현된 두 벡터의 $v$, $w$의 내적과 norm을 행렬곱의 형식으로 표현해보려 합니다.
행렬곱의 정의에 따르면 $v$와 $w$의 내적은 $v^Tw$와 같습니다.
그리고, $v$의 크기는 $v$와 그 자신의 내적, 즉 $v^Tv$에 루트를 씌운 값과 같습니다.

**정의 5**\\
(1) $n$차원 벡터 $v$, $w$에 대하여 $v$와 $w$의 내적을 $\langle v,w\rangle$로 나타내면,

$$\langle v,w\rangle=v^Tw$$

이 성립합니다.

(2) $n$차원 벡터 $v$에 대하여 $v$의 norm을 $||v||$로 나타내면,

$$||v||=\sqrt{<v,v>}=\sqrt{v^Tv}$$

이 성립합니다.
{: .notice--info}

## 1.5 orthogonal vectors / orthonormal vectors

## 1.6 orthogonal matrices / unitary matrices

## 1.7 eigenvalue / eigenvector



[1]:{{ site.url }}/assets/pdf/orthogonally_diagonalizable.pdf
