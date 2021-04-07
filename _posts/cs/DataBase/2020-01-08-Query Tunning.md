---
title:   "[Database] Query Tunning"
excerpt: "[Database] Query Tunning 정리"
toc: true
toc_sticky: true
categories:
  - cs
tags:
  - Database


---
https://12bme.tistory.com/73

https://d2.naver.com/helloworld/1155

<br>

# 📝옵티마이저(Optimizer)

* 옵티마이저는 SQL 개발자가 SQL을 작성하여 실행할 때, SQL을 어떻게 실행할 것인지를 계획한다.
* 즉, SQL 실행계획(Excution Plan)을 수립하고 SQL을 실행하는 데이터베이스 관리 시스템의 소프트웨어 이다.
* 동일한 결과가 나오는 SQL도 어떻게 실행하느냐에 따라서 성능이 달라진다.
* 따라서 옵티마이저의 실행계획은 SQL 성능에 아주 중요한 역할을 한다. 

<br>

## 📌 옵티마이저 특징

- 옵티마이저는 데이터 딕셔너리에 있는 오브젝트 통계, 시스템 통계 등의 정보를 사용해서 예상되는 비용을 산정한다. 
- 옵티마이저는 여러 개의 실행계획 중에서 최저비용을 가지고 있는 하나를 선택해서 SQL을 실행한다.

<br>

## 📌 옵피마이저의 실행 방법

- 개발자가 SQL을 실행하면 파싱을 실행해서 SQL의 문법 검사 및 구문 분석을 수행한다.
- 구문분석이 완료되면 옵티마이저가 규칙 기반 혹은 비용 기반으로 실행계획을 수립한다.
- 옵티마이저는 기본적으로 비용 기반 옵티마이저를 사용해서 실행계획을 수립한다. 비용기반 옵티마이저는 통계정보를 활용해서 최적의 실행계획을 수립하는 것이다.
- 실행계쇡 수립이 완료되면 최종적으로 SQL을 실행하고 실행이 완료되면 데이터를 인출(Fetch)한다. 

------

<br>

# 🔎 출처 & 더 알아보기

- [이기적 SQL 개발자이론서+문제집](https://book.naver.com/bookdb/book_detail.nhn?bid=14364997)

