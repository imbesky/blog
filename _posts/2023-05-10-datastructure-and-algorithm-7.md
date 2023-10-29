---
title: "[자료구조알고리즘] 7. 동적 프로그래밍"
excerpt: "동적 프로그래밍"

categories:
  - Concept
tags:
  - [자료구조알고리즘, CS개념]

permalink: /concept/datastructure-and-algorithm-7/

toc: true
toc_sticky: true

date: 2023-05-10
last_modified_at: 2023-10-29
---
# 7. 동적 프로그래밍 

## 추가적인 재귀 호출 

우선 다음과 같이 주어진 배열의 최솟값을 찾는 알고리즘이 있다고 하자.
``` python
def min(array):
  if len(array) == 1:
    return array[0]
  
  if array[0] > min(array[1:]): // 첫 번째 호출
    return array[0]
  else:
    return min(array[1:]) // 두 번째 호출
```
이때 array = [a, b]이고 a<b 라고 가정해 보자(a, b는 임의의 양수이다).
이 함수는 `if array[0] > min(array[1:])`에서 처음으로 min([b]) 를 호출한다.
그리고 `return min(array[1:])`에서 두 번째로 같은 함수를 호출한다.
즉 재귀 함수를 중복으로 호출하게 되고, 이미 계산한 값을 또다시 계산하게 된다.
이 함수의 효율성은 O(2^N) 

### 1. 변수에 저장하기 

이 중복 호출을 개선하기 위해서 계산한 결과값을 변수에 저장하는 방법을 사용할 수 있다.
``` python
def min(array):
  if len(array) == 1:
    return array[0]
  
  smaller_array_min = min(array[1:]) 

  if array[0] > smaller_array_min:
    return array[0]
  else:
    return smaller_array_min
```
개선된 이 함수의 효율성은 O(N)이다. 

## 하위 문제 중첩
피보나치 수열을 알고리즘으로 구현해 보자.
``` python
def fibonacci(n):
  if n==0 or n==1:
    return n 

  return fibonacci(n-2) + fibonacci(n-1)
```
n을 매개 변수로 가진 함수는 n-2, n-1을 매개변수로 가진 함수를 호출한다.
n-1은 n-3, n-2를
n-2는 n-4, n-3을 호출한다.
이때 같은 재귀 함수를 호출하게 되면서 하위 문제가 중첩되는 문제가 생긴다.
이 함수의 효율성은 O(2^N)이다. 

하위 문제: 동일한 문제를 작게 만들어 해결함으로써 생기는 어떤 문제의 더 작은 문제
하위 문제 중첩 overlapping subproblems: 같은 하위 문제가 중첩되는 현상


### 메모이제이션 memoization
메모이제이션: 하위 문제가 중첩될 때 재귀 호출을 감소시키는 기법
먼저 계산한 함수 결과를 기억해 중복되는 재귀 호출을 막는다. 

``` python
def fibonacci(n, data):
  if n==0 or n==1:
    return n 

  if not data.get(n):
    data[n] = fibonacci(n-2, data) + fibonacci(n-1, data) 

  return data[n]
```
함수를 처음 호출할 때 data에 빈 해시 테이블 {}을 매개변수로 넘긴다.
계산 결과를 data 해시 테이블에 저장하기 때문에 중복되는 재귀 호출이 일어나지 않는다.
이 함수의 효율성은 O(N)이다. 

### 상향식
같은 문제를 재귀가 아닌 다른 방식으로 해결하는 방법 

``` python
def fibonacci(n):
  if n==0:
    return n 

  a = 0
  b = 1 

  for i in range(1, n):
    temp = a
    a = b
    b = temp + a 

  return b
```
루프를 사용해서 해결했다.
효율성은 O(N). 

`재귀가 직관적이지 않은 이상 일반적으로 상향식을 사용하는 것이 더 낫다`
메모이제이션을 사용하더라도 재귀는 호출 스택을 통해 메모리를 소모하기 때문