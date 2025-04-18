# 객체 지향 프로그래밍

## 객체 지향의 주요 개념

### Class ( 클래스 )

- Class 는 속성(데이터 요소: 변수)과 행동(특정 작업: 메서드)을 호함한 객체를 정의한다.
- Object 를 만들기 위한 **설계도**

``` python
class Dog:
    def bark(self):
        print("멍멍!")
```

### Object ( 객체 )

- 클래스에서 **실제로 만들어진 실체(instance)**
- Entity는 다른 Entity 와 상호 작용을 하며 목적을 달성한다.

```python
my_dog = Dog()  # Dog 클래스에서 만든 객체 (인스턴스)
my_dog.bark()  # "멍멍!" 출력
```

### Method ( 메소드 )

- 클래스 내부에 정의된 함수입니다.
- 객체가 가진 데이터(속성)를 이용해 특정 동작을 수행합니다.
- 첫 번째 인자로 항상 self를 받는데, 이는 메서드가 호출된 객체 자신을 가리킵니다.

```python
class Dog:
    def __init__(self, name):  # 생성자
        self.name = name

    def bark(self):
        print(f"{self.name}가 멍멍 짖어요!")


my_dog = Dog("초코")
my_dog.bark()  # "초코가 멍멍 짖어요!" 출력
```

## 객체 지향의 주요 기능

### 캡슣화 ( Encapsulation )

- 객체의 기능과 상태 정보를 외부로부터 은닉
- 객체의 **데이터(속성)**를 외부에서 직접 접근하지 못하게 하고, 메서드를 통해서만 접근하도록 하는 방식
- 내부 구현을 숨기고(public/private), 필요한 기능만 노출
- Python 에서는 Public, Private 와 같은 접근 제어가 없기 때문에, 함수나 변수 앞에 언더바(_) 를 붙여서 구분한다.

```python
class Person:
    def __init__(self, name):
        self.__name = name  # __name은 private 변수

    def get_name(self):  # public getter
        return self.__name

    def set_name(self, name):  # public setter
        self.__name = name


p = Person("Alice")
print(p.get_name())  # Alice
p.set_name("Bob")
print(p.get_name())  # Bob

# print(p.__name)  # ❌ 오류! 직접 접근 불가
```

### 다형성 (Polymorphism )

- 같은 인터페이스로 다른 동작을 수행할 수 있는 성질
- Method Overloading : 객체는 Parameter 에 따라 다른 메소스를 호출한다.
    - 하지만, Python 에서는 Method Overloading 를 지원하지 않는다.
- Method Overriding : 동일한 인터페이스를 여러 형식의 객체들이 공유한다.

```python
class Animal:
    def speak(self):
        pass


class Dog(Animal):
    def speak(self):
        return "멍멍"


class Cat(Animal):
    def speak(self):
        return "야옹"


def animal_sound(animal):
    print(animal.speak())


animal_sound(Dog())  # 멍멍
animal_sound(Cat())  # 야옹
```

### 상속 ( Inheritance )

- 클래스의 기능이 부모 클래스로부터 파생
- 부모 클래스에 정의된 함수를 재사용할 수 있다.
- Python에 대해서 다중 상속을 지원한다.
    - Python 에서의 다중 상속은 MRO(Method Resolution Order) 에 따라 부모 클래스의 함수 실행 순서를 결정한다.

```python
class A:
    def greet(self):
        print("A")


class B(A):
    def greet(self):
        super().greet()
        print("B")


class C(A):
    def greet(self):
        super().greet()
        print("C")


class D(B, C):  # D -> B -> C -> A
    def greet(self):
        super().greet()
        print("D")


d = D()
d.greet()
```

### 추상화 ( Abstraction )

- 공통된 구조만 정의하고, 구체적인 동작은 자식 클래스에서 정의
- 보통 abc 모듈의 ABC, abstractmethod를 사용

```python
from abc import ABC, abstractmethod


class Shape(ABC):  # 추상 클래스
    @abstractmethod
    def area(self):
        pass


class Circle(Shape):
    def __init__(self, r):
        self.r = r

    def area(self):
        return 3.14 * self.r ** 2


circle = Circle(5)
print(circle.area())  # 78.5

# shape = Shape()  # ❌ 오류! 추상 클래스는 인스턴스화 불가
```

### 컴포지션 ( Composition )

- 객체나 클래스를 더 복잡한 자료구조나 모듈로 묶는 행위
- 특정 객체는 상속 구조 없이 다른 모듈의 함수를 호출 할 수 있다.

```python
class Engine:
    def start(self):
        print("엔진이 켜짐")


class Car:
    def __init__(self):
        self.engine = Engine()  # Engine을 포함 (has-a 관계)

    def start(self):
        self.engine.start()
        print("자동차 출발")


car = Car()
car.start()
# 엔진이 켜짐
# 자동차 출발
```