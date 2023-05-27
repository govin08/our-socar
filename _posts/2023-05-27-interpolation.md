---
layout: single
title: "보간법(interpolation)"
categories: machine_learning
tags: [applied_mathematics, interpolation]
use_math: true
publish: false
author_profile: false
toc: true
---

interpolation(보간법)에 대하여 한 번 정리해봤습니다.
정확하게는, 어떤 정형데이터가 주어졌을 때 그 데이터의 특정 컬럼에 결측치가 발생했을 경우에 그 결측치를 처리하는 방법에 대해 고민해보았습니다.
아주 기본적인 interpolation에 대해서만 이야기해보았고, 세부적인 사항은 많이 생략하게 될 것 같습니다.

변수가 한 개인 경우의 보간법 (univariate interpolation)에서 nontrivial한 보간법은 당연히 다항함수로 knot들을 연결하는 것입니다.

# 1 Univariate interpolations

univariate interpolation이라는 말에서 변수가 한 개(univariate)라는 의미는 독립변수($x$)의 개수가 한 개라는 것입니다.
vector valued function을 다루지는 않으니 독립변수($y$)도 하나라고 하면, 실제로는 두 개의 변수를 다루게 됩니다.

여기에서 하려고 하는 것은, $n+1$개의 data sample $(x_i,y_i)$들이 주어져 있을 때 ($i=0,1,2,\cdots n$, $x_0\lt x_1\lt\cdots\lt x_n$), 모든 $i$에 대하여 $f(x_i)=y_i$를 만족시키는 함수 $f:\mathbb R\to\mathbb R$을 찾는 것입니다.
$y$좌표가 결측된 어떤 data sample $(x',?)$이 주어져있을 때, 이 결측치를 $f$를 통해 보간하여 $(x',f(x'))$로 만드는 것이 목적입니다.

<!-- <div class="notice--danger">
그러니까 $\sum_i||f(x_i)-y_i||^2$의 값을 최소로 하는 $f$를 찾아야 하는 일반적인 regression 문제와는 조금의 차이가 있겠습니다. -->

<!-- 또한, 각각의 $x_i$들이 다 달라야(distinct) 위의 문제가 성립할 수 있을 것입니다. -->
<!-- 또한, $x_i=x_j$, $y_i\ne y_j$를 만족시키는 서로 다른 $i$, $j$가 존재하는 경우에는 위의 문제가 성립할 수 없을 것입니다. -->
<!-- (regression 문제를 풀 때에는 그것이 문제가 되지 않았었습니다.)
이 경우에는 위의 $f(x_i)=y_i$ 조건 대신
$$f(x_i)=\frac1{|\{j:x_j=x_i\}|}\sum_{j:x_j=x_i}y_j$$
의 조건을 사용할 수도 있을 것 같습니다. -->
<!-- </div> -->

이 문제상황을 그림으로 그려보면 다음과 같습니다.
$n+1$개의 점이 이미 찍혀있는 상태에서, 이 점들을 적절히 이어서 새로운 함수 $f$를 만드는 것입니다.

![]({{site.url}}\images\2023-05-27-interpolation\1-1.png){: .img-50-center}

![]({{site.url}}\images\2023-05-27-interpolation\1-2.gif){: .img-50-center}

![]({{site.url}}\images\2023-04-14-socar_zones\collected_data.png){: .img-50-center}

![]({{site.url}}\images\2023-03-26-kocw_stats\stacks.png){: .img-50-center}

![]({{site.url}}\images\2023-03-26-kocw_stats\stats_2-2.png){: .img-50-center}


## 1.1 Vanilla interpolations

- nearest neighbor
- previous
- next

## 1.2 Polynomial interpolations (spline interpolation)

### 1.2.1 Linear interpolation

### 1.2.2 Quadratic interpolation

### 1.2.3 Cubic interpolation

# 2 Multivariate interpolation
