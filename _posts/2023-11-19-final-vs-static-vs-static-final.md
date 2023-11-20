---
title: "final vs. static vs. static final "
excerpt: "final, static, static final 차이점"

categories:
  - Concept
tags:
  - [concept, java]

permalink: /concept/final-vs-static-vs-static-final/

toc: true
toc_sticky: true

date: 2023-11-19
last_modified_at: 2023-11-20
---
# final vs. static vs. static final 

자바에는 여러 키워드가 존재한다.
`public`, `private` 같은 접근 제어자는 이름만으로 명확한 이해가 가능하지만 `final`, `static`, `static final`은 모호하게 다가올 때가 있어 한 번 정리해 보았다. 

## final 

### final class 

- class that is declared final cannot be subclassed
- it became immutable class like `String` 

### final method 

- method cannot be overridden by subclasses
- methods called from constructors should generally be declared final 

### final variable 

- can only be initialized once
- it can be an initializer or an assignment statement
- `blank final`: does not need to be initialized at the point of declaration but must be definitely assigned in every constructor of the class in which it is declared
- value of a final variable is not necessarily known at compile time 

참고 자료
[Oracle: Writing Final Classes and Methods](https://docs.oracle.com/javase/tutorial/java/IandI/final.html)
[wikipedia: final(Java)](https://en.m.wikipedia.org/wiki/Final_(Java)) 

## static 

- particular member belongs to a type itself, rather than to an instance of that type 

### static method 

- can be called without creating the object of class
``` java
public class Calculate{
  public static int plus(int number1, int number2){
    // logic
  }
} 

public class Calculation{
  Calculate.plus(1,2); // call method without creating object of class `Calculate`
}
```
- doesn't allow overriding
- can't use `this` or `super` 

### static fields (= class variable) 

- created and shared among all instances of that class
- no matter how many times class is instantiated, there will always be only one copy of static field belonging to it 

참고 자료
[baeldung: java static](https://www.baeldung.com/java-static) 

## static final 

이제 `static final` 키워드가 붙은 필드, 메서드에 대해서 이해할 수 있다.

### static final fields

`static`의 특성인 모든 클래스에서 공통으로 사용된다는 점과, `final`의 특성인 한 번만 값 할당이 가능하다는 점을 모두 갖춘 필드가 바로 `static final` 필드이다.

이러한 특성 때문에 `상수`의 값을 지정할 때 사용된다. 상수의 이름은 전부 대문자로 적고, 단어를 구분할 때에는 `_`를 사용하는 것이 관습이다.

### static final methods

역시 앞서 기술한 `static`과 `final` 키워드가 붙은 메서드의 특징을 모두 가졌다. 객체 생성 없이 호출 가능하며 오버라이딩 할 수 없는 메서드이다.