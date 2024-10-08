# 02. 단위 테스트란 무엇인가

## 단위 테스트 정의

1. 작은 코드 단위를 검증
2. 빠르게 수행
3. 격리된 방식으로 처리하는 자동화된 테스트

## 격리 문제

### 런던파

- 테스트 대상 시스템을 협력자로부터 격리한다.
- 즉, 테스트 대상이 다른 클래스에 이존하면 이 모든 의존성을 테스트 대역으로 대체하여야 한다.
- 특징
    - 테스트가 실패하면, 어느 부분에서 실패하였는지 확실히 알 수 있다.
    - 의존성을 가진 코드의 객체를 격리하여 의존성 문제 해결하고 테스트 구조를 단순화 할 수 있다.

### 고전파

- 코드를 반드시 격리할 필요는 없이, 단위 테스트간 격리가 우선된다.
- 즉, 테스트를 어떤 순서로 하든 가장 적합한 방식으로 실행하여 서로 간의 결과에 영향을 미치지 않는다.
- 여러 클래스를 한번에 테스트를 해도 괜찮다.
    - 하나의 테스트 내에서 다른 Class 간의 영향을 미쳐도 결과에 영향을 미치지 않는다는 의미이다.
- 여기서 단위 테스트 간 격리라는 의미는 공유 의존성을 격리한다는 의미이다. ( 아래 참고 )

## 의존성 문제

1. 공유 의존성
    - 테스트 간에 공유되고, 서로의 결과에 영향을 미칠수 있는 수단을 제공하는 의존성
    - 대표적인 예로는, 데이터베이스의 의존성
        - 데이터 베이스에 동일한 테스트 데이터를 입력하면 테스트 데이터이 간섭으로 실패할 수 있다.
2. 비공개 의존성
    - 공유하지 않는 의존성
    - 테스트에 영향을 미치지 않는 의존성
3. 프로세스 외부 의존성
    - 실행 프로세스 외부에서 실행되는 의존성으로 대부분 공유 의존성과 같은 개념이다.
    - 다만, 외부 운영 데이터베이스에 의존적이면, 프로세스 외부 의존성이자 공유 의존성이다.
    - 만약 테스트 실행 전 Docker 컨테이너로 데이터베이스를 실행하면 이는 곧 격리된 데이터베이스이므로 프로세스 외부 의존성이지만 공유 의존성을 아니다.
4. 공유 의존성과 휘발성 의존성
    - 휘발성 의존성
        - 개발자 머신에 설치된 런타임 환경 외에 데이터베이스나 외부 API 서비스 들
        - 비결정적 동작 ( 난수 생성기, 날짜 생성기 등 )
    - 예를 들어,
        - 데이터 베이스에 대한 의존성은 공유 의존성이자, 휘발성 의존성이다.
        - 파일 시스템은 테스트 간의 영향도를 미칠 수 있으므로 공유 의존성이지만, 기본 런타임 환경에 포함되며, 결정적으로 작동되므로 휘발성 의존성은 아니다.
        - 난수 생성기나 날짜 생성기는 각 테스트 별로 인스턴스를 생성할 수 있으므로, 공유 의존성은 아니지만, 일시적이므로 휘발성 의존성이다.

### 런던파와 고전파의 의존성에 따른 테스트 관점

- 런던파의 경우 단일 클래스에 대해서 모든 의존성을 격리하여 테스트를 수행한다.
- 고전파의 경우 단일 클래스 혹은 클래스 세트 단위로 공유 의존성 만을 격리하여 테스트를 수행한다.
- 런던파로 테스트 설계를 한다면,
    - 모든 단일 클래스에 대한 세밀한 테스트 케이스 작성이 가능하다.
    - 테스트 대상의 복잡도가 커져도 테스트 설계 방식은 동일하다.
    - 테스트가 실패하면 어떤 기능 혹은 어떤 클래스, 함수가 실패했는지 명확하다.
    - 런던파의 가장 큰 문제점은,
        - 검증이 동작의 단위가 아닌, 코드의 단위가 된다.
        - 코드별 버그를 찾기에는 쉬우나, 단위 테스트에서 검증하고자 하는 가장 큰 목적은 가장 마지막에 수정된 코드가 정상적으로 작동하는냐 이다.
        - 코드의 단위로 테스트케이스를 작성하고자 하면, 과잉 명세의 우려가 있다.
- 반면에 고전파로 테스트 설계를 한다면,
    - 런던파에 비해 세밀한 테스트 케이스 작성은 하지 않지만, 테스트와 운영 코드 사이에 결합도가 낮아지기 때문에 더 유연하게 대처 할 수 있다.
    - 정기적인 단위 테스트 수행은 클래스 집합에 대한 실패에 대해서 대응은 충분히 가능하다.

<table>
    <tr>
        <td></td>
        <td>격리 주체</td>
        <td>단위의 크기</td>
        <td>테스트 대역 사용 대상</td>
    </tr>
    <tr>
        <td>런던파</td>
        <td>단위</td>
        <td>단위 클래스</td>
        <td>불변 의존성 외 모든 의존성</td>
    </tr>
    <tr>
        <td>고전파</td>
        <td>단위 테스트</td>
        <td>단일 클래스 또는 클래스 세트</td>
        <td>공유 의존성</td>
    </tr>
</table>

### 통합 테스트

- 단위 테스트의 범위를 넘어선 모든 테스트는 통합 테스트로 간주한다.
- 런던파의 입장에서 바라보는 고전파의 테스트케이스는 통합 테스트 일 것이다.
- 공유 의존성에 접근하는 테스트(예를 들어, API 테스트)는 고전파/런던파의 입장에서는 통합 테스트이다.
- 엔드 투 엔트(end-to-end) 테스트(예를 들어, 사용자 테스트)는 통합 테스트의 일부이다.
    - 공유 의존성, 프로세스 외부 의존성 등 모든 의존성에 대한 동작을 검증한다.

#### 참고 및 결론

![01_Test_Area.png](01_Test_Area.png)

- 테스트는 코드의 단위가 아니라, 동작의 단위에 대해서 검증해야 한다.
- 모든 의존성에 대해서 Mock 과 Stub을 사용하여 격리하는 것인 테스트 커버리지나, 테스트 정확도에서는 높을 수 있다.
- 하지만, 실제 테스트를 작성하고, 이후 유지보수의 관점에서 들어가면, 테스트 코드와 운영 코드의 결합도가 너무 높아지면 테스트 관리가 어려워지고 개발자는 테스트 코드 관리를 기피하게 될 것이다.
- 만약, A 라는 Class 를 테스트 한다면,
    - A Class와 연결된 B Class 는 이미 테스트 대역으로 교체된 상태이다.
    - 그럼 B Class 의 테스트 대역을 다시 손보아야 하는 과정이 필요할 수도 있다.
    - 모든 테스트 대역에 이러한 관리가 들어간다는 것은 비효율적이다.
- 그럼 고전파의 관점에서 각 단위 테스트는 독립적이고 공유 의존성(데이터베이스나)