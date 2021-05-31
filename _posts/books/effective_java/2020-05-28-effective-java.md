---
layout: single
classes: wide

title: "effective java item-1 생성자 대신 정적 팩터리 메서드를 고려하라"
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
- jvm

# table of contents
toc: true # 오른쪽 부분에 목차를 자동 생성해준다.
toc_label: "Index" # toc 이름 설정
toc_icon: "cog" # 아이콘 설정
toc_sticky: true # 마우스 스크롤과 함께 내려갈 것인지 설정
---
<br>

## 클래스로부터 인스턴스를 얻는 방법
* public 생성자
```java
Person person = new Person()
```
* 정적 팩토리 메서드 (static factory method)

## 정적 팩토리 메서드가 생성자보다 좋은 장점 다섯가지
* 이름을 가질 수 있다.
* 호출할때마다 인스턴스를 새로 생성하지 않아도 된다.
* 반환 타입의 하위 타입 객체를 반환할 수 있다.
* 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.
* 정적 팩토리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.

## 정적 팩토리 메서드의 단점
* 상속을 하려면 public이나 protected 생성자가 필요하니 정적 팩토리 메서드만 제공하면 하위 클래스를 만들 수 없다.
* 정적 팩토리 메서드는 프로그래머가 찾기 어렵다.

# 참고
* effective java 3/E / Joshua Bloch / 인사이트
