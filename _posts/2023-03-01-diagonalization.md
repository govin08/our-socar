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
primary / 회색 / 성질
info / 파랑 / 정의
warning / 주황 / 증명
success / 연두 / 정리
danger / 빨강 / 참고 -->


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
사실, 어느 정도 선형대수에 대한 지식이 있다면, 간결하게 적어놓은 원래 파일이 더 잘 읽힐 수 있습니다.

---

이 포스트는 기본적으로 한글을 사용하지만, 사용된 수학용어들은 대부분 영어로 적었습니다.
해당 용어가 처음등장할 때에 한해서만 한글 표현을 병기해보았습니다.
다만, 고등학교 수준의 수학용어는 그냥 한국어 용어로 썼습니다.

# 1 정의

## 1.1 행렬

이 포스트에서 다루는 행렬들은 모두 성분(entry)들이 실수 혹은 복소수인 행렬들만을 다룹니다.
즉, 여기에서 행렬(matrix)이란, 실수 혹은 복소수를 직사각형 모양으로 배열해 괄호로 묶어 놓은 것을 말합니다.
예를 들어,

$$P=\begin{bmatrix}1&2\\0&1\end{bmatrix},\qquad Q=\begin{bmatrix}0&1&0\\1&0&0\end{bmatrix}$$

는 행렬입니다.
이때, $P$는 2개의 행과 2개의 열로 이루어진 행렬이어서 '$2\times 2$ 행렬'이라고 부르고 $Q$는 2개의 행과 3개의 열로 이루어진 행렬이어서 '$2\times3$ 행렬'이라고 부릅니다.
이 포스트에서는 $2\times 2$, $2\times 3$ 등을 그 행렬의 '모양'이라고 하겠습니다.

**참고**\\
개별적인 행렬들은 $P$, $Q$, $R$, $\cdots$, $M$, $N$, $K$, $\cdots$ 등으로 적었고, 일반적인 행렬은 $A$, $B$, $C$ 등으로 적었습니다.
{: .notice--danger}

행이 하나인 행렬과 열이 하나인 행렬도 행렬로 취급합니다.
이것들은 각각 '행벡터', '열벡터' 라는 이름으로도 불립니다.
예를 들어

$$R=\begin{bmatrix}2&4\end{bmatrix},\qquad S=\begin{bmatrix}1\\-1\\0\end{bmatrix}$$

이면 $R$는 $1\times2$ 행렬이기도 하지만 2차원의 행벡터라고도 불리고, $S$는 $3\times1$ 행렬이기도 하지만 3차원의 열벡터라고도 불립니다.

선형대수를 말할 때 늘 그렇듯이, 이 포스트에서도 벡터는 열벡터로 표시합니다.
그러니까, 고등학교 수학에서는 $v=(2,1)$을 2차원 벡터(평면 벡터), $w=(1,0,3)$을 3차원 벡터로 생각했었습니다.
그런데 선형대수에서는 보통 이것들을 열벡터로 쓰고

$$
v=\begin{bmatrix}2\\1\end{bmatrix},\qquad w=\begin{bmatrix}1\\0\\3\end{bmatrix}
$$

와 같이 나타내게 됩니다.

행렬을 대문자 알파벳으로 표시한다면, 이 행렬의 성분들은 소문자 알파벳과 두 개의 아래첨자로 표시합니다.
이때 첫번째 아래첨자는 행 번호를, 두번째 아래첨자는 열 번호를 각각 의미합니다.
예를 들어,
위의 행렬

$$P=\begin{bmatrix}1&2\\0&1\end{bmatrix}$$

에서

$$p_{11}=1,\quad p_{12}=2,\quad p_{21}=0,\quad p_{22}=1$$

입니다.

어떤 행렬의 모양을 나타낼 때, 두 개의 아래첨자가 있는 소문자 알파벳의 양옆에 소괄호를 붙이고, 거기에 다시 행렬의 모양을 특정해 표시하기도 합니다.
예를 들어

$$T=(e_ij)_{2\times2}$$

이면, 이것은 이 행렬이 $2\times2$ 행렬이라는 뜻이고, 그 성분들이 $t_{ij}$로 표시된다는 뜻입니다.
만약 $t_{ij}=i+j-1$이면

$$T=\begin{bmatrix}1&2\\2&3\end{bmatrix}$$

이 될 것입니다.

### 여러가지 행렬

어떤 행렬의 행의 개수와 열의 개수가 같으면 그 행렬을 **정사각행렬**(정방행렬, square matrix)이라고 부릅니다.
예를 들어, $P$, $T$는 정사각행렬이지만 $Q$, $R$, $S$는 정사각행렬이 아닙니다.

어떤 행렬 $A$에 대하여, $A$의 대각성분이란 $i=j$를 만족시키는 $a_{ij}$들을 말합니다.
만약 대각성분들을 제외한 모든 성분들

