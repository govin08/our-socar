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
 - **complex Hermitian 행렬은 왜 unitarily diagonalizable한지**
 
에 대해서는 이해하지 못했습니다.

그리하여, 한 번 시간을 잡고 위의 두 내용에 대해 고민해본 적이 있습니다.
많은 자료들을 뒤졌지만 정작 제가 궁금해하는 저 위의 사실에 대하여 AtoZ로 알려주는 자료는 찾지 못했습니다.
그래서, 해당 내용을 직접 TeX으로 정리해 본 적이 있습니다.
[링크]({{ site.url }}/assets/pdf/orthogonally_diagonalizable.pdf){: .btn .btn--primary}

해당 파일은 영어로 작성해본 것인데, 이번 포스트에서는 이것을 한글로 적으면서 내용도 풀어서 다시 정리해보고자 합니다.
사실, 어느 정도 선형대수에 대한 지식이 있다면, 간결하게 적어놓은 원래 파일이 더 잘 읽힐 수 있습니다.

<div class="notice--danger">
<b>참고 </b> <br>
이 포스트는 기본적으로 한글을 사용하지만, 사용된 수학 용어들은 대부분 영어로 적었습니다.
해당 용어가 처음 등장할 때에 한해서만 한글 표현을 병기해보았습니다.
다만, 고등학교 수준의 수학 용어는 그냥 한국어 용어로 썼습니다.
</div>

# 1 정의

## 1.1 행렬

이 포스트에서 다루는 행렬들은 모두 성분(entry)들이 실수 혹은 복소수인 행렬들만을 다룹니다.
즉, 여기에서 **행렬(matrix)**이란, 실수 혹은 복소수들을 직사각형 모양으로 배열해 괄호로 묶어 놓은 것을 말합니다.
예를 들어,

$$P=\begin{bmatrix}1&2\\0&1\end{bmatrix},\qquad Q=\begin{bmatrix}0&1&0\\1&0&0\end{bmatrix}$$

는 행렬입니다.

<div class="notice--danger">
<b>참고 </b> <br>
<ul>
    <li>개별적인 행렬들은 $P$, $Q$, $R$, $\cdots$ 등으로 적었고, 일반적인 행렬은 $A$, $B$, $C$ 등으로 적었습니다.</li>
    <li>개별적인 벡터들은 $u$, $v$, $w$ 등으로 적었고, 일반적인 벡터는 $x$, $y$ 등으로 적었습니다.</li>
</ul>
</div>

이때, $P$는 2개의 행과 2개의 열로 이루어진 행렬이어서 '$2\times 2$ 행렬'이라고 부르고 $Q$는 2개의 행과 3개의 열로 이루어진 행렬이어서 '$2\times3$ 행렬'이라고 부릅니다.
이 포스트에서는 $2\times 2$, $2\times 3$ 등을 그 행렬의 모양이라고 하겠습니다.

행이 하나인 행렬과 열이 하나인 행렬도 행렬로 취급합니다.
이것들은 각각 '행벡터', '열벡터' 라는 이름으로도 불립니다.
예를 들어

$$R=\begin{bmatrix}2&4\end{bmatrix},\qquad S=\begin{bmatrix}1\\-1\\0\end{bmatrix}$$

이면 $R$는 $1\times2$ 행렬이기도 하지만 2차원의 행벡터라고도 불리고, $S$는 $3\times1$ 행렬이기도 하지만 3차원의 열벡터라고도 불립니다.

선형대수를 말할 때 흔히 그렇듯이, 이 포스트에서도 벡터는 열벡터로 표시합니다.
그러니까, 고등학교 수학에서는 $v=(2,1)$을 2차원 벡터, $w=(1,0,3)$을 3차원 벡터로 생각했었습니다.
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

가끔씩은, 소문자가 아닌 대문자 알파벳에 아래첨자를 주어 행렬의 성분을 표시하기도 합니다.
즉, 행렬 $A$가 주어졌을 때 이 행렬의 $i$행 $j$열 성분은 보통 $a_{ij}$로 나타내지만, 가끔씩은 $A_{ij}$로 나타내기도 합니다.
이것은 행렬 자체의 표현이 조금 복잡할 때 많이 쓰입니다.
만약 $AB+C$라는 행렬의 $i$행 $j$열 성분을 표현하고 싶다면 $\left(AB+C\right)_{ij}$라고 표현하는 것입니다.

어떤 행렬을 나타낼 때, 행렬의 성분을 소괄호로 감싸고, 거기에 다시 아래첨자로 행렬의 모양을 특정해 표시하기도 합니다.
즉

$$A=(a_{ij})_{m\times n}$$

이면, 이것은 이 행렬 $A$가 $m\times n$ 행렬이고, 그 성분이 $a_{ij}$라는 뜻입니다.
예를 들어, 

$$T=\left(t_{ij}\right)_{2\times2}=\left(i+j-1\right)_{2\times2}$$

이면

$$T=\begin{bmatrix}1&2\\2&3\end{bmatrix}$$

이 될 것입니다.

### 여러가지 행렬

어떤 행렬의 행의 개수와 열의 개수가 같으면 그 행렬을 **정사각행렬**(정방행렬, square matrix)이라고 부릅니다.
예를 들어, $P$, $T$는 정사각행렬이지만 $Q$, $R$, $S$는 정사각행렬이 아닙니다.
사실, 이후에 나오는 모든 행렬들은 정사각행렬입니다.

어떤 행렬 $A$에 대하여, $A$의 대각성분이란 $i=j$를 만족시키는 $a_{ij}$들을 말합니다.
만약 대각성분들을 제외한 모든 성분들이 0이면, 이 행렬을 **대각행렬**이라고 부릅니다.

예를 들어,

$$
\begin{align*}
D&=\begin{bmatrix}2&0\\0&5\end{bmatrix}\\
E&=\begin{bmatrix}1&0&0\\0&0&0\\0&0&2\end{bmatrix}\\
F&=\begin{bmatrix}-1&0&0\\0&4&0\end{bmatrix}
\end{align*}
$$

와 같은 행렬들은 대각행렬입니다.
반면, 위에서 정의한 $P$, $Q$, $R$, $S$, $T$는 모두 대각행렬이 아닙니다.

대각행렬 중 가장 간단하면서 중요한 행렬은 **항등행렬**이라고 불리는 행렬입니다.
항등행렬은, 정사각행렬 중에서 대각성분이 모두 1인 대각행렬을 말합니다.
즉,

$$
\begin{bmatrix}1&0\\0&1\end{bmatrix},\quad\begin{bmatrix}1&0&0\\0&1&0\\0&0&1\end{bmatrix},\quad\cdots
$$

와 같은 행렬을 말합니다.
항등행렬의 행의 수(=열의 수)가 $n$개이면 그 항등행렬을 $I_n$으로 표현합니다.
($n$이 중요하지 않다면 $n$를 생략하여 그냥 $I_n$이라고 쓸 수도 있습니다.)
즉, 위의 항등행렬들은

$$
I_2=\begin{bmatrix}1&0\\0&1\end{bmatrix},quad
I_3=\begin{bmatrix}1&0&0\\0&1&0\\0&0&1\end{bmatrix},\quad\\
\cdots
$$

와 같이 표현될 수 있습니다.

두 정사각행렬 $A$, $B$에 대하여

$$AB=BA=I$$

가 성립하면, $B$를 $A$의 역행렬이라고 말하고, $B=A^{-1}$라고 씁니다.
반대로, $A$는 $B$의 역행렬이기도 합니다.
즉 $A=B^{-1}$이기도 합니다.
따라서 $A$의 역행렬이 존재하면

$$AA^{-1}=A^{-1}=I$$

입니다.

<div class="notice--danger">
<b>참고 </b> <br>
    <center>
    두 정사각행렬 $A$, $B$에 대하여 $AB=I$이면 $BA=I$가 성립합니다.
    </center>
<br>
이것은 당연한 말 같아보이기는 해도, 쉽게 증명되지는 않습니다.
뒤에 나오는 정리 16(a)를 사용하면 determinant를 사용하여
<a href="https://math.stackexchange.com/q/852390">증명</a>
할 수 있습니다.
만약, 정사각행렬들의 집합이 algebra over a field 라는 사실을 사용하면 선형대수의 다른 개념들을 많이 사용하지 않고도
<a href="https://math.stackexchange.com/q/3860">증명</a>
할 수 있습니다.
<br>
여하튼, 이것을 정리하면 다음과 같이 쓸 수 있습니다.
    <center>
    두 정사각형 $A$, $B$에 대하여 $AB=I$이면 $B=A^{-1}$ 입니다.
    </center>
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
이때, $AB$의 성분은

