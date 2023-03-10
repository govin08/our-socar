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
예를 들어,

$$A=\begin{bmatrix}1&2\\0&1\end{bmatrix},\qquad B=\begin{bmatrix}0&1&0\\1&0&0\end{bmatrix}$$

는 행렬입니다.
이때, $A$는 2개의 행과 2개의 열로 이루어진 행렬이어서 '$2\times 2$ 행렬'이라고 부르고 $B$는 2개의 행과 3개의 열로 이루어진 행렬이어서 '$2\times3$ 행렬'이라고 부릅니다.

행이 하나인 행렬과 열이 하나인 행렬도 행렬로 취급합니다.
이것들은 각각 '행벡터', '열벡터' 라는 이름으로도 불립니다.
예를 들어

$$C=\begin{bmatrix}2&4\end{bmatrix},\qquad D=\begin{bmatrix}1\\-1\\0\end{bmatrix}$$

이면 $C$는 $1\times2$ 행렬이기도 하지만 2차원의 행벡터라고도 불리고, $D$는 $3\times1$ 행렬이기도 하지만 3차원의 열벡터라고도 불립니다.

<!-- 선형대수를 말할 때 늘 그렇듯이, 이 포스트에서도 벡터는 열벡터로 표시합니다.
그러니까, 고등학교 수학에서는 $v=(2,1)$을 2차원 벡터(평면 벡터), $w=(1,0,3)$을 3차원 벡터로 생각했었습니다.
그런데 선형대수에서는 보통 이것들을 열벡터로 쓰고

$$
v=\begin{bmatrix}2\\1\end{bmatrix},\qquad w=\begin{bmatrix}1\\0\\3
$$ -->

행렬을 대문자 알파벳으로 표시한다면, 이 행렬의 entry는 소문자 알파벳과 두 개의 아래첨자로 표시합니다.
이때 첫번째 아래첨자는 행 번호를, 두번째 아래첨자는 열 번호를 각각 의미합니다.
예를 들어,
위의 $A$의 정의에서

$$a_{11}=1,\quad a_{12}=2,\quad a_{21}=0,\quad a_{22}=1$$

입니다.
어떤 행렬의 모양을 나타낼 때, 두 개의 아래첨자가 있는 소문자 알파벳의 양옆에 소괄호를 붙이고, 거기에 다시 행렬의 모양을 특정해 표시하기도 합니다.
예를 들어

$$E=(e_ij)_{2\times2}$$

이면, 이것은 이 행렬이 $2\times2$ 행렬이라는 뜻이고, 그 성분들이 $e_{ij}$로 표시된다는 뜻입니다.
만약 $e_{ij}=i+j-1$이면

$$E=\begin{bmatrix}1&2\\2&3\end{bmatrix}$$

이 될 것입니다.

## 1.2 행렬의 연산

### 이항연산
두 행렬의 모양이 같으면 두 행렬을 더할 수 있습니다.
두 행렬을 더할 때에는 성분별로 더하면 됩니다.
예를 들어, $A$와 $E$는 모양이 서로 같으므로 서로 더할 수 있고, 그 결과가
$$A+E=\begin{bmatrix}1&2\\0&1\end{bmatrix}+\begin{bmatrix}1&2\\2&3\end{bmatrix}=\begin{bmatrix}1+1&2+2\\0+2&1+3\end{bmatrix}=\begin{bmatrix}2&4\\2&4\end{bmatrix}$$
로 나타나지만, $A$와 $B$는 모양이 서로 다르므로 더할 수 없습니다.

두 행렬에 대해서 첫번째 행렬의 열의 수와 두번째 행렬의 행의 수가 같으면 두 행렬을 곱할 수 있습니다.
그러니까, $P$가 $m\times n$ 행렬이고, $Q$가 $n\times l$ 행렬이면, 두 행렬 $P$, $Q$의 곱 $PQ$를 생각할 수 있습니다.
$PQ=R$이라고 하면,

$$r_{ij}=\sum_{k=1}^np_{ik}q_{kj}$$

입니다.

