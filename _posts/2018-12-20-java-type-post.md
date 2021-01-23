---
layout: post
title: "JAVA 변수 타입 별 사용"
description: "java의 변수 기본형 타입 별 사용방법 정리"
date: 2018-12-20
tags: [JAVA, 자바, 프로그래밍]
comments: true
share: true
---

## 코드

~~~
		 //long 타입 값에는 소문자 l이나 대문자 L을 붙여야 합니다.
		 long longNum= 3456789L;
		 
		 // float 타입 값에는 소문자 f나 대문자 F를 붙여야 합니다.
	         float floatNum = 32.5f;

		 double ddoubleNum = 23.34; //실수형

		 boolean flag = false; //논리형

		 char charValue = 'a'; //문자형

		 int intValue = 20; //정수형
	
~~~


### 기본형 타입(Primitive type)
총 8가지의 기본형 타입(boolean, byte, short, int, long, float, double, char)이 있다.
기본값이 있기 때문에 Null이 존재하지 않는다. 만약 기본형 타입에 Null을 넣고 싶다면 래퍼 클래스를 활용한다.
실제 값을 저장하는 공간으로 스택(Stack) 메모리에 저장된다.
만약 컴파일 시점에 담을 수 있는 크기를 벗어나면 에러를 발생시키는 컴파일 에러가 발생한다.

---
> 타입 : 할당 메모리 - 기본값 - 표현범위
#### 논리형 -
> boolean : 1byte - false - true/false

#### 정수형
> byte : 1byte - 0 - (-128)~127

> short : 2byte - 0 - (-32,768)~32,767

> int(기본) : 4byte - 0 - (-2,147,483,648) ~ 2,147,483,647

> long : 8byte - 0L - (-9,223,372,036,854,775,808) ~ 9,223,372,036,854,775,807

#### 실수형
> float : 4byte - 0.0F -  (3.4 X 10^-38) ~ (3.4 X 10^38) 의 근사값

> double(기본) : 8byte - 0.0 - (1.7 X 10^-308) ~ (1.7 X 10^308) 의 근사값

#### 문자형
> char : 2byte(유니코드) -  '\u0000' - 0 ~ 65,535
--- 

### 참조형 타입(Reference type)
기본형 타입을 제외한 타입들은 모두 참조형 타입(Reference type)이다.
Null이 존재하며 값이 힙(Heap) 메모리에 저장된다.
객체나 배열을 Null 값으로 받으면 NullPointException이 발생하므로 변수값을 넣어야 한다.


### 예제1

~~~

	public static void main(String[] args) {
		// 정수를 담는 변수 count 선언
		int count = 1;
		// 실수를 담는 변수, average 선언
		double average = 2;
		// 두 수를 출력하시오.
        System.out.println(count);
        System.out.println(average);
	}
~~~

	

--- 


### 예제2

~~~

public static void main(String[] args) {
		int number; //정수형 변수 number 선언
		number = 20; //number값에 20 넣기

		System.out.println(number); //number값 출력
		System.out.println(number+10); //number값에 10 더한 값 출력

		double a = 4.14; // 실수형 변수 a 선언하고 4.14 값 넣기
		System.out.println(a); // a 값 출력
		System.out.println((int)a); // 실수형 a를 정수형으로 형변환해서 출력

		int num1, num2; //정수형 변수 num1과 num2 선언
		num1 = 4; //num1에 4넣기
		num2 = 14; //num2에 14 넣기

		System.out.println(num1+num2); //num1값과 num2값을 더한 값 출력
		System.out.println(num1*num2); //num1값과 num2값을 곱한 값 출력
	}
~~~
	

--- 
