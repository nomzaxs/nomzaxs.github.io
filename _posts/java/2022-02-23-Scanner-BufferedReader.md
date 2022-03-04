---
layout: post
title: "Scanner vs BufferedReader"
categories: [Java]
tags: [Programing, Java]
description: Scanner와 BufferedReader 정리

comments: true

toc: true
toc_sticky: true
---

## Scanner & BufferedReader

Java를 처음 배울 때 Scanner를 먼저 배웠고 Scanner가 익숙하지만 좀 더 효율적인 코드를 작성하기 위해서 BufferReader를 사용해야 한다.

<b>왜?</b> 라는 생각에 동작 방식부터 알아봤고, 먼저 Oracle의 docs를 비교해 보면

<br>

  <img
    src="https://user-images.githubusercontent.com/84614785/155346165-eb21d48c-a8c3-4ca8-a127-0d18e9fb9754.png"
    width="350"
  />

편의성을 제공하는 java.util Package 안에 Scanner가 있고

<br>

  <img
    src="https://user-images.githubusercontent.com/84614785/155346435-f52fcc46-0e87-4c96-a40e-bceb271e315f.png"
    width="350"
  />

입출력과 관련된 java.io Package 안에 BufferedReader가 있다.

<br>

Java Standrd API는 여러 패키지로 구성되어 제공되는데 각 패키지는 다음과 같다.

<br>

|Java Package | 설명|
|:-----:|:-------------:|
|java.lang|프로그래밍의 기본적인 Class들을 제공 // import 호출하지 않아도 기본적으로 로딩됨|
|java.util|프로그래밍의 유용한 유틸리티 Class들을 제공|
|java.io|프로그램 입출력과 관련된 Class들을 제공|
|java.net|네트워크 프로그램과 관련된 클래스들을 제공|
|java.awt|GUI 프로그램 개발을 위한 클래스들을 제공|

<br>

<b><u>Scanner</u></b>는 공란과 줄 바꿈을 모두 입력값의 경계로 인식해 더 쉽게 데이터를 입력받을 수 있고, 데이터 타입을 입력받는 시점에서 결정되므로 별도의 Casting이 필요하지 않다는 편의성을 제공하기에 속도적인 측면에서 오래 걸린다는 단점이 있다.

<br>

다음과 같이 선언해 사용한다.

<br>

```java
import java.util.Scanner;         // import

Scanner scan = new Scanner(System.in);

String s = scan.next();        // 다음 토큰을 문자열로 입력
int num = scan.nextInt();      // 다음 토큰을 int타입으로 입력
```

<br>

<b><u>BufferedReader</u></b>는 InputStreamReader의 한 글자 단위로 읽어오는 단점을 보완해 버퍼링 기능이 추가된 Class로 사용자의 요청마다 데이터를 읽어오는 것이 아닌 일정한 크기의 데이터를 한 번에 읽어와 버퍼에 보관한 후, 요청이 있을 때 버퍼에서 데이터를 읽어오는 방식이다.

그렇기에 속도가 빠르고 시간 부하가 적다.

<br>

다음과 같이 선언해 사용한다.

<br>

```java
import java.io.BufferedReader;    // import
import java.io.InputStreamReader;

BufferedReader br = new BufferedReader(new InputStramReader(System.in));

String s = br.readLine();         // 한 줄을 입력
int num = Integer.parseInt(br.readLine());  // int값을 받아오기 위해서 형변환이 필요하다.
```

<br>

<b>즉</b>, Scanner는 편의성을 제공하지만 속도적인 측면에서 느리다는 단점을 가지고 있다.

이와 달리 BufferedReader는 Buffer를 이용해 단순하게 데이터를 읽어 들이기 때문에 속도가 빠르지만, 데이터를 따로 가공해야 하므로 조금 번거롭다는 단점을 가지고 있다.

Scanner와 BufferedReader의 차이점을 비교하면 다음과 같다.

<br>

||Scanner|BufferedReader|
|:---:|:---:|:---:|
|Buffer Size|1024|8192|
|Synchronized|X|O|
|Parsing|문자열 파싱 가능|단순히 String으로 읽어 들임|
|Exception|IOException 처리를 숨겨준다|IOException을 써줘서 예외 처리해야 한다|