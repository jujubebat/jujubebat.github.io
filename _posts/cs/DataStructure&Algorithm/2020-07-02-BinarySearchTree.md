---
title:  "[Data Structure & Alogrithm] Binary Search Tree"
excerpt: "[Data Structure & Alogrithm] Binary Search Tree 정리"
toc: true
toc_sticky: true
categories:
  - cs
tags:
  - Data Structure & Alogrithm

---

# 📝 **Binary Search Tree**



![img](https://k.kakaocdn.net/dn/ctdXE9/btqDahiX5zP/58N04am38bSh6AiU3TkibK/img.gif)



## 📌 핵심 요약

`"BST는 기본적으로 이진 트리 형태이며, BST를 구성하는 모든 노드는 다음과 같은 특성을 가진다. 기준 노드의 왼쪽 서브 트리를 구성하는 모든 노드의 값은 기준 노드의 값보다 작고, 기준 노드의 오른쪽 서브 트리를 구성하는 모든 노드의 값은 기준 노드의 값보다 크다. BST는 완전 이진 트리에 가까울수록 즉, 균형적일수록 탐색 시간이 O(logN)에 가까워진다."`



## 📌 설명

* BST는 기본적으로 이진 트리이다.
* BST의 저장되는 원소는 유일하다.
* BST의 모든 노드는 다음과 같은 특성을 지닌다.
  * 기준 노드의 왼쪽 서브 트리를 구성하는 모든 노드의 키는 기준 노드의 키보다 작다.
  * 기준 노드의 오른쪽 서브 트리를 구성하는 모든 노드의 키는 기준 노드의 키보다 크다.



## 📌 시간 복잡도

- 탐색/삽입/삭제 
  * BST가 완전 이진 트리 형태일때 (균형)
    * `O(logN)` : 트리의 높이가 1씩 커질수록 추가할 수 있는 노드수는 2배가 된다.
  * BST가 사향 트리일때 (불균형)
    * `O(N)` : 링크드 리스트와 같아진다. 





# 🔥 참고

* [https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%A7%84_%ED%83%90%EC%83%89_%ED%8A%B8%EB%A6%AC](https://ko.wikipedia.org/wiki/이진_탐색_트리)