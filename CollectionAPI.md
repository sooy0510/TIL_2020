# Collection API

- java.util package에 정의
- Collection : 모든 클래스들의 **Object**를 요소로 저장하는 객체의 최상위 Interface

<br>

![image-20200217153953924](images/image-20200217153953924.png)

- LinkedList : List & Deque
  - List와 Queue를 구현하기에 모두 유용한 구조

<br>

## Set

### HashSet

- 순서 관리 x

- 중복 허용 x : 같은 데이터(equals(), hashCode() 비교시) 는 무시

  - vm은 equals나 hashCode 둘 중 하나라도 다르면 다르다고 생각한다

    ```java
    HashSet<Point> hsPoint = new HashSet<Point>();
    //vm입장에서 equals()나 hashcode 중 하나라도 다르면 Point(1,3)은 서로 다른객체라고 생각
    hsPoint.add(new Point(1,3));
    hsPoint.add(new Point(2,4));
    hsPoint.add(new Point(1,3));
    hsPoint.add(new Point(5,7));
    
    
    //Iterator 사용
    Iterator<Point> itrPoint = hsPoint.iterator();
    while(itrPoint.hasNext()) {
        System.out.println(itrPoint.next());
    }
    ```

    

- sortedset - treeset : set계열 중 순서 관리

<br>

## List

### ArrayList

- 순서 관리
- 중복 허용
- 객체 저장 시 index를 가지고 관리(순서대로)
- 넣은 순서대로 순차적으로 나온다
- descendingIterator() 지원 안함

<br>

### LinkedList

- ArrayList와 유사
- descendingIterator() 지원 => 역순으로 출력

<br>

### Arraylist vs LinkedList

- Arraylist는 내부적으로 index를 가지고 있다.

- 단순증가시에는 상관이 없지만, 삭제시에는 index를 수정하는 추가적인 작업이 필요하다

- 따라서, 삭제 작업이 필요할때는 LinkedList가 훨씬 유리하다

  ```java
  import java.util.ArrayList;
  import java.util.LinkedList;
  import java.util.List;
  
  public class ListPerformanceTest {
  
      public static void main(String[] args) {
          long startTime = System.nanoTime();
  
          List<Point> l = new ArrayList<Point>();
          //List<Point> l = new LinkedList<Point>();
  
          for(int i=0; i<900000; i++) {
              l.add(new Point(i,i));
          }
  
          for(int i=1000; i<50000; i++) {
              l.remove(i);
          }
  
  
          long stopTime = System.nanoTime();
  
          System.out.println(stopTime - startTime);
      }
  
  }
  
  
  => ArrayList : 3724730800
      LinkedList : 2967678700
  ```

  

<br>

<br>

## Stack

- search(int) : index+1을 반환

  ```java
  Stack<Integer> sInt = new Stack<Integer>();
  sInt.push(1);
  sInt.push(4);
  sInt.push(7);
  sInt.push(1);
  sInt.push(5);
  
  System.out.println();
  System.out.println(sInt.search(7)); //index+1
  => 3
  //없으면 -1반환
  ```

<br>

<br>

## PriorityQueue

- 제네릭에 사용자지정 클래스를 사용하면 내부적으로 Comparable을 호출하려고 함

- CompareTo가 오버라이딩 안되어있으면 에러

- offer하는 동시에 정렬

- Comparable 사용 예제

  - QueuePriorityQueueTest

    ```java
    import java.util.PriorityQueue;
    import java.util.Queue;
    
    public class QueuePriorityQueueTest {
    
        public static void main(String[] args) {
            //Point내에서 우선순위를 따질 수 없어서 오류, Comparable을 호출하려고 함
            Queue<Point> qPoint = new PriorityQueue<Point>();
            qPoint.offer(new Point(14,27));
            qPoint.offer(new Point(5,5));
            qPoint.offer(new Point(17,1));
            qPoint.offer(new Point(8,63));
            qPoint.offer(new Point(5,2));
    
            System.out.println(qPoint.size());
            System.out.println(qPoint.poll() + " " + qPoint.poll());
            
            //Iterator로 출력하면 랜덤으로 리턴(내부적으로 정렬은 하지만 리턴값은 랜덤)
            Iterator<Point> itr = qPoint.iterator();
            while(itr.hasNext()) {
                System.out.print(itr.next()+" ");
            }
        }
    
    }
    
    ```

  <br>

  - Point

    ```java
    package chap7.base;
    
    public class Point implements Comparable<Point> {
        public int r;
        public int c;
    
        public Point() {}
        public Point(int r, int c) {
            super();
            this.r = r;
            this.c = c;
        }
    
       ...
    
        @Override
        //r 먼저 비교하고, 같으면 c로 비교 - 오름차순
        public int compareTo(Point o) {
            if(this.r == o.r) {
                return this.c - o.c;
            }else {
                return this.r - o.r;
            }
        }
    
    }
    
    ```

  <br>

  - 실행결과

    ```java
    5
    [5,2] [5,5]
    [8,63] [14,27] [17,1] 
    ```

<br>

<br>

## ArrayList

- remove : index와 요소값으로 삭제가능

  ```java
  public class CollectionRemoveTest {
  
      public static void main(String[] args) {
          ArrayList<String> al = new ArrayList<String>();
          al.add("Cass");
          al.add("IsBack");
          al.add("Cass");
          al.add("Terra");
          al.add("Jangsu");
          al.add(new String("Jangsu"));
  
          Iterator<String> itrAl = al.iterator();
          while(itrAl.hasNext()) {
              System.out.print(itrAl.next()+" ");
          }
  
          //al.remove(1);
          al.remove("Jangsu");
          al.remove("Jangsu");
  
          System.out.println();
  
          itrAl = al.iterator();
          while(itrAl.hasNext()) {
              System.out.print(itrAl.next()+" ");
          }
      }
  
  }
  
  => Cass IsBack Cass Terra Jangsu Jangsu 
  Cass IsBack Cass Terra 
  
  ```

<br>

<br>

## Map

- object가 key와 value의 쌍으로 관리됨

- 똑같은 key를 가진 요소가 추가되면 Overwrite효과(덮어씌운다)

- keySet() : key를 set형태로 받아온다

  ```java
  public class MapHashMapTest {
  
      public static void main(String[] args) {
          Map<String, Integer> productPrice = new HashMap<>();
          productPrice.put("TV", 220);
          productPrice.put("Refrigerator", 180);
          productPrice.put("Desk", 40);
          productPrice.put("Computer", 70);
          productPrice.put("Desk", 50);	//Overwrite, 덮어씀
  
          System.out.println(productPrice.size());
  
          int price = productPrice.get("Computer");
          System.out.println("Computer Price is "+price);
  
          Set<String> keys = productPrice.keySet();
  
          for(String key : keys) {
              System.out.print(key +" " + productPrice.get(key) + " | ");
          }
  
          if(productPrice.containsKey("Desk")) {
              System.out.println("Desk key exist!!");
          }
      }
  
  }
  
  => 4
  Computer Price is 70
  TV 220 | Computer 70 | Refrigerator 180 | Desk 50 | Desk key exist!!
  ```

- containsKey([key]) : key로 검색

- containsValue([value]) : value로 검색

 