$$\left(AB\right)_{ij}=\sum_{k=1}^na_{ik}b_{kj}$$

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
행렬 하나에 대해서도 연산을 정의할 수 있는데, 대표적인 것이 **transpose** (전치)와 **conjugate transpose** (켤레전치)입니다.

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

conjugate transpose에 대해 설명하기 전에 conjugation(켤레복소수화, 공액)에 대해 먼저 이야기하겠습니다.
어떤 복소수 $z=a+bi$에 대하여 ($a$, $b$는 실수) 이 복소수의 켤레복소수는 $a-bi$이고, 이것을 $\bar z$로 표시합니다.
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
두 복소수가 같으려면 실수부분과 허수부분이 서로 같아야 하므로 $b=-b$, $2b=0$, $b=0$입니다.
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
<!-- 복소수로 이루어진 행렬 $A$를 $A=\left(a_{ij}\right)_{m\times n}$으로 표현하겠습니다. -->
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

한편, 정리 2에 따르면 실수로 이루어진 행렬이면 $A$에 대하여 transpose를 취하는 것과 conjugate transpose를 취하는 것에는 차이가 없습니다 ; 

$$
A^H=\overline{\left(a_{ij}\right)^T}
=\overline{\left(a_{ji}\right)_{n\times n}}
=\left(\overline{a_{ij}}\right)_{n\times n}
=\left(a_{ji}\right)_{n\times n}
=A^T
$$

또한, 두 행렬 $A$, $B$의 곱 $AB$에 대하여 transpose나 conjugation을 취한 결과는 각 행렬을 transpose 혹은 conjugation한 후 순서를 바꾸어 얻은 결과와 같습니다 ;

$$
%\begin{align*}
\left((AB)^T\right)_{ij}
=\left(AB\right)_{ji}
=\sum_{k=1}^na_{jk}b_{ki}
=\sum_{k=1}^m{B^T}_{ik}{A^T}_{kj}
=\left(B^TA^T\right)_{ij}
%\end{align*}
$$

이상을 정리하면 다음과 같습니다.

<div class="notice--info">
<b> 정의 3 : 행렬의 연산 </b> <br>
정사각행렬 $A=\left(a_{ij}\right)_{n\times n}$, $B=\left(b_{ij}\right)_{n\times n}$와 실수 $c$에 대하여
<br>
(a) $A+B=\left(a_{ij}+b_{ij}\right)_{n\times n}$
<br>
(b) $A-B=\left(a_{ij}-b_{ij}\right)_{n\times n}$
<br>
(c) $AB=\left(\sum_{k=1}^na_{ik}b_{kj}\right)_{n\times n}$
<br>
(d) $cA=\left(ca_{ij}\right)_{n\times n}$
<br>
(e) $A^T=\left(a_{ji}\right)_{n\times n}$
<br>
(f) $$A^H=\left(\overline{a_{ji}\,}\right)_{n\times n}$
</div>

<!-- (a) $A+B=\left(a_{ij}+b_{ij}\right)_{n\times n}$
<br>
(b) $A-B=\left(a_{ij}-b_{ij}\right)_{n\times n}$
<br>
(c) $AB=\left(\sum_{k=1}^na_{ik}b_{kj}\right)_{n\times n}$
<br>
(d) $cA=\left(ca_{ij}\right)_{n\times n}$
<br>
(e) $A^T=\left(a_{ji}\right)_{n\times n}$
<br>
(f) $A^H=\left(\overline{a_{ji}\,}\right)_{n\times n}$
<br> -->

<div class="notice">
<b> 성질 4 </b> <br>
정사각행렬 $A=\left(a_{ij}\right)_{n\times n}$, $B=\left(b_{ij}\right)_{n\times n}$에 대하여 <br>
(a) $A$가 실수로 이루어진 행렬이면 $\overline A=A$가 성립하고 그 역도 성립합니다.
<br>
(b) $A$가 실수로 이루어진 행렬이면 $A^T=A^H$가 성립하고 그 역도 성립합니다.
<br>
(c) $(AB)^T=B^TA^T$, $(A^T)^T=A$
<br>
(d) $(AB)^H=B^HA^H$, $(A^H)^H=A$
<br>
(e) $A$, $B$의 역행렬이 존재하면 $(AB)^{-1}=B^{-1}A^{-1}$ 입니다.
</div>

## 1.3 symmetric / Hermitian

이제, 이 포스트에서 목표로 하는 두 명제에 등장하는 두 표현인 'symmetric'과 'Hermitian'을 정의할 수 있습니다.
<!-- transpose와 conjugate transpose를 사용하면, 어떤 행렬에 대하여 symmetric, Hermitian이라는 말이 무엇인지 정의할 수 있습니다. -->

### symmetric 행렬

symmetric 행렬 (symmetric matrix, 대칭 행렬)이란, 행렬의 대각성분들을 기준으로 양옆이 대칭인 행렬을 말합니다.
예를 들어 행렬

$$T=\begin{bmatrix}1&2\\2&3\end{bmatrix}$$

의 대각성분들은 $t_{11}=1$, $t_{22}=3$인데 이것들을 기준으로 양옆이 대칭입니다.
따라서 $T$는 symmetric 행렬입니다.
반면, 행렬

$$P=\begin{bmatrix}1&2\\0&1\end{bmatrix},\qquad Q=\begin{bmatrix}0&1&0\\1&0&0\end{bmatrix}$$

는 대각성분들을 기준으로 대칭이 아니므로 symmetric 행렬이 아닙니다.
$Q$와 같은 $2\times 3$ 행렬은 어떻게 해도 symmetric하지 않습니다.
즉, symmetric 행렬이 되기 위해서는 일단 그 행렬이 정사각행렬일 필요가 있습니다..

행렬의 symmetricity는 transpose를 사용하면 쉽게 정의할 수도 있습니다.

**정의 5**\\
행렬 $A$에 대하여 $A^T=A$이면 $A$를 symmetric 행렬이라고 부릅니다.
{: .notice--info}

### Hermitian 행렬

한편, Hermitian 행렬(Hermitian matrix, 에르미트 행렬)이란, 대각선을 기준으로 양옆이 서로 켤레관계인 행렬을 말합니다.
이것을 conjugate transpose로 표현하면 다음과 같이 간단하게 정의할 수 있습니다.

**정의 6**\\
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

으로, $x$의 길이는

$$
\sqrt{\sum_{k=1}^n{x_k}^2}
$$

으로 정할 수 있을 것입니다.

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

한편, $x$의 크기는 $x$와 그 자신의 내적, 즉 $x^Tx$에 루트를 씌운 값과 같습니다;

$$
\sqrt{x^Tx}=\sqrt{x_1\,^2+x_2\,^2+\cdots+x_n}\,^2=\sqrt{\sum_{k=1}^n{x_k}^2}
$$

이 포스트에서는 내적을 표현할 때 $x\cdot y$라는 표현 대신 $\langle x,y\rangle$라는 표현을 쓰겠습니다.
또한 $x$의 크기는 $||x||$로 표시하며, '크기'라는 표현 대신 'norm'이라는 표현을 사용하겠습니다.

<div class="notice--info">
<b> 정의 7 </b> <br>
(a) $n$차원 실수 벡터 $x$, $y$에 대하여 $x$와 $y$의 내적은

$$\langle x,y\rangle=x^Ty$$

입니다.
<br>
(b) $n$차원 실수 벡터 $x$의 norm은

$$||x||=\sqrt{\langle x,x\rangle}=\sqrt{x^Tx}$$

입니다.
</div>

### orthogonal / orthonormal

고등학교 수학에서, 영벡터가 아닌 두 벡터가 서로 **수직(orthogonal)**이면 그 내적이 0이며, 그 역도 성립한다는 것을 다룹니다.

예를 들어, 세 개의 2차원 벡터 $u_1$, $u_2$, $u_3$가

$$
u_1=\begin{bmatrix}1\\-2\end{bmatrix},\quad
u_2=\begin{bmatrix}2\\1\end{bmatrix},\quad
u_3=\begin{bmatrix}1\\0\end{bmatrix}
$$

이면

![diagonalization_1-4-1]({{site.url}}\images\2023-03-01-diagonalization\diagonalization_1-4-1.png){: .img-50-center}

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

![diagonalization_1-4-2]({{site.url}}\images\2023-03-01-diagonalization\diagonalization_1-4-2.png){: .img-100-center}

$v_1$와 $v_2$, $v_1$와 $v_3$, $v_2$와 $v_3$는 모두 서로 수직입니다($v_1\perp v_2$, $v_1\perp v_3$, $v_2\perp v_3$);

$$
\begin{align*}
{v_1}^Tv_2&=\begin{bmatrix}1&-2&0\end{bmatrix}\begin{bmatrix}2\\1\\0\end{bmatrix}=0\\
{v_1}^Tv_3&=\begin{bmatrix}1&-2&0\end{bmatrix}\begin{bmatrix}0\\0\\1\end{bmatrix}=0\\
{v_2}^Tv_3&=\begin{bmatrix}2&1&0\end{bmatrix}\begin{bmatrix}0\\0\\1\end{bmatrix}=0
\end{align*}
$$

