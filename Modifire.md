# Modifire

- Access Modifier(접근제한자) - 클래스 구성원의 접근에 대한 제한
  - public, protected, default, private
- **Usage Modifier**(사용에 대한 제한)
  - static, final, abstract

<br>

## static 

### static variables(멤버변수)

- 객체 생성 없이 사용할 수 있다
  - class명.변수명
- 물론 object로 생성해서 사용도 가능(=class명.변수명 으로 접근하는 변수와 같은 값이다)
- 그 클래스를 instance한 객체들 간의 공용변수로 사용한다

<br>

### static method

- 객체 생성 없이 호출할 수 있다

- **static 메서드는 객체 생성 없이 사용되므로 메서드안에서 static 변수만 사용할 수 있다**

- 일반(non-static)변수나 메서드는 사용 불가 => 객체가 생성되어야 사용할 수 있다. Heap 공간에서 사용가능한 변수

- this.super 변수 사용 불가 => this는 현재 사용중인 객체를 가리키므로

- Overriding 안됨

- **static block** : 클래스가 메모리에 로딩된 후 **자동 호출**된다

  - 보통은 생성자로 초기화를 하지만, static을 이용해서 초기화도 가능하다 => 보통은 표준 API에서 많이 사용

  - 클래스를 여러번 new하여 객체가 여러개 생성돼도 static block 은 처음 클래스 로딩시에 한번만 호출됨

  - StaticBlock 

    ```java
    public class StaticBlock {
        public StaticBlock() {
            System.out.println("StaticBlock()!!");
        }
    
        static void m1() {
            System.out.println("Static m1()!!");
        }
    
        {
            System.out.println("initialization block!!");
        }
    
        static {
            System.out.println("Static Block!!");
        }
    }
    ```

  <br>

  - StaticBlockTest

    ```java
    public class StaticBlockTest {
    
        public static void main(String[] args) {
            StaticBlock.m1();
            StaticBlock sb = new StaticBlock();
        }
    }
    ```

  <br>

  - 실행결과

    ```java
    // 1. static block 먼저 호출 
    // 3. 초기화(Initialization)블록은 객체 만들때 실행(생성자보다 먼저 호출) 
    Static Block!!
    Static m1()!!
    initialization block!!
    StaticBlock()!!
    ```

  <br>

  - Main메서드와 static block 이 한 클래스 내에 있을떄, Main메서드도 결국 클래스가 메모리에 로드되어야지 호출되는 것이므로 Main 메서드보다 static block 이 먼저 수행됨

    ```java
    public class StaticBlockTest {
        static {
            System.out.println("Static Block2!!");
        }
    
        public static void main(String[] args) {
            System.out.println("Main!!");
        }
    }
    
    => Static Block2!!
    	Main!!	
    ```

    

<br>

### static class

- 보통 Utility Class에 많이 사용

<br>

<br>

## Final

- 마지막을 의미
  - Class : (다른 클래스에서)더 이상 상속받을 수 없음. 상속을 허락하지 않음
  - Method : Overriding 할 수 없음
  - variable : 값을 변경할 수 없음 = 상수

<br>

<br>

## Interface

> final(상수) + 구현되지 않은 메서드(과거) => 현재는 인터페이스에서도 메서드가 구현될 수 있다
>
> 서비스에 대한 **명세**를 인터페이스로 제공 => 내부구현은 숨김
>
> (어떤 기능을 특징지어서 표현해놓은것) 똑같은 사용방법으로 서비스를 이용할 수 있다
>
> => ex) jdbc : 인터페이스 집합. Oracle, MySQL등 다양한 DB를 jdbc(인터페이스)를 이용해 같은 방법으로 사용할 수 있다. 모든 DB 벤더사들이 jdbc인터페이스를 받아 구현해서 개발자들은 같은 메서드로 DB를 이용할 수 있다.
>
> 설계자와 개발자의 약속

<br>

- Interface간에 상속가능

- 상수로 정의하지 않아도 컴파일러에 의해 자동으로 상수로 변경

- 메서드 정의시 public 으로 정의하지 않아도 컴파일러가 public 제한자를 삽입

- 컴파일 시 다음 제한자가 자동삽입

  ```java
  public static final + 상수;
  public abstract + 메서드;
  ```

<br>

### 인터페이스의 특징

- 인터페이스는 객체 생성을 할 수 없다 => 구현되지 않은 메서드를 포함하기 때문이다

- super type으로 사용할 수 있다 => 부모 클래스처럼 사용할 수 있다

- 상속되어지면 sub class가 모든 메서드 구현(Overriding)해야 한다

- 상속한 sub class들의 명세서 역할로 사용

- **자바는 단일상속이 원칙이지만 interface로 다중상속 효과**

  - 본질적으로 비슷한 부분을 상속(extends)로, 행동, 특징 등을 그룹핑(implements)하는 효과

- 인터페이스의 추상메서드가 body를 가지고 있을 때는 키워드 default를 붙여줘야한다 : 재정의 가능함

  ```java
  public interface InterfaceA {
      void mA();
      default void mD() {	//body를 가지고있을때 키워드default를 붙여줘야함
          System.out.println("InterfaceA = mD()");
      }
  }
  
  ```

<br>

- 상위 Interface(InterfaceA)의 body를 가지고 있는 default method를 상속받은 하위 Interface(InterfaceB)에서 다시 추상 메서드로 바꾸면, Interface를 구현해야하는 클래스에서 추상메서드를 다시 구현 해줘야한다

<br>

<br>

## abstract

