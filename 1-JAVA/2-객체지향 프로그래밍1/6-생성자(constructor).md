## 1. 생성자란? 
- new연산자로 클래스로부터 객체를 생성할 때 호출되어 객체의 초기화 담당
- 객체 초기화 : 필드를 초기화하거나 메소드를 호춣해서 객체를 사용할 준비를 하는 것
- new연산자에 의해 생성자가 실행되면 힙 영역에 객체가 생성되고 객체의 번지가 리턴됨
- 모든 클래스는 생성자가 반드시 존재
- 생성자를 하나 이상 가질 수 있음

## 2. 기본 생성자(default constructor) 
- 매개변수가 없는 생성자
```java
클래스이름() {} // 기본 생성자
```
- 생성자가 하나도 없을 때만, 컴파일러가 기본 생성자 자동 추가
	- 생성자 선언을 생략하면 컴파일러는 기본 생성자를 바이트 코드에 추가
- 명시적 선언한 생성자가 1개라도 있으면 컴파일러는 기본 생성자를 추가하지 않음

## 3. 매개변수가 있는 생성자
- 생성자는 메소드와 미슷한 모양을 가지고, 리턴 타입이 없고, 클래스 이름과 동일
```java
클래스 ( 매개변수선언, ... ) {
	// 객체의 초기화 코드
}
```
```java
public class Car {
	String model;
	String color;
	int maxSpeed;
	
	Car(String m, String c, int s) {
		model = m;
		color = c;
		maxSpeed = s;
	}
}

Car car = new Car("그랜저", "검정", 300);
/*
명시적 생성자가 있는 경우 기본 생성자를 추가하지 않아 선언된 생성자를 호출해서 객체를 생성해야 함
*/
```
#### ※ 기본 생성자는 컴파일러에 의존하지 말고 항상 만들어 주는 습관 필요

### 3.1. 생성자 오버로딩
- JAVA에서 다양한 방법으로 객체를 생성할 수 있는 **생성자 오버로딩** 제공
- 매개 변수 달리하는 생성자를 여러개 선언
```java
public class Car{
	Car() {...}
	Car(String m) {...}
	Car(String m, String c) {...}
	Car(String m, String c, int m) {...}
}
```

## 4. 생성자에서 다른 생성자 호출하기 - this(), this
### 4.1. this() : 다른 생성자 호출(생성자)
- 객체 자신의 또 다른 생성자를 호출할 때 사용
- this()는 반드시 생성자의 첫 줄에서만 허용
```java
Car(String m) {
	this.model = m;
	this.color = 은색:
	this.masSpeed = 100;
}
Car(String m, String c) {
	this.model = m;
	this.color = c;
	this.masSpeed = 100;
}
...

/*
코드의 중복 발생
*/

Car(String m) {
	this(m, "은색", 100); // Car(String m, String c, int m) 생성자 호출
}
Car(String m, String c) {
	this(m, c, 100); // Car(String m, String c, int m) 생성자 호출
}
Car(String m, String c, int s) { // this()로 호출되는 생성자
	model = m;
	color = c;
	maxSpeed = s;
}
/*
this()를 사용하여 코드 중복을 줄임
*/
```

### 4.2. this : 참조변수
- 인스턴스 자신을 가리키는 참조변수
- 인스턴스의 주소가 저장
- 인스턴스 메서드, 생성자에서 사용 가능
- 지역변수와 인스턴스 변수 구별할 때 사용
```java
Car(String m, String c, int s) { 
	model = m;
	color = c;
	maxSpeed = s;
} 
/*
지역변수와 인스턴스 변수 이름이 다름
*/

Car(String model, String color, int maxSpeed) { 
	this.model = model;
	this.color = color;
	this.maxSpeed = maxSpeed;
} 
/*
지역변수와 인스턴스 변수 이름이 같음
*/
```

## 5. 생성자를 이용한 인스턴스의 복사
- 현재 사용하고 있는 인스턴스의 값을 복사하여 이와 같은 값을 가지는 인스턴스를 만들 때 생성자를 사용
```java
Car(String model, String color, int maxSpeed) { 
	this.model = model;
	this.color = color;
	this.maxSpeed = maxSpeed;
} 

Car(Car car) {
	this(car.model, car.color, car.maxSpeed);
}

Car c1 = new Car("그랜저", "검정", 300);
Car c2 = new Car(c2); // Car(Car car) 생성자 호출하여 복사본 생성
```