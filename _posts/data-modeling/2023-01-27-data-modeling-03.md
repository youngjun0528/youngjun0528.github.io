---
title: "03 - 주식별자와 데이터타입"
description: 
published: true
date: 2021-07-23T06:08:33.295Z
tags: 
- database
- modeling
editor: markdown
dateCreated: 2021-07-16T07:04:32.729Z
categories:
- modeling
author_profile: true
sidebar_main: true
toc: true
toc_sticky: true
toc_label: "03 - 주식별자와 데이터타입"
---

## Key의 정의	
- 하나의 테이블에서 각 레코드를 고유하게 식별할 수 있는 컬럼 또는 컬럼의 조합
- 키의 조건은 NOT NULL, UNIQUE
- 테이블 디자인시 키를 정하고 테이블을 데이터베이스에 만들때 명시적으로 키를 선언함.
- 키는 키에 대응하는 인덱스 테이블이 생성됨.
(인덱스 테이블을 키 값에 의해서 정렬)

## 후보키
- 주 식별자가 될 가능성이 있는 식별자
- 모든 식별자는 주 식별자가 될 수 있는 후보이므로, 식별자와 후보 식별자는 사실상 동일어
- 결정자(Determinant) : 이 값을 알면 나머지 속성값도 알 수 있는 속성

## Primary Key 설계
- 유일하고, 모든 레코드에 NOT NULL일 수 있는 컬럼을 찾는다.
- 후보 식별자가 없는 경우 임의의 식별자(인조 식별자)를 만들어 부여한다.
#### PK 데이터 타입 결정 고려사항
1. 발생가능한 최대 레코드 수를 커머할 수 있는 데이터 타입을 선언한다.
    - 만약 대상 레코드가 수십만개 정도하면 999,999로 커버할 수 있다.
    - 따라서 32bit int를 사용할 수 있다.
    - 또한, varchar(6)를 사용할 수 있다.

2. PK의 데이터 타입 후보를 대상으로 다음을 고려한다.
    - int 등 숫자를 PK로 채택할 경우 자동 증분 속성을 사용할 수 있다.
    - String을 사용하면 숫자가 아닌 문자를 섞어서 PK값에 의미를 부여할 수 있다.
    - 특별한 의미를 부여할 필요가 없을 겨아우 정수형을 사용하는 것이 바람직하다.

3. PK는 고유 식별자 기능으로 충분
    - PK에 어떤 의미를 부여하는 것은 부담이다.

***
> __참고자료__
>
> [RDMS Modeling 기초](https://www.inflearn.com/course/%EA%B4%80%EA%B3%84%ED%98%95%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-rdbms/dashboard)