---
title:  "[Data Structure & Alogrithm] Quick Sort"
excerpt: "[Data Structure & Alogrithm] Quick Sort 정리"
toc: true
toc_sticky: true
categories:

  - cs
tags:
  - Data Structure & Alogrithm
---

# 📝 Quick Sort (퀵정렬)

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/af/Quicksort-diagram.svg/1024px-Quicksort-diagram.svg.png" alt="img" style="zoom: 33%;" />

* 퀵소트 예제 : 두꺼운 선으로 둘러싸인 원소는 pivot 원소로서, 배열의 마지막 원소를 pivot으로 잡는 경우다.

## 📌 핵심 요약

`"Quick sort는 정렬할 원소들중 하나를 pivot을 지정하고 그 pivot을 기준삼아 정렬을 진행한다. 그리고 pivot을 기준으로 정렬 과정을 반복한다."`



## 📌 설명

<img src="https://k.kakaocdn.net/dn/bm7CoU/btqC9xTZifT/4q2eSikw7iTv395TDIMS80/img.png" alt="img" style="zoom:65%;" />

* 위 그림은 정렬의 대상이 되는 배열이다. 퀵 정렬의 과정을 살펴보자. (오름차순 정렬)

* 용어 설명

  * `left` : 정렬대상의 가장 왼쪽 지점을 가리키는 이름
  * `right`: 정렬대상의 가장 오른쪽 지점을 가리키는 이름
  * `pivot` : 정렬을 진행하는데 필요한 기준
  * `low` : 피벗을 제외한 가장 왼쪽에 위치한 지점을 가리키는 이름
  * `high` : 피벗을 제외한 가장 오른쪽에 위치한 지점을 가리키는 이름

  

<img src="https://k.kakaocdn.net/dn/ch6lk6/btqC9OnGdOE/U5LwMC4BgKfbCtYmGTbJE1/img.png" alt="img" style="zoom:60%;" />

* 오름차순을 기준으로, low는 피벗보다 큰 값을 만날 때까지 오른쪽 방향으로 이동하고, high는 피벗보다 작은 값을 만날 때까지 왼쪽 방향으로 이동한다. 

<img src="https://k.kakaocdn.net/dn/bPy9fA/btqC5pwCyRA/lfqkJSYlIQ5NSgby0eZNm0/img.png" alt="img" style="zoom:60%;" />

* 그 다음 low와 high를 교환한다. 그러면 위와 같은 상태가 된다. 

<img src="https://k.kakaocdn.net/dn/qxgFo/btqC6Qgaqtb/q3FwRZMlZ6VDBdaU0AGK9K/img.png" alt="img" style="zoom:60%;" />

* 7과 4의 교환 후에도 계속해서 low는 오른쪽으로, high는 왼쪽으로 이동한다. 마찬가지로 low는 피벗보다 큰 값을 찾고, high는 피벗보다 작은 값을 찾는다. 따라서 low와 high는 각각 9와 2를 가리키고, 이번에도 이 둘을 교환하여 위와 같은 상태가 되게 한다.

<img src="https://k.kakaocdn.net/dn/bWalHI/btqC9OnGdP8/7uorsXHkXv5a5F4wU9eDW0/img.png" alt="img" style="zoom:60%;" />

* 이후에도 low는 피벗보다 큰 값을 찾을 때까지 오른쪽으로, high는 피벗보다 작은 값을 찾을 때까지 왼쪽으로 이동한다. 그러면 결국 위와 같이 low와 high가 가리키는 위치가 교차되는 상황이 발생한다.

<img src="https://k.kakaocdn.net/dn/bwwdgg/btqC5pi58nS/CBXw2SzTrV4EKdHsDrUcP0/img.png" alt="img" style="zoom:60%;" />

*  이렇게 low와 high가 교차되는 상황은 이동 및 교환의 모든 과정이 완료되었음을 의미한다. 따라서 이번에는 피벗과 high가 가리키는 데이터를 서로 교환하여 위와같은 상태가 되게 한다.

* 위를 유심히 관찰해보자. 피벗의 왼편에는 피벗보다 작은 값들이 위치하고, 피벗의 오른편에는 피벗보다 큰 값들이 위치한다. 따라서 피벗이었던 5는 정렬되었을 때의 제 위치를 찾았다. 피벗이었던 숫자 5는 홀로 정렬이 완성되었다.

<img src="https://k.kakaocdn.net/dn/uwrab/btqC5nFBAs3/O2NnwnFRvqXL8HTFyjv2k0/img.png" alt="img" style="zoom:60%;" />





*  제자리를 찾은 5를 기준으로 왼쪽 영역과 오른쪽 영역을 대상으로 지금까지 설명한 과정을 재귀적으로 반복하면 정렬이 완성된다. 




## 📌 시간 복잡도

* 정렬수행 - 평균적인 경우 `O(NlogN)`  

  * 중간값에 가까운 pivot을 선택할 경우, 정렬 대상이 균등하게 나뉘기 때문이다.
  * 최대한 중간 값에 가까운 pivot을 선택하기 위해 정렬대상에서 3개의 데이터를 추출한다음 그 중에서 중간 값에 해당하는 것을 pivot으로 선택하는 방법이 있다.

* 정렬수행 - 최악의 경우 `O(N^2)` 

*  Quick 정렬은 데이터 이동횟수가 상대적으로 적고, Merge Sort와 같이 별도의 메모리 공간을 요구하지 않으므로 동일한 시간복잡도를 갖는 다른 정렬 알고리즘 중에서 평균적으로 가장 빠른 정렬 속도를 보인다. 

  

![img](https://k.kakaocdn.net/dn/c821qZ/btqC8IPiXc2/AHVbECKjnZbncZdXSLihhK/img.gif)



# 🔥 참고

* [https://ko.wikipedia.org/wiki/%ED%80%B5_%EC%A0%95%EB%A0%AC](https://ko.wikipedia.org/wiki/퀵_정렬)

