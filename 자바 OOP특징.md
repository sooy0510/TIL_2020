# 자바 OOP특징

## 1. method 구현 overloading

### - method signature

- method 이름, parameter(type, 개수)
- method signature가 다르면 별개의 method

<br>

## 2. method 구현 overriding

### - 상위 class의 method

- 하위 class에서 공통적으로 사용 가능(**protected, public**)
- 하위 class에서 재정의
- extends
- 단일상속

<br>

## 3. method 구현 interface

- method만 기술
- **Java 추상화의 상징**
- abstract method(추상메소드) + default method(body(구현부분)를 가지는 method)
- class에 기능/역할 부여
- **서로 다른 class들은 동일한 interface를 구현함으로써 기능/역할의 공통성을 가짐**
- implements
- 다중 구현이 가능

<br>

## 4. Java Collections - interface & classes

| Interface | 구현 class                    | 설명                               |
| --------- | ----------------------------- | ---------------------------------- |
| List      | LinkedList, Stack, ArrayList  | 순서(o), 중복(o)                   |
| Set       | HashSet, TreeSet              | 순서(x), 중복(x)                   |
| Queue     | **LinkedList**, PriorityQueue | 순서(o), 중복(o)                   |
| Map       | HashTable, HashMap, TreeMap   | key, value 쌍, 순서(x), key중복(x) |

<br>

## 5. List vs HashSet

### List

- List는 Object Class의 equals()를 수행해서 ==연산자로 비교한다

- List에서 attribute들이 모두 동일한 객체를 동일하다고 생각하고 remove하고 싶을때, equals()를 overriding해서 reference값 비교가 아닌  attribute를 비교하는 코드로 오버라이딩 해줘야 한다
- List는 중복된 값을 허용하기 때문에 hashCode로 비교하지 않는다 => hashCode overriding 필요없음

<br>

### HashSet

- Hash를 사용한 Collection(HashMap, HashSet 등)은 key를 결정할 때 hashCode()를 사용하기 떄문에 equals()가 true인 두 Object를 동일한 key로 인식하고 싶은 경우 hashCode를 overriding해서 수정해줘야 함