이때, $v_1$, $v_2$, $v_3$의 경우처럼 벡터들이 모두 서로 수직일때, 이 벡터들이 pairwisely orthogonal (mutually orthogonal) 하다고 말합니다.
위의 예에서 $u_1$, $u_2$, $u_3$는 pairwisely orthogonal하지 않고, $v_1$, $v_2$, $v_3$는 pairwisely orthogonal합니다.

$v_1$, $v_2$, $v_3$를 조금 변형해서 $w_1$, $w_2$, $w_3$를 다음과 같이 만들면

$$
w_1=\begin{bmatrix}\frac1{\sqrt5}\\-\frac2{\sqrt5}\\0\end{bmatrix},\quad
w_2=\begin{bmatrix}\frac2{\sqrt5}\\\frac1{\sqrt5}\\0\end{bmatrix},\quad
w_3=\begin{bmatrix}0\\0\\1\end{bmatrix}
$$

이 경우에도 $w_1\perp u_2$, $w_1\perp w_3$, $w_2\perp w_3$가 성립합니다.
즉 $w_1$, $w_2$, $w_3$은 pairwisely orthogonal합니다.
여기에 더해, 그 벡터들의 크기가 1이라는 성질이 있습니다;

$$
\begin{align*}
||w_1||&=\sqrt{\left(\frac1{\sqrt5}\right)^2+\left(-\frac2{\sqrt5}\right)^2+0^2}=1\\
||w_2||&=\sqrt{\left(\frac2{\sqrt5}\right)^2+\left(\frac1{\sqrt5}\right)^2+0^2}=1\\
||w_3||&=\sqrt{0^2+0^2+1^2}=1
\end{align*}
$$

이런 경우에, 이 벡터들이 orthonormal하다고 말합니다.
<!-- 즉, $u_1$, $u_2$, $u_3$와 $v_1$, $v_2$, $v_3$는 orthonormal하지 않고, $w_1$, $w_2$, $w_3$는 orthonormal한 것입니다. -->

<!-- 정리하면 다음과 같이 정의할 수 있습니다.
- $x_1$, $x_2$, $\cdots$, $x_n$가 모두 서로 수직이면 $x_1$, $x_2$, $\cdots$, $x_n$가 pairwisely orthogonal하다고 합니다.
- $x_1$, $x_2$, $\cdots$, $x_n$가 모두 서로 수직이고, $||x_1||=1$, $||x_2||=1$, $\cdots$, $||x_n||=1$이면 $x_1$, $x_2$, $\cdots$, $x_n$가 orthonormal하다고 합니다. -->

정리하면 다음과 같습니다.

<div class="notice--info">
<b> 정의 8 </b> <br>
(a) 두 실수 벡터 $x$, $y$에 대하여

$$x^Ty=0$$

이면 두 벡터가 orthogonal 하다(수직이다)고 말하고, $x\perp y$라고 표현합니다.
<br>
(b) $n$개의 실수 벡터 $x_1$, $x_2$, $\cdots$, $x_n$에 대하여

$${x_i}^Tx_j=0\quad(i\neq j)$$

이면, 이 벡터들이 pairwisely orthogonal하다고 말합니다.
<br>
(c) $n$개의 실수 벡터 $x_1$, $x_2$, $\cdots$, $x_n$에 대하여

$$
{x_i}^Tx_j=
\begin{cases}0&(i\neq j)\\1&(i=j)\end{cases}
$$

이면, 이 벡터들이 orthonormal하다고 말합니다.
</div>

<!-- 위의 두 조건 (a), (b)를 다음과 같이 간단하게 적을 수도 있습니다.

$$
\begin{align*}
(a)\:\:{x_i}^Tx_j&=0\quad(i\neq j)\\
(b)\:\:{x_i}^Tx_j&=\begin{cases}0&(i\neq j)\\1&(i=j)\end{cases}
\end{align*}
$$ -->

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
재밌는 사실은, 이 아홉 개의 계산을 하나의 행렬곱으로 표현할 수 있다는 것입니다.
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
일반적으로, 정사각행렬 $A$가 pairwisely orthogonal한 벡터들을 가로로 나열한 행렬이면, $A^TA$는 대각행렬입니다.

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
이때, $W$와 같은 행렬을 **orthogonal 행렬**이라고 합니다.
<!-- 즉, orthonormal한 열벡터들이 가로로 나열되어 있는 정사각행렬을 orthogonal 행렬이라고 합니다. -->

<div class="notice--info">
<b> 정의 9 </b> <br>
정사각행렬 $A$가

$$A^TA=I$$

를 만족시키면 $A$를 orthogonal 행렬(orthogonal matrix, 직교행렬)이라고 부릅니다.
</div>

$w_1$, $w_2$, $w_3$와 $W$ 사이의 관계에서 볼 수 있듯 다음의 성질 9(a), 9(b)가 성립합니다.
또한, 1.1의 두번째 참고에 의해 성질 9(c)가 성립합니다.

<div class="notice">
<b>성질 10 </b> <br>
(a) $n$차원의 orthonormal한 실수벡터들 $n$개를 가로로 나열해서 얻은 행렬은 orthogonal 합니다.
<br>
(b) $A$가 orthogonal 행렬이면 $A$의 각 열들은 orthonormal 합니다.
<br>
(c) $A$가 orthogonal 행렬이면, $A$의 역행렬은 $A$의 transpose와 같습니다 ;
$$A^{-1}=A^T$$
</div>

<div class="notice--danger">
<b> 주의 </b> <br>
이 포스트에서 orthogonal이라는 말은 두 가지 의미를 가집니다.
두 의미를 혼동하지 않고 잘 사용해야 합니다.
<ul>
    <li> 두 벡터가 orthogonal한 것은 두 벡터를 내적했을 때 0이 된다는 뜻입니다.</li>
    <li> 어떤 정사각행렬이 orthogonal한 것은 역행렬과 transpose가 일치한다는 뜻입니다.</li>
</ul>
</div>

### unitary 행렬

지금까지 정의한 내적, norm, orthogonality 등은 성분이 실수인 벡터 혹은 행렬에 대한 개념입니다.
일반적으로, 성분이 복소수인 벡터 혹은 행렬(복소 벡터, 복소 행렬)에 대해 생각한다면, 그에 따른 내적, norm, orthogonality 등의 개념은 실수일 때와는 조금 다르게 정의됩니다.

<div class="notice--info">
<b> 정의 11 </b> <br>
(a) $n$차원 복소 벡터 $x$, $y$에 대하여 $x$와 $y$의 내적 $\langle x,y\rangle$은

$$\langle x,y\rangle=x^Hy$$

입니다.
<br>
(b) $n$차원 복소 벡터 $x$의 norm $||x||$은

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
&=\overline{x_1}y_1+\overline{x_2}y_2+\cdots+\overline{x_n}y_n=\sum_{k=1}^n\overline{x_k}y_k\\
||x||
&=\sqrt{|x_1|^2+|x_n|^2+\cdots+|x_n|^2}=\sqrt{\sum_{k=1}^n|x_k|^2}
\end{align*}
$$

인 것입니다.
$\left(|z|=\sqrt{z\bar z},\quad|a+bi|=\sqrt{a^2+b^2}\right)$
예를 들어, 벡터 $u_1$, $u_2$가

$$
u_1=\begin{bmatrix}1+2i\\2-i\end{bmatrix},\quad
u_2=\begin{bmatrix}3\\1-i\end{bmatrix}
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

위와 같이 정의한 내적을 이용해 복소벡터의 수직(orthogonality)의 개념도 정의할 수 있습니다.

<div class="notice--info">
<b> 정의 12 </b> <br>
(a) 두 복소 벡터 $x$, $y$에 대하여 

$$x^Hy=0$$

이면 두 벡터가 서로 수직(orthogonal)이라고 말하고, $x\perp y$ 라고 씁니다.
<br>
(b) $n$개의 복소 벡터 $x_1$, $x_2$, $\cdots$, $x_n$에 대하여

$$x_i\,^Hx_j=0\quad(i\neq j)$$

이면 이 벡터들이 pairwisely orthogonal하다고 말합니다.
<br>
(c) $n$개의 복소 벡터 $x_1$, $x_2$, $\cdots$, $x_n$에 대하여

$$x_i\,^Hx_j=
\begin{cases}
0\quad(i\neq j)\\
1\quad(i=j)
\end{cases}
$$

이면 이 벡터들이 orthonormal하다고 말합니다.
</div>

즉,

