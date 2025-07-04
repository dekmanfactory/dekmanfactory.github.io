---
layout: single
title: "금융 거래 당사자 모델 - 상속 관계 데이터베이스 설계"
date: 2025-06-08
categories:
  - database
  - design
tags:
  - database
  - inheritance
  - modeling
  - 금융
  - 설계
sidebar:
  nav: "main"
toc: true
toc_sticky: true
---

다음 상속 관계 모델을 관계형 데이터베이스 테이블로 구현할 때, 적절하지 않은 설계 방식은?

[상속 관계 모델]

① 각 하위 엔티티별로 상위 엔티티의 모든 속성을 복사하여 완전한 개별 테이블을 구성하는 방식

② 상위 엔티티의 속성 중 일부는 채무자 테이블에, 나머지는 채권자 테이블에 무작위로 배분하는 방식

③ 모든 엔티티 정보를 하나의 통합 테이블로 구성하고 타입 구분자로 구별하는 방식

④ 상위 엔티티(금융 거래 당사자)는 공통 테이블로, 하위 엔티티(채무자, 채권자)는 각각 독립 테이블로 설계하는 방식


**정답: ②**

## 해설

상속 관계 모델을 관계형 테이블로 변환하는 표준적인 방법은 다음과 같습니다:

### 1. 개별 완전 테이블 방식
각 하위 엔티티마다 상위 엔티티의 모든 속성을 포함하는 독립적인 테이블을 생성합니다. 조인이 불필요하지만 공통 속성이 중복 저장됩니다.

### 2. 상위 속성 무작위 배분 방식 (부적절한 방법)
상위 엔티티 속성을 하위 엔티티들에 무작위로 배분하는 방식은 데이터베이스 설계 원칙에 위반됩니다. 이는 엔티티의 논리적 완전성을 훼손하고, 데이터 일관성과 무결성을 보장할 수 없으며, 실제 데이터베이스 구현에서 사용되지 않는 비표준 방법입니다.

### 3. 통합 테이블 방식
모든 상위/하위 엔티티 속성을 단일 테이블에 저장하며, 엔티티 타입을 구분하는 식별자 컬럼을 사용합니다. 구조가 간단하지만 사용하지 않는 속성에 대해 NULL 값이 많이 발생할 수 있습니다.

### 4. 분리 테이블 방식
상위 엔티티용 공통 테이블과 각 하위 엔티티용 개별 테이블을 생성합니다. 하위 테이블들은 상위 테이블의 기본키를 외래키로 참조합니다. 정규화가 잘 되어 있지만 데이터 조회 시 조인 연산이 필요합니다.
