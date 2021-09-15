---
layout: single
classes: wide

title: "싱글톤 패턴"
excerpt: "싱글톤 패턴에 대해서"

date: 2021-09-14 21:00:00 +0900
lastmod: 2021-09-14 21:00:00 +0900

author_profile: false

sidebar:
nav: "docs"

categories:
- design pattern

tags:
- design pattern
- singleton
- enum
- Lazy Initialization  
- double checked lock

# table of contents
toc: true # 오른쪽 부분에 목차를 자동 생성해준다.
toc_label: "Index" # toc 이름 설정
toc_icon: "cog" # 아이콘 설정
toc_sticky: true # 마우스 스크롤과 함께 내려갈 것인지 설정
---
<br>

# 싱글톤 패턴이란?
* 하나의 애플리케이션 내에 특정 클래스에 대한 객체가 최초에 `하나만 생성`되도록 하는 패턴.

<br>

# 왜 사용할까?
* 특정 클래스에 대한 하나의 객체만 생성하기 때문에 `메모리를 절약`할 수 있다.

<br>

# 싱글톤 패턴의 문제점
* 멀티쓰레드 환경에서 동기화 처리를 하지 않으면 문제가 발생할 수 있다. 
  * thread의 동시 접근 시 Thread-safe하게 작성해야 할 필요가 있다.
* 일반적으로 private 생성자를 통해 구현하기 때문에 해당 클래스를 상속할 수 없다.
  * 객체지향의 장점인 다형성을 이용할 수 없다.
* 테스트가 힘들다.
  * 클래스를 싱글톤으로 만들면 이를 사용하는 클라이언트를 테스트하기가 어려워 질 수 있다. 
  * 타입을 인터페이스로 정의한 다음 그 인터페이스를 구현해서 만든 싱글톤이 아니라면 싱글톤 인스턴스를 가짜(mock) 구현으로 대체할 수 없기 때문이다
* 싱글톤이 하나만 만들어지는 것을 보장하지 못한다.
  * 자바의 reflection을 이용하면 private 생성자를 사용했다고 하더라도 싱글톤을 쉽게 깨버릴 수 있다.
    * AccessibleObject.setAccessible을 사용하면 private 생성자를 호출할 수 있기 때문.

<br>

# 싱글톤 구현 방식
## 1. 고전적인 방식의 Singleton 패턴

```java
public class Singleton { 
    private static Singleton instance; 
    
    // 접근 제한자가 private으로 설정된 생성자
    private Singleton() {
	} 
    
    public static Singleton getInstance() { 
    	if (instance == null) {
        	instance = new Singleton();
    	} 
        return instance; 
    } 
}
```

### 문제점
* 위의 코드는 멀티쓰레드 환경에서 문제가 발생할 수 있다.
  * A라는 Thread와 B라는 Thread가 실행되고 있다고 가정할 때, Thread A가 `if (instance == null)` 까지 진행한 상황에서 제어권이 Thread B로 넘어간 경우 Thread B역시 `if (instance == null)`가 수행 되어 인스턴스가 2개가 생성되는 문제가 발생한다.

<br>

## 2. synchronized 를 이용한 Singleton 패턴
```java
public class Singleton { 
    private static Singleton instance; 
    
    private Singleton() {
    } 
    
    public static synchronized Singleton getInstance() {
    	if (instance == null) {
      		instance = new Singleton();
    	}	 
  	
    	return instance; 
    } 
}
```

### 문제점
* synchronized getInstance()의 경우 인스턴스를 리턴 받을 때마다 Thread 동기화 때문에 불필요하게 lock이 걸리게 되어 비용 낭비가 크다.
  * 실제로 고전적인 방식에서 인스턴스가 2개 이상 생성될 확률은 매우 적다.
* 즉, synchronized로 인한 성능 이슈가 발생한다.  

<br>

## 3. Double-checked Locking을 이용한 Singleton 패턴
```java
public class Singleton {
    
    private static volatile Singleton instance;

    private Singleton() {
    }
    
    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton .class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

* synchronized를 이용하는 방법에서 발생하는 성능 이슈를 최소화시키기 위해, 먼저 객체를 생성해야 하는지 확인하고(if문) 객체를 생성하는 경우에만 잠금을 획득하는 것으로 시작할 수 있다.

### 문제점
* 코드가 장황해져 읽기 어렵게 만든다.

<br>

## 4. static 초기화를 이용한 Singleton 패턴
```java
public class Singleton { 
    private static Singleton instance = new Singleton(); // static 초기화 시 바로 할당 
    
    private Singleton() {
    } 
    
    public static Singleton getInstance() { 
    	return instance; 
    } 
}
```

* 위의 방식은 멀티 쓰레드 환경에서 야기되는 모든 문제를 해결한다.
* Thread-safe 하며 소스가 간결하고 성능도 좋다.
* Thread가 getinstance()를 호출하는 시점이 아닌, Class가 로딩되는 시점. 즉 Static영역의 데이터 로딩시점에 `private static Singleton instance = new Singleton();` 를 호출하여 하나의 인스턴스만 생성되는 것을 보장한다.

### 문제점
* 실제로 사용할지 안할지 모르는 인스턴스를 굳이 미리 만들어 놓는 것이 옳지 않은 방법일 수 있다. 
* 애플리케이션이 인스턴스를 필요로 하는 시점이 아니라 사전에 생성하는 것은 메모리의 낭비일 수 있다.

<br>

## 5. LazyHolder Singleton 패턴
```java
public class Singleton { 
    
    private Singleton() {
    } 
    
    public static Singleton getInstance() {
    	return LazyHolder.INSTANCE; 
    } 
    
    private static class LazyHolder {
    	private static final Singleton INSTANCE = new Singleton(); 
    } 
}
```

* 가장 완벽하다고 평가받는 방법이다. JAVA 버젼에 무관하고 성능도 뛰어나다.
* 이 방법은 static 영역에 초기화를 하지만 객체가 필요한 시점까지 초기화를 미루는 방식이다. (Lazy Initialization)
* Singleton 클래스가 메모리에 로딩되는 순간에는 LazyHolder 클래스를 초기화 하지 않는다.
* getInstance() 메서드에서 LazyHolder.INSTANCE를 참조하는 순간 LazyHolder Class가 로딩되어 초기화가 진행된다.

<br>

## 6. Enum을 통한 Singleton 패턴

```java
public enum Singleton {
    INSTANCE;
}
```

* enum은 인스턴스가 여러 개 생기지 않도록 확실하게 보장해준다.
* enum은 Thread-safety 하다.
  * 단, Enum 내의 다른 메소드에 대해서는 프로그래머가 thread safe를 직접 책임져야 한다.
* enum은 Serialization을 스스로 해결한다.
  * 별도의 코드추가 없이 JVM은 기본적으로 Enum의 Serialization을 보장해준다.
  * 반면, 일반적인 싱글톤에서는 직렬화할 때, 싱글톤이 싱글톤이 아니게되는 문제가 발생한다.
    * 왜냐하면 직렬화 하려면 readObject()를 구현해야하는데, readObject()는 매번 새로운 인스턴스를 리턴하기 때문이다.
* enum은 reflection 공격에 대한 방어가 가능하다.
* 즉, `enum은 Reflection 공격과 아주 복잡한 직렬화 상황에도 제2의 인스턴스가 생기는 일을 완벽히 방어할 수 있다.`

<br>
 
# 참고
* effective java 3/E / Joshua Bloch / 인사이트
* [https://jeong-pro.tistory.com/86](https://jeong-pro.tistory.com/86)