$$
u_1=\begin{bmatrix}1+2i\\2-i\end{bmatrix},\quad
u_2=\begin{bmatrix}3\\1-i\end{bmatrix}
$$

는 pairwisely orthogonal 하지도, orthonormal하지도 않습니다.
반면,

$$
v_1=\begin{bmatrix}3-i\\i\end{bmatrix},\quad
v_2=\begin{bmatrix}1-i\\-2-4i\end{bmatrix}
$$

는 pairwisely orthogonal 하지만, orthonormal하지는 않습니다;

<!-- $$
\begin{align*}
v_1\,^Hv_2
&=\begin{bmatrix}3+i&(-i)\end{bmatrix}\begin{bmatrix}1-i\\-2-4i\end{bmatrix}\\
&=(3+i)(1-i)+(-i)(-2-4i)=0
\end{align*}
$$

만약, 가능한 모든 $v_i$에 대하여 내적하여 결과를 내면 -->

$$
\begin{align*}
v_1\,^Hv_1&=\sqrt{11}    &v_1\,^Hv_2&=0\\
v_2\,^Hv_1&=0            &v_2\,^Hv_2&=\sqrt{22}
\end{align*}
$$

입니다.
따라서 두 열벡터 $v_1$과 $v_2$를 좌우로 나열하여 행렬

$$V=\begin{bmatrix}|&|\\v_1&v_2\\|&|\end{bmatrix}$$

를 만들면

$$V^HV=\begin{bmatrix}\sqrt{11}&0\\0&\sqrt{22}\end{bmatrix}$$

가 성립합니다.

이번에는 $v_1$, $v_2$를 조금 변형하여

$$
w_1=\begin{bmatrix}\frac3{\sqrt{11}}-\frac1{\sqrt{11}}i\\\frac1{\sqrt{11}}i\end{bmatrix},\quad
w_2=\begin{bmatrix}\frac1{\sqrt{22}}-\frac1{\sqrt{22}}i\\-\frac2{\sqrt{22}}-\frac4{\sqrt{22}}i\end{bmatrix}
$$

를 만들면, $w_1$, $w_2$는 orthonormal하고

$$
\begin{align*}
w_1\,^Hw_1&=1 &w_1\,^Hw_2&=0\\
w_2\,^Hw_1&=0 &w_2\,^Hw_2&=1
\end{align*}
$$

입니다.
행렬 $W$를

$$W=\begin{bmatrix}|&|\\w_1&w_2\\|&|\end{bmatrix}$$

로 두면

$$W^HW=I$$

가 성립합니다.

이때 $W$와 같은 행렬을 **unitary 행렬**이라고 부릅니다.

<div class="notice--info">
<b> 정의 13 </b> <br>
복소수를 성분으로 가지는 정사각행렬 $A$가

$$A^HA=I$$

를 만족시키면 $A$를 unitary 행렬(unitary matrix, 유니터리 행렬)이라고 부릅니다.
</div>

$w_1$, $w_2$, $w_3$와 $W$ 사이의 관계에서 볼 수 있듯 다음의 성질 14(a), 14(b)가 성립합니다.
또한, 1.1의 두번째 참고에 의해 성질 14(c)가 성립합니다.

<div class="notice">
<b>성질 14 </b> <br>
(a) $n$차원의 orthonormal한 복소 벡터들 $n$개를 가로로 나열해서 얻은 행렬은 unitary 합니다.
<br>
(b) $A$가 unitary 행렬이면 $A$의 각 열들은 orthonormal 합니다.
<br>
(c) $A$가 unitary 행렬이면, $A$의 역행렬은 $A$의 conjugate transpose와 같습니다 ;
$$A^{-1}=A^H$$
</div>

<div class="notice--danger">
<b> 참고 </b> <br>
$A^TA=I$를 만족시키는 실수 행렬을 orthogonal 행렬이라고 했었습니다.
그리고 $A^HA=I$를 만족시키는 복소 행렬을 unitary 행렬이라고 했습니다.

따라서, 모든 orthogonal 행렬은 unitary 행렬이기도 합니다.
$A$가 orthogonal 행렬이면, $A$의 모든 성분들은 실수이고 $A^TA=I$입니다.
그러면, 성질 3(a)에 의해

$$A^HA=A^TA=I$$

이기 때문입니다.
</div>

## 1.5 eigenvalue / eigenvector

어떤 행렬을 대각화할 때 반드시 등장하게 되는 eigenvalue, eigenvector에 대해 적어보았습니다.
eigenvalue를 계산할 때, 많은 경우에 **행렬식(determinant)**이 사용되므로 이에 대해 먼저 이야기했습니다.
하지만, 행렬식에 대해 말하려면 복잡하면서도 기본적인 설명들이 많이 들어갈 수밖에 없습니다.
아래의 '행렬식' 단락을 이해하는 것이 힘들면, 정리 16 정도만 인정하고 넘어가도 이 포스트의 뒷부분을 이해하는 데에는 문제가 없을 것 같습니다.

고등학교 수학에서 행렬식의 개념에 대해 다룹니다.
행렬

$$A=\begin{bmatrix}a&b\\c&d\end{bmatrix}$$

의 행렬식 $D=ad-bc$가 0이면 역행렬이 존재하지 않고, 0이 아니면 역행렬이 존재한다는 것입니다.
이 포스트에서는 $A$의 행렬식을 $\text{det}(A)$ (또는 $\text{det}\;A$)로 적으려 합니다.
지금까지 써왔던 $A$의 표현식

$$A=\begin{bmatrix}a_{11}&a_{12}\\a_{21}&a_{22}\end{bmatrix}$$

으로 나타내면

$$\text{det}A = a_{11}a_{22}-a_{12}a_{21}$$

이 됩니다.
또한, 흔히 대학 1학년 수준의 미적분학에 보면 $3\times3$ 행렬

$$A=\begin{bmatrix}a_{11}&a_{12}&a_{13}\\a_{21}&a_{22}&a_{23}\\a_{31}&a_{32}&a_{33}\end{bmatrix}$$

에 대한 행렬식이

$$
\begin{multline*}
\text{det}A
= a_{11}a_{22}a_{33}-a_{11}a_{23}a_{32}-a_{12}a_{21}a_{33}
+a_{12}a_{23}a_{31}-a_{13}a_{21}a_{32}+a_{13}a_{22}a_{31}
\end{multline*}
$$

라는 것을 다루기도 합니다.
일반적인 행렬식에 대해 정의하고 논의하려면 먼저 permutation(순열)에 대해 말해야합니다.
여기서 말하는 순열은 고등학교 수학에서 다루는 $_5P_3=5\times4\times3=60$와 는 조금 다릅니다.

### permutation
중학교 수학(혹은 고등학교 수학)에서 **함수**란 두 집합 $X$, $Y$가 주어졌을 때

$X$의 모든 원소 $x\in X$에 대하여 $Y$의 한 원소 $f(x)$에 대응시키는 것
{: .text-center}

을 말합니다.
이때, $X$를 정의역(domain), $Y$를 공역(codomain)이라고 부릅니다.
예를 들어, 두 집합 $X=\\{a,b,c\\}$, $Y=\\{1,2,3\\}$에 대하여
$a$를 $1$로 대응시키고, $b$를 $3$으로 대응시키고 $c$도 3으로 대응시키는 함수를 $f$라고 하면,

$$
\begin{align*}
f(a)&=1\\
f(b)&=3\\
f(c)&=3
\end{align*}
$$

로 표현할 수 있고, 아래의 (1)번 그림으로도 나타낼 수 있습니다.

![diagonalization_1-5-1]({{site.url}}\images\2023-03-01-diagonalization\diagonalization_1-5-1.png)
<!-- {: .img-100-center} -->

이 그림의 (2)번은 $a$가 3으로 대응되고 $b$가 2로 대응되었으나, $c$는 어디에도 대응되지 않았기 때문에 함수라고 할 수 없습니다.
(3)번 또한, $a$가 서로 다른 두 개의 $Y$의 원소 1, 2에 대응되었으므로 이것도 함수라고 할 수 없습니다.

함수 중에서

$x_1\ne x_2$이면 $f(x_1)\ne f(x_2)$이다.
{: .text-center}

를 만족시키키는 함수를 일대일함수(one-to-one function, injection)라고 합니다.
또한, 일대일함수 중에서

모든 $y\in Y$에 대하여 $y=f(x)$를 만족시키는 $x$가 적어도 하나 존재한다.
{: .text-center}

라는 조건을 만족시키는 함수를 일대일대응(one-to-one correspondence, bijection)이라고 합니다.

