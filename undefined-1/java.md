# JAVA

### JVM이란?

* JVM 역할은 자바 애플리케이션을 클래스 로더를 통해 읽어 들여 자바 API와 함께 실행하는 것
* JVM과 OS사이에서 **중계자 역할**을 수행하여 JAVA가 OS에 구애받지 않고 재사용을 가능하게 해줌
* 메모리관리, Garbage collection을 수&#x20;
* 스택기반의 가상머신



### JAVA 프로그램 실행과정

1.  프로그램이 실행되면 JVM은 OS로부터 이 프로그램이 필요로 하는 메모리를 할당받는다.

    JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다.
2. 자바 컴파일러(javac)가 자바 소스코드(.java)를 읽어들여 자바 바이트코드(.class)로 변환시킨다.
3. Class Loader를 통해 class파일들을 JVM으로 로딩한다.
4. 로딩된 class파일들은 Execution engine을 통해 해석된다.
5.  해석된 바이트코드는 Runtime Data Areas 에 배치되어 실질적인 수행이 이루어지게 된다.

    이러한 실행과정 속에서 JVM은 필요에 따라 Thread Synchronization과 GC같은 관리작업을 수행

