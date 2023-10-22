---
title: "[자료구조알고리즘] 6. 재귀"
excerpt: "재귀"

categories:
  - Concept
tags:
  - [자료구조알고리즘, CS개념]

permalink: /concept/datastructure-and-algorithm-6/

toc: true
toc_sticky: true

date: 2023-05-09
last_modified_at: 2023-10-21
---
# 6. 재귀 

## 재귀 recursion
함수가 자기 자신을 호출하는 것
- 기저 조건 base case; 기저 조건이 없으면 재귀가 끝나지 않고 함수 무한 루프를 실행하기도 함 

### 호출 스택 call stack
어떤 함수를 호출 중인지 기록하는 스택 

- 재귀 함수를 사용하면 호출 스택에 이전 함수가 지속적으로 쌓임
- passing a value up through the call stack; 호출 스택을 통해서 각 재귀 함수의 계산된 값을 부모 함수에 반환하게 되고, 최초로 호출된 함수(스택 가장 밑에 있던 함수)가 최종적으로 값을 계산하게 됨 

### 스택 오버플로우
호출 스택이 늘어나 단기 메모리에 데이터를 저장할 공간이 없을 때 발생 

- call stack pointer가 stack bound를 뛰어넘었을 때 발생
- call stack의 주소 공간에 한계가 있기 때문에 존재 

## 재귀 카테고리: 반복 실행
반복적으로 한 작업을 실행하는 알고리즘 

### 반복 실행 예시
빵의 개수가 0이 될때까지 판매하는 알고리즘
``` python
def breadSell(number):
  print(number)
  if number==0:
    return;
  else:
    breadSell(number-1)
```
빵의 개수를 1씩 줄여 나가는 작업을 반복적으로 실행함 

### 추가 인자 넘기기
같은 작업을 반복 실행하면서 원본 배열을 제자리 수정하는 알고리즘
``` python
def twice(array, index=0):
  if index >= len(array):
    return 

  array[index] *= 2
  twice(array, index + 1)
```
- 배열과 인덱스를 parameter로 넘기는 재귀 알고리즘
- 기저 조건으로는 index가 항상 배열의 길이보다 작도록 했다
- 또한 첫 번째 재귀 호출에서 인덱스가 항상 0이 될 수 있도록 기본값을 할당했다 

## 재귀 카테고리: 계산
하위 문제의 계산 결과에 기반해 계산할 수 있을 때의 재귀 

- 하위 문제: 입력을 더 작게 한 똑같은 문제 

### 하위 문제의 두 가지 계산 방식
1. 상향식 botton up
``` python
def factorial(n, i=1, product=1):
  if i>n:
    return product
  return factorial(n, i+1, product*i)
```
- 루프에 비해 특별한 장점 없음
- 상향식에서 루프와 재귀는 계산 방식이 같다 

2. 하향식 top down
주어진 문자열에서 특정 문자의 개수를 세는 알고리즘
``` python
def find-x(str):
  if str[0]=="x":
    return 1 + find-x(str[1:])
  else:
    return find-x(str[1:])
```
- 문제를 해결하는 새로운 사고 전략 제공
- 배열의 합, 문자 뒤집기 등에 응용 가능 

3. 하향식 사고 절차
- 1) 작성 중인 함수가 이미 구현되었다고 상정
- 2) 하위 문제를 탐색
- 3) 하위 문제에 대한 함수를 호출하면 어떻게 될지 가정하고, 시작 

## 계단 문제
N개짜리 계단이 있고 한 번에 올라갈 수 있는 계단의 최대 개수가 정해져 있을 때 계단 끝에 올라가는 경로의 개수 구하기 

``` python
def stair(n):
  if n<0:
    return 0
  elif n==1||n==0:
    return 1 

  return stair(n-1) + ... + stair(n-limit)
```
- 계단의 총 개수가 n 개이고 한 번에 오를 수 있는 계단의 최대 개수가 limit일 때 경로의 수를 계산하는 하향적 재귀 알고리즘 

## 애너그램
문자열 내 모든 문자들을 재배열한 문자열 

애너그램의 배열을 반환하는 함수
```python
def anagram(str):
  if len(str)==1:
    return [str] 

  array = []
  sub_anagram = anagram(str[1:]) 

  for a in sub_anagram:
    for i in range(len(a)-1):
      array.append(a[:i]+str[0]+a[i:]) 

  return array
``` 

### 애너그램의 효율성
O(N!) factorial time