$$a_{ij}\quad(i\neq j)$$

이 0이면, 이 행렬을 **대각행렬**이라고 부릅니다.

예를 들어,

$$
\begin{align*}
D&=\begin{bmatrix}2&0\\0&5\end{bmatrix}\\
E&=\begin{bmatrix}1&0&0\\0&3&0\\0&0&2\end{bmatrix}\\
F&=\begin{bmatrix}-1&0&0\\0&4&0\end{bmatrix}
\end{align*}
$$

와 같은 행렬들은 대각행렬입니다.
반면, $P$, $Q$, $R$, $S$, $T$는 모두 대각행렬이 아닙니다.

대각행렬 중 가장 간단하면서 중요한 행렬은 **항등행렬**이라고 불리는 행렬입니다.
항등행렬은, 정사각행렬 중에서 대각성분이 모두 1인 대각행렬을 말합니다.
즉,

$$
\begin{bmatrix}1&0\\0&1\end{bmatrix},\quad\begin{bmatrix}1&0&0\\0&1&0\\0&0&1\end{bmatrix},\quad\cdots
$$

와 같은 행렬을 말합니다.
항등행렬의 행의 수(=열의 수)가 $n$개이면 그 항등행렬을 $I_n$으로 표현합니다.
($n$이 중요하지 않다면 $n$은 생략될  수 있습니다.)
즉, 위의 항등행렬들은

$$
\begin{align*}
I_2&=\begin{bmatrix}1&0\\0&1\end{bmatrix}\\
I_3&=\begin{bmatrix}1&0&0\\0&1&0\\0&0&1\end{bmatrix}\\
&\vdots
\end{align*}
$$

와 같이 표현될 수 있습니다.

두 정사각행렬 $A$, $B$에 대하여

$$AB=BA=I$$

가 성립하면, $B$를 $A$의 역행렬이라고 말하고, $B=A^{-1}$라고 씁니다.
반대로, $A$는 $B$의 역행렬이기도 합니다.
즉 $A=B^{-1}$이기도 합니다.

<div class="notice--danger">
<b>참고 </b> <br>
두 정사각행렬 $A$, $B$에 대하여 $AB=I$이면 $BA=I$가 성립합니다.
<br>
(a) 이것은 당연한 말 같아보이기는 해도, 아주 쉽게 증명되지는 않습니다.
보통은 선형대수의 다른 개념들을 많이 동원해야 증명됩니다.
이 포스트에서는 해당 개념들에 대해 다루지 않을 예정이므로 링크로 그 증명을 대체합니다.
<ul>
    <li> <a href="https://math.stackexchange.com/questions/852387/if-ab-i-then-ba-i-is-my-proof-right">determinant를 이용한 Surb의 증명</a></li>
    <li> <a href="https://sharmaeklavya2.github.io/theoremdep/nodes/linear-algebra/matrices/product-equals-identity-implies-invertible.html">연립방정식과 rank를 이용한 증명</a></li>
</ul>
그 중 아래 증명에에서는 정사각행렬들의 집합이 algebra over a field 라는 사실과 subspace의 dimension의 개념만을 이용하여 증명하고 있어서 읽기 좋은 것 같습니다.
<ul>
    <li> <a href="https://math.stackexchange.com/questions/3852/if-ab-i-then-ba-i">algebra over a field을 이용한 Martin Brandenburg의 증명</a></li>
</ul>
그러니까 다음과 같이 쓸 수 있습니다 ;
두 정사각형 $A$, $B$에 대하여 $AB=I$이면 $B=A^{-1}$ 입니다.
</div>

## 1.2 행렬의 연산

### 이항연산
두 행렬의 모양이 같으면 두 행렬을 더할 수 있습니다.
두 행렬을 더할 때에는 성분별로 더하면 됩니다.
예를 들어, $P$와 $T$는 모양이 서로 같으므로 서로 더할 수 있고, 그 결과가

$$P+T=\begin{bmatrix}1&2\\0&1\end{bmatrix}+\begin{bmatrix}1&2\\2&3\end{bmatrix}=\begin{bmatrix}1+1&2+2\\0+2&1+3\end{bmatrix}=\begin{bmatrix}2&4\\2&4\end{bmatrix}$$

로 나타나지만, $P$와 $Q$는 모양이 서로 다르므로 더할 수 없습니다.

두 행렬에 대해서 첫번째 행렬의 열의 수와 두번째 행렬의 행의 수가 같으면 두 행렬을 곱할 수 있습니다.
그러니까, $A$가 $m\times n$ 행렬이고, $B$가 $n\times l$ 행렬이면, 두 행렬 $A$, $B$의 곱 $AB$를 생각할 수 있습니다.
$AB=C$이라고 하면, $C$의 각 성분들인 $c_{ij}$는

$$c_{ij}=\sum_{k=1}^na_{ik}b_{kj}$$

