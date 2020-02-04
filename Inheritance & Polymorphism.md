# Inheritance & Polymorphism

<br>

# 1. Inheritance

- Generalization : 추출된 class들의 공통적인 특성을 모아 super class로 정의
- Specialization : 비슷한 속성과 기능을 가지고 있는 다른 class를 상속받아 새로운 class를 정의할수 있다

<br>

- **상속받은 기능 중 수정을 원하는 기능은 재정의(Overriding)**할 수 있고, 필요한 속성이나 기능은 추가하여 작성할 수 있다.

- Java는 단일상속(single inheritance)
  - 단점은 interface가 보완(다중 상속 효과)

- 자식 클래스와 부모 클래스 간 겹치는 멤버변수가 없을 때에는 상관없이 똑같은 멤버변수를 가리키지만 겹치는 멤버변수가 생기면 `super.` 키워드는 부모 클래스의 멤버변수를, `this.` 키워드는 자식 클래스의 멤버변수를 가리킨다.

- private 정의된 super의 member는 상속은 되지만 접근할 수는 없다

- ### @Override

  - 상속관계에서 재정의를 의미하는 어노테이션
  - 재정의된 메서드가 Overriding 문법에 맞는지 컴파일러에서 체크 요청한다.


<br>

### toString()

- 모든 자바 클래스는 default로 Object클래스를 상속받고 있다.
  - Object 클래스는 java.lang 패키지안에 있음
  - 항상 모든 자바 클래스는 자동으로 java.lang 을 import 하고있다
  - Object 클래스에는 toString()이 있다
  - 따라서 모든 클래스에서 toString()을 쓸수 있으며, Overriding해서 쓸수도 있다



<br>

<br>



## Overloading  VS  Overriding

- method 정의 시 사용되는 기법
- method 이름을 같게 정의
- 사용의 편리성
- Polymorphism(다형성) 효과

<br>

### Overriding 

- 상속을 기반

- super부터 상속받은 기능 중 특정 기능을 재정의하는 기법

- **이름하고 파라미터 리스트가 같아야** Overriding하는 method라고 인식(판단기준)

  - 이때 @Override 붙이면 컴파일러가 체크해준다

    - @Override 붙이면 상속관계에 있다고 생각하기 떄문에.. 부모나 자식 메서드가 달라져도(이름같은거) 다른 메서드로 인식하지 않고 Overriding 규칙에 따라 맞았는지 틀렸는지 체크해준다

      ​	=> 유지보수하기 좋음

  - Overriding 한다고 판단된 method는  **return type**, 이름, 파라미터 리스트가 같아야 한다

<br>

#### overriding 체크 3가지!

- Return type
  - 상속관계에 있을 떄 재정의한 메서드가 리턴하는 타입은 상위 클래스의 메서드가 리턴하는 타입보다 커서는 안된다
  - 자식메서드가 더 범용적인 타입을 리턴할 수 없다!
- Access Modifier
  - 같거나 보다 넓은 범위로 정의
- 예외처리(throws) : 부모가 처리할 수 있는 예외보다 더 넓은 범위를 에러처리할 수 없다
  - NullPointException < RuntimeException < Exception

<br>

### Overloading

- 하나의 클래스나, 상속받은 클래스의 내에 같거나 비슷한 기능의 method의 이름을 같게 정의해서 편리성 추구
- **이름은 같게, 파라미터 리스트는 다르게 정의**
- 나머지 method형식, body는 상관 없음



<br>

<br>

## Polymorphism

### object polymorphism

- super type 변수가 다양한 형태의 sub type을 참조하는 것

- sub 객체 생성시 super도 같이 생성되어지기 때문에 memory에 존재하는 super type으로 변수선언이 가능하다

  - 메서드 호출 시 VM은 그 메서드가 Overriding되어 있는지 여부를 확인하고, 생성된 객체의 상속 관계에서 마지막 Overriding된 메서드를 호출한다

- 선언되어있는 변수의 type에 해당하는 변수에만 접근가능하다

  ```java
  Member m = new Member("홍길동",20,"hong@gildong.com");
  m.age = 10;
  m.name = "Lee";
  m.email = "@";
  m.showMember();
  ```

  

### method polymorphism

- overloading method call , overriding method call
- 메서드 호출 시 VM은 그 메서드가 Overriding되어 있는지 여부를 확인하고, 생성된 객체의 상속 관계에서 마지막 Overriding된 메서드를 호출한다



## Method Overriding + Polymorphism





## Reference Type Casting

- 레퍼런스 타입의 변수들은 상속관계일 경우 형변환 허용
- super var = new sub(묵시적 형변환)
- sub var = **(sub)**super (명시적 형변환)

