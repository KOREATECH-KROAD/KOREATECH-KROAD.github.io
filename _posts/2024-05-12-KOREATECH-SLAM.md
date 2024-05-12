---
layout: post
cover: 'assets/images/blog/2024-05-12-KOREATECH-SLAM/3_중앙공원.png'
navigation: True
title: KOREATECH SLAM
date: 2024-05-12 23:00:00
tags: tech slam
subclass: 'post tag-tech tag-slam'
logo: 'assets/images/kroad_white.png'
use_math: true
author: garamkim
categories: garamkim
---

안녕하세요. K-ROAD 5기 김가람입니다.

오늘은 SLAM이 무엇인지에 대한 간단한 이야기와 교내에서 SLAM 기술을 이용하여 진행한 실험에 대한 글을 적으려고 합니다.

<hr>
## SLAM이란?

**SLAM**이란 **S**imultaneous **L**ocalization **A**nd **M**apping의 약자입니다. 말 그대로 localization과 mapping을 동시에 하는 기술을 의미합니다.

자율주행에서 자신의 위치를 추정하는 일은 매우 중요합니다. 자신의 위치와 주변 환경이 어떻게 생겼는지 알아야만 원하는 위치로 효율적이고 안전하게 이동할 수 있습니다. LiDAR SLAM의 원리는 간단하게 말해서 포인트 클라우드 형식으로 받아온 데이터에서 특징점을 찾아 기존에 받아온 포인트 클라우드 정보들과 대조하여 위치를 찾는 것입니다. 이 과정에서는 GNSS, IMU 등의 센서가 보정을 위해 활용될 수 있습니다.

따라서 필드를 돌며 map을 생성하고 이 과정에서 LiDAR를 통해 받아오는 포인트 클라우드 정보와 센서 정보들을 통해 자신의 위치를 추정합니다.

<hr>
## SLAM in KOREATECH

한국기술교육대학교 자율주행차연구회 K-ROAD는 얼마 전 교내를 대상으로 LiDAR SLAM 기술을 실험하였습니다.

