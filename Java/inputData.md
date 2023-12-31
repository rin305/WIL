# Scanner, BufferedReader

> 데이터를 입력받을 때 둘 중 어떤 클래스를 이용해야 할까?

##  Scanner
```java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);

int n = sc.nextInt();
String s = sc.next();
String str = sc.nextLine(); //띄어쓰기가 포함된 문자열을 입력받는 경우
```
 - 비교적 적은 양의 데이터를 입력 받을 때
 - 입력받은 값을 가공할 필요 없이 바로 정의하여 사용 가능

 ## BufferedReader
 ```java
 import java.io.BufferedReader;
 import java.io.IOException;
 import java.io.InputStreamReader;

 BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
 StringTokenizer stringtokenizer = new StringTokenizer(br.readLine());

 int n = Integer.parseInt(st.nextToken());
 String s = st.nextToken();
 ```

- 비교적 많은 양의 데이터를 입력 받을 때
<br> (Scanner보다 속도가 훨씬 빠름)
- 입력받은 값을 따로 가공해야 함
<br><br>

### BufferedReader 사용 시 함께 사용되는 클래스

1. InputStreamReader
   - 데이터를 문자(char) 단위로 처리할 수 있다.
   <br> (단순 InputStream의 경우 1byte만 인식하기 때문에 문자를 온전하게 읽어들일 수 없음)

 2. StringTokenizer
     - 문자열을 띄어쓰기를 기준으로 토큰(token) 단위로 끊어줌
     - 입력받은 값이 다음 줄로 넘어갈 경우   
    `stringtokenizer = new StringTokenizer(br.readLine())`
     <br>
    위와 같이 객체를 재선언한 후 다시 데이터를 받아준다.