입니다.

예를 들어, $P$와 $Q$는 각각 $2\times2$, $2\times3$ 행렬이고 따라서 두 행렬을 곱할 수 있습니다.
($m=2$, $n=2$, $l=3$)
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
이상은 행렬이 두 개 주어졌을 때 만들 수 있는 이항연산인 **덧셈**과 **곱셈**입니다.

### 단항연산
행렬 하나에 대해서도 연산을 정의할 수 있는데, 대표적인 것이 **transpose** (전치轉置)와 **conjugate transpose** (켤레전치)입니다.

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

conjugate transpose에 대해 설명하기 전에 conjugation(켤레복소수화, 공액共軶)에 대해 먼저 이야기하겠습니다.
어떤 복소수 $z=a+bi$에 대하여 ($a$, $b$는 실수) 이 복소수의 켤레복소수(conjugate)는 $a-bi$이고, 이것을 $\bar z$로 표시합니다.
이와 같이, 주어진 복소수를 그 켤레복소수로 변환하는 연산을 conjugation이라고 합니다.

예를 들어

$$
\begin{align*}
\overline{2+3i}&=2-3i\\
\overline{2-3i}&=2+3i\\
\overline{i}&=-i\\
\overline{3}&=3\\
\overline{\frac{i-2}3}&=\frac{-i-2}3\\
\end{align*}
$$

입니다.
이때, 실수의 켤레복소수가 자기 자신이 된다는 것은 중요합니다.

**정리 1** \\
$z$가 실수이면, $\bar z=z$이고, 그 역도 성립합니다.
{: .notice--success}

**증명** \\
복소수 $z=a+bi$에 대하여, 만약 $z$가 실수이면 $b=0$이고 $z=a$입니다.
따라서 $\bar z=a=\overline{a+0i}=a-0i=a=z$입니다.
반대로,$\bar z=z$이면 $a+bi=a-bi$입니다.
두 복소수가 같으려면 실수부분과 허수부분이 서로 같아야 하므로 $b=-b$, $2b=0$, $b=0$이 됩니다.
따라서 $z$는 실수입니다.
{: .notice--warning}

conjugation은 단순히 복소수에 대해서만이 아니라, 복소수를 성분으로 가지는 행렬에 대해서도 취할 수 있습니다.
행렬 $A$에 대하여 $A$의 conjugate은 $\bar A$로 표시하며, $A$의 각 성분들에 conjugation을 취한 행렬로 정의합니다;

$$\bar A = \left(\overline{a_{ij}}\right)_{m\times n}$$

예를 들어 복소수를 성분으로 갖는 행렬 $Z$가

$$Z=\begin{bmatrix}0&2-3i\\2+3i&3\end{bmatrix}$$

와 같이 정의될 때,

$$
\begin{align*}
\overline Z
&=\begin{bmatrix}0&\overline{2-3i}\\\overline{2+3i}&\overline3\end{bmatrix}\\
&=\begin{bmatrix}0&2+3i\\2-3i&3\end{bmatrix}
\end{align*}
$$

인 것입니다.
한편, 정리 1을 응용하면 다음과 같이 쓸 수도 있습니다.

**정리 2** \\
$A$가 실수로 이루어진 행렬이면, $\bar A=A$이고, 그 역도 성립합니다.
{: .notice--success}

<div class="notice--warning">
<b>증명 </b> <br>
복소수로 이루어진 행렬 $A$를 $A=\left(a_{ij}\right)_{m\times n}$으로 표현하겠습니다.
만약, $A$가 실수로 이루어진 행렬이면,
$\bar A = \left(\overline{a_{ij}}\right)_{m\times n} = \left(a_{ij}\right)_{m\times n} = A$
입니다.
반대로, $\bar A=A$이면, 모든 $i$, $j$에 대하여 $\overline{a_{ij}}=a_{ij}$가 성립한다는 뜻입니다.
따라서 $a_{ij}$들은 모두 실수입니다.
</div>

지금까지 정의한 행렬 $P$, $Q$, $R$, $S$, $T$, $Z$에서 정리 2를 간단히 확인해볼 수 있습니다.
$P$, $Q$, $R$, $S$, $Z$는 실수로 이루어진 행렬들이고 $\overline P=P$, $\overline Q=Q$, $\overline R=R$, $\overline S=S$, $\overline T=T$가 성립합니다.
$Z$는 실수로만 이루어진 행렬이 아니고, 허수가 포함된 행렬입니다.
따라서 $\bar Z\neq Z$입니다.

이제 행렬의 conjugate transpose를 정의할 수 있습니다.
어떤 행렬 $A$의 conjugate transpose는 $A^H$와 같이 표시하는데, 이것은 $A$를 transpose하고, conjugation한 것을 말합니다.
즉,

$$
A^H=\overline{A^T}
$$

