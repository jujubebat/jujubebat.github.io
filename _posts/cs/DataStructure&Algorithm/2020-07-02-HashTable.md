---
title:  "[Data Structure & Alogrithm] Hash Table"
excerpt: "[Data Structure & Alogrithm] Hash Table 정리"
toc: true
toc_sticky: true
categories:
  - cs
tags:
  - Data Structure & Alogrithm

---

# 📝 **Hash Table**

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7d/Hash_table_3_1_1_0_1_0_0_SP.svg/315px-Hash_table_3_1_1_0_1_0_0_SP.svg.png)

## 📌 핵심 요약

`"해시 테이블은 Key-Value 쌍으로 이루어진 데이터를 저장하는 자료구조다. Key를 통해 데이터에 상수시간에 빠르게 접근할 수 있다. 해시 함수를 사용해 큰 범위를 갖는 Key를 유한한 범위의 Key로 매핑한다. 이는 공간의 효율을 높여주는 장점을 갖는다."`



## 📌 설명

* Hash Table에 저장되는 데이터는 Key-Value로 쌍을 이룬다. Key를 통해 데이터에 빠르게 접근할 수 있다.
* 모든 Key는 중복되지 않는다.
* 테이블 자료구조는 사전구조 혹은 맵(map)이라 불리기도 한다.



## 📌 **해시 함수**

* 해시 테이블의 해시 함수는 큰 범위를 갖는 Key를 유한한 범위의 Key로(hash 값) 매핑한다. 이는 공간의 효율을 높여준다. (유한한 범위의 배열만 만들면 되기 때문)
*  두 개 이상의 다른 Key가 동일한 해시 값으로 매핑될 수 있는데, 이를 충돌이라고 한다. 



## 📌 **충돌 대응 기법**

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Hash_table_5_0_1_1_1_1_1_LL.svg/450px-Hash_table_5_0_1_1_1_1_1_LL.svg.png)

* 선형 조사법 : 충돌이 발생했을 때 비어있는 옆자리에 접근한다. 
* 이중 해쉬 : 1차 해쉬 함수로 해쉬값을 얻고, 2차 해쉬 함수로는 충돌 발생시 몇 칸 옆자리에 접근할지 결정
* 체이닝 : 하나의 해쉬 값에 링스트 리스트 형태로 다수의 슬롯을 두는 방식



# 🔥 참고

* https://en.wikipedia.org/wiki/Hash_table