- 일부 구현되지 않은 메서드를 포함할 수 있는 클래스 정의 시에 사용하며, 구현되지 않은 메서드 정의 시에 사용

  => Interface와 일반 Class의 중간역할, 적절하게 활용할 용도

- 추상클래스는 object를 만들 수 없음 => 상속을 통해 상속 받은 클래스가 abstract 메서드를 모두 구현해야 객체 생성 가능

- abstract 메서드는 abstract 클래스에 정의해야한다

### abstract 클래스를 사용하는 이유

- Interface를 바로 구현을 하게되면 모든 메서드를 구현해야하는 불편함이 생긴다

- abstract 클래스가 Interface를 받아 안쓰는 메서드들을 구현하고(abstract클래스는 오버라이딩 안해도 되기떄문에), 일반 클래스에서 abstract를 상속받아 구현하면 자주쓰는 메서드들만 Overriding 하면 되서 편하다.  

  => Interface와 일반 class의 중계자 역할(Adapter 클래스)

  - AbstractClassInterface

    ```java
    public interface AbstractClassInterface {
        void m1();
        void m2();
        void m3();
        void m4();
        void m5();
        void m6();
    }
    
    ```

  <br>

  - AbstractNormalClass(=> NormalClass에서 구현해야하는 쓸데없는 메소드들을 막아주는 역할, 대신 구현해준다)

    ```java
    public abstract class AbstractNormalClass implements AbstractClassInterface{
    
        @Override
        public void m2() {	}
    
        @Override
        public void m3() {	}
    
        @Override
        public void m4() {	}
    
        @Override
        public void m5() {	}
    
        @Override
        public void m6() {	}
    }
    
    ```

  <br>

  - NormalClass

    ```java
    public class NormalClass extends AbstractNormalClass implements AbstractClassInterface{
    
        @Override
        public void m1() {
    
        }
    
    }
    
    ```

<br>

<br>

## Outer vs Inner(nested) 클래스

- nested클래스 -  inner클래스, static클래스

  - 객체로 만들어질 수 있으면 inner클래스, static이 붙으면 static  클래스

- inner에서 outer로는 접근이 가능하지만, 역은 성립하지 않는다

- outer에서 inner로 접근하려면 객체 생성해야 접근할 수 있다

  ```java
  public class OuterClass {
  
      int outerInt = 10;
      void outerMethod1() {
          System.out.println("outerInt : " + outerInt);
          //System.out.println("innerInt : " + innerInt);
          Inner1 inner1 = new Inner1();
          System.out.println("innerInt : " + inner1.innerInt);
      }
  
      class Inner1{
          int innerInt = 20;
          void innerMethod1() {
              System.out.println("outerInt : " + outerInt);
              System.out.println("innerInt : " + innerInt);
          }
      }
  
  }
  
  ```

<br>

### Method내에 class

- 메소드가 호출된 때에만 의미가 있음, 로컬변수처럼 사용

<br>

### Nested - static 클래스

- 어떤 클래스안에 nested클래스를 추가할 수 있는데 static 을 붙일 수 있다. 

- 그리고 이런 static 변수는 클래스 이름으로 접근 가능하다

  ```java
  public class StaticOuterClass {
      static class StaticClass{
          int MAX_NUM = 100;
          static int STATIC_MAX_NUM = 200;
      }
  
      void m1() {
          //StaticClass.MAX_NUM = 400; //컴파일 에러, MAX_NUM은 static이 아님
  
          //어떤 클래스안에 nested클래스를 추가할 수 있는데 static을 붙일 수 있다. 
          //그리고 이런 static 변수는 클래스 이름으로 접근가능하다
          StaticClass.STATIC_MAX_NUM = 300;
          StaticClass sc = new StaticClass();
          //물론 object로도 접근가능
          sc.MAX_NUM = 500;
          sc.STATIC_MAX_NUM = 600;
      }
  }
  
  ```

<br>

 - 같은 inner 클래스더라도 static으로 선언되면 new없이 생성가능하다

   ```java
   public class StaticClassTest {
   
       public static void main(String[] args) {
           //MAX_NUM은 static 아니여서 컴파일 에러
           //System.out.println(StaticOuterClass.StaticClass.MAX_NUM);	
           System.out.println(StaticOuterClass.StaticClass.STATIC_MAX_NUM);
           StaticOuterClass.StaticClass sc = new StaticOuterClass.StaticClass();
           //StaticClass가 static이 붙어있는 static클래스여서 new안하고 접근가능
           System.out.println(sc.MAX_NUM);	//객체 생성했으니까 접근 가능
       }
   }
   
   ```

<br>

<br>

## Anonymous Class

- 주로 이벤트 핸들링시 사용

- 호출당시만 필요할 때 사용(재사용 가능성이 없는 경우)

- AnonymousClass

  ```java
  public class AnonymousClass {
      public void callWrite(AnonymousInterface ai) {
          ai.write();
      }
  }
  
  ```

<br>

- AnonymousInterface

  ```java
  public interface AnonymousInterface {
      void write();
  }
  
  ```

<br>

- AnonymousClassTest

  ```java
  public class AnonymousClassTest {
  
      public static void main(String[] args) {
          AnonymousClass ac = new AnonymousClass();
  
          //Anonymous 클래스를 실제로 object화 하고, 인자로 넘기는 과정까지
          ac.callWrite(new AnonymousInterface() {
  
              //새롭게 interface를 받아 구현해야하니까 Overriding해줘야함
              @Override
              public void write() {
                  System.out.println("AnonymousClass - write()");
              }
          });
      }
  }
  ```

  

