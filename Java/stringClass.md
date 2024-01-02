# String, StringBuffer와 StringBuilder
> String과 StringBuffer, StringBuilder의 차이점이 뭘까?

## String vs StringBuffer, StringBuilder
- String: 생성 후 서로 연결, 수정 시 새로운 String 객체를 생성하며 불변(immutable)적이다.<br>
- StringBuffer, StringBuilder: 계속해서 수정이 가능하기 때문에 전자에 비해 메모리를 덜 소모함.

## StringBuffer vs StringBuilder
- StringBuffer: 멀티스레드 환경에서도 동기화를 지원<br>
- StringBuilder: 멀티스레드 환경에서는 동기화를 보장하지 않으므로 단일스레드 환경에서 사용하기 적합하다.
<br><br>

#### StringBuffer 객체의 char변수 포함여부를 알고 싶을 때?
```java
StringBuffer sb = new StringBuffer("abcde");
sb.indexOf("a");
```
기본적으로 indexOf 메서드를 이용하지만 이 때 indexOf 메서드에는 String값이 들어가야함 <br>
만약, 찾는 문자가 다른 String 객체 내의 값이라면? (charAt 메서드를 쓴 경우)   
```java
String str = "cake";
//sb.indexOf(str.charAt(0)); char값이 들어가므로 오류발생
sb.indexOf(String.valueOf(str.char(0)));
```
위와 같이  `String.valueOf` 메서드로 한번 더 값을 포장하여 집어넣어야 한다.