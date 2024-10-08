# 01. 단위 테스트의 목표

- 소프트웨어의 안전망
- 대부분 회귀에 대한 보험을 제공하는 도구
    - 새로운 기능을 도입하거나, 새로운 요구사항에 더 잘 맞게 리팩터링 한 다음 잘 작동하는 지 확인

## 가이드

### 모든 테스트를 똑같이 작성할 필요는 없다.

- 각각의 테스트에는 비용과 편익 요소가 있으며, 둘 다 신중히 따져볼 필요가 있다.
- 가장 좋은 Case는 최소한의 유지비로 최대의 가치를 끌어내는 것
- 코드 베이스에서 가장 중요한 부분만을 대상으로 한다. ( ex. 비즈니스 로직 )

### 단위 테스트 코드 기능과 커버리지 지표는 좋은 부정 지표이지만, 나쁜 긍정 지표이기도 하다.

- 단위 테스트를 할 수 없는 코드는 품질이 좋지 않지만, 단위 테스트를 할 수 있다고 품질을 보증하지 않는다.

### 특정 커버리지 숫자는 동기부여가 잘못된 것이다.

- 커버리지 숫자가 낮으면(대략 60%) 문제 징후라 할 수 있디만, 숫자가 높다고 해서 큰 의미를 두어선 안된다.
- 코드 커버리지는 좋은 테스트 품질을 가기 위한 첫걸음이다.

> # 커버리지 지표
> 테스트가 소스 코드를 얼마나 실행하는지를 나타내는 백분율

- 문제점
    - 테스트 대상의 시스템의 모든 가능한 결과를 검증한다고 보장할 수 없다.
    - 외부 라리브러리의 코드 경로를 고려할 수 있는 커버리지 지표는 없다.