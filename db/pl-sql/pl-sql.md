# PL/SQL이란?

### <mark style="background-color:blue;">PL/SQL 이란?</mark>

* Procedurral Language SQL 약자로 오라클에 내장되어 있는 <mark style="color:blue;">**절차적 언어**</mark>
* SQL만으로 처리 할 수 없는 복잡한 업무 프로그램을 작성할 수 있도록 다양한 프로그래밍 기능을 제공
* SQL문장에서 <mark style="color:blue;">**변수정의, 조건처리(IF), 반복처리(LOOP, WHILE, FOR)**</mark>등을 지원
* DECLARE문을 이용하여 정의되며, 선언문의 사용은 선택 사항
* PL/SQL 문은 블록 구조로 되어 있고 PL/SQL자신이 컴파일 엔진을 가지고 있음&#x20;



### <mark style="background-color:blue;">PL/SQL 장점</mark>

* PL/SQL 문은 BLOCK 구조로 다수의 SQL 문을 한번에 ORACLE DB로 보내서 처리하므로 수행속도를 향상 시킬 수 있음
* PL/SQL 의 모든 요소는 하나 또는 두 개 이상의 블록으로 구성하여 모듈화가 가능
* 보다 강력한 프로그램을 작성하기 위해서 큰 블록안에 소블럭을 위치시킬 수 있음
* VARIABLE, CONSTANT, CURSOR, EXCEPTION을 정의하고, SQL문장과 Procedural 문장에서 사용
* 단순, 복잡한 데이터 형태의 변수를 선언함&#x20;
* 테이블의 데이터 구조와 컬럼명에 준하여 동적으로 변수를 선언 할 수 있음&#x20;
* EXCEPTION 처리 루틴을 이용하여 Oracle Server Error를 처리
* 사용자 정의 에러를 선언하고 EXCEPTION 처리 루틴으로 처리 가능
