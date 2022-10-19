## 1. 오버라이딩이란?
- 상위 클래스에 정의한 메서드가 하위클래스에서 메서드를 재정의하는 것
- 선언부는 그대로, 구현부만 변경 가능
```java
public class Customer {
	public int calcPrice(int price){
		return price;
	}
}


public class VIPCustomer extends Customer {
	private double discountRate;

	@Override
	public int calcPrice(int price){
		return (int) (price * discountRate);
	}
	
}
```
- **상속받은 메서드를 자신에 맞게 변경하는 것을 오버라이딩**

## 2. 오버라이딩의 조건
1. 선언부가 상위 클래스의 메서드와 일치
2. 접근 제어자(public, protected, default, private)를 상위클래스 메서드보다 넓어야 함
	- public > protected > default > private
3. 예외를 상위클래스보다 많이 선언할 수 없음

## 3. 오버로딩 vs 오버라이딩
- 이름만 비슷하지 둘이 전혀 관계없음
- **오버로딩** : 기존에 없는 새로운 메서드 정의 (new)
- **오버라이딩** : 상속받은 메서드의 내용을 변경하는 것 (change, modify)

## 4. super 
- 상위 클래스에 선언한 멤버 변수나 메서드를 하위클래스에서 참조할 때 super 사용, this와 비슷
- super 예약어는 상위 클래스의 참조 값 가지고 있음
- 상위 클래스의 멤버와 자신의 멤버를 구별할 때 사용

## 5. super() - 조상 클래스의 생성자
- 상위 클래스 생성자 호출
- 하위 클래스 생성 시 상위 클래스 생성자 먼저 호출
	- 하위 클래스가 생성될 때 상위클래스의 디폴트 생성자를 호출하는 super()가 자동으로 생성
- super()를 호출하면 상위클래스의 디폴트 생성자 호출
- super(매개변수), 매개변수가 있는 경우에는 매개변수가 있는 생성자 호출
- 생성자 첫줄에 작성하여 호출해야함
