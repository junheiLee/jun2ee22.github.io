---
layout: single
title: "[Java] IDE로 Java 개발 시작하기"
categories: Language
tag: [Java, Java의 정석]
---
Java의 정석 01장 정리(3)

# 개발 시작
## 개발 환경 구축
1. JDK Download

   실행 파일 폴더 경로: ****`C:\Program Files\Java\jdk-11\bin`

   > 바이트 코드로 변환 후(javac.exe) 실행되어야 하므로
   ide에서 사용할 수 있도록 환경 변수 설정 해줘야 함.

2. 환경 변수 설정

   `내 pc 우클릭` → `속성` → `관련 설정` → `고급 시스템 설정` → `환경 변수`

   > *상단: 로그인 계정 환경 변수
   ✔하단: window system 환경 변수*
   >

   → path에 실행 파일 폴더 [경로](https://www.notion.so/Java-a50b41329271470fa11a28cacddbf06b?pvs=21) 추가

3. 설정 확인

   명령 프롬프트: `java`, `javac` 명령어 실행 여부 확인

path

OS가 파일의 위치(directory)를 파악하는데 사용하는 경로

→ path에 directory 등록 시, 해당 directory의 파일은 경로 없이 파일 이름만으로 사용 가능

CLASSPATH
java.exe나 JVM이 class의 위치를 파악하는데 사용하는 경로

## 실행 과정