---
layout: post
cover: 'assets/images/cover2.jpg'
navigation: True
title: KOREATECH SLAM
date: 2024-05-12 09:00:00
tags: tech slam
subclass: 'post tag-tech tag-slam'
logo: 'assets/images/kroad_white.png'
use_math: true
author: garamkim
categories: garamkim
---

안녕하세요. K-ROAD 5기 김가람입니다.

오늘은 SLAM이 무엇인지에 대한 간단한 이야기와 교내에서 SLAM 기술을 이용하여 진행한 실험에 대한 글을 적으려고 합니다.

# SLAM이란?

**SLAM**이란 **S**imultaneous **L**ocalization **A**nd **M**apping의 약자입니다. 말 그대로 localization과 mapping을 동시에 하는 기술을 의미합니다.

# SLAM in KOREATECH

한국기술교육대학교 자율주행차연구회 K-ROAD는 얼마 전 교내를 대상으로 SLAM 기술을 실험하였습니다.

사용한 플랫폼은 ERP-42이고, 작업에 사용한 라이브러리는 hdl_graph_slam(https://github.com/koide3/hdl_graph_slam)입니다.

주행 경로는 자율주행차연구회의 연구실이 위치한 산학협력관부터 주요 학교 건물이 있는 중앙공원 주변, 후문, 그리고 운동장까지입니다.

* 재학생 및 교직원 분들의 편의와 안전을 위해 통행이 적은 시간대에 실험을 진행하였습니다.

## 인문경영관

![한국기술교육대학교 인문경영관 PCL 이미지](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/1_slam_인문경영관.png)

한국기술교육대학교 인문경영관 PCL 이미지

![출처: [https://ko.wikipedia.org/wiki/한국기술교육대학교](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B5%AD%EA%B8%B0%EC%88%A0%EA%B5%90%EC%9C%A1%EB%8C%80%ED%95%99%EA%B5%90)](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/2_인문경영관.jpg)

출처: [https://ko.wikipedia.org/wiki/한국기술교육대학교](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B5%AD%EA%B8%B0%EC%88%A0%EA%B5%90%EC%9C%A1%EB%8C%80%ED%95%99%EA%B5%90)

## 중앙공원

재학생들에게는 일명 텔동(텔레토비 동산)이라고 불리는 중앙공원입니다.

![한국기술교육대학교 중앙공원 PCL 이미지](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/3_slam_중앙공원.png)

한국기술교육대학교 중앙공원 PCL 이미지

![출처: [https://ko.wikipedia.org/wiki/한국기술교육대학교](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B5%AD%EA%B8%B0%EC%88%A0%EA%B5%90%EC%9C%A1%EB%8C%80%ED%95%99%EA%B5%90)](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/4_중앙공원.png)

출처: [https://ko.wikipedia.org/wiki/한국기술교육대학교](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B5%AD%EA%B8%B0%EC%88%A0%EA%B5%90%EC%9C%A1%EB%8C%80%ED%95%99%EA%B5%90)

## 대학본부 & 중앙공원

![한국기술교육대학교 대학본부 PCL 이미지](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/5_slam_대학본부_중앙공원.png)

한국기술교육대학교 대학본부 PCL 이미지

![출처: [https://ko.wikipedia.org/wiki/한국기술교육대학교](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B5%AD%EA%B8%B0%EC%88%A0%EA%B5%90%EC%9C%A1%EB%8C%80%ED%95%99%EA%B5%90)](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/6_대학본부_중앙공원.png)

출처: [https://ko.wikipedia.org/wiki/한국기술교육대학교](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B5%AD%EA%B8%B0%EC%88%A0%EA%B5%90%EC%9C%A1%EB%8C%80%ED%95%99%EA%B5%90)

## 학교 전체

![한국기술교육대학교 전체 PCL 이미지 1](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/7_slam_학교.png)

한국기술교육대학교 전체 PCL 이미지 1

![한국기술교육대학교 전체 PCL 이미지 2](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/8_slam_학교_2.png)

한국기술교육대학교 전체 PCL 이미지 2

![출처: Google maps](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/9_학교_구글맵.png)

출처: Google maps

<iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3196.312720045096!2d127.28166769846388!3d36.7630647553576!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x357b2ac6c614c717%3A0x820bda83618bd53b!2sKorea University of Technology %26 Education (KOREATECH)%2C Campus 1!5e0!3m2!1sen!2skr!4v1715522416158!5m2!1sen!2skr" width="600" height="450" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>

![출처: Google maps](https://KOREATECH-KROAD.github.io/assets/images/blog/2024-05-12-KOREATECH-SLAM/10_학교_위성사진.png)

출처: Google maps

# 참고 자료

- **SLAM이란?**
    
    https://kr.mathworks.com/discovery/slam.html
    
- **Simultaneous localization and mapping**
    
    https://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping
    
- **SLAM이란?**
    
    [https://cvlearnblog.notion.site/SLAM-f16a75f894ca48d3aa851bca99ec7cce](https://www.notion.so/SLAM-f16a75f894ca48d3aa851bca99ec7cce?pvs=21)