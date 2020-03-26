# Java XML Programming

## 1. XML 이해 - 개요

- Mark-up Language
  - 태그 등을 이용하여 문서나 데이터의 구조를 명기하는 언어의 한 가지
  - SGML : 문서의 구조를 기술할 수 있도록 하는 표준 언어
  - HTML : SGML에 기반한 마크업 언어, 데이터의 표현에 집중

- eXtensible Markup Language
  - 작은 SGML
  - 범용적
  - 데이터의 표현 보다는 저장, 교환, 공유
  - 미리 정의된 tag없음(사용자 지정 태그 가능)
  - 표현으로부터 분리

<br>

### 확장

- ebXML
  - 전자상거래
- MathML
  - 수학공식 표현
- SVG
  - Scalable Vector Graphics
  - 이미지 등 그래픽은 WEB상에서 표현



<br>

### 주요 syntax

- 대소문자 구별
- attribute의 값음 " ",' '
- white space 보존



<br>

### Namespace

- 자유로운 tag의 생성에 따른 tag의 중복 문제 해결

<br>

<br>

## 2. XML DTD

- Document Type Definition
- 문서의 구성 요소와 유효한 값 명시

<br>

<br>

## 3. XML Parser

- XML문서의 구조(DOM)을 이해하고 필요에 따라 활용
- SAX
  - SAX는 위에서부터 읽어들임 
    - 특정 태그 발견시 이벤트 실행하는 방식(handler 필요)

<br>

- DOM
  - 돔 방식으로 파싱/트리를 만듬 
    - 해당 파일을 parse다 할때까지 기다려야함
    - 모든 DOM구조를 알수있기 때문에 모든 태그에 접근가능함

<br>

<br>

## 4. JSON

- Javascript의 object와 array를 이용하여 데이터를 표현
- GSON이용

<br>

### Member

```java
class Member{
	public String name;
	public int age;
	
	public Member(String name, int age) {
		this.name = name;
		this.age = age;
	}
}
```



### json => java

```java
//object
{
    Gson gson = new Gson();
    String jsonStr = "{ 'name' : 'Hong', 'age' : 25}";
    Member member = gson.fromJson(jsonStr,Member.class);
    System.out.println(member.name + " "+member.age);

}

//array
{
    Gson gson = new Gson();
    String jsonArrayStr = "[{'name':'Hong', 'age':25}, "
        + "{'name':'Kim', 'age':26}, {'name':'Park', 'age':31}]";
    Member[] memberArray = gson.fromJson(jsonArrayStr, Member[].class);

    for(Member m : memberArray) {
        System.out.println(m.name +" "+m.age);
    }
}
```

<br>

### java => json

```java
//object

{
    Gson gson = new Gson();
    Member member = new Member("Kang", 29);
    String jsonStr = gson.toJson(member);
    System.out.println(jsonStr);
}

//array
{
    Gson gson = new Gson();

    Member[] memberArray = {new Member("Lee",30),new Member("Kim",35), new Member("Part",40)};
    String jsonArrayStr = gson.toJson(memberArray);

    System.out.println(jsonArrayStr);
}
```

