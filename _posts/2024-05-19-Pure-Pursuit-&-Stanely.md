---
layout: post
cover: 'assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/1_kinematic_bicycle.png'
navigation: True
title: Pure Pursuit & Stanely
date: 2024-05-19 02:00:00
tags: tech control
subclass: 'post tag-tech tag-control'
logo: 'assets/images/kroad_white.png'
use_math: True
author: gyeomhan
categories: gyeomhan
---

안녕하세요. K-ROAD 5기 한겸입니다.<br>
오늘은 많은 사람들에게 잘 알려져있는 Pure Pursuit와 Stanely 경로 추종 알고리즘에 대해 소개하려고 합니다.

---

## Kinematic bicycle model이란?
Kinematic bicycle model은 단순화 된 자동차의 수학적 모델로 일반적인 주행 조건에서 차량 움직임을 매우 잘 포착하는 모델입니다.<br>
실제 자전거처럼 뒷바퀴는 고정되어 있고 앞바퀴를 통해 차량의 방향을 제어합니다. 

![Kinematic bicycle model](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/1_kinematic_bicycle.png)

**Motion Equation**은 다음과 같습니다.

<!-- ![Kinematic bicycle model Motion Equation](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/2_kbm_motion_equation.png) -->

<img src="https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/2_kbm_motion_equation.png" alt="Kinematic bicycle model Motion Equation" width="600px">

---

## Pure Pursuit 알고리즘이란?
Pure Pursuit 알고리즘은 **경로 추종** 알고리즘 중 하나로, **차량의 후륜축의 중심**을 **기준점**으로 사용하여 차량의 **운동 방정식**과 **경로의 지오메트리**만을 사용하는 간단한 알고리즘입니다.

### Pure Pursuit 제어 방식

![Pure Pursuit 제어 방식 1](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/3_Pure_Pursuit_1.png)

먼저 Reference Path위에 Ld 거리만큼 떨어진 Look Ahead Point를 정하고 

![Pure Pursuit 제어 방식 2](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/4_Pure_Pursuit_2.png)

이때 뒷바퀴 중심과 Look Ahead Point를 지나는 원의 곡률을 따라서 조향각을 조절합니다. 

**L** : 차량 길이<br>
**δ** : 조향각<br>
**α :** 두 점을 지나는 직선과 차량이 바라보는 방향의 직선 사이의 각도 <br>
**Ld :** 뒷바퀴 중심과 목표 지점 사이의 거리<br>
**R :** 두 점을 지나는 원의 반지름(자동차의 선회반경)

<!-- $\frac{ld}{\sin2(\alpha)}=\frac {R}{\sin(\frac{\pi}{2}-\alpha)}$<br>
$\frac{ld}{2\sin(\alpha)*\cos(\alpha)}=\frac{R}{\cos(\alpha)}$<br>
$\frac{ld}{\sin(\alpha)}=2R$<br>
$k=\frac{1}{R}=\frac{2\sin(\alpha)}{ld}$ -->

<!-- ![Untitled](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/5.png) -->

<img src="https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/5.png" width="450px" height="auto">

관련된 수식은 위와 같으며 Kinematic bicycle model에 의해

![Untitled](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/6.png)

이 되며 결과적으로 조향각**δ**는 다음과 같이 정의됩니다.

![Untitled](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/7.png)

## Look Ahead Distance(Ld)

다음은 Pure Pursuit 알고리즘의 중요 파라미터인 Look Ahead Distance에 대해 설명하겠습니다.<br>
Look Ahead Distance는 Look Ahead Point까지의 거리를 결정합니다.<br>
이때 **Look Ahead Distance를 짧게** 설정하면 경로를 추종하는 시간을 줄일 수 있지만 아래 그림에서 볼 수 있듯 **진동하며 경로를 벗어날 수 있습니다.**

