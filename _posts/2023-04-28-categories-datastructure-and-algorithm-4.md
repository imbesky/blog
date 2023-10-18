---
title: "[자료구조알고리즘] 4. 정렬(버블, 선택, 삽입)"
excerpt: "버블, 선택, 삽입 정렬"

categories:
  - Concept
tags:
  - [자료구조알고리즘, CS개념]

permalink: /concept/datastructure-and-algorithm-4/

toc: true
toc_sticky: true

date: 2023-04-28
last_modified_at: 2023-10-18
---

# 4. 정렬(버블 정렬, 선택 정렬, 삽입 정렬)

정렬 알고리즘: 정렬되지 않은 배열이 주어졌을 때 오름차순으로 정렬하는 방법

## 버블 정렬 bubble sort
비교 comparison + 교환 swap

### pass through
1. 첫 번째 항목과 두 번째 항목을 비교
2. 첫 번째 항목 > 두 번째 항목이면 교환
3. 포인터를 한 칸씩 오른쪽으로 이동
4. 배열의 끝 혹은 이미 정렬된 부분까지 반복
5. 교환이 일어나지 않는 패스스루가 생길 때까지 반복

### 코드 구현

``` python
def bubble_sort(list):
  index = len(list) - 1
  sorted = false

  while not sorted:
    sorted = true
    for i in range(index):
      if list[i] > list[i+1]:
        list [i], list[i+1] = list[i+1], list[i]
        sorted = false
    index -= 1

  return list
```

### 빅 오
최악의 시나리오에서 비교와 교환 각 N-1 + ... + 1번
총 단계 수 2(N-1 + ... + 1) = (N-1)N 번

따라서 O(N^2), 이차 시간 quadratic time

### 선형 해결법
중첩 루프를 쓰지 않고 버블 정렬을 구현할 수 있음

``` python
def duplicateValueCheck(array):
  existingValues = []

  for i in array:
    if existingValues[i] == 1:
      return true
    else:
      existingValues[i] == 1
  return false
```

빅 오로는 O(N)
다만 새로운 배열을 형성하므로 메모리 낭비가 발생한다는 단점이 있음

## 선택 정렬 selection sort

### pass through
1. 포인터를 오른쪽으로 이동하면서 가장 작은 값을 찾는다
2. 패스스루 시작점에 있던 값과 교환한다
3. 배열 끝에서 시작하는 패스스루가 나올 때까지 반복한다

### 코드 구현
``` python
def selection_sort(list):
  len = len(list)

  for i in range(len-1):
    smallest = i
    for j in range(i+1, len):
      if list[i]<list[j]:
        smallest = j
    if i != smallest:
      list[i], list[j] = list[j], list[i]
  return list
```

### 빅 오
최악의 시나리오: 비교 N-1 + ... + 1 번, 교환 N-1번
빅 오 표기로는 O(N^2)이라 버블 정렬과 동일하지만 실제로는 더 효율적

## 삽입 정렬 insertion sort
최악의 시나리오 외에 고려할 가치가 있는 상황

### pass through
1. 인덱스 1의 값 삭제, 임시 변수에 저장
2. 시프트 단계 시작: 공백(삭제한 인덱스의 자리) 왼쪽에 있는 각 값과 임시 변수의 값 비교
3. 임시 변수 < 공백 왼쪽 값 이라면 그 값을 오른쪽으로 시프트; 공백은 왼쪽으로 옮겨짐
4. 임시 변수보다 작은 값을 만나거나 배열의 왼쪽 끝에 도달하면 시프트 종료
5. 임시 변수를 현재 공백에 삽입
6. 배열의 마지막 인덱스에서 패스스루를 시작할 때까지 반복

### 코드 구현

``` python
def insertion_sort(array):
  for i in range(1, len(array)):
    temp = array[i]
    pointer = i -1
    while pointer>=0:
      if temp < array[pointer]:
        array[pointer+1] = array[pointer]
        pointer -= 1
      else:
        break
      array[pointer+1] = temp
  return array
```

### 빅 오
최악의 시나리오: (N-1)번의 비교, 시프트
O(N^2)

## 평균 시나리오
최악의 시나리오에서는 선택 정렬이 삽입 정렬보다 빠르다.
단, 가장 빈번하게 일어나는 평균 시나리에서는 이야기가 좀 다르다.

데이터의 반 정도를 비교/교환/시프트 등등 해야 하는 평균 시나리오의 경우 두 정렬의 단계 수는 유사하다.