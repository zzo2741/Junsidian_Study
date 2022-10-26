## 1. 내부 클래스란?
- 클래스 내부에 선언한 클래스
```java
class ABC { // 외부 클래스
	class DEF { // 내부 클래스
	}
}
```
### 1. 1. 내부클래스 장점
- 내부 클래스에서 외부 클래스 멤버들을 쉽게 접근 가능
- DEF클래스가 ABC 클래스 안에서만 사용되면 단독으로 둘 필요가 없어 내부클래스로 만들어 코드 복잡성 줄임

## 2. 내부 클래스의 종류와 특징
### 2.1. 특징
- 변수의 선언 위치에 따른 종류와 같음
### 2.2. 종류
#### 2.2.1. 인스턴스 내부 클래스
- 인스턴스 변수 선언 위치와 같음
- 다른 외부 클래스에서 사용할 일이 없는 경우 내부 인스턴스 클래스로 정의
- 내부 클래스를 private으로 선언했다면 다른 클래스에서 사용할 수 없음
- 외부 클래스가 생성한 이후에 사용해야 하기 때문에 정적 변수, 정적 메서드 선언할 수 없음
```java
class OutClass { // 외부 클래스
	private InClass inClass; // 내부 클래스 자료형 변수 선언
	public OutClass() {
		inClass = new InClass(); // 외부 클래스 디폴트 생성자, 외부 클래스가 생성된 후 내부 클래스 생성 가능
	}

	class InClass { // 인스턴스 내부 클래스
		void inTest() {
			System.out.println("test");
		}
	}
	public void usingClass() {
		inClass.inTest();
	}
}

...
OutClass outClass = new OutClass();
outClass.usingClass(); // 내부 클래스 기능 호출

/*결과
test
*/

// 내부 클래스가 private가 아니라면 먼저 OutClass를 만들고, 생성한 참조 변수를 사용하여 내부 클래스를 생성 가능
OutClass outClass = new OutClass();
outClass.InClass inClass = outClass.new InClass();
```
#### 2.2.2. 정적 내부 클래스
- 외부 클래스 생성과 무관하게 사용하려면 정적 내부 클래스 사용
- 인스턴스 변수 위치에 정의하며 static 사용
- 정적 내부 클래스에 선언한 메서드나 변수는 private가 아닌 경우 다른 클래스에서 바로 사용
```java
class OutClass { // 외부 클래스
	private static int sNum = 20;
	static class InStaticClass { // 정적 내부 클래스
		void inTest() {
			System.out.println("inTest");
		}
		static void sTest() {
			System.out.println("sTest");
		}
	}
}

...
OutClass.InStaticClass sInClass = new OutClass.InStaticClass(); // 외부 클래스 생성 없이 바로 정적 내부 클래스 생성 가능
sInClass.inTest(); // 정적 내부 클래스 일반 메서드 호출
sInClass.sTest(); // 정적 내부 클래스 정적 메서드 호출
OutClass.InStaticClass.sTest(); // 정적 내부 클래스 정적 메서드 호출

/*결과
inTest
sTest
sTest
*/
```
#### 2.2.3. 지역 내부 클래스
- 지역 변수처럼 메서드 내부에 클래스를 정의하여 사용(메서드 안에서만 사용)
- 지역 내부 클래스에서 사용하는 지역 변수는 상수처리가 됨
```java
class OutClass{  
Runnable getRunnable() {  
	int i = 10;  
	class InClass implements Runnable{ // 지역 내부 클래스, 예시로 스레드 생성에 사용하는 Runnable인터페이스 사용  
		public void testMethod() { // 사용할 수 없음  
			System.out.println("testMethod");  
		}  
		
		@Override
		public void run() { // 무조건 run() 메서드 오버라이딩 해야함  
			System.out.println("run");  
		}  
	}  
	return new InClass();  
	}  
}  

...
OutClass outClass = new OutClass();  
Runnable runner = outClass.getRunnable(); // Runnable을 참조하는 InClass객체 생성  
// runner.testMethod(); // Runnable를 참조하기에 Runnable의 run()메서드만 사용 가능  
runner.run();  

/*결과
run
*/
```

## 3. 내부 클래스의 선언
```java
class OutClass { // 외부 클래스
	class InClass { // 인스턴스 내부 클래스
	}
	static class StaticInClass { // 정적 내부 클래스
	}
	public void method() { 
		class LocalInClass{ // 지역 내부 클래스
		}
	}
}
```

## 4. 내부 클래스의 제어자와 접근성
- 내부 클래스의 제어자는 변수에 사용 가능한 제어자와 동일(참고 : [[4-제어자(modifier)#6. 제어자(modifier)의 조합]])
	-  클래스는 default, public만 가능하지만 내부 클래스에는 모든 접근 제어자가 가능
```java
class OutClass { // 외부 클래스
	private int privateIv = 11;
	static int staticIv = 22;
	int value = 100;
	
	class InClass { // 인스턴스 내부 클래스
		int iv = 10;
		// static int cv = 20; // 에러 인스턴스 내부 클래스에서는 static 변수를 선언할 수 없음
		final static int CONST = 30; // 상수이므로 허용
		int value = 200;

		int v1 = privateIv; // 내부 클래스는 외부 클래스 private 변수 접근 가능
		int v2 = staticIv; // static 변수 사용 가능

		void method(){
			int value = 300;
			System.out.println(value); // 300
			System.out.println(this.value); // 200
			System.out.println(OutClass.this.value); // 100
		}
	}
	
	static class StaticInClass { // 정적 내부 클래스
		int iv = 100;
		static int cv = 200; // static 내부 클래만 static 변수 선언 가능
		
		// int v1 = privateIv; // 인스턴스 변수 접근 불가
		int v2 = staticIv; // static 변수 사용 가능
	}
	
	public void method() { 
		int lv = 10;
		
		class LocalInClass{ // 지역 내부 클래스
			int iv = 1000;
			// static int cv = 2000; // 에러 인스턴스 내부 클래스에서는 static 변수를 선언할 수 없음
			final static int CONST = 3000; // 상수이므로 허용

			int v1 = privateIv; // 내부 클래스는 외부 클래스 private 변수 접근 가능
			int v2 = staticIv; // static 변수 사용 가능
			int v3 = lv; // JDK1.8부터 가능 자동적으로 상수 처리
			/*
			메서드 변수는 메서드 종료와 함께 소멸
			지역 내부 클래스의 객체는 메서드 변수보다 오래 존재할 가능성이 있어 값이 변하지 않는 상수로 처리
			*/
		}
	}

	/* 메서드 접근 */
	static void staticMethod() { // static 메서드에서는 static멤버만 가능
		// InClass ic = new InClass(); 
		StaticInClass sic = new StaticInClass();
		// LocalInClass lc = new LocalInClass(); 지역 내부 클래스는 접근 불가
	}
	
	void instanceMethod() { // 인스턴스 메서드에서는 둘 다 가능
		InClass ic = new InClass();
		StaticInClass sic = new StaticInClass();
		// LocalInClass lc = new LocalInClass(); 지역 내부 클래스는 접근 불가
	}

	
}

...
System.out.println(InClass.CONST); // 30;
System.out.println(StaticInClass.cv); //  200;
// System.out.println(LocalInClass.CONST); // 지역 내부 클래스 상수는 접근 불가, 메서드에서만 사용

```

## 5. 익명 클래스(anonymous class)