입니다.
그런데, 사실 transpose를 먼저 취하나, conjuagtion을 먼저 취하나 그 결과는 같으므로

$$
A^H = \bar A^T
$$

와 같이 정의해도 정확히 같은 정의가 됩니다.

한편, 정리 2에 따르면 실수로 이루어진 행렬이면 $A$에 대하여 transpose를 취하는 것과 conjugation을 취하는 것에는 차이가 없습니다.
또한, 두 행렬 $A$, $B$의 곱 $AB$에 대하여 transpose나 conjugation을 취한 결과는 각 행렬을 transpose 혹은 conjugation한 후 순서를 바꾸어 얻은 결과와 같습니다.
나중에 이 사실들을 써먹을 예정이므로, 아래와 같이 성질 3으로 적어놓겠습니다.
이에 관한 증명들은 생략하겠습니다.

<div class="notice">
<b>성질 3 </b> <br>
(a) $A$가 실수로 이루어진 행렬이면 $A^T=A^H$입니다.
<br>
(b) $A$, $B$가 복소수로 이루어진 행렬이고 행렬곱 $AB$가 정의될 때, 아래 식이 성립합니다.
$$
\begin{align*}
(AB)^T&=B^TA^T\\
(AB)^H&=B^HA^H\\
(AB)^{-1}&=B^{-1}A^{-1}
\end{align*}
$$
</div>

## 1.3 symmetric / Hermitian

이제 드디어 symmetric, Hermitian이라는 말을 쓸 수 있습니다.

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
즉, symmetric 행렬이 되기 위해서는 일단 그 행렬이 정사각행렬일 필요가 있습니다..

행렬의 symmetricity는 transpose를 사용하면 쉽게 정의할 수도 있습니다.

**정의 4**\\
행렬 $A$에 대하여 $A^T=A$이면 $A$를 symmetric 행렬이라고 부릅니다.
{: .notice--info}

### Hermitian 행렬

한편, Hermitian 행렬(Hermitian matrix, 에르미트 행렬)이란, 대각선을 기준으로 양옆이 서로 켤레관계인 행렬을 말합니다.
이것을 conjugate transpose로 표현하면 다음과 같이 간단하게 정의할 수 있습니다.

**정의 5**\\
행렬 $A$에 대하여 $A^H=A$이면 $A$를 Hermitian 행렬이라고 부릅니다.
{: .notice--info}

symmetric 행렬에서와 마찬가지로, 어떤 행렬이 Hermitian이기 위해서는 일단 정사각행렬이어야 합니다.
$P$, $Q$, $R$, $S$, $T$, $Z$ 중에서 정사각행렬인 것은

$$
\begin{align*}
P&=\begin{bmatrix}1&2\\0&1\end{bmatrix}\\
T&=\begin{bmatrix}1&2\\2&3\end{bmatrix}\\
Z&=\begin{bmatrix}0&2-3i\\2+3i&3\end{bmatrix}
\end{align*}
$$

입니다.
이 중에서 $T$, $Z$는 Hermitian 행렬이고, $P$는 Hermite 행렬이 아닙니다.
$P$, $T$는 실수로 이루어진 행렬이므로 성질 3(a)을 사용하여

<!-- $$
\begin{align*}
P^H&=P^T=\begin{bmatrix}1&2\\0&1\end{bmatrix}^T=\begin{bmatrix}1&0\\2&1\end{bmatrix}\ne P\\
T^H&=T^T=\begin{bmatrix}1&2\\2&3\end{bmatrix}^T=\begin{bmatrix}1&2\\2&3\end{bmatrix}=T
\end{align*}
$$ -->

$$
\begin{align*}
P^H&=P^T\ne P\\
T^H&=T^T=T
\end{align*}
$$

임을 확인할 수 있습니다.
$Z$에 대해서는 직접 complex conjugate를 계산하여

$$
Z^H
=\overline{Z^T}=\overline{\begin{bmatrix}0&2+3i\\2-3i&3\end{bmatrix}}
=\begin{bmatrix}\bar0&\overline{2+3i}\\\overline{2-3i}&\bar3\end{bmatrix}=Z
$$

와 같이 계산할 수 있습니다.

<!-- 
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
$$ -->

## 1.4 orthogonal / unitary

### inner product / norm

고등학교 수학에 따르면, 2차원 벡터 $x$, $y$가 다음과 같이 주어져 있을 때,

$$
x=\begin{bmatrix}x_1\\x_2\end{bmatrix},\quad y=\begin{bmatrix}y_1\\y_2\end{bmatrix}
$$

두 벡터의 내적 $x\cdot y$은

$$
x\cdot y=x_1y_1+x_2y_2
$$

로 정의됩니다.
또한, 벡터 $x$의 길이는

$$\sqrt{x_1\,^2+x_2\,^2}$$

