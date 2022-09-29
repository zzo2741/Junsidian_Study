> 로버트 C.마틴이 2000년대 초반 객체 지향 프로그래밍 및 설계의 5가지 기본원칙으로 제시한 것

## 1. **S**RP(Single responsibility principle) : 단일 책임 원칙
- **한 클래스는 하나의 책임만 가져야 함**
	- 하나의 모듈에 여러가지 책임이 있다면 수정해야 하는 이유도 여러개가 될 수도 있음
	- 클래스에 하나의 책임 만 갖고 있다면 해당 클래스만 변경하면 됨
```java
public class UserService { 
	public void addUser(){ // 사용자 추가 기능
		... // 암호화 하는 로직
		... // 사용자 코드 자동 생성 로직
	}
}
/*
암호화 방식 개선, 사용자 코드 자동 생성 규칙 변경이라는 요구사항이 생길 시 하나의 모듈에 수정해야 하는 이유도 여러개가 됨
*/
	
public class UserService { 

	private PasswordEncoder passwordEncoder;
	private UserCodeCreater userCodeCreater;
	
	public void addUser(){ // 사용자 추가 기능
		// 메서드 호출
		passwordEncoder.encode();
		userCodeCreater.createUserCode();
	}
}

public class PasswordEncoder {
	public void encode(){
		... // 암호화 하는 로직
	}
}

public class UserCodeCreater {
	public void createUserCode(){
		... // 사용자 코드 자동 생성 로직
	}
}
/*
각각 책임사항에 대해 요구사항이 생길 시 수정해야될 클래스가 명확해짐	
*/
```

## 2. **O**CP(Open-closed principle) : 개방-폐쇄 원칙
- **소프트웨어 구성요소(클래스, 모듈, 함수 등)는 확장에는 열리고 변경에는 닫힘.**
	- 확장에 열림 : 요구사항이 변경될 때 새로운 동작을 추가하여 기능 확장.
	- 변경에 닫힘 : 기존 코드를 수정하지 않고 동작 추가 변경 가능해야 함.
```java
public class StandardPasswordEncoder {
	public void encode(){
		... // 암호화 하는 로직
	}
}

public class UserService { 

	// private PasswordEncoder passwordEncoder; // 기존
	private StandardPasswordEncoder passwordEncoder; // 변경
	...
}
/*
새로운 암호화 정책을 적용하려고 했더니 수정했던 부분과 무관한 UserService 코드를 수정해야하는 상황이 발생함.
-> 변경에 닫히는 원칙에 위반됨
*/

public interface PasswordEncoder{
	void encode();
}

public class StandardPasswordEncoder implements PasswordEncoder {
	@Override
	public void encode(){
		... // 암호화 하는 로직
	}
}

public class UserService { 

	private PasswordEncoder passwordEncoder; // 기존대로 사용
	// private StandardPasswordEncoder passwordEncoder; // 변경안해도 됨
	...
}
/*
StandardPasswordEncoder가 PasswordEncoder를 의존하도록 하여 개방 폐쇄의 원칙에 충족되도록 할 수 있음.
*/
```

## 3. **L**SP(Liskov substitution principle) : 리스코프 치환 원칙
- **서브 타입은 언제나 자신의 기반 타입(Base type)으로 교체할 수 있어야 함.**
	- 상위 타입이 하위 타입으로 변경되어도, 상위 타입의 퍼블릭 인터페이스를 통해 서브 클래스를 사용할 수 있어야 함.
	- 상속은 조직도나 계층도가 아닌 분류도가 되어야 함.
	- 리스코프 치환을 지키지 위한 두가지 조건
- 형식적 측면
			- 자식 클래스가 오버라이딩 하는 변수와 메서드는 부모클래스와 형식이 일치해야함
			- 지키지 않으면 에러남
```java
public class Rectangle { 
	private int width; 
	private int height; 
	
	public void setWidth(int width) { 
		this.width = width; 
	} 
	public void setHeight(int height) { 
		this.height = height; 
	} 
	public int getWidth() { 
		return width; 
	} 
	public int getHeight() { 
		return height; 
	} 
}

public class Square extends Rectangle {
	@Override 
	public void setWidth(int width, int height) { // 형식이 맞지 않으면 에러 발생
		...
	}

	...
}
```
- 내용적 측면
	- 자식 클래스가 부모 클래스의 메서드에 담긴 의도, 행동 규약을 위반하지 않아야 함
	- 에러가 안나도 의도하지 않는 결과가 나옴
```java
public class Rectangle { 
	...
	
	public void setWidth(int width) { 
		this.width = width; 
	} 
	public void setHeight(int height) { 
		this.height = height; 
	} 
	
	...
}

public class Square extends Rectangle {
	@Override 
	public void setWidth(int width) { // 의도가 달라지면 다른 결과가 나올 수 있음
		super.setWidth(width); 
		super.setHeight(width);
	}

	@Override 
	public void setHeight(int height) { // 의도가 달라지면 다른 결과가 나올 수 있음
		super.setWidth(height); 
		super.setHeight(height);
	}

	/*
	자식 클래스가 부모 클래스의 메서드에 담긴 의도를 위반 하면 의도하지 않는 결과가 나올 수 있음
	*/
}
```

## 4. **I**SP(Interface segregation principle) : 인터페이스 분리 원칙
- **하나의 일반적인 인터페이스보다 여러 개의 구체적인 인터페이스가 나음.**
	- 클라이언트는 자신이 사용하지 않는 메서드에 의존 관계를 맺으면 안됨
```java
public interface PasswordEncoder{
	void encode();
}

public class StandardPasswordEncoder implements PasswordEncoder {
	@Override
	public void encode(){
		... // 암호화 하는 로직
	}

	public boolean validate() {
		... // 비밀번호 규칙이 맞는지 체크
	}
}
/*
validate() 메서드를 사용하기 위해서는 구체 클래스인 StandardPasswordEncoder를 주입받아야 하는데 
그러면 불필요한 encode() 메서드까지 접근 가능해지며 인터페이스 분리 원칙을 위배하게 됨
*/

public interface PasswordChecker{
	void validate();
}

public class StandardPasswordEncoder implements PasswordEncoder, PasswordChecker {
	@Override
	public void encode(){
		... // 암호화 하는 로직
	}

	@Override
	public boolean validate() {
		... // 비밀번호 규칙이 맞는지 체크
	}
}
/*
위의 상황을 해결하기 위해서는 비밀번호를 검사하는 별도의 인터페이스를 만들고 인터페이스로 주입받도록 하는 것이 적합
*/
```

## 5. **D**IP(Dependency inversion principle) : 의존관계 역전 원칙
- **구체적인 것이 추상화된 것에 의존해야 함. 자주 변경되는 구체 클래스에 의존하면 안됨, OCP와 유사한 원칙**
	- UserService --의존--> StandardPasswordEncoder
		- StandardPasswordEncoder는 변하기 쉬운 구체 클래스이기 때문에 StandardPasswordEncoder에 의존하는 것은 의존 역전 원칙에 위반됨
	- UserService --의존--> PasswordEncoder <--구현-- StandardPasswordEncoder
		- PasswordEncoder에 의존하므로 비밀번호 암호화 정책이 변경되어도 다른 곳들로 변경이 전파되지 않아 유연한 어플리케이션이 됨.

## 6. 정리
### - SOLID의 핵심은 결국 추상화(모델링)