반대로,  **Look Ahead Distance를 길게** 설정하면 경로를 부드럽게 추종하지만 **코너에서 더 큰 곡률이 발생할 수 있으며, 경우지를 정확히 따라가지 않아 경로 추종 성능이 저하**될 수 있기에 적절한 튜닝값을 구하는 것이 중요합니다.

![Look Ahead Distance(Ld)](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/8_Look_Ahead_Distance.png)

---

## Stanley 알고리즘이란?
Stanley 알고리즘은 운동방정식, 기준이 되는 경로의 지오메트리, **차량의 헤딩 방향을 사용**하여 기존 경로를 추종하고 접근하는 방식의 알고리즘입니다.<br>
스탠포드 대학교의 Darpa Grad Challenge 팀에서 사용하여 우승까지 했던 알고리즘입니다.

### Stanley 제어 방식
차량의 후륜축을 기준으로 하는 Pure Pursuit 알고리즘과는 달리 **Stanley 방식은 전륜축을 기준**으로 합니다.<br>
또한 Stanley의 경우 차량과 목표지점까지의 오차만 고려하는 Pure Pursuit과는 달리 **차량과 목표지점까지의 오차 + 목표지점과 차량의 헤딩방향의 오차도 함께 고려**합니다.<br>
이때 차량의 목표지점까지의 오차는 전륜축에서 Reference Path에 가장 가까운 목표점까지의 거리로 정의합니다.

![Untitled](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/9_Stanley.png)

**ψ** : 경로의 방향과 차량의 Heading 사이의 각도<br>
**δ** : 조향각<br>
**e** : 차량의 목표지점까지의 오차<br>
**v** : 차량의 속도벡터

Stanley 방식은 헤딩 오차와 횡방향 오차를 고려하여 차량을 제어합니다.

1. **헤딩 오차 고려**
    차량 경로의 방향 및 자동차의 축방향에 맞춰 헤딩 오차를 없애기 위한 조향각 결정

    ![Untitled](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/10.png)
    <!-- <img src="https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/10.png" width="150px"> -->

2. **횡방향 오차 고려**
    조향각을 횡방향 오차에 비례하여 제어하는데 이때 차량의 속력에 따라 조향 속도가 너무 크지 않도록 제어합니다. k값은 튜닝 파라미터 입니다.

    ![Untitled](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/11.png)

3. **헤딩 오차 + 횡방향 오차**
    두 값을 합쳐 최종적으로 조향각을 제어합니다. 이때 최대, 최소 조향각을 제한합니다.

    ![Untitled](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/12.png)

### 속도 상수 h
위 조향각 식에서 속도가 0에 가까울 때 tan역함수 값이 매우 커질 수 있기 때문에 이것을 해결하기 위해 아래와 같이 속도 상수 h를 추가해줍니다.

![Untitled](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/13.png)

---

## Pure Pursuit & Stanley 알고리즘 비교
마지막으로 지금까지 살펴본 Pure Pursuit과 Stanley 알고리즘의 차이점을 간단하게 살펴보면 다음과 같습니다.

![Pure Pursuit vs Stanley](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-19-Pure-Pursuit-&-Stanely/14.png)

두 제어방식 모두 완벽한 제어방식이 아닌 각각의 장단점이 존재하는 제어방식들입니다. 따라서 주행 상황에 맞는 제어 알고리즘의 도입과 적절한 튜닝값 선정이 중요합니다. 

### 참고자료

- **Vehicle Dynamics & Control - 05 Kinematic bicycle model**<br>
    [https://youtu.be/HqNdBiej23I?si=a5vnrRaK_8k-ndQm](https://youtu.be/HqNdBiej23I?si=a5vnrRaK_8k-ndQm)
    
- **Pure Pursuit**<br>
    [https://blog.naver.com/rich0812/222592223219](https://blog.naver.com/rich0812/222592223219)
    

- **stanley**<br>
    [https://blog.naver.com/rich0812/222598072957](https://blog.naver.com/rich0812/222598072957)