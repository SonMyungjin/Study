# HTTP 기본

### <mark style="background-color:blue;">모든 것이 HTTP</mark>

* HTML, TEXT&#x20;
* IMAGE, 음성, 영상, 파일
* JSON, XML (API)
* 거의 모든 형태의 데이터 전송 가능
* 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용



### <mark style="background-color:blue;">HTTP 역사</mark>

* HTTP/0.9 1991년: GET 메서드만 지원, HTTP 헤더X
* HTTP/1.0 1996년: 메서드, 헤더 추가
* **HTTP/1.1 1997년: 가장 많이 사용, 우리에게 가장 중요한 버전**
  * RFC2068 (1997) -> RFC2616 (1999) -> RFC7230\~7235 (2014)
* HTTP/2 2015년: 성능 개선
* HTTP/3 진행중: TCP 대신에 UDP 사용, 성능 개선



### <mark style="background-color:blue;">HTTP 특징</mark>

* 클라이언트 서버 구조
* 무상태 프로토콜(스테이스리스), 비연결성
* HTTP 메시지를 통해 클라이언트와 서버가 통신&#x20;
* 단순함, 확장 가능



#### <mark style="background-color:orange;">클라이언트 서버 구조</mark>

* Request Response 구조
* 클라이언트는 서버에 요청을 보내고, 응답을 대기
* 서버가 요청에 대한 결과를 만들어서 응답



#### <mark style="background-color:orange;">무상태 프로토콜</mark> -> <mark style="color:red;">스테이스리스(Stateless)</mark>

* 서버가 클라이언트의 상태를 보존X
* 무상태는 응답 서버를 쉽게 바꿀 수 있 -> 무한한 서버 증설 가능
* 장점: 서버 확장성 높음(스케일 아웃)
*   단점: 클라이언트가 추가 데이터 전송


* Stateful, Stateless 차이
  * Stateful : 중간에 서버가 터지면 새로운 요청을 받아야  함&#x20;
  * Stateless : 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있 &#x20;

![](<../.gitbook/assets/image (16).png>)

![](<../.gitbook/assets/image (9).png>)

![](<../.gitbook/assets/image (12).png>)

![](<../.gitbook/assets/image (14).png>)

![](<../.gitbook/assets/image (11).png>)

* Stateless 실무 한계
  * 모든 것을 무상태로 설계 할 수 있는 경우도 있고 없는 경우도 있음
    * 무상태 ex) 로그인이 필요 없는 단순한 서비스 소개 화면
    * 상태 유지 ex) 로그인
  * 로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지
  * 일반적으로 브라우저 쿠키와 서버 세션등을 사용해서 상태 유지
  * 상태 유지는 최소한만 사용
  * Stateful에 비해 데이터를 너무 많이 보냄  &#x20;



### <mark style="background-color:blue;">비 연결성(connectionless)</mark>

* HTTP는 기본이 연결을 유지하지 않는 모델
* 일반적으로 초 단위의 이하의 빠른 속도로 응답
* 1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시 처리하는 요청은 수십개 이하로 매우 작음
  * ex) 웹 브라우저에서 계속 연속해서 검색 버튼을 누르지는 않
* 서버 자원을 매우 효율적으로 사용할 수 있음



#### <mark style="background-color:orange;">비 연결성 한계와 극복</mark>

* TCP/IP 연결을 새로 맺어야 함 - 3 way handshake 시간 추가
* 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, css, 추가 이미지 등 등 수 많은 자원이 함께 다운로드
* 지금은 HTTP 지속 연결(Persistent Connections)로 문제 해결
* HTTP/2, HTTP/3에서 더 많은 최적화



![](<../.gitbook/assets/image (15).png>)

![](<../.gitbook/assets/image (13).png>)



### <mark style="background-color:blue;">HTTP 메시지</mark>

![](<../.gitbook/assets/image (22).png>)
