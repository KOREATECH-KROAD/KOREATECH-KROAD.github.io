---
layout: post
cover: 'assets/images/cover2.jpg'
navigation: True
title: Holistic Grid Fusion Based Stop Line Estimation - 1
date: 2024-05-06 23:00:00
tags: tech sensor-fusion
subclass: 'post tag-tech tag-sensor-fusion'
logo: 'assets/images/kroad_white.png'
use_math: true
author: minseokkim
categories: minseokkim
---

안녕하세요. K-ROAD 5기 김민석입니다.

저는 이번 기술 블로그 주제로 정지선과 관련된 이야기를 진행하려고 합니다.

정지선과 관련된 여러 논문을 찾았고, 그 중에서 저희가 구현하고자 하는 방향과 제일 유사한 Holistic Grid Fusion Based Stop Line Estimation@ICPR2020의 논문을 읽고 Review해보는 글을 작성하게 되었습니다.

# Introduction

![출처 : 차량 기계 기술 법인](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-06-Holistic-Grid-Fusion-Based-Stop-Line-Estimation-1/1.png)

*출처 : 차량 기계 기술 법인*

실제 자동차의 경우 안정적인 정지를 위해 53m 정도를 필요로 하고 있습니다. 자율주행에서의 정지는 정지 유/무를 판별하는 공주거리, 이후 제동거리를 합해 안정적인 정지거리를 구할 수 있습니다. 만약 카메라만 활용한다면 거리는 30m로 터무니 없게 부족합니다. 그렇다고 lidar만 활용하기에는 정지선에 대한 intensity 값을 정확하게 가져오기 힘들어 아무리 200m를 보는 lidar라 하더라도 정지선에 인식하기에는 무리가 있습니다.

![출처 : Holistic Grid Fusion Based Stop Line Estimation@arXiv2020](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-06-Holistic-Grid-Fusion-Based-Stop-Line-Estimation-1/2.png)

*출처 : Holistic Grid Fusion Based Stop Line Estimation@arXiv2020*

그래서 이번 Paper에서는 여러 단서를 활용하여 교차로의 존재를 감지하고 교차로의 정지선을 예측하는 것입니다. 이때 저희가 사용한 데이터는 stereo 카메라입니다. stereo 카메라는 흔히 depth 카메라라고도 불리는데 이건 rgb의 값만 가져오는 기존의 카메라와 달리 rgbd(depth)의 값을 가져옵니다.

![출처 : IDS](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-06-Holistic-Grid-Fusion-Based-Stop-Line-Estimation-1/3.png)

*출처 : IDS*

다음으로 HD(High Definintion)를 활용하는 것입니다. HD는 도로의 위치, 크기, 차선의 수, 교차로 등의 세부 정부가 포함되어 있는 지도로 도로의 곡률, 경사, 고도 등의 지형 정보도 제공합니다.  센서 데이터만 활용해서 정지선 검출에는 한계를 보이기에 HD를 활용해 localizing도 함께 진행하는 것입니다.

마지막으로 Ransac에 대해서 알고 넘어가도록 하겠습니다. Ransac의 경우 Random Sample Consensus로 데이터를 랜덤하게 샘플링하여 사용하고자 하는 모델을 fitting한 다음 결과가 원하는 목표치에 도달하였는지 확인하는 과정을 통해 모델을 데이터에 맞게 최적화하는 것입니다.