으로 나타낼 수 있었습니다.
고등학교 수학에서는 3차원까지 다룹니다.
3차원 벡터 $x$, $y$가 

$$
x=\begin{bmatrix}x_1\\x_2\\x_3\end{bmatrix},\quad y=\begin{bmatrix}y_1\\y_2\\y_3\end{bmatrix}
$$

와 같이 주어질 때, 두 벡터의 내적은

$$
x\cdot y=x_1y_1+x_2y_2+x_3y_3
$$

이고, $x$의 길이는

$$\sqrt{x_1\,^2+x_2\,^2+x_3\,^2}$$

입니다.

이것을 일반적인 $n$차원으로 확장하면, 두 벡터

$$
x=\begin{bmatrix}x_1\\x_2\\\vdots\\x_n\end{bmatrix},\quad y=\begin{bmatrix}y_1\\y_2\\\vdots\\y_n\end{bmatrix}
$$

에 대하여 $x$와 $y$의 내적은

$$
x\cdot y=\sum_{k=1}^nx_ky_k
$$

이고, $x$의 길이는

$$
\sqrt{\sum_{k=1}^n{x_k}^2}
$$

입니다.

이것이, $n$차원 벡터의 내적(inner product)과 놈(norm)에 해당합니다.
더 정리해서 말하기 전에, 열벡터로서 표현된 두 벡터의 $x$, $y$의 내적과 norm을 행렬곱의 형식으로 표현해보려 합니다.
위의 정의된 $x\cdot y$의 식은 행렬곱의 정의에 의해 $x^Ty$와 같습니다;

$$
\begin{align*}
x^Ty
&=\begin{bmatrix}x_1&x_2&\cdots&x_n\end{bmatrix}\begin{bmatrix}y_1\\y_2\\\vdots\\y_n\end{bmatrix}\\
&=x_1y_1+x_2y_2+\cdots+x_ny_n=x\cdot y.
\end{align*}
$$

그리고, $x$의 크기는 $x$와 그 자신의 내적, 즉 $x^Tx$에 루트를 씌운 값과 같습니다;

$$
\sqrt{x^Tx}=x_1\cdot x_1+x_2\cdot x_2+\cdots+x_n\cdot x_n=\sqrt{\sum_{k=1}^n{x_k}^2}
$$

<div class="notice--info">
<b> 정의 6 </b> <br>
(a) $n$차원 실수 벡터 $x$, $y$에 대하여 $x$와 $y$의 내적(inner product)은 $x\cdot y$로 쓰기도 하지만 $\langle x,y\rangle$로 나타내기도 합니다.
$\langle x, y\rangle$의 정의는

$$\langle x,y\rangle=x^Ty$$

입니다.
<br>
(b) $n$차원 실수 벡터 $x$의 크기는 $x$의 norm이라고도 부르며, $||x||$로 나타냅니다.
$||x||$의 정의는

$$||x||=\sqrt{\langle x,x\rangle}=\sqrt{x^Tx}$$

입니다.
</div>

### orthogonal / orthonormal

고등학교 수학에서, 영벡터가 아닌 두 벡터가 서로 수직이면 그 내적이 0이며, 그 역도 성립한다는 것을 다룹니다.

예를 들어, 세 개의 2차원 벡터 $u_1$, $u_2$, $u_3$가

$$
u_1=\begin{bmatrix}1\\-2\end{bmatrix},\quad
u_2=\begin{bmatrix}2\\1\end{bmatrix},\quad
u_3=\begin{bmatrix}1\\0\end{bmatrix}
$$

이면

![diagonalization_1-5-1]({{site.url}}\images\2023-03-01-diagonalization\diagonalization_1-5-1.png){: .img-50-center}

$u_1$와 $u_2$는 서로 수직입니다($u_1\perp u_2$);

$$
{u_1}^Tu_2=\begin{bmatrix}1&-2\end{bmatrix}\begin{bmatrix}2\\1\end{bmatrix}=0
$$


하지만 $u_1$와 $u_3$, $u_2$와 $u_3$는 수직이 아닙니다($u_1\not\perp u_3$, $u_2\not\perp u_3$);

$$
\begin{align*}
{u_1}^Tu_3&=\begin{bmatrix}1&-2\end{bmatrix}\begin{bmatrix}1\\0\end{bmatrix}=1\neq0\\
{u_2}^Tu_3&=\begin{bmatrix}2&1\end{bmatrix}\begin{bmatrix}1\\0\end{bmatrix}=2\neq0\\
\end{align*}
$$

예를 들어, 세 개의 3차원 벡터 $v_1$, $v_2$, $v_3$가

$$
v_1=\begin{bmatrix}1\\-2\\0\end{bmatrix},\quad
v_2=\begin{bmatrix}2\\1\\0\end{bmatrix},\quad
v_3=\begin{bmatrix}0\\0\\1\end{bmatrix}
$$

이면

