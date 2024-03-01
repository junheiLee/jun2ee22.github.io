---
layout: single
title: "[Java] Java 개발 시작하기"
categories: Language
tag: [Java, Java의 정석]
---
Java의 정석 01장 정리(3)

# 개발 시작
## 개발 환경 구축(Windows)
1. JDK Download


   저의 실행 파일 폴더 경로는 `C:\Program Files\Java\jdk-11\bin` 입니다.<br>

   > [🔗실행 파일](/language/standard-of-java-01_2/#실행-파일)은 JDK의 bin 디렉토리에 존재합니다.<br>
   > 터미널이나 커맨드 라인에서 `java`, `javac`를 어느 위치에서나 직접 호출할 수 있도록 "환경 변수"를 설정해야 합니다.

   <br>
2. 환경 변수 설정


   `고급 시스템 설정` → `환경 변수`<br>
   &nbsp; 저는 하단의 `시스템 변수`를 건들겠습니다.<br>
   - &nbsp; &nbsp; 상단: 현재 사용자 계정에만 적용<br>
   - ✔ 하단: 모든 사용자 게정과 시스템 전체에 적용<br>
   <br>
   [PATH에 경로 추가]<br>
   `Path` 변수 더블클릭 → `새로 만들기` → 실행 파일 경로 추가(ex.C:\Program Files\JetBrains\jdk-11\bin\)<br>

   [JAVA_HOME] 환경 변수 추가<br>
   `새로 만들기` → 이름: JAVA_HOME, 값: JDK 경로(ex.C:\Program Files\JetBrains\jdk-11)

   <br>

   > &nbsp; <span style="background-color: #E2E2E2">환경 변수</span>란 OS에서 시스템이나 프로그램의 작동 방식을 설정하는 데 사용하는 변수입니다.
   > 값은 키-값 쌍인 문자열 형태로 저장됩니다. 하나의 환경 변수에 여러 값이 있는 경우 Windows는 `;`으로 구분합니다.
   >
   > &nbsp; <span style="background-color: #E2E2E2">PATH 환경변수</span>는 OS가 프로그램이나 실행 파일을 찾을 때, 파일의 위치(directory)를 파악하는 데 사용합니다.
   > 파일의 경로(directory)를 PATH 환경 변수에 추가하면 해당 파일은 어떤 경로에서든 이름만으로 실행할 수 있습니다.
   > 
   > &nbsp; <span style="background-color: #E2E2E2">JAVA_HOME 환경변수</span> 빌드 도구(gradle, maven), IDE(intelliJ), Java 기반 응용 프로그램 등(Tomcat)에서 JDK의 위치를 찾기 위해 사용하는 환경 변수입니다.
   > JDK 폴더까지의 경로로 설정하면 됩니다.

   <br>

3. 설정 확인

   명령 프롬프트에서 `java`, `javac` 명령어를 실행해도 되지만 귀찮으니 `java -version`으로 합니다.<BR><bR>


## 실행을 위한 기본 구조 



## public class

&nbsp; public class가 있는 경우, 소스 파일의 이름은 public class와 대소문자까지 동일해야 합니다.
또한 하나의 소스 파일에 public class는 단 한 개만 존재할 수 있으며,
public class가 없는 경우에는 소스 파일의 이름은 포함된 class 중 하나를 선택할 수 있습니다.

&nbsp; 하나의 소스 파일에 여러 개의 class가 있으면 컴파일 시, 클래스 마다 class 파일이 생성됩니다.

---
<p> 
  <strong>👀 참고: </strong>
  <span itemprop="keywords">
    <a href="https://product.kyobobook.co.kr/detail/S000001550352" class="page__taxonomy-item p-category">남궁성, 'Java의 정석'</a>
  </span>
</p>
<p> 
  <strong>📑 목차: </strong>
  <span itemprop="keywords">
    <a href="/목차/standard-of-java" class="page__taxonomy-item p-category">Java의 정석 정리</a>
  </span>
</p>

<nav class="pagination">
<a href="/language/standard-of-java-01_2" class="pagination&#45;&#45;pager" title="{{ page.previous.title | markdownify | strip_html }}"> 👈 01장(2)</a>
<a href="#" class="pagination&#45;&#45;pager" title="{{ page.previous.title | markdownify | strip_html }}"> 아직 음슴 </a>
</nav>