![출처 : [https://go-hard.tistory.com/123](https://go-hard.tistory.com/123)](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-06-Holistic-Grid-Fusion-Based-Stop-Line-Estimation-1/4.png)

*출처 : [https://go-hard.tistory.com/123](https://go-hard.tistory.com/123)*

# Related Work

현재 정지선을 예측하는 Task는 대표적으로 두 가지가 있습니다.

## 1. Deep Learning

1. 엣지 검출과 란삭을 통한 정지선 후보들 검출
2. 정지선 후보의 주변의 HOG features를 추출하고, 정지선 구별을 위해 TER based classifier 적용
3. [ 1 ], [ 11 ] 을 학습 기반과 체계 기반 둘 다에 각각 정지선 검출을 진행한다.
4. 이후 수평 모폴로지 연산을 통해 이미지의 수평방향으로 구조 요소를 이용하여 패턴을 찾거나 수정하는 데 사용됩니다.

[ 1 ]  Stop-line detection and localization method for intersection scenarios@IEEE2011

[ 11 ] Stop sign andstop line detection and distance calculation for autonomous vehicle control@IEEE2018

이와 같은 경우는 정지선과 위치 추정을 추적하는 과정에 있어 안정화해준다.

즉, 이번 논문에서 개발한 시스템은 이상적 형태와 위치적 관계에 대한 가정을 측정하기 위해 지워진 페인트가 있어도 정지선을 검출하는 것이다.

### 2. Vision Learning

정지선 검출에 있어 CNN 모델을 활용하는 것이다. CNN의 모델은 딥러닝 아키텍처로 합성공 신경망을 의미한다. CNN 모델의 Resnet 활용함으로써 잘못된 경고를 줄일 수 있고, 잘못된 정보와 날씨 조건에 있어서도 정확도를 높여준다.

다만 아쉬운 점이라 한다면 카메라 센서 데이터에 의지하기에 감지 범위는 제한될 뿐더러 부분적으로 아쉬운 결과를 가져오기도 한다.

## Method

![출처 : Holistic Grid Fusion Based Stop Line Estimation@arXiv2020](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-06-Holistic-Grid-Fusion-Based-Stop-Line-Estimation-1/5.png)

*출처 : Holistic Grid Fusion Based Stop Line Estimation@arXiv2020*

위 그림은 논문에서 제안하고 있는 방법론으로 멀티센서를 활용해 학습 기반의 Architecture입니다.

이와 같은 시스템은 안전성과 경로 설정을 보장하기 위해 Stereo Camera, Lidar, Radar 센서를 사용해 감지 영역을 강화시킵니다.

먼저 정적인 환경 정보와 동적인 물체 정보를 받는 것을 우선으로 진행합니다.

정적인 환경은 Segmentation mask를 생성하는 그리드 맵으로 생성되고, 생성된 그리드 맵은 Incoder-Decoder Nueron Network에 값을 넘겨줍니다.

마지막으로 Nueron Network에서는 정지선에 관한 값들을 예측합니다.

### Input data

전반적인 Pipe-Line은 이와 같지만 좀 더 세부적으로 들어가보도록 하겠습니다.

입력받은 데이터에 있어 비어있는 공간과 장애물의 위치는 셀의 공간 기질과 가능성으로부터 추정합니다. 이와 같은 특징을 활용해 다른 위치에 장착되어 있는 센서들을 혼합시킬 수 있습니다.

Sensor Fusion한 결과는 센서의 불확실성을 고려해 확률론적 환경 모델을 구축하기 위해 Bayes' theorem(베이시안 이론)을 활용합니다. 그뿐 아니라 SDC(Self-Driving Car)가 도시 주행에 있어 적용시킬 환경이 구축되지 않았을 경우에도 Grid Map을 재구축할 수 있습니다.

위 시스템은 기하학적이면서 의미론적인 정보 둘 다 부호화한 차량이 중심인 그리드 맵인 정보를 혼합해줍니다. 혼합된 그리드맵은 멀티 레이어로 점유도, 도로 표시, 라이다 강도, 의미 지면, 교통 이력을 포함하고 있고, bird’s eye view로 구현되어 있습니다.


> 💡 **의미론적 vs 기하학적** <br>
데이터의 의미나 의도 초점을 맞추는 것은 의미론적 <br>
데이터의 공간의 특성에 초점을 맞추는 것은 기하학적


### Network Architecture

이렇게 만들어진 Grid Map은 UNet과 유사한 Network로 전달됩니다. UNet은 말 그대로 Network 구조과 U자 형태와 유사하게 구현된다고해서 이름이 붙었습니다. 

![[https://wikidocs.net/148870](https://wikidocs.net/148870)](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-06-Holistic-Grid-Fusion-Based-Stop-Line-Estimation-1/6.png)

*출처: [https://wikidocs.net/148870](https://wikidocs.net/148870)*

UNet에는 3가지 핵심 아이디어가 있습 인코더의 피처맵을 디코더의 피처맵에 Concat하여 위치 정보를 전달하고, 데이터셋의 전처리, 변형을 이용하여 데이터 수를 증가시킵니다. 마지막으로 테두리를 더 잘 분할하기 위해 Weight를 추가한 손실함수를 활용합니다.

정지선의 유무에 따라 binary 값을 활용해 값을 예측하는데 이 값은 데이터가 편향되어 있을 때 기울기 오류 역전파에 있어 제한된 정보를 분할해줍니다. 분할된 픽셀은 특정 class와 관련되어 있음을 표현해주기 때문입니다.

따라서 공간의 근접한 정보를 제공할 수 있는 거리 맵을 언급하는 연속되는 표현으로 SDT를 사용합니다.

또, 공간 방향 정보를 제공하고, 데이터의 근본적인 공간 구조를 잘 이해할 수 있는 인공신경망을 돕는 방향 맵을 예측해줍니다.

이러한 두가지 마스킹(공간맵, 거리맵)은 학습을 통한 보조회귀손실을 추가해줍니다.


> 💡 SDT : 이미지의 픽셀에서 객체 경계까지의 최단 거리를 계산하는 방법 중 하나<br>
방향 지도를 사용하는 이유 : 데이터의 공간적 방향 정보를 제공하고, 신경망이 데이터의 기본적인 공간 구조를 더 잘 이해하도록 돕는데 도움이 됩니다.<br>
PCA : 다차원 데이터 세트의 차원을 축소하는 기술로, 데이터를 가장 잘 설명하는 주요한 변수를 찾아내는 데 사용된다. ⇒ 차원을 줄이지만 데이터의 정보를 최대한 보존하는데 사용된다.


추가적인 계산 비용을 피하기 위해 추론하는 동안은 segmentation mask(이미지 처리에서 특정 객체나 영역을 분할하여 표시하는 데 사용되는 이미지)는 생성됩니다. 낮은 디테일이나 높은 수준의 의미론적 정보 둘 다 얻는 능력때문에 공동의 학습에 있어 네트워크의 핵심 구조로 UNet을 사용합니다.

### Distance and Direction Map

![출처 : Holistic Grid Fusion Based Stop Line Estimation@arXiv2020](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-06-Holistic-Grid-Fusion-Based-Stop-Line-Estimation-1/7.png)

*출처 : Holistic Grid Fusion Based Stop Line Estimation@arXiv2020*

> x : 이미지의 픽셀 2D 좌표 벡터<br>
M : 정지선 영역을 표현하는 foreground(이미지의 중요한 정보) masking<br>
d : 거리값<br>
F : foreground point


Linear Time에 있어 각각의 픽셀에서 가장 가까운 foreground point를 찾을 수 있는 알고리즘을 활용할 것입니다.

이때 표현되는 F는 음수가 나올 경우 0으로 짤리고, 양수가 나올 경우 0에서 1 사이의 값으로 normalization해줍니다.

이렇게 표현된 맵의 경우 한 가지 주의할 점이 있습니다. 하나의 정지선이지만 두 가지 이상으로 감지할 수 있습니다. 이를 보완하기 위해 Direction Map을 사용해주는 것입니다.

$$
L_{seg} = L_{cross}(S_{pred}, S_{gt}) + \lambda_1L_2(D_{pred}, D_{gt}) + \lambda_2L_2(E_{pred}, E_{gt})
$$

방향맵은 당연히 각각의 픽셀에서 정지선을 연속적인 공간의 방향으로 알려주고 있습니다.

1. 하이퍼 파라미터인 람다를 학습 과정에서 0.5로 세팅해줍니다. 
2. 분할 맵 S는 존재하는 정지선의 희미한 표현들을 추출해줍니다. 
3. 정지선 L_i에 있어 네 가지 특성 p, p, l, s은 2d image 좌표로 표현되고, 이미지 공간에서 시작과 끝 점이고, 시작과 끝, 정지선의 기울기 사이에서 유클리드 거리이다. 
4. 요소 레이블링은 다른 그룹에서 positive prediction으로 연결되어 나눠진 segmentation map S에 적용해줍니다. 
5. 각각의 그룹은 2d point의 cluster이기에 pca를 근본적인 정지선의 기울기 값과 클러스터의 주요한 축들에 적용합니다. 
6. 그룹의 왼쪽과 오른쪽 좌표를 정지선의 일부로 희미하게 표현된 선 segment의 시작과 끝 포인트를 측정하기 위해 경사축제 정사영합니다.

※ object segmentation mask는 항상 연속적인 결과를 산출하지 않습니다.

1. 같은 정지선으로부터 두 가지 선은 segmetation 짤림때문에 두 가지 다른 그룹으로 간주합니다.
2. 정지선 두 개를 양방향 비교를 기반한 정련의 알고리즘을 수행하고, 조건에 맞다면 중복하는 선을 지웁니다.

위의 과정을 거치면서 최적의 정지선을 추출하는 과정을 갖습니다.

train한 값을 테스트 하기 위한 기준으로 가장 가까운 실제 정지선과의 연관성을 사용합니다. 두 선이 겹치고 정렬되어야 하는데 방향에 대한 오차 한계를 a_thersh로 설정하여  오류역전파와 함께 제약을 완화합니다.

![출처 : Holistic Grid Fusion Based Stop Line Estimation@arXiv2020](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-06-Holistic-Grid-Fusion-Based-Stop-Line-Estimation-1/8.png)

*출처 : Holistic Grid Fusion Based Stop Line Estimation@arXiv2020*

## Review

내용 이해에 있어 100% 내 것을 만들었다고 보기는 힘들 것 같습니다. 다만 새로운 Task에 대해서 배울 수 있는 시간이었고, 다만 아쉬운 점은 논문은 선택하는 과정이었던 것 같습니다. 현재 하기 힘든 정지선 관련 논문을 찾다가 발견하였지만 정지선 관련 내용이라기보다 Grid Map에 더 비중이 높아보여 다음에는 논문 선택하는 과정에 있어 더 집중해야 할 것 같습니다.

이번 논문은 공부를 하면서 처음으로 읽어본 논문이었습니다. 내용을 정리하는 과정에 있어서도 많이 부족했을 것이고, 이해하는 시간이 오래 걸리다보니 실험쪽은 이번 글에 작성하지 못했습니다. 남은 내용은 다음 게시물을 통해 작성할 예정입니다. 부족한 글 읽어주셔서 감사합니다.