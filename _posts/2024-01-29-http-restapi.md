---
layout: single
title: "[Network] REST API"
categories: CS
tag: [network, http]
---
# 🤜Representational State Transfer Application Programming Interface🤛
<br>
새삼 별다줄
<br>

## 👉REpresentational State Transfer?👈
&nbsp;[ORACLE](https://docs.oracle.com/database/apex-18.1/AEUTL/what-is-REST.htm#AEUTL29132)에서 다음과 같이 정의합니다.<br> 
> a way of providing interoperability between computer systems on the Internet<br>
*인터넷상에서 컴퓨터 시스템 간의 상호 운용성을 제공하는 방법*
 
&nbsp; [상호운용성](https://aws.amazon.com/ko/what-is/interoperability/)이라는 단어가 와닿지 않는데, 다음의 **등장 배경**을 보고 나서 직관적으로 이해했습니다.


### 등장 배경🧩
&nbsp;Roy 씨가 HTTP 명세를 작성하는 당시, HTTP는 Word Wide Web(www)의 전송 프로토콜로 이용되고 있었다고 합니다.<br>
&nbsp;HTTP를 제멋대로 고치면 이미 구축되어 있는 Web과 호환에 문제가 생길 것 같아요.<br>
<br>
 따라서 다음과 같은 고민을 합니다.<br>
![@Schema](../../images/2024-01-30-http-restapi/why.PNG)
<br> &nbsp;이에 대한 해결책으로 `HTTP Object Model`이 등장하고, 
<br>1998년 `REST`라는 이름으로 발표합니다.
> [Representational State Transfer: An Architectural Style for Distribution Hypermedia Interaction](https://ics.uci.edu/~fielding/talks/webarch_9805/index.htm)
<br> *표현적인 상태 전송: 분산 하이퍼미디어 시스템(ex. web)을 위한 아키텍처 스타일*

&nbsp;이게 지금 그거는 아니고, 대학원생이었던 Roy 씨는 야무지게 정리해서 2년 후인<br>
2000년, 지금의 `REST`라고 정의하는 논문을 발표합니다.
> [Architectural Styles and the Design of Network-based Software Architectures](https://ics.uci.edu/~fielding/pubs/dissertation/top.htm)
, Roy T. Fielding

영어 잘하게 되면 이 논문을 읽어보겠습니다.

### REST🌏
❗`HTTP`❗로 통신할 때, `상호운용성`을 제공하기 위해 나온 ❗아키텍처 스타일❗

<br><br>
## 👉Application Programming Interface?👈
&nbsp;고유한 기능을 가진 소프트웨어에서 구성 요소가 상호 간에 통신할 수 있도록 하는 메커니즘이라고 합니다.
<br> 정의는 언제나 어려운 것 같아요. 코딩애플에서는 메뉴판이라고 비유하는 데 직관적으로 이해됐어요.

### 등장🧩
2000년, Salesforce API가 거의 최초로 공개된 API라고 합니다.
바로 요 녀석이 SOAP API입니다.
```xml
<?xml version="1.0" encoding="utf-8" ?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:urn="urn:enterprise.soap.sforce.com">
    <soapenv:Header>
        <urn:SessionHeader>
            <urn:sessionId><b>QwWsHJyTPW.1pd0_jXLNKOSU</b></urn:sessionId>
        </urn:SessionHeader>
    </soapenv:Header>
    <soapenv:Body>
        <urn:retrieve>
            <urn:fieldList><b>Id, Name, Website</b></urn:fieldList>
            <urn:sObjectType><b>Account</b></urn:sObjectType>
            <!-- Zero or more repetitions:-->
            <urn:ids><b>001D000000HS2Su</b></urn:ids>
            <urn:ids><b>001D000000HRzKD</b></urn:ids>
        </urn:retrieve>
    </soapenv:Body>
</soapenv:Envelope>
<!-- ID로 Object 하나를 가져오는 API 요청 메시지인데 잠 깰 겸 쳐봤지만 끔찍하군요-->
```

### 4개 밖에 있음🧩

&nbsp; 저는 개인적으로 REST API부터 접했기에 API랑 REST API를 분리하는 게 어려웠어요^^> <br>
그래서 API의 종류를 간단하게 찾아봤습니다.

1. SOAP API - `STMP`로도 요청 가능.
2. RPC API
3. Websocket API - `TCP` 냅다 연결
4. REST API - `HTTP`를 효율적으로 쓰기위해서 고안한 아키텍쳐 스타일임.


`SOAP`: Microsoft가 개발한 XML-RPC(1998) 프로토콜에 부가적인 기능을 추가한 `프르토콜`, ~~XML-RPC가 더 많이 사용된다고 합니다.~~ <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;그렇지만 보안이 깨나 엄격하고, ACID를 준수해서 기업용 애플리케이션에 쓰일 수 있다고 합니다. <br>
`RPC`: remote procedure call, 원격으로 다른 시스템의 메서드를 호출할 수 있는 `프로토콜`, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;REST는 자원이나 객체에 초점을 맞추는 반면, 이 친구는 기능이나 작업에 초점을 맞춘다고 합니다.<br>

### API🌏
프로그램의 메뉴판!!
<br>

# 🤜REST API🤛

## 등장🧩

2004년, flickr에서 여러가지 형태의 API가 나왔습니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<s:Envelope xmlns:s="http://www.w3.org/2001/06/soap-envelope">
  <s:Body>
    <s:Fault>
      <faultcode>flickr.error.[error-code]</faultcode>
      <faultstring>[error-message]</faultstring>
      <faultactor>http://www.flickr.com/services/soap/</faultactor>
      <details>Plese see http://www.flickr.com/services/docs for more details</details>
    </s:Fault>
  </s:Body>
</s:Envelope>
```
&nbsp; SOAP API( ↑ ), REST API( **↓** )

```xml
<?xml version="1.0" encoding="utf-8" ?>
<rsp stat="fail">
  <err code="[error-code]" msg="[error-message]" />
</rsp>
```

&nbsp;하지만 변태가 아니라면 REST를 쓰고 싶잖아요.<br>
그렇다면 REST API, 그러니까 REST라는 아키텍처 스타일을 만족하려면 어떻게 해야 할지 알아볼게요.

## Rest 아키텍처 스타일 제약 조건🧩
&nbsp; 완벽할 수 없다는 것은 알지만 이왕 공부하는 거 완벽하게 하고 싶어요...<br>
[Joy씨의 논문](https://ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#sec_5_1) CHAPTER 5.1에 해당하는 부분을 "제멋대로" 해석해 보겠습니다.
이 Chapter에서는 REST가 아키텍처 스타일로서 파생되는 과정을 따라가며 개요를 제공해줍니다.

### 0. Null
&nbsp;an empty set of constraint! 처음은 당연히 어떤 제약조건도 없습니다.<br>
![@Schema](../../images/2024-01-30-http-restapi/0.PNG)<br>
&nbsp;다만 아키텍처를 설계할 때, 제약없이 요구 사항만으로 시작해서 시스템과 전체적인 조화를 이루도록 제약 조건을 적용했다고 합니다.
이렇게 하면 시스템의 맥락에 대한 제약과 이해를 더 강조한다고 하네요. 마냥 구성 요소를 추가하는 것 보다는 당연히 제약이 강조되고, 그러다 보면 맥락이 이해가 되지 않을까요?<br>
<br>
**저는 바보라서 그냥 Null에서 시작한다고 알고 넘어가겠습니다.**


### 1. client-server
&nbsp; 첫 번째로 추가된 이 녀석의 기본 원칙은 **관심사의 분리(Soc)** 입니다. <br>
'사용자 인터페이스'와 '데이터의 저장' 두 관심사를 분리해서 확장성을 향상할 수 있어요.
**분리**가 각 구성 요소를 독립적으로 진화할 수 있게 한다는 것이죠.
그러면 인터넷 규모의 여러 도메인들의 요구사항을 지원할 수 있습니다.
![@Schema](../../images/2024-01-30-http-restapi/1.PNG)<br>
&nbsp; client는 trigger, server는 trigger에 따라 반응하는 process라고 Andrews 씨가 말했대요.
생각해보면 client는 필요할 때만 방아쇠를 당기겠지만 server는 연신 돌아가고 있어야 하죠.




### 2. stateless
### 3. cache
### 4. layered system
### 5. code-on-demand(optional)
- 서버에서 코드를 클라이언트에게 보내 실행시킬 수 있어야 한다.(=자바스크립트)

### 6. uniform interface
1. identification of resources<br>
   *자원을 URI로 식별할 수 있다.*
2. manipulation of resources through representations<br>
   *representation 전송을 통해 자원 조작할 수 있다.(HTTP method에 표현을 담아 보낸다.)*
3. self-descriptive messages
   - 메시지는 스스로를 설명해야 한다.
   - ex. Host, Content-Type, 각 json에 대한 명세
4. hypermedia as the engine of application state(HATEOAS)
   - 애플리케이션의 상태는 Hyperlink를 이용해 전이되어야 한다.
   - JSON의 경우 Link Header를 통해 구현 가능



### Why
1. 독립적 진화
   1. 서버와 클라이언트가 각각 독립적으로 진화한다.
   2. 서버의 기능이 변경되어도 클라이언트를 업데이트할 필요가 없다.
   3. REST를 만들게 된 계기: "How do I improve HTTP without breaking the Web"

- WEB
  - 웹 페이지를 변경해도 웹 브라우저를 업데이트할 필요가 없다.
  - 웹 브라우저를 업데이트 했다고 웹 페이지를 변경할 필요도 없다.
  - HTTP 명세가 변경되어도 웹은 잘 동작한다.
  - HTML 명세가 변경되어도 웹은 잘 동작한다.
- Mobile
  - 강제 업데이트

### interoperability에 대한 집착
- referer 오타지만 고치지 않음
- charset 잘못 지은 이름이지만 고치지 않음
- HTTP 상태 코드 418 포기함(i'm a teapot)
- HTTP/0.9 아직도 지원함(크롬, 파이어폭스)


# 마무리
일단 너무 졸려서 자구 일어나서 수정하겠읍니다.


🌟
---

**[참고]**  
이응준, ['그런 REST API로 괜찮은가'](https://www.youtube.com/watch?v=RP_f5dMoHFc)<br>
aws, ['API란 무엇인가요?'](https://aws.amazon.com/ko/what-is/api/)<br>
코딩애플, ['코딩초보들이 헷갈리는 용어 : API가 뭐냐면'](https://www.youtube.com/watch?v=ckSdPNKM2pY&t=106s)<br>
aws, ['RESTful API란 무엇인가요?'](https://aws.amazon.com/ko/what-is/restful-api/)