![diagonalization_1-5-2]({{site.url}}\images\2023-03-01-diagonalization\diagonalization_1-5-3.png){: .img-100-center}

하지만 $u_1$와 $u_2$, $u_1$와 $u_3$, $u_2$와 $u_3$는 모두 서로 수직입니다($u_1\perp u_2$, $u_1\perp u_3$, $u_2\perp u_3$);

$$
\begin{align*}
{v_1}^Tv_2&=\begin{bmatrix}1&-2&0\end{bmatrix}\begin{bmatrix}2\\1\\0\end{bmatrix}=0\\
{v_1}^Tu_3&=\begin{bmatrix}1&-2&0\end{bmatrix}\begin{bmatrix}0\\0\\1\end{bmatrix}=0\\
{v_2}^Tu_3&=\begin{bmatrix}2&1&0\end{bmatrix}\begin{bmatrix}0\\0\\1\end{bmatrix}=0
\end{align*}
$$

이때, $v_1$, $v_2$, $v_3$의 경우처럼 벡터들이 서로 모두 수직일때, 이 벡터들이 orthogonal하다고 말합니다.
위의 예에서 $u_1$, $u_2$, $u_3$는 orthogonal하지 않고, $v_1$, $v_2$, $v_3$는 orthogonal한 것입니다.

$v_1$, $v_2$, $v_3$를 조금 변형해서 $w_1$, $w_2$, $w_3$를 다음과 같이 만들면

$$
w_1=\begin{bmatrix}\frac1{\sqrt5}\\-\frac2{\sqrt5}\\0\end{bmatrix},\quad
w_2=\begin{bmatrix}\frac2{\sqrt5}\\\frac1{\sqrt5}\\0\end{bmatrix},\quad
w_3=\begin{bmatrix}0\\0\\1\end{bmatrix}
$$

이 경우에도 $w_1\perp u_w$, $w_1\perp w_3$, $w_2\perp w_3$가 성립합니다.
즉 $w_1$, $w_2$, $w_3$은 orthogonal합니다.
이때, $w_1$, $w_2$, $w_3$은 $v_1$, $v_2$, $v_3$의 경우와 다르게 그 벡터들의 크기가 1이라는 성질이 있습니다;

$$
\begin{align*}
||w_1||&=\sqrt{\left(\frac1{\sqrt5}\right)^2+\left(-\frac2{\sqrt5}\right)^2+0^2}=1\\
||w_2||&=\sqrt{\left(\frac2{\sqrt5}\right)^2+\left(\frac1{\sqrt5}\right)^2+0^2}=1\\
||w_3||&=\sqrt{0^2+0^2+1^2}=1
\end{align*}
$$

이런 경우에, 이 벡터들이 orthonormal하다고 말합니다.
즉, $u_1$, $u_2$, $u_3$와 $v_1$, $v_2$, $v_3$는 orthonormnal하지 않고, $w_1$, $w_2$, $w_3$는 orthonormal한 것입니다.

<div class="notice--info">
<b> 정의 7 </b> <br>
$n$개의 $m$차원 실수 벡터 $a_1$, $a_2$, $\cdots$, $a_n$에 대하여
<br>
(a) $a_1$, $a_2$, $\cdots$, $a_n$가 모두 서로 수직이면 $a_1$, $a_2$, $\cdots$, $a_n$가 orthogonal하다고 합니다.
<br>
(b) $a_1$, $a_2$, $\cdots$, $a_n$가 모두 서로 수직이고, $||a_1||=1$, $||a_2||=1$, $\cdots$, $||a_n||=1$이면 $a_1$, $a_2$, $\cdots$, $a_n$가 orthonormal하다고 합니다.
</div>

### orthogonal 행렬

orthogonal한 세 개의 3차원벡터 $v_1$, $v_2$, $v_3$에 대해 다시 생각해봅시다.

$$
v_1=\begin{bmatrix}1\\-2\\0\end{bmatrix},\quad
v_2=\begin{bmatrix}2\\1\\0\end{bmatrix},\quad
v_3=\begin{bmatrix}0\\0\\1\end{bmatrix}
$$

$v_i$로 만들 수 있는 모든 조합의 내적을 나열해보면

$$
\begin{align*}
{v_1}^Tv_1 = 5  &&{v_1}^Tv_2 = 0 &&{v_1}^Tv_3 = 0 \\
{v_2}^Tv_1 = 0  &&{v_2}^Tv_2 = 5 &&{v_2}^Tv_3 = 0 \\
{v_3}^Tv_1 = 0  &&{v_3}^Tv_2 = 0 &&{v_3}^Tv_3 = 1
\end{align*}
$$

이 됩니다.
재밌는 사실은, 이 아홉가지의 계산을 하나의 행렬곱으로 표현할 수 있다는 것입니다.
행렬곱의 정의를 상기해보면

