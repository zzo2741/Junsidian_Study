## 1. 인터페이스란?
- 추상 메서드와 상수로만 이루어짐
- 인스턴스를 생성할 수 없음
- 인터페이스 모든 멤버는 public
- 메서드에 public abstract, 변수에 public static final을 쓰지 않아도 자동으로 변환

### 1.1 추상클래스와 차이
- 추상클래스 : 일반 메서드 + 추상 메서드
- 인터페이스 : 추상 메서드만

## 2. 인터페이스의 작성  
```java
interface Calc {
	public static final double PI = 3.14; // 상수
	int ERRORCODE = -9999999; //  public static final 쓰지 않아도 자동으로 변환

	public abstract int add(...); // 추상 메서드
	int substract(...); //  public abstract 쓰지 않아도 자동으로 변환
	int divide(...);
}
```

## 3. 인터페이스의 상속 
- 인터페이스 조상은 인터페이스만 가능
- 인터페이스는 인스턴스 변수를 가질 수 없음

## 4. 인터페이스의 구현
```java
class Calculator implements Calc {
	@Override
	public int add(...) { ... }
	@Override
	public int substract(...) { ... }
	@Override
	public int divide(...) { ... }
} 
/*
인터페이스에 정의된 추상 메서드를 모두 구현해야 함
만약 추상 메서드를 모두 구현하지 않으면 abstract 즉 추상 클래스임
*/
```

## 5. 인터페이스를 이용한 다중상속
- 다중상속은 메서드 충돌 문제가 있지만, 추상 메서드는 충돌할게 없음
- 선언부가 똑같아도 구현부가 없기 때문에 다중 상속 가능
```java
interface X {}
interface Y {}

interface MyInterface extends X, Y {}
```

## 6. 인터페이스를 이용한 다형성
- 다형성 : 상위 타입 참조변수로 하위 타입 객체를 가리키는 것
- 클래스의 다형성과 동일하게 인터페이스도 다형성 성립
```java
class Junseung extends Human implements readable {}

Human h = new Junseung(); // 하위 클래스를 상위 타입의 참조변수로 가리키는 것이 가능
readable r = new Junseung(); // 인터페이스타입 참조변수로 하위 클래스를 가리키는 것이 가능
```
- 인터페이스 타입 매개변수는 인터페이스로 구현한 클래스 객체만 가능
```java
interface readable { 
	void read(readable r);
}

readable r = new Junseung();
r.read(new Junseung());
```
- 인터페이스를 메서드 리턴타입으로 지정 가능
	- 인터페이스를 구현한 클래스 객체만 가능
```java
readable method() {
	return new Junseung();
}
```

## 7. 인터페이스의 장점
- 두 대상 간의 중간역할
	- 기계의 껍데기, ex) 컴퓨터 사용하던 사람이 노트북을 사용해도 익숙함
	- 의존성을 줄이고 인터페이스를 통하면 유연함을 가짐
- 설계와 구현을 분리
	- 인터페이스를 사용하여 변경에 유리
- 느슨한 결합으로 변경에 유리
	- A가 B를 의존하면 B가 C로 바뀌면 수정요소가 많음
	- 인터페이스를 사용하면 B가 C로 바뀌어도 A는 수정할게 많이 없음
- 개발 시간을 단축
	- A가 B를 의존할 때는 B완성을 기다려야 함
	- 인터페이스를 사용하면 B가 개발되지 않아도 껍데기만 있으면 됌
- 표준화가 가능
	- 느슨한 결합과 비슷
	- ex) JDBC, 오라클을 쓰다가 MySql로 바꿀 경우 연결부분만 바꾸면 됌
- 서로 관계 없는 클래스들 끼리 관계를 맺어줌
	- 지상 동물에 강아지, 사람, 고양이, 해상 동물에 고래, 상어있을 때
	- 수의학 치료에 지상동물 객체를 받으면 사람도 들어가게 됨
	- 강아지, 고양이, 고래 상어를 수의학치료라는 인터페이스를 구현하여 관계를 맺어줌

## 8. 인터페이스의 이해
1. 클래스를 사용하는 쪽과 제공하는 쪽이 있음
2. 메서드를 호출하는 쪽에서는 사용하려는 메서드의 선언 부만 알면 됨(내용은 몰라도 됨)
	- A-B관계에서 인터페이스를 사용함으로 A-I-B관계로 바꿈

## 9. 디폴트 메서드와 static메서드
### 9.1. 디폴트 메서드
- 인터페이스에서 구현코드까지 작성한 메서드
- 인터페이스를 구현한 클래스가 생성되면 그 클래스에서 사용할 기본 기능
- 한 클래스에 여러 인터페이스를 구현할 수 있지만 같은 이름의 디폴트 메서드가 있는 경우 문제가 됨
	- 디폴트 메서드가 중복되는 경우 클래스에서 재정의 해야함
```java
interface Calc {
	default void description() {
		System.out.pringln("계산기 구현");
	}
}
```
- 하위 클래스에서 디폴트 메서드 재정의 가능
```java
class Calculator implements Calc {
	@Override
	public void description() {
		// super.description(); // 인터페이스에서 선언한 메서드
		// 클래스에서 원하는 기능으로 재정의
	}
}
```
### 9.2. static 메서드
- 인스턴스 생성과 상관없이 사용할 수 있는 메서드
- 인터페이스 이름으로 참조
```java
interface Calc {
	static int total() {};
}

Calc.total();
```
### 9.3. private 메서드
- Java 9부터 인터페이스에 pricate 메서드 구현
- private 메서드는 재정의 할 수 없음
- private 메서드는 모두 구현해야해서 추상메서드에는 private를 사용할 수 없음
- static 예약어는 함께 사용할 수 있음
