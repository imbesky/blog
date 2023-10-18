---
title: "[자료구조알고리즘] 3. 빅 오 표기법"
excerpt: "빅 오 표기법"

categories:
  - Concept
tags:
  - [자료구조알고리즘, CS개념]

permalink: /concept/datastructure-and-algorithm-3/

toc: true
toc_sticky: true

date: 2023-04-27
last_modified_at: 2023-10-18
---

# 3. 빅 오 표기법

## 빅 오
데이터 원소가 N개일 때 알고리즘에 필요한 단계 수

## 특징
- 데이터가 늘어날 때 알고리즘의 성능 변화를 나타냄
- 일반적으로 최악의 시나리오를 의미
- syntax: O(단계 수)
- 계수와 상수는 생략함

## 유형
1. 선형 시간 linear time
O(N)
ex 선형 검색

2. 상수 시간 constant time
O(상수)
ex 읽기

3. 로그 시간 log time
O(logN)
ex 이진 검색

## 카테고리
- 빅 오 표기법은 일종의 카테고리를 나누는 표기법
- 같은 빅 오 카테고리 내라도 효율성의 차이가 있을 수 있음
- ex 선택 정렬과 버블 정렬은 같은 빅 오 표기법으로 나타낼 수 있으나 실제로는 선택 정렬이 더 효율적