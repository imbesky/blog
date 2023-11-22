---
title: "[자료구조알고리즘] 8. 속도를 높이는 재귀 "
excerpt: "효율적인 재귀 알고리즘 사용법"

categories:
  - Concept
tags:
  - [자료구조알고리즘, CS개념]

permalink: /concept/datastructure-and-algorithm-8/

toc: true
toc_sticky: true

date: 2023-05-16
last_modified_at: 2023-11-22
---
# 8. 속도를 높이는 재귀 

## 퀵 정렬 Quicksort 

컴퓨터 언어 중 대다수가 내부적으로 채택한 정렬 알고리즘 

- 특히 평균적인 시나리오에서 효율적
- 최악의 시나리오(역순으로 정렬된 배열)에서는 삽입 정렬이나 선택 정렬과 성능이 유사
- 분할이라는 개념에 기반 

[삽입 정렬이나 선택 정렬이 궁금하다면?](https://imbesky.github.io/concept/datastructure-and-algorithm-4/) 

### 분할 partitioning 

배열로부터 임의의 수(피벗 pivot)를 가져와 피벗보다 작은 수는 모두 왼쪽에, 큰 수는 모두 오른쪽에 두는 것 

1. 피벗 고르기 

- 어떤 위치든 무방 

2. 두 포인터를 설정 

- 하나는 배열의 가장 왼쪽 값에 할당
- 다른 하나는 피벗을 제외한 배열의 가장 오른쪽 값에 할당 

3. 왼쪽 포인터를 한 셀씩 오른쪽으로 옮기면서 피벗보다 크거나 같은 값에 도달하면 정지 

4. 오른쪽 포인터를 한 셀씩 왼쪽으로 옮기면서 피벗보다 작거나 같은 값, 혹은 배열 맨 앞에 도달하면 정지 

5. 왼쪽 포인터가 오른쪽 포인터에 도달하거나 넘어섰다면 다음 단계 진행 

- 그렇지 않다면 가리키고 있는 값을 교환한 후 3~5단계 반복 

6. 왼쪽 포인터가 현재 가리키고 있는 값과 피벗 교환 

- 분할 이후에는 피벗 왼쪽의 값은 모두 피벗보다 작고, 오른쪽의 값은 모두 피벗보다 큼 

#### 코드로 보는 분할 

- 분할해야 하는 리스트는 필드라고 가정 

``` python
def partitioning(start_index, end_index):
  pivot = list[end_index]
  left_pointer = start_index
  right_pointer = end_index - 1 

  while(true):
    while(list[left_pointer] < pivot):
      left_pointer++
    while(list[right_pointer] > pivot):
      right_pointer++
    if(left_pointer >= right_pointer):
      break
    else:
        list[left_pointer], list[right_pointer] = list[right_pointer], list[left_pointer]
        left_pointer++ 

  list[left_pointer], pivot = pivot, list[left_pointer] 

  return left_pointer
``` 

### 퀵 정렬의 단계 

1. 배열을 분할 

2. 피벗의 왼쪽과 오른쪽에 있는 하위 배열에 대해 1~2단계를 재귀적으로 반복 

- 하위 배열들을 또다시 분할한다. 

3. 기저조건: 하위 배열의 원소 개수가 0또는 1이면 끝 

### 코드로 보는 퀵 정렬 

- 정렬해야 하는 리스트는 필드라고 가정
- `partitioning()`과 같은 클래스 

``` python
def quickSort(start_index, end_index):
  if(start_index - end_index <= 0):
    return 

  index = partitioning(start_index, end_index)
  quickSort(start_index, index - 1)
  quickSort(index + 1, end_index)
``` 

### 퀵 정렬의 효율성 

분할의 효율성
- 비교: 평균적으로 N번
- 교환: 평균적으로 N.4번
따라서 O(N) 

퀵 정렬의 효율성
- 배열 하위 배열로 나누기: logN
- 배열 분할: N
O(N*logN) 

### 최악의 시나리오 

= 피벗이 한쪽 끝에 있을 때
- 교환 한 번
- 배열의 원소 수만큼 비교
따라서 O(N^2) 

최선의 시나리오: 피벗의 하위 배열의 한 가운데에 있을 때 

### 퀵 정렬 vs. 삽입 정렬 

1. 최악의 시나리오 

삽입 정렬: O(N^2)
퀵 정렬: O(N^2) 

2. 최선의 시나리오 

삽입 정렬: O(N)
퀵 정렬: O(NlogN) 

3. 평균 시나리오 

삽입 정렬: O(N^2)
퀵 정렬: O(NlogN) 

## 퀵 셀렉트 

- 분할에 기반
- 퀵 정렬과 이진 검색을 닮은 알고리즘
- 무작위로 정렬된 배열이 있을 때 배열에서 특정한 위치의 숫자를 구할 때 용이
- 전체 배열을 정렬하지 않고도 값을 찾을 수 있음 

### 배열에서 n번째로 크거나 작은 숫자 찾기 

n번째로 작은 숫자를 찾는다고 가정하자 

1. 배열을 분할 

2. 피벗이 n번째보다 크다면 피벗의 오른쪽을, n번째보다 크다면 피벗의 왼쪽을 다시 분할 

3. 원하는 순서의 숫자가 피벗이 될 때까지 반복 

### 코드로 구현한 퀵 셀렉트 

앞선 코드들과 같은 클래스에 있다고 가정 

``` python
def quickSelect(target):
  start_index = 0
  end_index = len(list) - 1 

  while(true):
    pivot = partitioning(start_index, end_index)
    if(pivot == target):
      break
    else if(pivot > target):
      end_index = pivot - 1
    else if(pivot < target):
      start_index = pivot + 1 

  return list[pivot]
``` 

책에 있는 예제에서는 재귀를 활용했다. 

### 효율성 

평균 시나리오: O(N) 

## 알고리즘과 정렬 

- 현재까지 가장 빠른 정렬 알고리즘의 속도는 O(NlogN)
- 병합 정렬 mergesort 등
- 정렬의 속도는 다른 알고리즘에도 영향을 미침 

- 배열을 미리 정렬하면 중복 확인 알고리즘도 개선할 수 있음 

``` python
for i in range(len(sortedList) - 1):
  if(sortedList[i] == sortedList[i + 1]): 
    // 중복이 존재함
    return
```