$$
\begin{bmatrix}
1&-2&0\\
2&1&0\\
0&0&1
\end{bmatrix}
\begin{bmatrix}
1&2&0\\
-2&1&0\\
0&0&1
\end{bmatrix}
=
\begin{bmatrix}
5&0&0\\
0&5&0\\
0&0&1
\end{bmatrix}
$$

와 같이 표현할 수 있는 것입니다.
위 식의 좌변의
첫번째 행렬은 세 행벡터 ${v_1}^T$, ${v_2}^T$, ${v_3}^T$를 세로로 쌓아놓은 것이고,
두번째 행렬은 세 열벡터 $v_1$, $v_2$, $v_3$를 가로로 나열한 것입니다.
즉,

$$
\begin{bmatrix}
-&{v_1}^T&-\\
-&{v_2}^T&-\\
-&{v_3}^T&-
\end{bmatrix}
\begin{bmatrix}
|&|&|\\
v_1&v_2&v_3\\
|&|&|
\end{bmatrix}
=
\begin{bmatrix}
5&0&0\\
0&5&0\\
0&0&1
\end{bmatrix}
$$

입니다.
이때, 세 열벡터 $v_1$, $v_2$, $v_3$를 가로로 나열한 행렬을 $V$로 표기하면
위의 식을 간단히

$$V^TV=
\begin{bmatrix}
5&0&0\\
0&5&0\\
0&0&1
\end{bmatrix}$$

로 쓸 수 있습니다.
일반적으로, 정사각행렬 $A$가 orthogonal한 벡터들을 가로로 나열한 행렬이면, $A^TA$는 대각행렬입니다.

이번에는 orthonormal한 세 개의 3차원벡터 $w_1$, $w_2$, $w_3$에 대해 다시 생각해봅시다.

$$
w_1=\begin{bmatrix}\frac1{\sqrt5}\\-\frac2{\sqrt5}\\0\end{bmatrix},\quad
w_2=\begin{bmatrix}\frac2{\sqrt5}\\\frac1{\sqrt5}\\0\end{bmatrix},\quad
w_3=\begin{bmatrix}0\\0\\1\end{bmatrix}
$$

아까처럼, $w_i$로 만들 수 있는 모든 조합의 내적을 나열해보면

$$
\begin{align*}
{w_1}^Tv_1 = 1  &&{w_1}^Tv_2 = 0 &&{w_1}^Tv_3 = 0 \\
{w_2}^Tv_1 = 0  &&{w_2}^Tv_2 = 1 &&{w_2}^Tv_3 = 0 \\
{w_3}^Tv_1 = 0  &&{w_3}^Tv_2 = 0 &&{w_3}^Tv_3 = 1
\end{align*}
$$

이고

$$
\begin{bmatrix}
-&{w_1}^T&-\\
-&{w_2}^T&-\\
-&{w_3}^T&-
\end{bmatrix}
\begin{bmatrix}
|&|&|\\
w_1&w_2&w_3\\
|&|&|
\end{bmatrix}
=
\begin{bmatrix}
1&0&0\\
0&1&0\\
0&0&1
\end{bmatrix}
$$

입니다.
좌변의 두번째 행렬을 $W$로 표기하면

$$W^TW=I$$

가 됩니다.
이때, $W$와 같은 행렬을 orthogonal 행렬이라고 합니다.
즉, orthonormal한 열벡터들이 가로로 나열되어 있는 정사각행렬을 orthogonal 행렬이라고 합니다.

<div class="notice--info">
<b> 정의 8 </b> <br>
실수를 성분으로 가지는 정사각행렬 $A$가

$$A^TA=I$$

를 만족시키면 $A$를 orthogonal 행렬(orthogonal matrix, 직교행렬)이라고 부릅니다.
</div>

<div class="notice--info">
<b> 정의 8 </b> <br>
실수를 성분으로 가지는 정사각행렬 $A$가

$$A^TA=I$$

를 만족시키면 $A$를 orthogonal 행렬(orthogonal matrix, 직교행렬)이라고 부릅니다.
</div>

$w_1$, $w_2$, $w_3$와 $W$ 사이의 관계에서 볼 수 있듯 다음이 성질이 성립합니다.

(a) $A$가 orthogonal 행렬($n\times n$)이면 $A$의 각 열들은 orthonormal하다.

(b) $n$차원의 orthonormal한 벡터들 $n$개를 가로로 나열해서 얻은 행렬은 orthogonal하다.

<div class="notice--danger">
<b> 참고 9 </b> <br>
이 포스트에서 (그리고 선형대수에서) orthogonal이라는 말은 두 가지 의미를 가집니다.
두 의미를 혼동하지 않고 잘 사용해야 합니다.
<br>
(a) 벡터 $x_1$, $x_2$, $\cdots$, $x_n$에 대하여
$${x_i}^Tx_j=0\qquad(i\neq j)$$
을 만족시킬 때 이 벡터들을 orthogonal 하다고 말합니다.
<br>
(b) 정사각행렬 $A$에 대하여
$$A^TA=I$$
이면 이 행렬 $A$가 orthogonal 하다고 말합니다.
</div>

