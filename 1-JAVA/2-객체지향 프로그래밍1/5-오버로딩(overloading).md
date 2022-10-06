## 1. 오버로딩이란? 
- 하나의 메서드 이름으로 여러 기능을 담음
- 클래스 내에 같은 이름의 메서드 여러개 선언하는 것

## 2. 오버로딩의 조건 
- 메서드명 동일
- 매개 변수의 타입, 개수, 순서가 달라야함

## 3. 오버로딩의 예
```java
int plus(int x, int y) { return x + y; }
double plus(double x, double y) { return result; }

plus(1, 2);     // 매개값이 정수이므로 처음 메서드 실행
plus(1.1, 2.2); // 매개값이 실수이므로 두번째 메서드 실행

int x = 1;
int y = 2.2;
plus(x, y);
/*
JVM이 매개 변수 타입이 일치하지 않는 경우 자동 타입 변환 가능 여부를 판단
int는 double로 타입 변환이 가능하여 plus(double x, double y) 메서드 선택
*/

```
- 잘못된 예시
```java
int divide(int x, int y) { ... }
double divide(int boonja, int boonmo) { ... }
/*
리턴 타입만 다르고 매개 변수가 동일하면 오버로딩 아님
리턴 타입은 JVM이 메소드 선택 시 도움을 주지 못하여 컴파일 에러 발생
*/
```
- 대표적인 예
```java
void println() { ... }
void println(int x) { ... }
void println(boolean x) { ... }
void println(String x) { ... }
...
/*
메서드 이름은 println으로 같지만, 매개변수가 전부 다름
*/
```

## 4. 오버로딩의 장점 
- 하나의 이름으로 사용하기 때문에 같은 기능이라고 예측 가능
- 메서드 이름 절약

## 5. 가변인자(varargs)와 오버로딩 
- 가변인자 : 여러 문자열을 하나로 결합하여 반환하는 메서드
```java
String concatenate(String s1, String s2) { ... }
String concatenate(String s1, String s2, String s3) { ... }
String concatenate(String s1, String s2, String s3, String s4) { ... }


String concatenate(String...str) {...} //가변인자를 사용해서 간단히 대체
/*
타입... 변수명과 같은 형식으로 사용
*/

System.out.println(concatenate());                        // 인자가 없는 것도 가능
System.out.println(concatenate("a"));                     // 인자가 하나 인것도 가능
System.out.println(concatenate("a", "b"));                // 인자가 둘 인것도 가능
System.out.println(concatenate(new String[] {"A", "B"})); // 배열도 가능```
```
- 가변인자를 선언한 메서드를 오버로딩하면 메서드 구분이 안되어 'ambiguous' 에러 발생
- 가변인자를 사용한 메서드는 오버로딩 하지 않는 것이 바람직
```java
String concatenate(String delim, String... args) { 
	...
}
// static String concatenate(String... args) { 
//     ...
// }
/*
주석 해제 후 컴파일 시 에러 발생
*/
```
