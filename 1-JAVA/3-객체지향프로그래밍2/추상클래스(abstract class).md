## 1. 추상클래스란?
- 미완성 설계도, 미완성 메서드를 갖고 있는 클래스 (concrete class 반대)
- 다른 클래스 작성에 도움 주기 위한 것, 인스턴스 생성 불가
```java
public abstract class Computer { // 추상 클래스
	public abstract void display(); // 추상 메서드
	public abstract void typing();
}

Computer c1 = new Computer(); // 에러 발생, 인스턴스 생성 불가
Computer c2 = new NoteBook(); // 상속을 통해서 인스턴스 생성 가능
```

## 2. 추상메서드(abstract method)
- abstract 예약어를 사용하여 선언부만 작성하고 구현부는 작성하지 않은 메서드
- 꼭 필요하지만 자손마다 다르게 구현될 것으로 예상하는 경우 사용

## 3. 추상클래스의 작성
```java
public class test3 {
	public static void main(String[] args) {
		// Animal a = new Human(); 에러 발생, Human은 미완성 클래스
		Animal a = new Pig();
		Pig a2= new Pig();
		a.move(0);
		a.jump(0);
		System.out.println(a.distance);
		System.out.println(a2.distance);
		
	}
}

abstract class Animal {
	int distance = 10;
	abstract void move(int distance);
	abstract void stop(int distance);
	void jump(int distance) {
		move(distance);
		System.out.println("Animal move");
	}
}

abstract class Human extends Animal { // 모든 메소드가 구현되지 않아 미완성 클래스, abstract 붙여야함
	@Override
	void move(int distance) {	
		System.out.println("Human move");
	}
	
}

class Pig extends Animal { // 모든 메소드 구현하여 완성 클래스
	int distance = 20; // 만약 없다면 a2.distance == 10
	@Override
	void move(int distance) {	
		System.out.println("Pig move");
	}
	@Override
	void stop(int distance) {	
		System.out.println("Pig stop");
	}
}

/* 결과
Pig move
Pig move
Animal move
10
20
*/
```