예를 들어, 아래 그림에서 (가)는 함수라고 할 수 없고 (나), (다), (라)는 함수라고 할 수 있는데, 그중 (나)는 $a\ne b$인데도 불구하고 $f(a)=f(b)$이므로 일대일함수가 아닙니다.
하지만 (다), (라)는 일대일함수 조건을 만족하므로 일대일함수입니다.
(다), (라) 중에서는 (라)가 일대일대응 조건을 만족시킵니다.
$1\in Y$은 $f(c)=1$을 만족시키는 $c\in X$가 존재하고, 
$2\in Y$은 $f(b)=2$을 만족시키는 $b\in X$가 존재하며,
$3\in Y$은 $f(a)=3$을 만족시키는 $a\in X$가 존재하기 때문입니다.
그런데 (다)의 경우에는 $4\in Y$가 $f(x)=4$를 만족시키는 $x\in X$가 존재하지 않기 때문에 일대일대응이 아닙니다.

![diagonalization_1-5-2]({{site.url}}\images\2023-03-01-diagonalization\diagonalization_1-5-2.png)

이제 **permutation(순열)**을 정의할 수 있습니다.
$n$이 자연수일 때, 정의역과 공역이 모두 $\mathbb N_n=\\{1,2,\cdots,n\\}$인 일대일대응을 permutation이라고 합니다.

예를 들어 $n=3$인 permutation들은 아래와 같습니다.

![diagonalization_1-5-2]({{site.url}}\images\2023-03-01-diagonalization\diagonalization_1-5-3.png)

일반적으로 $n$의 permutation의 개수는 $n!$ 개일 것입니다.
따라서, $n=3$인 permutation들의 개수는 $3!=6$ 개이므로, 위의 그림은 모든 permutation들을 다 나타낸 셈입니다.

$n$의 permutation들의 집합을 $S_n$이라고 표기하겠습니다.
이 집합은 **symmetric group(대칭군)**이라는 이름을 가지고 있습니다.

$\sigma$가 permutation일 때, $\sigma$를 표현하는 방법은 다양하지만, 그 중 가장 간단한 방법은 $\sigma(1)$, $\sigma(2)$, $\cdots$, $\sigma(3)$를 단순히 나열하는 것입니다.
예를 들어 위 그림의 첫번째 permutation인 $\sigma_1$은

$$
\begin{cases}
\sigma_1(1)=1\\
\sigma_1(2)=2\\
\sigma_1(3)=3
\end{cases}
$$

을 만족시키므로 $$\sigma_1=123$$으로 나타내는 것입니다.
두번째 permutation인 $\sigma_2$는

$$
\begin{cases}
\sigma_2(1)=1\\
\sigma_2(2)=3\\
\sigma_2(3)=2
\end{cases}
$$

이므로, $\sigma_2=132$라고 간략히 씁니다.
이러한 표기법으로 여섯 개의 permutation $\sigma_i$를 모두 표현하면

$$
\begin{align*}
&\sigma_1=123,\quad&&\sigma_2=132,\quad&&\sigma_3=213, \\
&\sigma_4=231,\quad&&\sigma_5=312,\quad&&\sigma_6=321
\end{align*}
$$

이 됩니다.

이번에는 각각의 permutation들을 even permutation과 odd permutation으로 나누고, permutation $\sigma$의 부호 $\text{sgn}(\sigma)$를 정의하려 합니다.
어떤 permutation $\sigma=abc$에 대하여 $a$, $b$, $c$를 이 permutation의 '성분'이라고 할 때, $\sigma$의 서로다른 두 요소를 바꾸는 것을 '교환'이라고 하겠습니다.
예를 들어 $\sigma=abc$의 첫번째와 두번째 요소를 교환하면 $bac$가 됩니다.
$\sigma=abc$의 두번째 요소와 세번째 요소를 교환하면 $acb$가 됩니다.
이때,
- $\sigma$를 짝수번 교환하여 항등함수를 만들 수 있으면 $\sigma$를 even permutation이라고 합니다.
- $\sigma$를 홀수번 교환하여 항등행렬를 만들 수 있으면 $\sigma$를 odd permutation이라고 합니다.
- 함수 $\text{sgn}:S_n\to\\{1,-1\\}$을 다음과 같이 정의합니다;

$$
\text{sgn}(\sigma)=
\begin{cases}
1&(\sigma : \text{even})\\
-1&(\sigma : \text{odd})
\end{cases}
$$

여기에서 항등함수란, $f(x)=x$인 함수 $f$를 말합니다.
$S_3$에서는 $\sigma_1=123$이 항등함수가 될 것입니다.

예를 들어, $\sigma_1=123$의 경우에는 그 자체로 항등함수이므로 0번 교환하여 항등함수를 만들 수 있고, $0$은 짝수이므로 $\sigma_1$은 even permutation입니다.
따라서, $\text{sgn}(\sigma_1)=1$입니다.

$\sigma_2=132$의 경우에는 $132$의 3과 2를 교환하면 항등함수 $123$를 만들 수 있습니다.
1번 교환하여 항등함수를 만들었고, $1$은 홀수이므로 $\sigma_2$는 odd permutation이며 $\text{sgn}(\sigma_2)=-1$입니다.
사실, $\sigma_2=132$는 1과 3을 교환하여여 $312$를 만들고, 다시 3과 1을 교환하여 $132$로 돌아온 뒤, 3과 2를 교환하여 $123$를 만들 수 있습니다.
이 경우에는 $\sigma_2=132$의 성분을 3번 교환했는데, 그럼에도 불구하고 $\sigma$가 odd permutation이라는 사실은 변하지 않습니다.

$\sigma_4=231$의 경우에는 짝수번 교환해야 항등함수 $\sigma_1=123$이 됩니다.
예를 들어 $\sigma_4=231$의 1과 3을 교환하여 $\sigma_2=213$를 얻고, 다시 1과 2를 교환하여 $\sigma_1=123$을 얻을 수 있기 때문입니다.

$n=3$인 6개의 permutation에 대해서 부호를 계산하면 다음과 같습니다.

$$
\begin{align*}
\text{sgn}(\sigma_1)&=1  &\text{sgn}(\sigma_2)&=-1  &\text{sgn}(\sigma_3)&=-1  \\
\text{sgn}(\sigma_4)&=1  &\text{sgn}(\sigma_5)&=1   &\text{sgn}(\sigma_3)&=-1
\end{align*}
$$

즉, $n=3$인 permutation은 총 6개가 있는데, 그 중 even permutation은 3개, odd permutation은 3개가 있습니다.

<div class="notice--danger">
<b>참고 </b> <br>
(a)
자연수 $n$에 대하여, 모든 permutation들의 집합을 $S_n$이라고 쓰고, 이 집합을 permutation group이라고 부른다고 했었습니다.
모든 even permutation들의 집합은 $A_n$이라고 쓰고, 이 집합을 alternating group이라고 부릅니다.
모든 odd permutation들의 집합은 $S_n-A_n$이 되지만, 이것은 군(group)을 이루지는 않습니다.
<br>
일반적으로, even permutation의 개수와 odd permutation의 개수는 같습니다.
따라서 $n$에 대한 even permutation들의 개수는 $\frac{n!}2$이고, odd permutation들의 개수도 $\frac{n!}2$입니다.
<br>
이에 대한 증명은 꽤 쉽습니다.
odd permutation 중 하나를 골라서 $\beta$라고 하겠습니다.
임의의 even permutation $\alpha\in A_n$에 대하여 $g(\alpha)$를
<br>
$$g(\alpha)=\beta\circ\alpha$$
<br>
로 적습니다.
그러면 $g(\alpha)$는 odd permutation이 되고, 따라서 $g$는 $A_n$에서 $S_n-A_n$으로 가는 함수가 됩니다.
더구나 이 함수 $g$는 일대일대응 조건까지도 만족시킵니다.
따라서 $g$의 정의역인 $A_n$과 $g$의 공역인 $S_n-A_n$은 그 개수가 같습니다.
<br>
(b) permutation의 부호함수 $\text{sgn}$에 대하여 다음과 같은 사실들이 성립합니다.
($\alpha,\beta\in S_n$)
(증명은 생략합니다.)
<ul>
    <li> 함수 $\text{sgn}:S_n\to\{1,-1\}$은 잘 정의된 함수입니다.</li>
    <li> $\text{sgn}(\alpha\circ\beta)=\text{sgn}(\alpha)\text{sgn}(\beta)$</li>
    <li> $\text{sgn}(\alpha\circ\alpha)=1$</li>
    <li> $\text{sgn}(\alpha^{-1})=\text{sgn}(\alpha)$</li>
</ul>
</div>

한편, $n=2$이면 permutation의 개수는 $2!=2$개입니다.
$S_2=\\{\sigma_1,\sigma_2\\}$라고 하면,

$$
\begin{align*}
\sigma_1&=12,\quad&\text{sgn}(\sigma_1)&=1\\
\sigma_2&=21,\quad&\text{sgn}(\sigma_2)&=-1
\end{align*}
$$



