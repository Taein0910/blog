---
layout: post
title: "JAVA 객체지향 개념"
description: "java가 객체지향이라고 하는데, 그게 도대체 뭘까?"
date: 2019-05-17
tags: [JAVA, 자바, 프로그래밍]
comments: true
share: true
---


## 객체지향—
#### 여러 작업을 분업화한 다음 나중에 합치는 프로그래밍 패러다임

## 클래스 —
#### 프로그래밍에서 특정 객체를 생성하기 위해 변수와 메소드를 정의하는 틀


### 생성

~~~
public class 클래스명 {

}
~~~


## 객체 - 클래스에 의해 생성된 부수적인 조각들
> 클래스명 객체명 = new 클래스명()
### 객체변수는 각 클래스에서 <mark>독립적</mark>으로 활동 (서로 공유 X)

~~~
public static void main(String[] args) {
Animal cat = new Animal(); cat.setName("boby");
Animal dog = new Animal(); dog.setName("happy");
System.out.println(cat.name);
System.out.println(dog.name);
}
~~~
> [출력] boby happy

---
## 메소드 — 어떤 일을 수행한 다음에 결과물을 내어놓는 것
~~~
public int sum(int a, int b) {
return a+b;
public 자료형 메소드명(입력자료형1 입력변수1, 입력자료형2 입력변수2, …) {
…
return 리턴값;
}
~~~

### 메소드의 분류
- 입력과 출력이 모두 있는 메소드
- 입력과 출력이 모두 없는 메소드
- 입력은 없고 출력은 있는 메소드
- 입력은 있고 출력은 없는 메소드

### 생성자 — 클래스의 변수를 정하는 역할
### 상속 — 쉽게 말하면 자식클래스가 부모클래스로 부터 무언가를 물려받는 것

~~~
자식클래스 extends 부모클래스
public class Animal {
…
}
public class Dog extends Animal {
…
}
~~~

위 코드에서 <mark>Dog클래스는 Animal클래스와 상속</mark>되었다.
그래서 Animal과 Dog클래스의 메소드, 객체는 서로 공유한다.

단, 아래 코드를 작성하면
~~~
Dog dog = new Animal();
~~~
컴파일 오류: 부모 클래스로 만든 객체는 자식 클래스의 자료형으로 사용할 수 없다.

>다른 언어에서 가능한 다중 상속은 java에서 지원하지 않는다.

[참고]
https://wikidocs.net/218
