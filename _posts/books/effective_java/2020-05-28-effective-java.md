---
layout: single
classes: wide

title: "Item-1. 생성자 대신 정적 팩터리 메서드를 고려하라"
excerpt: "생성자 대신 정적 팩터리 메서드를 고려하라"

date: 2020-05-28 15:00:00 +0900
lastmod: 2020-05-28 15:00:00 +0900

author_profile: false

header:
overlay_image: assets/images/java.png
overlay_filter: 0.5
teaser: assets/images/java.png

sidebar:
nav: "docs"

categories:
- java

tags:
- effective java
- public constructor  
- static factory method

# table of contents
toc: true # 오른쪽 부분에 목차를 자동 생성해준다.
toc_label: "Index" # toc 이름 설정
toc_icon: "cog" # 아이콘 설정
toc_sticky: true # 마우스 스크롤과 함께 내려갈 것인지 설정
---
<br>

## 클래스로부터 인스턴스를 얻는 방법
### 1. public 생성자

```java
...
  
Person person = new Person()
  
...
```

### 2. 정적 팩토리 메서드 (static factory method)

```java
...

public static Boolean valueOf(boolean b) {
    return b ? Boolean.True : Boolean.FALSE;    
}

...

Boolean.valueOf(b);
```

<br>

## 정적 팩토리 메서드가 생성자보다 좋은 장점 다섯가지
### 1. 이름을 가질 수 있다.

```java
...

public static Person of(String name, int age) {
    return new Person(name, age);
}

...
```  

### 2. 호출할때마다 인스턴스를 새로 생성하지 않아도 된다.
### 3. 반환 타입의 하위 타입 객체를 반환할 수 있다.

```java
...

public static Person man(String name, int age, char gender) {
    return new Man(name, age, gender);
}

...

```
  
### 4. 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.

```java
...

public static Person man(String name, int age, char gender) {
    return gender == 'M' ? new Man(name, age, gender) : new Woman(name, age, gende);
}

...

```

### 5. 정적 팩토리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.
* 이러한 유연함은 서비스 제공자 프레임워크 (service provider framework)를 만드는 근간이 됨.
  * 대표적인 service provider framework로는 JDBC가 있음.

<br>

## 정적 팩토리 메서드의 단점
### 1. 상속을 하려면 public이나 protected 생성자가 필요하니 정적 팩토리 메서드만 제공하면 하위 클래스를 만들 수 없다.
* 어찌보면 상속을 못한다는 것이 상속보다 컴포지션을 사용하도록 유도하고 불변타입으로 만들려면 이 제약을 지켜야 한다는 점에서 오히려 장점으로 받아들여질 수도 있음.

### 2. 정적 팩토리 메서드는 프로그래머가 찾기 어렵다.
* 정적 팩토리 메서드는 생성자처럼 API 설명에 명확히 드러나지 않으니 직접 API 문서를 잘 작성하고 메서드 이름도 널리 알려진 규약에 맞게 짓는 식으로 문제를 완화 해야함.
* 정적 팩토리 메서드 명명 방식
  * from
    * 매개변수를 하나 받아서 해당 타입의 인스턴스를 반환하는 형변환 메서드
    * ex) `Date d = Date.from(instant)`
  * of
    * 여러 매개변수를 받아 적합한 타입의 인스턴스를 반환하는 집계 메서드
    * ex) `Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING);`
  * valueOf
    * from과 of의 더 자세한 버전
    * ex) `BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);`
  * instance 혹은 getInstance
    * 매개변수로 명시한 인스턴스를 반환하지만, 같은 인스턴스임을 보장하지는 않음.
    * ex) `StackWalker luke = StackWalker.getInstance(options);`
  * create 혹은 newInstance
    * instance 혹은 getInstance와 같지만, 매번 새로운 인스턴스를 생성해 반환함을 보장.
    * ex) `Object newArray = Array.newInstance(classObejct, arrayLen);`
  * getType
    * getInstance와 같으나, 생성할 클래스가 아닌 다른 클래스에 팩토리 메서드를 정의할 때 씀. "Type"은 팩토리 메서드가 반환할 객체의 타입임.
    * ex) `FileStore fs = Files.getFileStore(path);`
  * newType
    * newInstance와 같으나, 생성할 클래스가 아닌 다른 클래스에 팩토리 메서드를 정의할 때 쓴다. "Type"은 팩토리 메서드가 반환할 객체의 타입임.
    * ex) `BufferedReader br = Files.newBufferedReader(path);`
  * type:
    * getType과 newType의 간결한 버전
    * ex) `List<Complaint> litany = Collections.list(legacyLitany);`

<br>

> 핵심정리  
> 정적 팩토리 메서드와 public 생성자는 서로 상호 배타적인 관계가 아니라 각자 쓰임새가 있음.  
> 즉, 각각의 장단점을 이해하고 사용하는 것이 좋음.  
> 다만, 정적 팩토리 메서드를 사용하는 것이 유리한 경우가 더 많으므로 무작정 public 생성자를 제공하던 습관이 있다면 고치는 것이 좋을 것.

<br>

## 참고
* effective java 3/E / Joshua Bloch / 인사이트
