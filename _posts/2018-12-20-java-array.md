---
layout: post
title: "JAVA 배열"
description: "JAVA 배열 사용법"
date: 2021-01-10
tags: [JAVA]
comments: true
share: true
---

## 배열(Array, List, arrayList)
[(추가)1차 및 2차 배열 선언하기](#edited)
자료를 저장하는 공간으로 개념 자체는 변수와 비슷한데, 배열은 index를 통해 특정 위치의 값을 변경하거나 삭제, 가져올 수 있다.

즉 배열이란 동일한 타입의 값을 여러 개 저장할 수 있는 것
인덱스라고 불리는 []로 감싸며 인덱스는 0부터 시작한다.
이 인덱스를 통해 배열의 길이나 순서를 나타낸다.

배열은 한 번 작성하면 사이즈를 변경할 수 없다.
그렇기 때문에 기존 배열의 사이즈를 변경하려면 새로운 배열을 작성한 후 새로운 배열로 데이터를 복제해야 한다.

~~~
int[] newArray = Arrays.copyOf(기존배열, 기존배열.length);
~~~

---

#### 
~~~
int[] array = new int[11];
~~~

또는

~~~
int array[] = new int[11];
~~~

new int[]에서 대괄호 안에 있는 숫자는 배열의 크기를 의미 이렇게 말고, 아예 선언이랑 배열 안에 값을 지정하는 방법

~~~
int[] array = {1, 2, 3, 4, 5};
~~~

배열도 역시 자료의 타입이랑 변수 타입이랑 맞춰줘야 함. 문자를 배열에 넣으려면

~~~
String[] array = {"a", "b", "c", "d");
~~~

배열의 index는 0부터 시작 위 예제에서 a를 가져오려면 index 0값을 가져와야 함. 가져오는 방법은

배열의 이름[index값];

~~~
array[0];
~~~


값을 수정하는 것도 마찬가지

~~~
array[0] = 3;
~~~

---

<a name="edited"></a>
## 1차원 배열과 2차원 배열

~~~
 // 1차원 배열 선언
            int[] array = new int[5];
            int[] array2 = {0, 1, 2, 3, 4};
            int[] array3 = new int[]{0, 1, 2, 3, 4};

            // 2차원 배열 선언
            int[][] array4 = new int[5][5];
~~~