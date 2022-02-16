---
layout: post
title: "Back Tracking"
categories: [Algorithm]
tags: [Algorithm, Java]
description: Back Tracking 정리

comments: true

toc: true
toc_sticky: true
---

## Back Tracking

+ 재귀를 쓰는 이유: n 중 반복문 구현

<br>

**재귀**를 사용해 순열과 조합을 구현했다.

<br>

2자리 3진수

```java
/*
00
01
02
10
11
12
20
21
22
*/

for(int i = 0; i < 3; i++){
    for(int j = 0; j < 3; j++){
        System.out.println(i + "" + j);
    }
}
// N자리 M진수에서
// 3 = M 진수역할
// 반복문의 횟수가 N 자리 역할
```

<br>

### 1 번 템플릿 : 순열

<br>

```java
// 중복을 허용한 순열 m의 n승이 된다.

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    static int n;
    static int m;
    static int[] arr;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        arr = new int[n];

        recur(0);
    }

    public static void recur(int cur) {
        if (cur == n) {
            for (int i = 0; i < n; i++) {
                System.out.print(arr[i] + " ");
            }
            System.out.println();
            return;
        }

        for (int i = 0; i < m; i++) {
            arr[cur] = i;
            recur(cur + 1);
        }
    }
}
```

<br>

### 2번 템플릿 : 중복을 제거한 순열

<br>

```java
// n자리 m진수 중 한케이스 내에서 중복 제거
// visited

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    static int n;
    static int m;
    static int[] arr;
    static boolean[] visited;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        arr = new int[n];
        visited = new boolean[n];

        recur(0);
    }

    public static void recur(int cur) {
        
        // 기저 조건
        if (cur == n) {
            for (int i = 0; i < n; i++) {
                System.out.print(arr[i] + " ");
            }
            System.out.println();
            return;
        }

        // 재귀 호출
        for (int i = 0; i < m; i++) {
            if(visited[i]){
                continue;		// 사용중이면 건너뜀
            }
            arr[cur] = i;
            visited[i] = true; // 사용중인지
            recur(cur + 1);
            visited[i] = false; // 출력이 되면 해제
        }
    }
}
```

<br>

### 3번 템플릿 : 조합

<br>

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {
    static int n;
    static int m;
    static int[] arr;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        arr = new int[n];

        recur(0, 0);
    }

    public static void recur(int cur, int start) {
        if (cur == n) {
            for (int i = 0; i < n; i++) {
                System.out.print(arr[i] + " ");
            }
            System.out.println();
            return;
        }

        for (int i = start; i < m; i++) {
            arr[cur] = i;
            recur(cur + 1, i + 1);
        }
    }
}
```

<br>

<u>1 차원</u>에서의 Back Tracking이다.

<u>2 차원</u>에서의 Back Tracking은 다음에 다뤄보겠다.

<br>

### 시간 복잡도

+ 1번 템플릿 → 하나의 함수에서 m 개 호출 + n중 중첩 => m^n
+ 2번 템플릿 → nPm
+ 3번 템플릿 → nCm