<!-- 재밌는 것은, 순열을 행렬로서 표현할 수 있다는 것입니다.
어떤 permutation이 $i\in\{1,2,3\}$을 $j\in\{1,2,3\}$로 대응시켰다면, $3\times3$ 행렬의 $i$행 $j$열 성분에 1을 넣고, 나머지 성분에는 0을 넣는 행렬을 만드는 것입니다.

예를 들어, 위 그림의 첫번째 permuation은 1을 1로, 2는 2로, 3은 3으로 대응시켰습니다.
따라서 $a_{11}=a_{22}=a_{33}=1$이고 나머지 $(i,j)$에 대해서는 $a_{ij}=0$인 행렬

$$
\begin{bmatrix}
1&0&0\\0&1&0\\0&0&1
\end{bmatrix}
$$

을 생각하는 것입니다.
두번째 permutation은 1을 1으로, 2를 3으로, 3을 2로 대응시켰으므로 $a_{11}=a_{23}=a_{32}=1$인 행렬 

$$
\begin{bmatrix}
1&0&0\\0&0&1\\0&1&0
\end{bmatrix}
$$

을 만드는 것입니다.

여섯 개의 permutation 대한 각각의 행렬들은

$$
\begin{gather*}
P_1=
\begin{bmatrix}
1&0&0\\0&1&0\\0&0&1
\end{bmatrix}
,\quad
P_2=
\begin{bmatrix}
1&0&0\\0&0&1\\0&1&0
\end{bmatrix}
,\quad
P_3=
\begin{bmatrix}
0&1&0\\1&0&0\\0&0&1
\end{bmatrix}
\\
P_4=
\begin{bmatrix}
0&1&0\\0&0&1\\1&0&0
\end{bmatrix}
,\quad
P_5=
\begin{bmatrix}
0&0&1\\1&0&0\\0&1&0
\end{bmatrix}
,\quad
P_6=
\begin{bmatrix}
0&0&1\\0&1&0\\1&0&0
\end{bmatrix}
\end{gather*}
$$

입니다.
이 행렬들은 **permuation 행렬** (permuation matrix, 치환 행렬)이라고 불립니다.
이때, permutation $\sigma$와 그에 대응되는 permutation 행렬 $P$에 대해서는 긴밀한 관계가 있습니다.
permutation 행렬은 대응되는 permutation 자체와 같은 것이라고 보겠습니다.
이것은 충분히 말이 되는 이야기입니다.
여섯 개의 permutation 중 첫번째 permutation인 $\sigma_1$는

$$
\begin{align*}
\sigma_1(1)=1\\
\sigma_1(2)=2\\
\sigma_1(3)=3
\end{align*}
$$

를 만족시키는 일대일대응입니다.
그리고 이것은 마치 $\sigma_1$이 벡터
$$\begin{bmatrix}1\\2\\3\end{bmatrix}$$을
$$\begin{bmatrix}1\\2\\3\end{bmatrix}$$로 대응시켰다고 생각할 수 있는데, 정말로 벡터 $$\begin{bmatrix}1\\2\\3\end{bmatrix}$$의 왼쪽에 행렬 $P_1$을 곱하면 $$\begin{bmatrix}1\\2\\3\end{bmatrix}$$가 나오기 때문입니다;

$$
\begin{bmatrix}
1&0&0\\0&1&0\\0&0&1
\end{bmatrix}
\begin{bmatrix}1\\2\\3\end{bmatrix}
=
\begin{bmatrix}1\\2\\3\end{bmatrix}.
$$

마찬가지로 $\sigma_2$에 대해서는

$$
\begin{align*}
\sigma_1(1)=1\\
\sigma_1(2)=3\\
\sigma_1(3)=2
\end{align*}
$$

가 성립하는데 이것은 행렬로

$$
\begin{bmatrix}
1&0&0\\0&1&0\\0&0&1
\end{bmatrix}
\begin{bmatrix}1\\2\\3\end{bmatrix}.
=
\begin{bmatrix}1\\3\\2\end{bmatrix}.
$$

와 같이 표현할 수 있는 것입니다.

이번에는 각각의 permutation들을 even permutation과 odd permutation으로 나누고, permutation $\sigma$의 부호 $\text{sgn}(\sigma)$를 정의하려 합니다.
어떤 permutation $\sigma$의 permutation 행렬이 $P$일 떄,
- $P$의 행을 짝수번 교환하여 항등행렬 $I$을 만들 수 있으면 $\sigma$를 even permutation이라고 합니다.
- $P$의 행을 홀수번 교환하여 항등행렬 $I$를 만들 수 있으면 $\sigma$를 odd permutation이라고 합니다.
- 함수 $\text{sgn}:S_n\to\{1,-1\}$을 다음과 같이 정의합니다;

$$
\text{sgn}(\sigma)=
\begin{cases}
1&(\sigma : \text{even})\\
-1&(\sigma : \text{odd})
\end{cases}
$$

예를 들어, $\sigma_1$의 경우에는 $P_1=I$이므로 $P_1$의 행을 0번 교환하여 $I$를 만들 수 있는데, $0$은 짝수이므로 $\sigma_1$은 even permutation이고, $\text{sgn}(\sigma_1)=1$입니다.

$\sigma_2$의 경우에는 $P_2$의 두번째 행과 세번째 행을 교환하면 $I$를 만들 수 있습니다.
$1$은 홀수이므로 $\sigma_2$는 odd permutation이고 $\text{sgn}(\sigma_2)=-1$입니다.
사실, $P_2$는 첫번째 행과 두번째 행을 교환하여 $P_4$와 같은 형태를 만들고, 다시 첫번째 행과 두번째 행을 교환하여 $P_2$로 돌아온 뒤, 두번째 행과 세번째 행을 교환하여 $I$를 만들 수 있습니다.
이 경우에는 $P_2$의 행을 3번 교환했는데, 그럼에도 불구하고 $\sigma$가 odd permutation이라는 사실은 변하지 않습니다.

$n=3$인 6개의 permutation에 대해서 부호를 계산하면 다음과 같습니다.

$$
\begin{align*}
\text{sgn}(P_1)&=1  &\text{sgn}(P_2)&=-1  &\text{sgn}(P_3)&=-1  \\
\text{sgn}(P_4)&=1  &\text{sgn}(P_5)&=1   &\text{sgn}(P_3)&=-1
\end{align*}
$$

즉, $n=3$인 permutation은 총 6개가 있는데, 그 중 even permutation은 3개, odd permutation은 3개가 있습니다.

<div class="notice--danger">
<b>참고 </b> <br>
자연수 $n$에 대하여, 모든 permutation들의 집합을 $S_n$이라고 쓰고, 이 집합을 permutation group이라고 부른다고 했었습니다.
모든 even permutation들의 집합은 $A_n$이라고 쓰고, 이 집합을 alternating group이라고 부릅니다.
모든 odd permutation들의 집합은 $S_n-A_n$이 되지만, 이것은 군(group)을 이루지는 않습니다.
<br>
일반적으로, even permutation의 개수와 odd permutation의 개수는 같습니다.
따라서 $n$에 대한 even permutation들의 개수는 $\frac{n!}2$이고, odd permutation들의 개수도 $\frac{n!}2$입니다.
<br>
이에 대한 증명은 꽤 쉽습니다.
odd permutation 중 하나를 골라서 $\beta$라고 하겠습니다.
임의의 even permutation $\alpha\in A_n$에 대하여 $g(\alpha)$를
<br>
$$g(\alpha)=\beta\circ\alpha$$
<br>
로 적습니다.
그러면 $g(\alpha)$는 odd permutation이 되고, 따라서 $g$는 $A_n$에서 $S_n-A_n$으로 가는 함수가 됩니다.
더구나 이 함수 $g$는 일대일대응 조건까지도 만족시킵니다.
따라서 $g$의 정의역인 $A_n$과 $g$의 공역인 $S_n-A_n$은 그 개수가 같습니다.
</div>

한편, $n=2$에 대해서도 $\sigma_i$, $P_i$, parity(even/odd) 등에 대해 적으면 다음과 같습니다.
$n=2$일 때 permutation의 개수는 $2!=2$개입니다.
$S_2=\{\sigma_1,\sigma_2\}$라고 하면,

$$
\begin{cases}\sigma_1(1)=1\\\sigma_1(2)=2\end{cases},\qquad
\begin{cases}\sigma_2(1)=2\\\sigma_2(2)=1\end{cases}
$$

이고,

$$
P_1=\begin{bmatrix}1&0\\0&1\end{bmatrix},\qquad
P_2=\begin{bmatrix}0&1\\1&0\end{bmatrix}
$$

이며,

$$
\text{sgn}(\sigma_1)=1,\qquad \text{sgn}(\sigma_2)=-1
$$