예를 들어, $A$와 $B$는 각각 $2\times2$, $2\times3$ 행렬이고 따라서 두 행렬을 곱할 수 있습니다.
($m=2$, $n=2$, $k=3$)
그 결과는

$$
\begin{align*}
AB
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
AE&=\begin{bmatrix}1&2\\0&1\end{bmatrix}\begin{bmatrix}1&2\\2&3\end{bmatrix}=\begin{bmatrix}5&8\\2&3\end{bmatrix}\\
BD&=\begin{bmatrix}0&1&0\\1&0&0\end{bmatrix}\begin{bmatrix}1\\-1\\0\end{bmatrix}=\begin{bmatrix}-1\\1\end{bmatrix}\\
CA&=\begin{bmatrix}2&4\end{bmatrix}\begin{bmatrix}1&2\\0&1\end{bmatrix}=\begin{bmatrix}2&8\end{bmatrix}\\
A^2&=\begin{bmatrix}1&2\\0&1\end{bmatrix}^2=\begin{bmatrix}1&2\\0&1\end{bmatrix}\begin{bmatrix}1&2\\0&1\end{bmatrix}
=\begin{bmatrix}1&4\\0&1\end{bmatrix}
\end{align*}
$$

와 같이 계산할 수 있습니다.
이상은 행렬이 두 개 주어졌을 때 만들 수 있는 이항연산입니다.

### 단항연산
행렬 하나에 대해서도 연산을 정의할 수 있는데, 대표적인 것이 transpose(전치)와 conjugate transpose(켤레전치)입니다.

행렬 $A$에 대하여, $A$의 transpose는 $A^T$와 같이 표시하는데, $A$의 행번호와 열번호를 뒤집어놓은 것입니다.
예를 들면,

$$
\begin{align*}
A^T&=\begin{bmatrix}1&2\\0&1\end{bmatrix}^T=\begin{bmatrix}1&0\\2&1\end{bmatrix}\\
B^T&=\begin{bmatrix}0&1&0\\1&0&0\end{bmatrix}^T=\begin{bmatrix}0&1\\1&0\\0&0\end{bmatrix}\\
C^T&=\begin{bmatrix}2&4\end{bmatrix}^T=\begin{bmatrix}2\\4\end{bmatrix}
\end{align*}
$$

등입니다.

$A$의 conjugate transpose는 $A^H$와 같이 표시하는데, 이것은 $A$를 transpose하고, 각 entry들에 켤레 연산을 취한 것입니다.
즉,

$$
A^H=\overline{A^T}
$$

입니다.
그런데, 사실 transpose를 먼저 하나, 각 엔트리에 켤레 연산을 취하나 같으므로

$$
A^H = \overline A^T
$$

와 같이 정의해도 정확히 같은 정의가 됩니다.
이때, 어떤 복소수에 켤레 연산을 *취하는* 것은 이 복소수의 허수부분의 부호를 바꾸는 것을 말합니다.
즉 $2+3i$의 켤레 복소수는 $2-3i$인데, 이것을

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

\begin{equation}\label{real_conjugate_1}
z\text{가 실수이면 }\bar z=z\text{이고, 그 역도 성립합니다.}
\end{equation}

어떤 행렬에 켤레 연산을 취하는 것은 그 행렬의 각 entry에 각각 켤레연산을 취하는 것입니다.
예를 들어

$$F=\begin{bmatrix}2+3i&2-3i\\i&3\end{bmatrix}$$

이면

$$
\begin{align*}
\overline F
&=\begin{bmatrix}\overline{2+3i}&\overline{2-3i}\\\overline i&\overline3\end{bmatrix}\\
&=\begin{bmatrix}2-3i&2+3i\\-i&3\end{bmatrix}
\end{align*}
$$

인 것입니다.
한편, \eqref{real_conjugate_1}을 응용하면 다음과 같이 쓸 수도 있습니다.

\begin{equation}\label{real_conjugate_2}
A\text{가 실수로 이루어진 행렬이면 }\bar A=A\text{이고, 그 역도 성립합니다.}
\end{equation}



[1]:{{ site.url }}/assets/pdf/orthogonally_diagonalizable.pdf
