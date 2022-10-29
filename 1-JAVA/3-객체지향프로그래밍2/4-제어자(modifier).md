## 1. 제어자란?
- 클래스, 클래스의 멤버에 부가적인 의미 부여
- 여러 제어자 같이 사용 가능
	- 접근제어자는 하나만, 맨 앞에 쓰는 것이 관례
```java
public static final int a = 10;
```

## 2. static - 클래스의, 공통적인
### 2.1. static변수
- 클래스를 선언할 때 특정 메모리에 저장되어 모든 인스턴스가 공유
- 인스턴스보다 먼저 생성되어, 인스턴스가 아닌 클래스 이름으로도 참조하여 사용 가능
- 일반 메서드에서는 static변수 호출 가능
### 2.2. static메서드
- 인스턴스 참조 변수가 아닌 클래스 이름으로 직접 호출 가능
- 인스턴스가 생성될 때 만들어지는 인스턴스 변수는 static메서드에서 사용할 수 없음
- 지역변수, 클래스 변수는 사용가능하지만 인스턴스 변수는 사용할 수 없음

## 3. final - 마지막의, 변경될 수 없는
### 3.1. final변수
- 상수를 의미
- 상수를 선언할 때 일반 변수와 구별하기 위해 대문자로 쓰는 경우 많음
- 자바 프로젝트에서 여러 파일에서 공유해야 하는 상수 값은 한파일에 모다 public static final로 사용하면 좋음
### 3.2. final메서드
- 변경불가한 메서드
- 하위 클래스에서 재정의 할 수 없음, 오버라이딩 할 수 없는 메서드
### 3.3. final클래스
- 상속할 수 없음
- 보안과 관련되어 있거나, 기반 클래스가 변하면 안되는 경우 클래스를 final로 선언
- JDK에서 제공하는 클래스 중 대표적으로 String, Integer 클래스가 final클래스

## 4. abstract - 추상의, 미완성의
- 클래스나 메서드 앞에 붙여서 사용
- concrete(구상)와 반대
### 4.1. 추상 클래스
- 추상 메서드가 속하면 추상클래스
- 추상클래스는 인스턴스 생성 불가

### 4.2. 추상 메서드
- abstract 예약어를 사용하여 선언부만 작성하고 구현부는 작성하지 않은 메서드
```java
public abstract class Computer { // 추상 클래스
	public abstract void display(); // 추상 메서드
	public abstract void typing();
}
```

## 5. 접근 제어자(access modifier)
- private : 같은 클래스 내에서만 접근
- default : 같은 패키지 내에서만 접근
- protected : 같은 패키지 내에서, 다른 패키지의 자손 클래스에서 접근 가능
- public : 접근 제한이 없음

## 6. 제어자(modifier)의 조합
|대상|사용가능 제어자|
|-|-|
|**클래스**|public, default, final, abstract|
|**메서드**|모든 접근 제어자, final, abstract, static|
|**멤버변수**|모든 접근제어자, final, static|
|**지역변수**|final|

### 6.1. 제어자 조합 시 주의 사항
- 메서드에 static, abstract 함께 사용할 수 없음
- 클래스에 abstract, final 동시에 사용할 수 없음
- abstract메서드 접근 제어자가 private 일 수 없음
- 메서드에 private와 final을 같이 사용할 필요 없음