입니다. -->


### 행렬식

이제 행렬식을 정의할 수 있습니다.

<div class="notice--info">
<b> 정의 15 </b> <br>
$n\times n$ 정사각행렬 $A$에 대하여 행렬식 $\text{det}(A)$를

<!-- $$
A
=\begin{bmatrix}
a_{11}&\cdots&a_{1n}\\
\vdots&\ddots&\vdots\\
a_{n1}&\cdots&a_{nn}
\end{bmatrix}
$$

에 대하여  -->

$$\text{det}(A)=\sum_{\sigma\in S_n}\prod_{i=1}^n\text{sgn}(\sigma)a_{i,\sigma(i)}$$

로 정의합니다.
</div>

여기에서 $\prod$는 곱의 기호입니다.
이것은 합의 기호 $\sum$과 비슷하게 쓰입니다.
예를 들어 1, 2, $\cdots$, $n$을 차례로 더하는 것을

$$\sum_{k=1}^nk=1+2+\cdots+n=\frac{n(n+1)}2$$

와 같이 표현하듯이, 차례로 곱하는 것은

$$\prod_{k=1}^nk=1\times2\times\cdots\times n=n!$$

과 같이 표현됩니다.
더 예를 들면 다음과 같습니다.
등차수열 $a_k=2k$를 차례로 더하거나 곱하면

$$
\begin{align*}
\sum_{k=1}^n2k&=2\sum_{k=1}^nk=n(n+1)\\
\prod_{k=1}^n2k&=\left(\prod_{k=1}^n2\right)\left(\prod_{k=1}^nk\right)=2^n\times n!
\end{align*}
$$

이 되고, 등비수열 $b_k=2^k$를 차례로 더하거나 곱하면

$$
\begin{align*}
\sum_{k=1}^n2^k&=\frac{2(2^n-1)}{2-1}=2(2^n-1)\\
\prod_{k=1}^n2^k&=2^{1+2+\cdots+n}=2^{\frac{n(n+1)}2}
\end{align*}
$$

가 됩니다.

정의 15의 식은 복잡해보이지만, 잘 풀어보면 위에서 알아본 $2\times2$ 행렬에서의 $\text{det}A = a_{11}a_{22}-a_{12}a_{21}$와 $3\times3$ 행렬에서의

$$\text{det}A = a_{11}a_{22}a_{33}-a_{11}a_{23}a_{32}-a_{12}a_{21}a_{33}+a_{12}a_{23}a_{31}-a_{13}a_{21}a_{32}+a_{13}a_{22}a_{31}$$

에 대응되는 식임을 확인할 수 있습니다.

$2\times2$ 행렬의 경우를 먼저 보면, $S_2$의 원소의 개수는 2개이고 $(S_2=\\{\sigma_1,\sigma_2\\})$

$$
\begin{align*}
\sigma_1&=12,\quad&\text{sgn}(\sigma_1)&=1\\
\sigma_2&=21,\quad&\text{sgn}(\sigma_2)&=-1
\end{align*}
$$

였으므로

$$
\begin{align*}
\text{det}(A)
&=\sum_{\sigma\in S_2}\prod_{i=1}^2\text{sgn}(\sigma)a_{i,\sigma(i)}\\
&=\prod_{i=1}^2\text{sgn}(\sigma_1)a_{i,\sigma_1(i)}
+\prod_{i=1}^2\text{sgn}(\sigma_2)a_{i,\sigma_2(i)}\\
&=a_{1,\sigma_1(1)}a_{2,\sigma_1(2)}-a_{1,\sigma_2(1)}a_{2,\sigma_2(2)}\\
&=a_{11}a_{22}-a_{12}a_{21}
\end{align*}
$$

인 것입니다.

$3\times3$ 행렬의 경우에도
<!-- 마찬가지로, $n=3$의 경우, $|S_3|=6$이었고, -->

$$
\begin{align*}
\sigma_1&=12,\quad&\text{sgn}(\sigma_1)&=1\\
\sigma_2&=21,\quad&\text{sgn}(\sigma_2)&=-1
\end{align*}
$$

$$
\begin{align*}
\sigma_1&=123,\quad&\text{sgn}(\sigma_1)&=1\\
\sigma_2&=132,\quad&\text{sgn}(\sigma_2)&=-1\\
\sigma_3&=213,\quad&\text{sgn}(\sigma_3)&=-1\\
\sigma_4&=231,\quad&\text{sgn}(\sigma_4)&=1\\
\sigma_5&=312,\quad&\text{sgn}(\sigma_5)&=1\\
\sigma_6&=321,\quad&\text{sgn}(\sigma_6)&=-1
\end{align*}
$$
<!-- $$
\begin{align*}
&
\begin{cases}\sigma_1(1)=1\\\sigma_1(2)=2\\\sigma_1(3)=3\end{cases},
\qquad
\begin{cases}\sigma_2(1)=1\\\sigma_2(2)=3\\\sigma_2(3)=2\end{cases},
\qquad
\begin{cases}\sigma_1(1)=2\\\sigma_3(2)=1\\\sigma_3(3)=3\end{cases},
\\[10pt]
&
\begin{cases}\sigma_4(1)=2\\\sigma_4(2)=3\\\sigma_4(3)=1\end{cases},
\qquad
\begin{cases}\sigma_5(1)=3\\\sigma_5(2)=1\\\sigma_5(3)=2\end{cases},
\qquad
\begin{cases}\sigma_6(1)=3\\\sigma_6(2)=2\\\sigma_6(3)=1\end{cases},
\\[20pt]
&
\text{sgn}(\sigma_1)=1,\qquad
\text{sgn}(\sigma_2)=-1,\qquad
\text{sgn}(\sigma_3)=-1\\[10pt]
&
\text{sgn}(\sigma_4)=1,\qquad
\text{sgn}(\sigma_5)=1\quad
\text{sgn}(\sigma_6)=-1
\end{align*}
$$ -->

이었기 때문에

$$
\begin{align*}
\text{det}(A)
=&\sum_{\sigma\in S_3}\prod_{i=1}^3\text{sgn}(\sigma)a_{i,\sigma(i)}\\
=&\prod_{i=1}^3\text{sgn}(\sigma_1)a_{i,\sigma_1(i)}
+\prod_{i=1}^3\text{sgn}(\sigma_2)a_{i,\sigma_2(i)}
+\prod_{i=1}^3\text{sgn}(\sigma_3)a_{i,\sigma_3(i)}\\
&+\prod_{i=1}^3\text{sgn}(\sigma_4)a_{i,\sigma_4(i)}
+\prod_{i=1}^3\text{sgn}(\sigma_5)a_{i,\sigma_5(i)}
+\prod_{i=1}^3\text{sgn}(\sigma_6)a_{i,\sigma_6(i)}\\
=&a_{1,\sigma_1(1)}a_{2,\sigma_1(2)}a_{3,\sigma_1(3)}
-a_{1,\sigma_2(1)}a_{2,\sigma_2(2)}a_{3,\sigma_2(3)}
-a_{1,\sigma_3(1)}a_{2,\sigma_3(2)}a_{3,\sigma_3(3)}\\
&+a_{1,\sigma_4(1)}a_{2,\sigma_4(2)}a_{3,\sigma_4(3)}
+a_{1,\sigma_5(1)}a_{2,\sigma_5(2)}a_{3,\sigma_5(3)}
-a_{1,\sigma_6(1)}a_{2,\sigma_6(2)}a_{3,\sigma_6(3)}\\
=&a_{11}a_{22}a_{33}
-a_{11}a_{23}a_{32}
-a_{12}a_{21}a_{33}\\
&+a_{12}a_{23}a_{31}
+a_{13}a_{21}a_{32}
-a_{13}a_{22}a_{31}
\end{align*}
$$

이 됩니다.

<!-- 한편, 행렬식의 정의에 따르면 임의의 $n$에 대하여 $\text{det}(I)=1$입니다. -->

행렬식에 대하여 앞으로 사용될 사실은 다음의 두 명제입니다.

<div class="notice--success">
<b> 정리 16 </b> <br>
(a) 정사각행렬 $A$, $B$에 대하여
$$\text{det}(AB)=\text{det}(A)\text{det}(B)$$
입니다.
<br>
(b) 정사각행렬 $A$에 대하여 $A$의 역행렬이 존재하기 위한 필요충분조건은 $\text{det}(A)\neq0$인 것입니다.
</div>

**증명 : 정의 16(a)**
{: .notice--warning}

