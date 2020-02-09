# 1. String 클래스

- 리턴값(복사본) 이용

- immutable한 특성

- concat, replace, length, charAt, substring 등은 리턴값을 이용한다.

  ```java
  //concat : 자기자신이 아니라 리턴값이 concat됨
  String s1 = "Hello";
  s1.concat("SSAFY!!");
  System.out.println(s1);
  
  String s2 = s1.concat("SSAFY");
  System.out.println(s2);
  
  
  System.out.println("====================");
  
  //replace : 리턴값을 바꿈
  String s3 = "Hello";
  s3.replace('l', 'L');
  System.out.println(s3);
  
  String s4 = s3.replace('l', 'L');
  System.out.println(s4);
  
  System.out.println(s3.replace('l', 'L'));
  
  System.out.println("====================");
  
  // length, charAt, substring : 리턴값
  String s5 = "Hello";
  System.out.println(s5.length());
  System.out.println(s5.charAt(0));
  System.out.println(s5.charAt(4));
  System.out.println(s5.substring(0,3));
  
  System.out.println("====================");
  
  //startWith, endWith, indexOf
  String s6 = "Hello, SSAFY? We are here";
  System.out.println(s6.startsWith("He"));
  System.out.println(s6.endsWith("Here"));
  System.out.println(s6.indexOf("SSAFY"));
  System.out.println(s6.indexOf("e"));
  
  System.out.println("====================");
  
  //CompareTo
  String s7 = "AAA";
  String s8 = "BBB";
  String s9 = "DD";
  System.out.println(s7.compareTo(s8));
  System.out.println(s7.compareTo(s9));
  
  System.out.println("====================");
  
  //trim
  String s10 = " Use Trim method!! ";
  System.out.println(s10.trim());
  
  System.out.println("====================");
  
  //contains space 포함
  String s11 = "We are in SSAFY class!!";
  if(s11.contains(" in ")) {
      System.out.println("s11 contains it!!");
  }
  ```

  



<br>

<br>

# 2. Math 클래스

- Math.random() vs Random 클래스

  ```java
  System.out.println(Math.abs(-20));	//절대값 
  System.out.println(Math.max(10,20));
  System.out.println(Math.min(10,20));
  
  System.out.println(Math.round(13.74));	//소수점 이하 반올림.int, long return
  System.out.println(Math.round(133.74));	//int, long return
  System.out.println(Math.ceil(13.34));	//소수점 이하 올림 : double return
  System.out.println(Math.floor(13.34));	//소수점 이하 내림 : double return
  
  // random (1~10)
  for (int i = 0; i < 10; i++) {
      double d = Math.random();
      System.out.println(d + " : " + (d*10 + 1) +" : " + (int)(d*10 + 1));
  }
  
  //java.util.Random
  Random r = new Random();
  for(int i=0; i<10; i++) {
      System.out.println(r.nextInt(10) + 1);
  }
  ```

  

# 3. Wrapper 클래스

- primitive type을 객체화 시켜주는 클래스

- new로 객체 안만들고 바로 대입도 가능하다(java 5.0부터 허용)

  ```java
  // primitive 객체화
  Integer object = 300;
      
  
  // 객체를 primitive
  int ip = object;
  ```

  

<br>

<br>

# 4. StringBuilder

- 원본이용

  ```java
  //StringBuffer : thread safe(병렬처리)
  //StringBuilder : 
  
  StringBuilder sb1 = new StringBuilder();
  String end = "!!";
  sb1.append("Hello").append(" World").append(" and").append(" SSAFY ").append(end);
  System.out.println(sb1);
  System.out.println(sb1.hashCode());
  
  
  //insert
  StringBuilder sb2 = new StringBuilder("abcdefghijklmn");
  sb2.insert(5, "123");	//index 5에 넣기
  System.out.println(sb2);
  
  
  //setCharAt
  StringBuilder sb3 = new StringBuilder("abcdefghijklmn");
  sb3.setCharAt(5, 'X');
  System.out.println(sb3);
  
  //reverse(원본을 바꾼다)
  StringBuilder sb4 = new StringBuilder("abcdefghijklmn");
  sb4.reverse();
  System.out.println(sb4);
  
  //setLength(관리하는 영역지정) - 초기화할때 유용
  StringBuilder sb5 = new StringBuilder("abcdefghijklmn");
  sb5.setLength(5);
  System.out.println(sb5);
  ```







- 자바시험
  - printf

## Polymorphism

- A

  ```java
  public class A {
      public int i = 10;
  
      public void m() {
          System.out.println(i);
      }
  }
  ```

<br>

- B

  ```java
  public class B extends A{
      public int i = 20;
  
      public void m() {
          System.out.println(i);
      }
  }
  ```

<br>

- C

  ```java
  public class C extends B{
      public int i = 30;
  
      public void m() {
          System.out.println(i);
      }
  }
  ```

<br>

```java
//Polymorphism
//객체는 B만큼 만들어지지만, obj의 범위는 A만큼 만들어지기 때문에 A범위에 해당하는 범위까지만 이용할 수 있다.
//오버라이딩된 메서드만 제외. B에서 오버라이딩된 메서드 쓸 수 있다.

A obj = new B();
System.out.println(obj.i);
obj.m()
```

