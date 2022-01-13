# URI와 웹 브라우저 요청 흐름

### <mark style="background-color:blue;">URI(Uniform Resource Identifier)</mark>

* Uniform: 리소스 식별하는 통일된 방식&#x20;
* Resource: 자원, URI로 식별할 수 있는 모든 것(제한 없음)
*   Identifier: 다른 항목과 구분하는데 필요한 정보


* URI는 로케이터(locator), 이름(name) 또는 둘 다 추가로 분류될 수 있음
  * 리소스 식
  * URL과 URN을 포괄 &#x20;

![](<../.gitbook/assets/image (29) (1).png>)

![](<../.gitbook/assets/image (35).png>)

### <mark style="background-color:blue;">URL과 URN</mark>

* URL
  * Uniform Resource Locator
  * Locator : 리소스가 있는 위치를 지정  &#x20;
*   URN

    * Uniform Resource Name
    * Name : 리소스에 이름을 부여&#x20;


* 위치는 변할 수 있지만, 이름은 변하지 않음
* URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음&#x20;



### <mark style="background-color:blue;">URL 전체 문법</mark>

* https://www.google.com:443/search?q=hello\&hl=ko -> URL 분석&#x20;

&#x20;

![](<../.gitbook/assets/image (3).png>)

![](<../.gitbook/assets/image (25).png>)

![](<../.gitbook/assets/image (6).png>)

![](<../.gitbook/assets/image (23) (1).png>)

![](<../.gitbook/assets/image (33).png>)

![](<../.gitbook/assets/image (1) (1).png>)

![](<../.gitbook/assets/image (2) (1).png>)

![](<../.gitbook/assets/image (17) (1).png>)



### <mark style="background-color:blue;">웹 브라우저 요청 흐름</mark>

![](<../.gitbook/assets/image (21).png>)

![](<../.gitbook/assets/image (5) (1).png>)

![](<../.gitbook/assets/image (32).png>)

![](<../.gitbook/assets/image (31).png>)

![](<../.gitbook/assets/image (28).png>)

![](<../.gitbook/assets/image (4) (1).png>)

![](<../.gitbook/assets/image (36) (1).png>)

![](<../.gitbook/assets/image (19) (1).png>)

1. DNS 조회를 통해 IP와 PORT 번호를 알아냄
2. HTTP 요청 메시지 생성(HTTP 메소드 + path + query string + HTTP 버전 정보 + HOST 정보)
3. SOCKET 라이브러리를 통해 전달(TCP/IP 연결 + 데이터 전달)
4. TCP/IP 패킷 생성(출발지IP,PORT + 목적지 IP,PORT), HTTP 메시지 포함
5. 요청 패킷 전달 -> 서버에 요청 패킷 도착 &#x20;
6. 서버에서  HTTP 응답 메시지 생성(Content-Type 및 Content-Length 등 생성)
7. 응답 패킷 전달 -> 웹 브라우저에 응답 패킷 도착   &#x20;
8. 웹 브라우저는 응답받은 패킷을 HTML 렌더링    &#x20;