아래 증명은 이 [증명](https://math.stackexchange.com/q/302089)에서 오타로 보이는 것을 수정하고, 설명을 덧붙인 것입니다.

$$
\begin{align*}
\text{det}(AB)
&=\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^n(AB)_{k,\sigma(k)}\\
&=\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^n\left(\sum_{i=1}^nA_{ki}B_{i,\sigma(k)}\right)\\
&=\sum_{\sigma\in S_n}\text{sgn}(\sigma)\left(\sum_{f:\mathbb N_n\to\mathbb N_n}\prod_{k=1}^nA_{k,f(k)}B_{f(k),\sigma(k)}\right)\\
&=\sum_{\sigma\in S_n}\sum_{f:\mathbb N_n\to\mathbb N_n}\text{sgn}(\sigma)\prod_{k=1}^nA_{k,f(k)}B_{f(k),\sigma(k)}\\
&=\sum_{f:\mathbb N_n\to\mathbb N_n}\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^nA_{k,f(k)}B_{f(k),\sigma(k)}\\
&=\sum_{f:\mathbb N_n\to\mathbb N_n}\sum_{\sigma\in S_n}\text{sgn}(\sigma)\left(\prod_{k=1}^nA_{k,f(k)}\right)\left(\prod_{k=1}^nB_{f(k),\sigma(k)}\right)\\
=&\sum_{f:\mathbb N_n\to\mathbb N_n}\prod_{k=1}^nA_{k,f(k)}\left(\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^nB_{f(k),\sigma(k)}\right)
\end{align*}
$$

위의 계산에서 두번째 줄은 행렬의 곱 $AB$의 성분에 대한 정의를 쓴 것입니다.
세번째 줄에 대한 설명은 다음과 같습니다.

보통 중학교 과정에 있는 내용이지만, $(a_1+a_2)(b_1+b_2)$를 전개한다는 것은

$$(a_1+a_2)(b_1+b_2)=a_1b_1+a_1b_2+a_2b_1+a_2b_2$$

와 같이 쓰는 것입니다.
이것은

$a_1$와 $a_2$ 중에서 하나를 고르고 $b_1$와 $b_2$ 중에서 하나를 고른 뒤 가능한 모든 조합을 더하는 것
{: .text-center}

을 말합니다.
이것을 조금 형식적으로 쓰면,

$f:\\{1,2\\}\to\\{1,2\\}$인 함수 하나를 고르고, 가능한 모든 $a_{f(1)}b_{f(2)}$의 조합을 더하는 것
{: .text-center}

과 정확히 일치합니다.
$f:\\{1,2\\}\to\\{1,2\\}$인 함수는 다음의 네 개 함수입니다.

$$
\begin{align*}
&f_1(1)=1,\quad&&f_2(1)=1,\quad&&f_3(1)=2,\quad&&f_4(1)=2\\
&f_1(2)=1,\quad&&f_2(2)=2,\quad&&f_3(2)=1,\quad&&f_4(2)=2
\end{align*}
$$

따라서, 가능한 모든 $a_{f(1)}b_{f(2)}$의 조합은

$$
a_{f_1(1)}b_{f_1(2)}=a_1b_1,\quad\\
a_{f_2(1)}b_{f_2(2)}=a_1b_2,\quad\\
a_{f_3(1)}b_{f_3(2)}=a_2b_1,\quad\\
a_{f_4(1)}b_{f_4(2)}=a_2b_2,\quad
$$

이라서 이것들을 모두 더하면 $a_1b_1+a_1b_2+a_2b_1+a_2b_2$이 되는 것입니다.

함수 $f:\mathbb N_n\to\mathbb N_n$는 일대일대응인 것 $(f\in S_n)$과 그렇지 않은 것 $(f\not\in S_n)$ 으로 나눌 수 있습니다.

따라서

$$
\begin{align*}
\text{det}(AB)&=P+Q\\
P&=\sum_{f\in S_n}\prod_{k=1}^nA_{k,f(k)}\left(\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^nB_{f(k),\sigma(k)}\right)\\
Q&=\sum_{f:\not\in S_n}\prod_{k=1}^nA_{k,f(k)}\left(\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^nB_{f(k),\sigma(k)}\right)
\end{align*}
$$

로 쓸 수 있습니다.
$Q$를 먼저 계산합시다.
$f$가 일대일대응이 아니면 이것은 일대일함수가 아닙니다.
(항상 그런 것은 아니지만, 이 경우에는 정의역과 공역이 같기 때문에 그렇습니다.)
따라서 $f(k_1)=f(k_2)$인 $k_1\ne k_2$가 존재합니다.
만약, $k_1$과 $k_2$를 바꾸는 교환을 $\alpha$라고 하면, 임의의 $\sigma$에 대하여 $\alpha\circ\sigma\in S_n$이고, $\text{sgn}(\sigma)+\text{sgn}(\alpha\circ\sigma)=0$입니다.
그리고

$$
\prod_{k=1}^nB_{f(k),\sigma(k)}=\prod_{k=1}^nB_{(\alpha\circ f)(k),\sigma(k)}
$$

이기 떄문에, 위의 $Q$ 식에서 괄호친 부분의 두 배는 0이 됩니다;

$$
\begin{align*}
&2\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^nB_{f(k),\sigma(k)}\\
=&\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^nB_{f(k),\sigma(k)}
+\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^nB_{f(k),\sigma(k)}\\
=&\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^nB_{f(k),\sigma(k)}
+\sum_{\sigma\in S_n}\text{sgn}(\alpha\circ\sigma)\prod_{k=1}^nB_{f(k),(\alpha\circ\sigma)(k)}\\
=&\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^nB_{f(k),\sigma(k)}
+\sum_{\sigma\in S_n}\left(-\text{sgn}(\sigma)\right)\prod_{k=1}^nB_{f(k),(\alpha\circ\sigma)(k)}\\
=&0
\end{align*}
$$

따라서 $Q=0$입니다.
한편, $P$를 계산하면

$$
\begin{align*}
P
&=\sum_{f\in S_n}\prod_{k=1}^nA_{k,f(k)}\left(\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^nB_{f(k),\sigma(k)}\right)\\
&=\sum_{f\in S_n}\prod_{k=1}^nA_{k,f(k)}\left(\sum_{\sigma\in S_n}\text{sgn}(\sigma)\prod_{k=1}^nB_{(\sigma^{-1}\circ f)(k),k}\right)\\
&=\sum_{f\in S_n}\prod_{k=1}^nA_{k,f(k)}\left(\sum_{\sigma\in S_n}\text{sgn}(\sigma^{-1})\prod_{k=1}^nB_{(\sigma^{-1}\circ f)(k),k}\right)\\
&=\sum_{f\in S_n}\prod_{k=1}^nA_{k,f(k)}\left(\sum_{\sigma\in S_n}\text{sgn}(\sigma^{-1})\cdot\left(\text{sgn}(f)\right)^2\prod_{k=1}^nB_{(\sigma^{-1}\circ f)(k),k}\right)\\
&=\sum_{f\in S_n}\prod_{k=1}^nA_{k,f(k)}\left(\sum_{\sigma\in S_n}\text{sgn}(\sigma^{-1}\circ f)\cdot\text{sgn}(f)\prod_{k=1}^nB_{(\sigma^{-1}\circ f)(k),k}\right)\\
&=\sum_{f\in S_n}\prod_{k=1}^nA_{k,f(k)}\left(\sum_{\pi\in S_n}\text{sgn}(\pi)\cdot\text{sgn}(f)\prod_{k=1}^nB_{\pi(k),k}\right)\\
&=\left(\sum_{f\in S_n}\text{sgn}(f)\prod_{k=1}^nA_{k,f(k)}\right)\left(\sum_{\pi\in S_n}\text{sgn}(\pi)\prod_{k=1}^nB_{\pi(k),k}\right)\\
&=\text{det}(A)\text{det}(B)
\end{align*}
$$

입니다.
위의 결과를 요약하면

$$
\text{det}(AB)=P+Q=0+\text{det}(A)\text{det}(B)=\text{det}(A)\text{det}(B)
$$

가 됩니다.

**증명 : 정의 16(b)**
{: .notice--warning}

한쪽 방향인

$A$의 역행렬이 존재하면 $\text{det}(A)\neq0$ 입니다.
{: .text-center}

만 증명하고, 반대방향의 증명은 생략합니다.

만약 $A$의 역행렬이 존재하면 $AB=I$를 만족시키는 정사각행렬 $B$가 존재합니다.
그러면 (a)에 의해
$$\text{det}(A)\text{det}(B)=\text{det}(AB)=\text{det}(I)=1$$
입니다.
따라서 $\text{det}(A)=0$이 될 수는 없습니다.

---

### eigenvalue / eigenvector

# 2. 직교대각화

## 2.1. diagonalization

## 2.2. orthogonal / unitary diagonalization

## 2.3. 예시

# 3. 증명

## 3.1. distinct eigenvalues

## 3.2. repeated roots

[1]:{{ site.url }}/assets/pdf/orthogonally_diagonalizable.pdf
