# HTTP 메서드

### <mark style="background-color:blue;">HTTP 메서드 종류</mark>

* GET: 리소스 조회
* POST: 요청 데이터 처리, 주로 등록에 사용
* PUT: 리소스를 대체, 해당 리소스가 없으면 생성
* PATCH: 리소스 부분 변경
* DELETE: 리소스 삭제



#### <mark style="background-color:orange;">GET</mark>

* 리소스 조회
* 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달
* 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음

![](<../.gitbook/assets/image (8).png>)

![](<../.gitbook/assets/image (10).png>)

![](<../.gitbook/assets/image (30).png>)



#### <mark style="background-color:orange;">POST</mark>

* 요청 데이터 처리&#x20;
* 메시지 바디를 통해 서버로 요청 데이터 전달&#x20;
* 서버는 요청 데이터를 처리&#x20;
  * 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.&#x20;
* 주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용

![](<../.gitbook/assets/image (36).png>)

![](<../.gitbook/assets/image (9).png>)

![](<../.gitbook/assets/image (1).png>)



#### <mark style="background-color:orange;">PUT</mark>

* 리소스를 대체&#x20;
  * 리소스가 있으면 대체
  * 리소스가 없으면 생성
  * 쉽게 이야기해서 덮어버림
* 중요! 클라이언트가 리소스를 식별
  * 클라이언트가 리소스 위치를 알고 URI 지정
  * POST와 차이점

![](<../.gitbook/assets/image (12) (1).png>)

![](<../.gitbook/assets/image (22).png>)

![](<../.gitbook/assets/image (11).png>)

![](<../.gitbook/assets/image (15).png>)

![](<../.gitbook/assets/image (2).png>)

![](<../.gitbook/assets/image (16).png>)



#### <mark style="background-color:orange;">PATCH</mark>&#x20;

* 리소스 부분 변경

![](<../.gitbook/assets/image (29).png>)

![](<../.gitbook/assets/image (23).png>)



#### <mark style="background-color:orange;">DELETE</mark>

* 리소스 제거

![](<../.gitbook/assets/image (4).png>)

![](<../.gitbook/assets/image (13).png>)



### <mark style="background-color:blue;">HTTP 메서드의 속성</mark>

* 안전(Safe Methods)
* 멱등(Idempotent Methods)
* 캐시가능(Cacheable Methods)



#### <mark style="background-color:orange;">안전(Safe Methods)</mark>

* 호출해도 리소스를 변경하지 않음
* Q: 그래도 계속 호출해서, 로그 같은게 쌓여서 장애가 발생하면요?&#x20;
* A: 안전은 해당 리소스만 고려한다. 그런 부분까지 고려하지 않는다.

#### <mark style="background-color:orange;">멱등(Idempotent Methods)</mark>

* f(f(x)) = f(x)
* 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같음
*   멱등 메서드

    * **GET**: 한 번 조회하든, 두 번 조회하든 같은 결과가 조회
    * **PUT**: 결과를 대체. 따라서 같은 요청을 여러번 해도 최종 결과는 같음
    * **DELETE**: 결과를 삭제. 같은 요청을 여러번 해도 삭제된 결과는 같음
    * <mark style="color:red;">**POST**</mark>: 멱등이 아님! 두 번 호출하면 같은 결제가 중복해서 발생할 수 있음


* 활용&#x20;
  * 자동 복구 메커니즘

#### <mark style="background-color:orange;">캐시가능(Cacheable Methods)</mark>

* 응답 결과 리소스를 캐시해서 사용해도 되는가?
* GET, HEAD, POST, PATCH 캐시가능
* 실제로는 GET, HEAD 정도만 캐시로 사용
  * POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데, 구현이 쉽지 않음
