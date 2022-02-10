---
layout: post
title: "Binary Search"
categories: [Algorithm]
tags: [Algorithm, Java]
description: Java로 구현한 Binary Search

published: true
comments: true

toc: true
toc_sticky: true
---

## Binary Search

<u>정렬된</u> 배열 또는 리스트에 빠른 탐색을 위한 방법중 하나이다.

- 배열의 중앙의 값을 조사해 찾고자 하는 값보다 작으면 오른쪽 부분을 탐색, 크면 왼쪽 부분을 탐색해 탐색의 범위를 절반으로 줄이는 탐색기법이다.
- 탐색을 위해서는 **<u>정렬</u>**되어 있어야 한다.

<br>

### 구현 방법

1. - low = **0**
   - high = **arr.length - 1**
   - mid : **(low + high) / 2**
   - key : **찾는 값**
2. if(arr[mid] < key) { high = mid - 1 }
3. if(arr[mid] > key) { low = mid + 1 }
4. 다시 mid와 key를 비교한다.
5. if(arr[mid]  == key) { return mid }

<br>

반복문을 통해 나타내면 다음과 같다.

```java
int binSearch(int key, int low, int high) {
	int mid;

	while(low <= high) {
        mid = (low + high) / 2;
		
        if(key == arr[mid]) {			// 탐색 성공 시
            return mid;
        } else if(key < arr[mid]){		// 왼쪽 부분 탐색
            high = mid - 1;
        } else{							// 오른쪽 부분 탐색
            low = mid + 1;
        }
	}
	return -1; 							// key가 array에 없을 시
}
```

<br>

재귀 코드로 나타내면 다음과 같다.

```java
int binSearch(int key, int low, int high) {
	int mid = (low + high) / 2;

	if(low <= high) {
		if(key == arr[mid]) { 			// 탐색 성공 시
			return mid;
		} else if(key < arr[mid]) {		// 왼쪽 부분 탐색 
			return binarySearch1(key ,low, mid-1);
		} else {						// 오른쪽 부분 탐색
			return binarySearch1(key, mid+1, high);
		}
	}
	return -1; 							// key가 array에 없을 시
}
```

<br>

Binary Search의 시간 복잡도는 탐색을 반복 할 때마다 탐색 범위를 반으로 줄인다.

n의 범위에서 k번 반복하게 된다면 n/2^k = 1이 되기에 k = log 2 n이 되므로 **<u>O(log n)</u>**이 된다.

