---
title:  "[Data Structure & Alogrithm] Merge Sort"
excerpt: "[Data Structure & Alogrithm] Merge Sort 정리"
toc: true
toc_sticky: true
categories:
  - cs
tags:
  - Data Structure & Alogrithm

---

# 📝 Merge Sort (병합 정렬)

<img src="https://k.kakaocdn.net/dn/ODZ1l/btqC7qVOcKv/BbXSyczuyzepKvhM941UF1/img.png" alt="img" style="zoom: 40%;" />



![img](https://k.kakaocdn.net/dn/caUqKB/btqC6PauZrr/USaDLGILPn8kdaF3KFZnlk/img.gif)

## 📌 핵심 요약

`"Merge Sort는 전체 정렬 대상을 여러 부분집합으로 분할하고(Divide) 각 부분 집합에 대해 정렬작업을 수행한후에(Conquer) 정렬된 부분 집합들을 다시 결합하는(Combine) 과정을 재귀적으로 반복하여 정렬을 수행한다."`



## 📌 설명

*  Merge Sort는 분할정복 기법을 사용하는 정렬 알고리즘이다. 

* 전체 정렬 대상을 여러 부분 집합으로 분할하고(Divide) 각 부분 집합에 대해 정렬 작업을 수행한 후에(Conquer) 정렬된 부분 집합들을 다시 결합하는(Combine) 분할 정복 기법을 사용한다.

* 분할(Divide) : 원소들을 같은 크기의 부분집합 2개로 분할한다. 부분 집합의 크기가 충분히 작지 않으면 재귀 호출을 이용하여 다시 계속 분할한다. 

* 정복(Conquer) : 부분집합에 있는 원소들을 정렬한다. 

* 결합(Combine) : 정렬된 각 부분 집합들을 하나의 정렬된 집합으로 결합한다.

* "8개의 데이터를 정렬하는 것 보다 이를 둘로 나눠서 4개의 데이터를 정렬하는 것이 더 쉽고 또 이들 각각을 다시 한번 둘로 나눠서 2개의 데이터를 정렬하는 것이 더 쉽다." 

  

## 📌 시간 복잡도

* 정렬수행 `O(NlogN)` 

  * N개의 원소를 부분 집합으로 logN번 분할한다.
  * 분할된 각 부분 집합의 원소들을 정렬하면서 병합하는 각 단계에서 최대 N번의 비교 연산을 수행한다.
* Merge Sort의 시간 복잡도는 최악, 평균, 최선의 경우에 상관없이 모두 `O(NlogN)`이다.  항상 2분할을 하기 때문이다.
* Merge Sort는 부분 집합을 병합하는 과정에서 임시 메모리가 추가적으로 필요하다는 단점이 있다. (정렬 대상이 연결 리스트일 경우는 단점이 되지 않음)



## 📌 소스 코드

```c++
#include<iostream>
using namespace std;

int a[10], b[10]; // 배열 b는 Merge Sort에서 추가적으로 필요한 임시 메모리 공간이다.

void merge(int start, int end) { 
	int mid = (start + end) / 2;
	int i = start, j = mid + 1, k = 0;

	while (i <= mid && j<=end){
		if (a[i] <= a[j])
			b[k++] = a[i++];
		else
			b[k++] = a[j++];
	}

	while (i <= mid) b[k++] = a[i++];
	while (j <= end) b[k++] = a[j++];

	for (int i = start; i <= end; i++) {
		a[i] = b[i - start];
	}
}

void sort(int start, int end) {
	if (start == end) {
		return;
	}

	int mid = (start + end) / 2;
	sort(start, mid);
	sort(mid + 1, end);
	merge(start, end);
}


int main() {
	for (int i = 0; i < 10; i++) {
		cin >> a[i];
	}

	sort(0, 9);

	for (int i = 0; i < 10; i++) {
		printf("%d ", a[i]);
	}

	return 0; 
}
```



# 🔥 참고

* https://en.wikipedia.org/wiki/Hash_table

