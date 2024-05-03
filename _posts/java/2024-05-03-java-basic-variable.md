---
layout: single
title: "[Java] 변수 관련"
categories: Language
tag: [Java, basic-grammar]
---

# 변수

&nbsp; 하나의 값을 저장할 수 있는 메모리 공간

## 변수 선언 및 초기화

### 선언

```java
// 변수 타입 변수 이름;
int javaVariable;
```
&nbsp; 저장하고자 하는 값의 종류에 해당하는 타입으로 선언합니다.
Java에서는 lowerCamelCase로 명명하는 관례가 있답니다.

&nbsp; 조금 더 설명하자면 변수 이름은 저장하고자 하는 값 자체가 아닌 저장하는 위치(메모리 공간)의 별명입니다.
변수 이름을 통해 메모리 공간에 접근해 값을 사용하죠.

<br>

### 초기화

```java
// 변수 이름 = 초깃값;
javaVariable = 1;
```

&nbsp; 변수 이름으로 메모리 공간에 접근하고, 대입 연산자(=)로 초깃값을 저장합니다.


&nbsp; 사실 멤버 변수로 primitive type 변수를 선언하면 해당 Type의 default 값으로 자동 초기화됩니다. 
하지만 지역 변수로 선언 시, 메모리는 여러 프로그램이 공유하는 자원이기 때문에 반드시 초기화해야 합니다.
전에 사용하던 쓰레기 값(garbage value)이 운이 나쁘게 남아있을 수 있잖아요.

&nbsp; 개인적으로 초기화를 명시적으로 해주면 가독성에도 이점이 있다고 생각해요..

<br>

### 한 번에 하기

```java
int javaVariable = 1;
```

&nbsp; 저는 선언과 초기화를 굳이 따로 하지는 않고, 한 번에 합니다.

### 변수 vs 상수 vs 리터럴

&nbsp; 일상생활에서 상수를 리터럴이라고 이해하면 됩니다.
변수라는 통에 리터럴을 담고, 이를 변할 수 없도록 final 키워드를 붙이면 프로그래밍에서 상수가 됩니다.

&nbsp; 굳이 변하지 않는 값을 정의할 필요가 있을까 싶지만 예를 들어 어떤 게시판에 댓글을 5개만 달 수 있게 제한합니다.
```java
private boolean isMaxComment(int commentCount) {
  return commentCount >= 5;
}

private int getRemainComment(int commentCount) {
  return 5 - commentCount;
}
```
&nbsp; 이런 식으로 코드의 여기저기 5라는 숫자가 있겠죠?
그런데 유입이 늘어나서 댓글의 제한을 10개로 늘리게 된다면??
코드를 처음부터 하나하나 다 찾아야 합니다. 유지 보수가 너무너무너무 힘들게 돼요.

&nbsp; 하지만 이 녀석을 상수로 선언한다면?

```java
public static final MAX_COMMENT_COUNT = 5;

private boolean isMaxComment(int commentCount) {
  return commentCount >= MAX_COMMENT_COUNT;
}

private int getRemainComment(int commentCount) {
  return MAX_COMMENT_COUNT - commentCount;
}
```
&nbsp; 이렇게 코드를 짜면 제한된 댓글 개수를 변경할 때, 코드의 단 한 줄을 변경하면 됩니다.
컨벤션에 따라 상수를 대문자와 밑줄(_)로 명명하면, 코드를 읽을 때도, 해당 상수가 어떤 값을 의미하는지 알기 쉬워요!

## Type

&nbsp; Java는 객체지향언어지만, 객체가 아닌 변수 기본 타입이 딱 8개 있습니다.
- 논리
  - boolean: true, false
  - 다른 곳에서는 true를 1 false를 0으로 연산 가능하기도 하지만 Java는 아니지롱.
- 문자
  - char: 한 글자
  - 사실 내부적으로는 유니코드라는 정수로 저장하기 때문에 숫자형과 연산도 가능합니다.
- 숫자
  - 정수
    - byte, short, int(4byte), long
    - short 타입은 C언어와의 호환을 위해 추가됐대요.
    - CPU가 int를 가장 효율적으로 사용한다고 합니다. 실무에서는 아마 대부분 int를 사용할 듯?
  - 실수
    - float, double(8byte)

&nbsp; 딱 봐도 소문자로 시작하는 게 예약어처럼 생기지 않았나요?
이 녀석들은 메모리 공간에 리터럴을 저장해둡니다. 실제 연산에 사용하죠.

&nbsp; 대문자로 시작하는 타입은 참조형 변수입니다. Java에서 class는 UpperCamelCase를 쓰거든요.
그 녀석들은 변수에 참조해야 할 주소가 저장되어 있습니다. 참조형 변수끼리는 연산을 할 수 없어요.

### 그 외

&nbsp; 
### 주의할 내용

### Primitive Type vs Reference Type

## Scope






---
<p> 
  <strong>👀 참고: </strong>
  <span itemprop="keywords">
    <a href="https://product.kyobobook.co.kr/detail/S000001550352" class="page__taxonomy-item p-category">남궁성, 'Java의 정석(책)'</a><span class="sep">, </span>
    <a href="https://www.inflearn.com/course/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%9E%90%EB%B0%94-%EC%9E%85%EB%AC%B8" class="page__taxonomy-item p-category">김영한, '자바 입문(인프런)'</a>
  </span>
</p>
<p> 
  <strong>📑 목차: </strong>
  <span itemprop="keywords">
    <a href="/목차/java-list" class="page__taxonomy-item p-category">Java 목차</a>
  </span>
</p>


<nav class="pagination">
<a href="/language/java-start-03" class="pagination&#45;&#45;pager" title="{{ page.previous.title | markdownify | strip_html }}"> 👈 Java start(3) </a>
<a href="#" class="pagination&#45;&#45;pager" title="{{ page.previous.title | markdownify | strip_html }}"> 업슴 👉</a>
</nav>