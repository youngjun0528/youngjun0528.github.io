# 07. 가치있는 테스트를 위한 리팩터링

## Source Code 리팩터링

### 소드 코드의 분류

- 복잡도 또는 도메인 유의성
    - 코드 복잡도 : 코드내 의사결정(분기) 지점 수
    - 도메인 유의성 : 코드가 프로젝트의 문제 도메인에 대해서 얼마나 의미가 있는지 여부, 유틸리티 코드와 같은 경우 최종 사용자와 직접적인 연관성은 없다.
- 클래스 또는 메서드가 가진 협력자 수
    - 협력자 : 가변 의존성 또는 프로세스 외부 의존성
    - 협력자를 예상되는 조건으로 두고 상태나 상호작용을 확인하는 테스트 필요

### 소스 코드의 유형

![08_Test_Refactoring.png](08_Test_Refactoring.png)

- 도메인 모델과 알고리즘 : 함수형 코어 또는 도메인 계층
- 간단한 코드 : ex.) 생성자나 상수 반환 처리
- 컨트롤러 : 가변 셀 및 App. 서비스 계층 ex.) 외부 API 호출, 파일시스템 또는 RDS 호출
- 지나치게 복잡한 코드

> # 험블 객체(Humble Object) 패턴
> 테스트하기 어려운 의존성과 도메인 로직을 분리하는 작업 패턴  
> 단일 책임 원칙 ( Single Responsibility Principle ) : 각 클래스는 하나의 책임을 가져야 한다.  
> 예시)
> - 각 계층별 분리 : MVP( Model-View-Presenter ), MVC ( Model-View-Controller )
> - 도메인 주도 설계( Domain-Driven Design) 의 집계 패턴 ( Aggregate Pattern )
