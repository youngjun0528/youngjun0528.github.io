# 04. 1:M 관계 와 M:N 관계

## 식별관계와 비식별관계

1. 식별관걔는 실선, 기본키에 외래키가 포함되어 있다면 식별관계  
   ![data-modeling-04-01.jpg](data-modeling-04-01.jpg)

2. 비식별 관계는 점선, 기본키에 외래키가 포함되어 있지 않다면 비식별 관계  
   ![data-modeling-04-02.jpg](data-modeling-04-02.jpg)

## 1:M 관계

한쪽이 관계를 맺은 쪽의 여러 객체를 가진 것을 의미  
컴퓨터 디럭터리 구조(하나의 폴더 내에 여러 개의 파일)

## 재귀적 1:N 관계 (자기참조관계)

| 부서ID | 부서명  | 상위부서ID |
|------|------|--------|
| 1    | 총무부  | NNULL  |
| 2    | 총무1과 | 1      |
| 3    | 총무2과 | 1      |
| 4    | 회계팀  | 2      |
| 5    | 인사팀  | 2      |

SELECT A.부서ID, A.부서명, B.부서명 FROM 부서 AS A JOIN 부서 AS B ON A.부서ID = B.상위부서ID

| 상위부서ID | 상위부서명 | 하위부서명 |
|--------|-------|-------|
| 1      | 총무부   | 총무1과  |
| 1      | 총무부   | 총무2과  |
| 2      | 총무1과  | 회계팀   |
| 2      | 총무1과  | 인사팀   |

![data-modeling-04-03.jpg](data-modeling-04-03.jpg)

## M:N 관계

### 관계테이블의 독립형 Primary Key

학생이 동일한 과목을 2번 등록할 수 있는 문제 발생함.

![data-modeling-04-04.jpg](data-modeling-04-04.jpg)

### 관계테이블의 독립형 Primary Key와 Alternate Key(대체키) 사용

대체키(Alternative Key)를 사용하여 프로그래밍 적으로 사용하기 편하게 처리

![data-modeling-04-05.jpg](data-modeling-04-05.jpg)

### 관계테이블의 상속형 Primary Key ( Super Key )

![data-modeling-04-06.jpg](data-modeling-04-06.jpg)

> __참고자료__
>
> [RDMS Modeling 기초](https://inf.run/XhFbZ)