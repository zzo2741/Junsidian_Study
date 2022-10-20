## 1. 패키지(package)
- 물리적 형태는 파일 시스템의 폴더 형태이지만 폴더 기능만 하는 것이 아니라 클래스의 식별자 역할
- 클래스명이 동일해도 패키지가 다르면 다른 클래스로 인식

## 2. 패키지의 선언
- 해당 클래스가 어떤 패키지에 속할 것인지 선언하는 것
```java
package 상위패키지.하위패키지;

// EX) com.team 패키지의 Member 클래스 작성 시
package com.team;

public class Member {...}
```
- 패키지 선언이 없는 클래스를 default 패키지에 포함시킴, JDK 11 이후 버전부터 패키지가 없으면 컴파일 에러 발생

### 2.1. 패키지명 규칙
- 숫자로 시작하면 안되고, __, $를 제외한 특수문자도 안됌
- 모두 소문자로 작성하는 것이 관례
- 주로 도메인 이름을 패키지명으로 함
- 도메인 이름을 역순으로 함, 포괄적인 이름이 상위 패키지가 되도록 하기위해
	- kr.co.genexon.프로젝트명으로 하는 것이 관례

## 3. import문
- 다른 패키지의 클래스, 인퍼테이스를 사용할 것임을 컴파일러에 알리기 위해 import문 사용
- import문을 사용하여 패키지이름 생략
- java.lang패키지 클래스는 import없이 사용 가능
	- 자바언어의 가장 기본 패키지임으로 핵심 클래스는 import없이 사용 가능

## 4. import문의 선언
```java
import 상위패키지.하위패키지.클래스이름;

// 한 패키지에 여러 클래스가 있는 경우 '*' 사용, 프로그램 성능에 영향 없음
import 상위패키지.하위패키지.*;

// 상위 패키지를 import했다고 하위 패키지까지 import 되는 것은 아님
import 상위패키지.하위패키지.*;
import 상위패키지.하위패키지.하위패키지.*;

// import한 패키지에 같은 클래스명이 있는 경우 사용할때 패키지명을 붙여야함
import com.myteam.*;
import com.yourteam.*;

com.myteam.Member m1 = new com.myteam.Member();
com.yourteam.Member m2 = new com.yourteam.Member();
```

## 5. static import문
- static멤버를 사용할 때 클래스 이름을 생략할 수 있게 해준다.
```java
import static java.lang.Math.random;
import static java.lang.System.out;

// System.out.println(Math.random());
out.println(random());
```
- 가독성을 위해 static import문은 자주 사용하지 않음
