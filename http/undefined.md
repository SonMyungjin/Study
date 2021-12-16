# 인터넷 네트워크

### <mark style="background-color:blue;">IP 인터넷 프로토콜 역할</mark>

* 지정한 IP 주소(IP Address)에 데이터 전달
* 패킷(Packet)이라는 통신 단위로 데이터 전달



#### <mark style="background-color:orange;">IP 패킷 정보</mark>

![](<../.gitbook/assets/image (2).png>)

* 출발지IP : 나의 IP 정보
* 목적지IP : 목적지 IP 정보    &#x20;



#### <mark style="background-color:orange;">클라이언트 패킷 전달</mark>

![](<../.gitbook/assets/image (14) (1).png>)



#### <mark style="background-color:orange;">서버 패킷 전달</mark>

![](<../.gitbook/assets/image (15).png>)



### <mark style="background-color:blue;">IP 프로토콜의 한계</mark>

*   비연결성

    * 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송&#x20;


*   비신뢰성

    * 중간에 패킷이 사라지면? 해결x
    * 패킷이 순서대로 안오면? 해결x


* 프로그램 구분&#x20;
  * 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면?



### <mark style="background-color:blue;">TCP</mark>

* IP 프로토콜의 한계였던 비연결성, 비신뢰성 해결&#x20;
* IP 패킷 + TCP 세그먼트로  해결

#### <mark style="background-color:orange;">TCP/IP 패킷 정보</mark>

&#x20;

![](<../.gitbook/assets/image (12).png>)

#### <mark style="background-color:orange;">TCP 특징</mark>

* 전송 제어 프로토콜(Transmission Control Protocol)
* 연결지향 - TCP 3 way handshake (가상 연결)
* 데이터 전달 보증
* 순서 보장
* 신뢰할 수 있는 프로토콜 -> 현재는 대부분 TCP 사용



#### <mark style="background-color:orange;">TCP 3 way handshake</mark>

![](<../.gitbook/assets/image (7).png>)



#### <mark style="background-color:orange;">데이터 전달 보증</mark>

![](<../.gitbook/assets/image (6).png>)



#### <mark style="background-color:orange;">순서 보장</mark>

![](<../.gitbook/assets/image (13).png>)





### <mark style="background-color:blue;">UDP</mark>

#### <mark style="background-color:orange;">UDP 특징</mark>

* 사용자 데이터그램 프로토콜(User Datagram Protocol)&#x20;
* 하얀 도화지에 비유(기능이 거의 없음)&#x20;
* 연결지향 - TCP 3 way handshake X&#x20;
* 데이터 전달 보증 X  순서 보장 X&#x20;
*   데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름&#x20;


* &#x20;정리&#x20;
  * IP와 거의 같다. <mark style="color:blue;">+</mark><mark style="color:blue;">**PORT**</mark> <mark style="color:blue;"></mark><mark style="color:blue;">+</mark><mark style="color:blue;">**체크섬**</mark> 정도만 추가&#x20;
  * 애플리케이션에서 추가 작업 필요





### <mark style="background-color:blue;">PORT</mark>

* IP는 목적지 서버를 찾는 것  ex)아파트
* PORT는 서버에서 돌아가는 애플리케이션을 구분하는  것  ex)101동 105호&#x20;
* 같은 IP 내에서 프로세스 구분 &#x20;

![](<../.gitbook/assets/image (14).png>)



### <mark style="background-color:blue;">DNS</mark>

* 도메인 네임 시스템(Domain Name System)&#x20;
  * 전화번호부
  * 도메인 명을 IP 주소로 변환

![](<../.gitbook/assets/image (10).png>)

