# Wrapper Class

### &#x20;래퍼 클래스란(Wrapper Class)?  <a href="#h" id="h"></a>

* 기본 자료타입(primitive type)을 객체로 다루기 위해서 사용하는 클래스
* 자바 -> 모든 기본타입(primitive type)은 값을 갖는 객체를 생성할 수 있음
  * 이런 객체를 포장 객체라 함
  * &#x20;그 이유는 기본 타입의 값을 내부에 두고 포장하기 때문
* 래퍼 클래스로 감싸고 있는 기본 타입 값은 외부에서 변경할 수 없음&#x20;
  * 만약 값을 변경하고 싶다면 새로운 포장 객체를 만들어야 함



### 래퍼 클래스의 종류 <a href="#h_1" id="h_1"></a>

\


![](<../../.gitbook/assets/image (19).png>)

### &#x20; <a href="#h_3" id="h_3"></a>

### 박싱(Boxing)과 언박싱(UnBoxing)  <a href="#h_3" id="h_3"></a>

![](<../../.gitbook/assets/image (37).png>)

* 박싱(Boxing)
  * 기본 타입의 값을 포장 객체로 만드는 과정
* 언박싱(UnBoxing)
  * 포장객체에서 기본타입의 값을 얻어내는 과정



### 자동 박싱(AutoBoxing)과 자동 언박싱(AutoUnBoxing) <a href="#h_4" id="h_4"></a>

* 기본타입 값을 직접 박싱, 언박싱하지 않아도 자동적으로 박싱과 언박싱이 일어나는 경우가 있음
* 자동 박싱의 포장 클래스 타입에 기본값이 대입될 경우에 발생
  * int타입의 값을 Integer클래스 변수에 대입하면 자동 박싱이 일어나 힙 영역에 Integer객체가 생성



### 예제&#x20;



```
    public class Wrapper_Ex { public static void main(String[] args) { 
    String str = "10"; 
    String str2 = "10.5"; 
    String str3 = "true";
    
    byte b = Byte.parseByte(str);
    int i = Integer.parseInt(str);
    short s = Short.parseShort(str);
    long l = Long.parseLong(str);
    float f = Float.parseFloat(str2);
    double d = Double.parseDouble(str2);
    boolean bool = Boolean.parseBoolean(str3);
	
    System.out.println("문자열 byte값 변환 : "+b); // 10
    System.out.println("문자열 int값 변환 : "+i); // 10
    System.out.println("문자열 short값 변환 : "+s); // 10
    System.out.println("문자열 long값 변환 : "+l); // 10
    System.out.println("문자열 float값 변환 : "+f); // 10.5
    System.out.println("문자열 double값 변환 : "+d); // 10.5
    System.out.println("문자열 boolean값 변환 : "+bool); // true
    }
}
```

* 래퍼 클래스의 주요 용도는 기본 타입의 값을 박싱 해서 포장 객체로 만드는 것이지만,&#x20;
* 문자열을 기본 타입 값으로 변환할 때에도 사용
* 대부분의 래퍼 클래스에는 parse + 기본 타입명으로 되어있는 정적 메서드가 있음
* 이 메서드는 문자열을 매개 값으로 받아 기본 타입 값으로 변환\