### unitary 행렬

지금까지 정의한 내적(inner product), norm, orthogonality 등은 성분이 실수인 벡터 혹은 행렬에 대한 개념입니다.
만약, 그 성분이 일반적으로 복소수인 벡터 혹은 행렬에 대해 생각한다면, 그에 따른 내적, norm 등의 개념은 실수일 때와는 조금 다르게 정의됩니다.

<div class="notice--info">
<b> 정의 10 </b> <br>
(a) $n$차원 복소수 벡터 $x$, $y$에 대하여 $x$와 $y$의 내적(inner product) $\langle x,y\rangle$은

$$\langle x,y\rangle=x^Hy$$

입니다.
<br>
(b) $n$차원 복소수 벡터 $x$의 norm $||x||$은

$$||x||=\sqrt{\langle x,x\rangle}=\sqrt{x^Hx}$$

입니다.
</div>

정의 6과 비교해보면 transpose(T)였던 것이 conjugate transpose(H)로 바뀌었습니다.
다시 말해,

$$x=\begin{bmatrix}x_1\\x_2\\\vdots\\x_n\end{bmatrix},\quad y=\begin{bmatrix}y_1\\y_2\\\vdots\\y_n\end{bmatrix}$$

이면 ($x_i$, $y_i$는 복소수),

$$
\begin{align*}
\langle x, y\rangle
&=\overline{x_1}y_1+\overline{x_2}y_2+\cdots+\overline{x_n}y_n\\
&=\sum_{k=1}^n\overline{x_k}y_k\\
||x||
&=\sqrt{|x_1|^2+|x_n|^2+\cdots+|x_n|^2}\\
&=\sqrt{\sum_{k=1}^n|x_k|^2}
\end{align*}
$$

인 것입니다.
($|a+bi|=\sqrt{a^2+b^2}$)
예를 들어, 벡터 $u_1$, $u_2$가

$$
\begin{align*}
u_1=&\begin{bmatrix}1+2i\\2-i\end{bmatrix}\\
u_2=&\begin{bmatrix}3\\1-i\end{bmatrix}
\end{align*}
$$

이면

$$
\begin{align*}
\langle u_1, u_2\rangle
% &=\left\langle \begin{bmatrix}1+2i\\2-i\end{bmatrix}, \begin{bmatrix}3\\1-i\end{bmatrix}\right\rangle\\
&=u_1\,^Hu_2\\
&=\begin{bmatrix}1-2i&2+i\end{bmatrix}\begin{bmatrix}3\\1-i\end{bmatrix}\\
&=(1-2i)3+(2+i)(1-i)\\
&=(3-6i)+(3-i)=6-7i
\end{align*}
$$

이고

$$
\begin{align*}
||u_1||
&=\sqrt{u_1\,^Hu_1}\\
&=\sqrt{\begin{bmatrix}1-2i&2+i\end{bmatrix}\begin{bmatrix}1+2i\\2-i\end{bmatrix}}\\
&=\sqrt{(1-2i)(1+2i)+(2+i)(2-i)}\\
&=\sqrt{5+5}=\sqrt{10}\\
||u_2||
&=\sqrt{u_2\,^Hu_2}\\
&=\sqrt{\begin{bmatrix}3&1+i\end{bmatrix}\begin{bmatrix}3\\1-i\end{bmatrix}}\\
&=\sqrt{3\times3+(1+i)(1-i)}\\
&=\sqrt{11}
\end{align*}
$$

입니다.

위와 같이 정의한 복소벡터에 대한 내적을 가지고 '수직'의 개념도 정의할 수 있습니다.

<div class="notice--info">
<b> 정의 11 </b> <br>
(a) 두 복소수 벡터 $x$, $y$에 대하여 

$$\langle x,y\rangle=0$$

이면 두 벡터가 서로 수직이라고 말하고, $x\perp y$라고 씁니다.
<br>
(b) $n$개의 복소벡터 $x_1$, $x_2$, $\cdots$, $x_n$에 대하여

$$\langle x_i,x_j\rangle=0\quad(i\neq j)$$

이면 이 벡터들이 orthogonal하다고 말합니다.
<br>
(c) $n$개의 복소벡터 $x_1$, $x_2$, $\cdots$, $x_n$에 대하여

$$\langle x_i,x_j\rangle=
\begin{cases}
0\quad(i\neq j)\\
1\quad(i=j)
\end{cases}
$$

이면 이 벡터들이 orthonormal하다고 말합니다.
</div>

## 1.7 eigenvalue / eigenvector


[1]:{{ site.url }}/assets/pdf/orthogonally_diagonalizable.pdf
