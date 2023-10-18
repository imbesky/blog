---
title: "[자료구조알고리즘] 2. 알고리즘"
excerpt: "알고리즘 개론"

categories:
  - Concept
tags:
  - [자료구조알고리즘, CS개념]

permalink: /concept/datastructure-and-algorithm-2/

toc: true
toc_sticky: true

date: 2023-04-26
last_modified_at: 2023-10-18
---

# 2. 알고리즘

## 알고리즘
어떤 과제를 완수하는 명령어 집합

## 정렬된 배열 odered array의 연산
값이 순서대로 정렬된 배열에서의 연산

### 삽입
- 검색 -> 이동 -> 삽입
- 삽입된 값의 자리와 상관 없이 단계 수는 유사; 앞쪽에 놓이면 이동 수 증가, 뒷쪽에 놓이면 검색 수 증가

### 선형 검색 linear search

``` python
def linear_search(array, search_value):
  while i range(len(array)):
    if array[i] == search_value:
      return i
    elif array[i] > search_value:
      break
    return null
```

- 일반 배열에서 보다 효율적
- 찾는 값보다 큰 값이 나오면 멈춤
- 최악의 시나리오: n단계

### 이진 검색 binary search

``` python

def binary_search(array, search_value):
  lower_pointer = 0
  upper_pointer = len(array) - 1

  while lower_pointer <= upper_pointer:
    mid_pointer = round((lower_pointer + upper_pointer)/2)
    mid_value = array[mid_pointer]
    if search_value == mid_value:
      return mid_pointer
    elif search_value < mid_value:
      upper_pointer = mid_pointer - 1
    elif search_value > mid_value:
      lower_pointer = mid_pointer - 1
    return null

```

- 가운데 셀 값을 확인하면서 시작
- 남은 값들을 중간값과 비교, 원하는 값이 나올 때까지 반복
- 최악의 시나리오: logn/log2 즉 logn
- 선형 검색보다 빠르다