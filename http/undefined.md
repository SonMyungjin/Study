# 인터넷 네트워크

### <mark style="background-color:blue;">IP 인터넷 프로토콜 역할</mark>

* 지정한 IP 주소(IP Address)에 데이터 전달
* 패킷(Packet)이라는 통신 단위로 데이터 전달



#### IP 패킷 정보

![](<../.gitbook/assets/image (2).png>)

* 출발지IP : 나의 IP 정보
* 목적지IP : 목적지 IP 정보    &#x20;



#### 클라이언트 패킷 전달

![](<../.gitbook/assets/image (14).png>)



#### 서버 패킷 전달

![](<../.gitbook/assets/image (15).png>)



### <mark style="background-color:blue;">IP 프로토콜의 한계</mark>

*   비연결성

    * 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송&#x20;


*   비신뢰성

    * 중간에 패킷이 사라지면? 해결x
    * 패킷이 순서대로 안오면? 해결x


* 프로그램 구분&#x20;
  * 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면?



### <mark style="background-color:blue;">TCP/UDP</mark>

* TCP
  * IP 프로토콜의 한계였던 비연결성, 비신뢰성 해결&#x20;
  * IP 패킷 + TCP 세그먼트로  해&#x20;

#### TCP/IP 패킷 정보

&#x20;

![](<../.gitbook/assets/image (12).png>)

#### TCP 특징

* 전송 제어 프로토콜(Transmission Control Protocol)
* 연결지향 - TCP 3 way handshake (가상 연결)
* 데이터 전달 보증
* 순서 보장
* 신뢰할 수 있는 프로토콜 -> 현재는 대부분 TCP 사용



#### TCP 3 way handshake

![](<../.gitbook/assets/image (7).png>)



#### 데이터 전달 보증

![](<../.gitbook/assets/image (6).png>)



#### 순서 보장

![](<../.gitbook/assets/image (13).png>)
