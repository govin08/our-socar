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

# 1. 정의

이 포스트에서 다루는 행렬들은 모두 entry(성분)들이 실수 혹은 복소수인 행렬들만을 다룹니다.
즉, 여기에서 행렬(matrix)이란, 실수 혹은 복소수를 직사각형 모양으로 배열해 괄호로 묶어 놓은 것을 말합니다.
예를 들어,

$$A=\begin{bmatrix}1&2\\0&1\end{bmatrix},\qquad B=\begin{bmatrix}0&1&0\\1&0&0\end{bmatrix}$$

는 행렬입니다.
이때, $A$는 2개의 행과 2개의 열로 이루어진 행렬이어서 `$2\times 2$ 행렬'이라고 부르고 $B$는 2개의 행과 3개의 열로 이루어진 행렬이어서 `$2\times3$ 행렬'이라고 부릅니다.

행이 하나인 행렬과 열이 하나인 행렬도 행렬로 취급합니다.
이것들은 각각 '행벡터', '열벡터' 라는 이름으로도 불립니다.
예를 들어

$$C=\begin{bmatrix}2&4\end{bmatrix},\qquad D=\begin{bmatrix}1\\-1\\0\end{bmatrix}$$

이면 $C$는 $1\times2$ 행렬이기도 하지만 2차원의 행벡터라고도 불리고, $D$는 $3\times1$ 행렬이기도 하지만 3차원의 열벡터라고도 불립니다.
선형대수를 말할 때 늘 그렇듯이, 이 포스트에서도 벡터는 열벡터로 표시합니다.
그러니까, 고등학교 수학에서는 $v=(2,1)$을 2차원 벡터로 생각하고, $w=(1,0,3)


[1]:{{ site.url }}/assets/pdf/orthogonally_diagonalizable.pdf