사용한 플랫폼은 ERP-42이고, 작업에 사용한 라이브러리는 [hdl_graph_slam](https://github.com/koide3/hdl_graph_slam)입니다.

주행 경로는 자율주행차연구회의 연구실이 위치한 산학협력관부터 주요 학교 건물이 있는 중앙공원 주변, 후문, 그리고 운동장까지입니다.

재학생 및 교직원 분들의 편의와 안전을 위해 통행이 적은 시간대에 실험을 진행하였습니다.

<hr>
## 인문경영관

정문에서 올라오면 담헌실학관 다음으로 만날 수 있는 건문입니다. 중앙공원 앞에 위치해 있어서 자주 지나치게 되는 건물이기도 합니다. 공학을 전공하는 학생들은 교양 수업을 제외하면 자주 가지 않는 건물이기 때문에 생소할 수도 있지만, 한국기술교육대학교를 다니다보면 자주 지나가게 되는 길입니다.
![한국기술교육대학교 인문경영관 PCL 이미지](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/1_slam_인문경영관.png)
한국기술교육대학교 인문경영관 PCL 이미지

![출처: [https://ko.wikipedia.org/wiki/한국기술교육대학교](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B5%AD%EA%B8%B0%EC%88%A0%EA%B5%90%EC%9C%A1%EB%8C%80%ED%95%99%EA%B5%90)](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/2_인문경영관.jpg)
출처: [https://ko.wikipedia.org/wiki/한국기술교육대학교](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B5%AD%EA%B8%B0%EC%88%A0%EA%B5%90%EC%9C%A1%EB%8C%80%ED%95%99%EA%B5%90)

<hr>
## 중앙공원

재학생들에게는 일명 텔동(텔레토비 동산)이라고 불리는 중앙공원입니다.<br>
이곳에서는 축제, 동아리 박람회 등 다양한 행사가 열리기도 합니다. 중앙에 있는 나무를 기준으로 십자 모양의 길이 나 있는 것이 특징입니다.
![한국기술교육대학교 중앙공원 PCL 이미지](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/3_slam_중앙공원.png)
한국기술교육대학교 중앙공원 PCL 이미지

![출처: [https://ko.wikipedia.org/wiki/한국기술교육대학교](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B5%AD%EA%B8%B0%EC%88%A0%EA%B5%90%EC%9C%A1%EB%8C%80%ED%95%99%EA%B5%90)](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/4_중앙공원.png)
출처: [https://ko.wikipedia.org/wiki/한국기술교육대학교](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B5%AD%EA%B8%B0%EC%88%A0%EA%B5%90%EC%9C%A1%EB%8C%80%ED%95%99%EA%B5%90)

<hr>
## 대학본부 & 중앙공원

이곳은 중앙공원과 붙어 있는 대학본부 건물입니다. 학교의 행정문제를 처리하는 곳으로, 강의실이 없기 때문에 학생들은 재학 중에도 갈 일이 별로 없는 건문이기도 합니다. 하지만 기숙사에서 강의 건물로 올라오는 길목에 위치해 있기 때문에 학교를 다니다 보면 자주 지나치게 됩니다.

![한국기술교육대학교 대학본부 PCL 이미지](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/5_slam_대학본부_중앙공원.png)
한국기술교육대학교 대학본부 PCL 이미지

![출처: [https://ko.wikipedia.org/wiki/한국기술교육대학교](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B5%AD%EA%B8%B0%EC%88%A0%EA%B5%90%EC%9C%A1%EB%8C%80%ED%95%99%EA%B5%90)](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/6_대학본부_중앙공원.png)
출처: [https://ko.wikipedia.org/wiki/한국기술교육대학교](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B5%AD%EA%B8%B0%EC%88%A0%EA%B5%90%EC%9C%A1%EB%8C%80%ED%95%99%EA%B5%90)

<hr>
## 학교 전체

![한국기술교육대학교 전체 PCL 이미지 1](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/7_slam_학교.png)
한국기술교육대학교 전체 PCL 이미지 1

![한국기술교육대학교 전체 PCL 이미지 2](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/8_slam_학교_2.png)
한국기술교육대학교 전체 PCL 이미지 2

<iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3196.312720045096!2d127.28166769846388!3d36.7630647553576!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x357b2ac6c614c717%3A0x820bda83618bd53b!2sKorea University of Technology %26 Education (KOREATECH)%2C Campus 1!5e0!3m2!1sen!2skr!4v1715522416158!5m2!1sen!2skr" width="100%" height="500" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
한국기술교육대학교 지도

<iframe src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d8040.655696704383!2d127.28194100000002!3d36.763718!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x357b2ac6c614c717%3A0x820bda83618bd53b!2sKorea%20University%20of%20Technology%20%26%20Education%20(KOREATECH)%2C%20Campus%201!5e1!3m2!1sen!2skr!4v1715530978828!5m2!1sen!2skr" width="100%" height="500" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
한국기술교육대학교 위성 사진

<!-- ![출처: Google maps](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/10_학교_위성사진.png)
출처: Google maps -->

<br><br>
한국기술교육대학교 SLAM의 경우  YouTube 영상으로도 제작되었으니 관심 있으신 분들은 다음 영상도 확인해보시면 좋을 것 같습니다.

<iframe width="560" height="315" src="https://www.youtube.com/embed/-DC6ZDe-v5w?si=sIj0hRa2g_KQ3_Ru" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<hr>
## 참고 자료

- **SLAM이란?**<br>
    [https://kr.mathworks.com/discovery/slam.html](https://kr.mathworks.com/discovery/slam.html)
    
- **Simultaneous localization and mapping**<br>
    [https://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping](https://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping)
    
- **SLAM이란?**<br>
    [https://cvlearnblog.notion.site/SLAM-f16a75f894ca48d3aa851bca99ec7cce](https://www.notion.so/SLAM-f16a75f894ca48d3aa851bca99ec7cce?pvs=21)