## 1. 다형성이란?
- 하나의 코드가 여러 자료형으로 구현되어 실행되는 것
- 상위 타입 참조 변수로 하위 타입 객체를 다루는 것
- 하위 타입 참조 변수로 상위 타입 객체를 다루는 것은 허용하지 않음
```java
class Animal { ... }
class Human extends Animal { ... }

Animal animal = new Human(); // 상위 타입 참조변수로 하위 타입 인스턴스 참조
Human human = new Animal(); // 에러
```

## 2. 참조변수의 형변환
- 사용할 수 있는 멤버의 갯수를 조절하는 것
- 참조변수를 형변환 한다고 해서 기본형의 형변환 처럼 값이 달라지는 것이 아님
- 상속관계의 참조변수일 때 서로 형변환 가능
```java
class Animal { ... }
class Human extends Animal { ... }
class Pig extends Animal { ... }

Human h = new Human();
Animal a = (Animal)h; // 상위 타입으로 형변환 (생략가능), 멤버의 갯수가 줄어드는 안전한 형변환
Human h2 = (Human)a; // 하위 타입으로 형변환 가능 (생략불가), 멤버의 갯수가 증가하는 안전하지 않는 형변환
Pig p = (Pig)h; // 에러, 상속관계 아님
```

## 3. instanceof연산자
- 참조변수의 형변환 가능 여부 확인하기 위해 instanceof 사용
- 가능하면 true반환
```java
Animal a = new Animal();
if (a instanceof Human) { // 가능한지 확인
	Human h = (Human)a; // 형변환
}
```

## 4. 참조변수와 인스턴스의 연결
```java
class Parent {  
	int x = 200;  
	void method() {  
	System.out.println("1234");  
	}  
}  
  
  
class Child extends Parent {  
	int x = 100;  
	void method() {  
	System.out.println("4321");  
	}  
}

Parent p = new Parent();  
Parent p2 = new Child();  
Child p3 = new Child();  
  
System.out.println(p.x); // 200 참조변수가 Parent일 때
System.out.println(p2.x);// 200 참조변수가 Parent일 때
System.out.println(p3.x);// 100 참조변수가 Child 때
/*
변수의 경우 참조타입의 멤버변수로 접근
*/  

p.method(); // 1234  
p2.method();// 4321  
p3.method();// 4321  
/*
메서드의 경우 오버라이딩 된 메서드를 실행
*/  
```

## 5. 매개변수의 다형성
- 참조형 매개변수는 메서드 호출 시, 자신과 같은 타입 또는 하위 타입의 인스턴스 넘길 수 있음
```java
Human h = new Human();
Pig p = new Pig();
Dog h = new Dog();

void move(Animal a) {
	...
}
/*
여러개의 메서드를 만들 필요 없이 매개변수 타입을 Animal로 하여 코드 중복을 줄일 수 있는 다형성의 장점
*/
```

## 6. 여러 종류의 객체를 배열로 다루기
- 상위 타입의 배열에 자손들을 담을 수 있음
```java
Animal a[] = new Animal[3];
a[0] = new Human();
a[1] = new Pig();
a[2] = new Dog();
/*
자신과 같은 타입, 하위 타입의 객체를 배열로 넣을 수 있는 다형성의 장점
*/
```

#### ※ 참고로 가변 배열이 가능한 Vector클래스가 있음, 공부 필요
