---
title:  "[Data Structure & Alogrithm] Linked List"
excerpt: "[Data Structure & Alogrithm] Linked List 정리"
toc: true
toc_sticky: true
categories:
  - cs
tags:
  - Data Structure & Alogrithm

---

# 📝Linked List

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9c/Single_linked_list.png/400px-Single_linked_list.png)

## 📌 핵심 요약

`"연결리스트는 데이터와 포인터로 구성된 각 노드로 구성되어있다. 각 노드의 포인터는 다른 노드를 가리키는데, 이를 통해서 한 줄로 연결되어 있는 구조를 가진다. 삽입/삭제시 상수시간이 걸리는 장점이 있지만, 특정 위치의 데이터 탐색시 O(N)의 시간이 걸린다."`



## 📌 설명

* 연결리스트의 각 원소(=노드)는 다음 원소의 주소를 가진다. 이를 통해 각 원소가 순서대로 연결된다.

* 연결리스트의 각 원소들은 메모리에 연속적으로 저장되지 않는다. 각 원소들은 메모리 여기저기에 저장되고 포인터로 연결된다.

  

## **⚔️ 연결 리스트의 장점**

*  특정 위치에서 원소의 삽입/삭제가 빠르다. (연결리스트의 맨 앞 또는 맨 뒤에서 삽입/삭제를 수행하면 상수시간이 걸린다.)



## 📌 시간 복잡도

* 탐색 `O(N)` : 첫 번째 원소부터 순차적으로 찾고자하는 원소를 탐색한다.
* 삽입 `O(N)` : 삽입 하려는 위치를 탐색하고 삽입한다.
* 삭제 `O(N)` : 삭제 하려는 위치를 탐색하고 삭제한다. 
  * 삽입/삭제 자체는 O(1) 상수시간이 걸린다. 하지만 탐색에 걸리는 시간을 고려해야한다. 