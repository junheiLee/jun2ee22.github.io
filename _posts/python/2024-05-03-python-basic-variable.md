---
layout: single
title: "[Python] 변수 관련"
categories: Language
tag: [Python, basic-grammar]
---

# 변수

&nbsp; 하나의 값을 저장할 수 있는 메모리 공간

<br>

&nbsp; Java와 다르게 파이썬의 변수는 동적으로 타입을 지정합니다.
3.5부터 Type Hinting을 지원하지만 실질적으로 의미는 없다고 합니다.
저는 Java를 먼저 공부해서 그런지 영 불안해서 변수의 타입을 체크한 후 사용할 것 같아요,,

##  변수 선언 및 초기화

```python
# 변수 이름 = 초기값
python_variable = 1
```

&nbsp; 초깃값을 None 타입으로 설정할 수는 있지만, 변수 선언만 하는 것은 불가능합니다.

### 파이썬 짱!! SWAP

&nbsp; 왜 그런 말 있잖아요. 코딩 테스트는 python이라고,,,
저는 그 말에 체감한 게 바로 Python의 스왑입니다.

```python
a = 10
b = 20
a, b = b, a
```
&nbsp; 저한테는 정말 신세계였어요.


## 주의할 내용


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