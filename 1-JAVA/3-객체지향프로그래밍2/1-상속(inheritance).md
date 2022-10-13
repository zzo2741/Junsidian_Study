## 1. 상속의 정의와 장점 
- 이미 잘 개발된 클래스를 재사용하여 새로운 클래스를 만들어 중복되는 코드를 줄여주는 것
- 부모 클래스의 수정으로 모든 자식 클래스들도 수정되는 효과를 가져와 유지 보수 시간 최소화
- 자식클래스가 부모클래스 보다 더 많은 내용을 가짐
```java
public class 자식클래스 extends 부모클래스{
	...
}
```

## 2. 클래스간의 관계 - 포함관계  
- 클래스 멤버로 참조변수를 선언하는 것
```java
class Circle {
	int x, y, r;
}
/* 
위 코드를 아래 코드로 작성할 수 있음
*/
class Point { int x, y; }

class Circle {
	Point c = new Point();
	int r;
}
/*
Circle클래스는 Point클래스를 포함
작은 단위를 클래스로 만들고, 이들을 조합해서 클래스를 만든다.
*/
```

## 3. 클래스간의 관계 결정하기 
```java
// 1. 포함일 경우
class Point { int x, y; }

class Circle {
	Point c = new Point();
	int r;
}

// 2. 상속 일 경우
class Circle extends Point {
	int r;
}
```
- '원은 점이다.' 보다 '원은 점을 가지고 있다.'가 더 적합하다.
- 상황에 맞게 잘 설계해야 함

## 4. 단일상속(single inheritance)
- Java는 단일 상속만 허용
```java
public class 자식클래스 extends 부모클래스1, 부모클래스2 { // 에러 발생
	...
}
```
- 다중 상속의 경우 부모클래스들로 부터 같은 이름의 메서드 상속 시 충돌 발생
- 인터페이스를 이용하여 충돌문제를 해결하면서 다중상속 효과 낼 수 있음
- 비중이 높은 클래스만 상속, 나머지는 포함

## 5. Object클래스 - 모든 클래스의 조상
- 부모가 없는 클래스는 자동적으로 Object클래스 상속 받음
	- Object클래스는 모든 클래스의 최고 조상
- 모든 클래스는 Object클래스에 정의된 11개의 메소드 상속 받음
	- ex) toString(), equals(object obj) 등
