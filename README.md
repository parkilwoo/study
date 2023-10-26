**평소 궁금하거나 면접에서 받은 질문 혹은 공부한 내용들을 간단하게 정리합니다.**

## Pyhon
1. [매직메소드 init과 new의 차이](#매직메소드-init과-new의-차이)
2. [Namespace란?](#namespace란)

## Nginx
1. [Nginx 사용시 server블록 설정이 겹칠 경우](#nginx-사용시-server블록-설정이-겹칠-경우)

## OS
1. [Swap 영역이란?](#swap-영역이란)

## JPA
1. [영속성 컨텍스트란?](#영속성-컨텍스트란)

## Web
1. [Filter, Interceptor, AOP의 개념과 차이점](#filter-interceptor-aop의-개념과-차이점)

--- 

### 매직메소드 init과 new의 차이
  * `new` 메소드는 객체의 생성을 담당하며, 객체가 메모리에 할당될때 호출됩니다. 클래스의 인스턴스를 반환합니다. 첫번째 매개변수로 클래스(cls)를 받아야 합니다. 객체 생성을 사용자 정의하려면 new 메소드를 오버라이드 해야합니다.
  * `init` 메소드는 객체의 초기화를 담당하며, 주로 객체가 생성된 후 속성 값 등을 설장하기 위해 호출됩니다. 첫번째 매개변수로 인스턴스(self)를 받으며 반환값은 없습니다. 객체의 속성을 초기화 하려면 init 메소드를 사용합니다.
  * 대부분의 경우 객체의 초기화만 필요하기 때문에 `init`만 오버라이드 하지만, 특별한 객체 생성이 필요한 경우(ex.인스턴스 개수 제한)에는 `new`도 오버라이드 할 수 있습니다.

### Nginx 사용시 server블록 설정이 겹칠 경우
 * Server 블록이 겹칠경우 Nginx에서 우선순위
  1. **server_name 지시어 사용**: 먼저 `server_name`지시어를 사용하여 요청된 호스트 이름과 일치하는 `server`블록을 찾고 선택합니다. 만약 모든 설정에 `server_name`지시어가 명시되지 않았거나 일치하지 않을 경우, 다른요소를 고려합니다.
  2. **default_server 옵션**: `listen` 지시어에 `default_server` 옵션이 사용된 경우, 해당 `server` 블록이 기본 서버로 선택됩니다. 예를들어, `custom.conf` 파일에 `listen 80 default_server;` 옵션이 설정되어 있다면, 80포트로 들어오는 모든 요청의 기본 서버로 작동합니다.
  3. **설정 파일의 읽는 순서**: 지시어에 대한 명시적인 설정이 없는 경우, Nginx는 설정 파일을 읽는 순서에 따라 `server`블록을 선택합니다. 일반적으로 알파벳순서로 파일을 읽습니다. 예를들어 `custom.conf` 파일과 `default.conf` 파일 모두에 `listen 80`이 설정되어 있을경우 80 포트로의 모든 요청은 `custom.conf`파일의 설정이 우선으로 적용됩니다.

### Swap 영역이란?
	swap 영역은 운영체제에서 사용하는 중요한 컴포넌트중 하나입니다.
 1. **정의:** 
	*	Swap 영역은 하드 드라이브의 일부분으로, RAM이 가득 찼을경우 메모리를 확장하는데 사용됩니다. 즉, RAM의 일부분이 필요할 때 이 영역에 데이터를 임시로 저장합니다.
 2. **사용 목적:**
	* `메모리관리`: RAM이 가득 찼을 경우, 운영체제는 사용되지 않는 메모리 페이지를 swap 영역으로 이동시켜 RAM 공간을 확보합니다.
	* `메모리 오버커밋`: 물리적 RAM 크기보다 더 많은 메모리를 프로세스에 할당할 수 있습니다. 이를 통해 시스템은 더 많은 프로세스를 동시에 실행할 수 있습니다.
	* `휴면(hibernate)지원`: 휴면 상태로 전환할 때, 시스템의 현재 상태(RAM의 내용)를 swap 영역에 저장하여 전원을 완전히 끌 수 있습니다. 전원을 다시 켤 때, swap에서 RAM으로 데이터를 복원하여 이전 상태로 돌아올 수 있습니다.
 3. **장/단점:**
	*	`장점`: RAM이 부족할 때 시스템의 메모리 부족 문제를 완화시켜줍니다. 또한, 더 많은 애플리케이션을 동시에 실행할 수 있도록 합니다.
 	*	`단점`: swap영역도 하드 드라이브 이므로 RAM에 비해 상대적으로 느립니다. 따라서, swap 영역에 많은 데이터가 저장되면 시스템의 성능이 저하될 수 있습니다.

### Namespace란?
	네임스페이스(Namespace)는 이름(name)을 객체에 매핑하는 것입니다. 
	네임스페이스는 변수나 함수, 클래스 등의 이름이 그것이 참조하는 실제 객체를 어떻게 찾아가는지를 결정하는 매핑입니다.
	파이썬에서는 여러 유형의 네임스페이스가 있으며, 각 네임스페이스는 다른 생명주기를 가집니다.
 - **Namspace 유형:**

 	1. **로컬 네임스페이스(Local namespace)**: `함수 내부`에서 정의된 변수들의 네임스페이스입니다. 함수가 호출될 때 생성되고, 함수가 종료될 때 소멸됩니다.
	 2. **인클로징 네임스페이스(Enclosing namespace)**: 중첩된 함수의 `바깥쪽 함수`에 대한 네임스페이스입니다. 인클로징 네임스페이스는 내부 함수를 감싸고 있는 바깥 함수의 `로컬 변수`들을 참조할 수 있게 해줍니다.
	 3. **전역 네임스페이스(Global namespace)**: `모듈 또는 스크립트의 최상위` 수준에서 정의된 변수, 함수, 클래스 등이 여기에 포함됩니다. 모듈이 임포트될 때 생성되며, 인터프리터가 종료되거나 `del`문을 사용하여 명시적으로 삭제될때까지 유지됩니다.
 	4. **내장 네임스페이스(Built-in namespace)**: 파이썬에서 `내장된 함수와 예외`들이 여기에 포함됩니다. 파이썬 인터프리터가 시작될 때 생성되고 프로그램 종료시 소멸됩니다.

 - **Namspace 접근순서:**
   	<br/>변수나 함수 이름에 접근할 때 파이썬은 다음 순서로 네임스페이스를 검색합니다. **LEGB RULE**

 	1. **Local(L)**: 현재 함수의 로컬 네임스페이스
  	2. **Enclosing(E)**: 중첩된 함수의 네임스페이스
   	3. **Global(G)**: 모듈의 전역 네임스페이스
   	4. **Built-in(B)**: 파이썬의 내장 네임스페이스
	```python
	x = 10  # 전역 변수
	
	def outer_function():
	    x = 20  # 인클로징 변수
	    
	    def inner_function():
	        x = 30  # 로컬 변수
	        print(x)  # 30 출력 (로컬 네임스페이스의 x)
	
	    inner_function()
	    print(x) # 20 출력 (인클로징 네임스페이스의 x)
	
	outer_function()
	print(x) # 10 출력 (전역 네임스페이스의 x)

 	```
 ### 영속성 컨텍스트란?
 	JPA의 핵심 개념중 하나이며, 엔티티의 생명 주기를 관리하고 데이터베이스와의 상호 작용을 최적화 하는 로직을 담당하는 논리적인 개념입니다.
  - **생명주기 관리**: JPA에서는 엔티티의 생명주기가 명확하게 정의되어 있습니다. 영속성 컨텍스트는 엔티티의 `생명주기 상태(비영속, 영속, 준영속, 삭제)`를 관리합니다.
  - **1차 캐시**: 영속성 컨텍스트는 내부에 `1차 캐시`를 가지고 있습니다. 1차 캐시에는 조회한 엔티티들이 저장되며, 동일한 엔티티를 다시 조회하려고 할 때 `데이터베이스에 접근하지 않고` 1차 캐시에서 엔티티를 가져옵니다.
  - **동일성 보장**: 1차 캐시 덕분에 `동일한 트랜잭션`에서 데이터베이스의 동일한 엔티티를 두 번 조회하면, Java의 `참조 비교(==)`로 같은 것이라는 것을 보장할 수 있습니다.
  - **트랜잭션을 지원하는 쓰기 지연**: 영속성 컨텍스트는 트랜잭션이 커밋되는 시점까지 DB에 반영하지 않습니다. 이를 쓰기 지연이라 하며, 이를 통해 필요한 `SQL을 배치 처리`할 수 있습니다.
  - **변경 감지(Dirty Checking)**: 영속 상태의 `엔티티에 대한 모든 변경`은 영속성 컨텍스트에서 감지됩니다. 트랜잭션이 커밋되는 시점에 변경된 엔티티에 대한 `Update SQL`이 자동으로 실행됩니다.
  - **지연 로딩(Lazy Loading)과 즉시 로딩(Eager Loading)**: 영속성 컨텍스트는 엔티티의 `연관된 필드나 컬렉션`을 로딩하는 전략을 관리합니다. 이를 통해 `필요한 시점`에만 특정 데이터를 로딩할 수 있게 됩니다.
  - **캐스케이드(Cascade)**: 영속성 컨텍스트는 엔티티 간의 연관 관계에 설정된 `캐스케이드 옵션`을 처리합니다. 이를 통해 한 엔티티의 변경이 관련된 다른 엔티티에도 `전파될 수 있습니다.`

### Filter, Interceptor, AOP의 개념과 차이점
	필터(Filter),인터셉터(Interceptor) 그리고 AOP(Aspect-Oriented Programming)는 프로그래밍과 특히 웹 애플리케이션 개발에서 흔히 마주치는 개념들입니다.
	주로 애플리케이션의 핵심 로직에서 분리되어야 하는 공통된 작업(EX.로깅,보안,트랜잭션 처리 등)을 위해 사용됩니다.
**주요 개념**

1. **필터(Filter)**:
	- 주로 웹 애플리케이션에서 `요청과 응답`을 가로채는 역할을 합니다.
	- `HTTP` 요청이 서버로 들어오거나 나갈 때 특정 작업을 수행합니다.
	- EX: 인증 또는 인가, 요청/응답 로깅, 요청 데이터의 캐싱 및 압축 등.

2. **인터셉터(Interceptor)**:
	- 필터와 유사한 역할을 하지만, 주로 `프레임워크 수준`에서 제공하는 더 세밀한 메커니즘입니다.
	- 일반적으로 `액션 또는 라우트 수준`에서 작동하며, 특정 `액션이나 컨트롤러 메서드`가 실행되기 전 후로 로직을 삽입합니다.
	- EX: 사용자 세션 검사, 특정 페이지 접근 권한 확인 등.

3. **AOP(Aspect-Oriented Programming)**:
	- 관심사를 `핵심 로직에서 분리`하여 모듈화 하는 프로그래밍 패러다임입니다.
	- `Advice`라는 코드 조각을 `Pointcut`이라는 지정된 지점에 주입함으로써 작동합니다.
	- AOP는 메서드 호출 전후, 예외 발생 시점 등 다양한 지점에서 코드를 주집할 수 있습니다.
	- EX: 비즈니스 로직에 관한 로깅, 트랜잭션 관리, 보안 등.

**차이점**

1. **적용 범위**:<br/>
	필터는 주로 `웹 요청과 응답`에 관련된 작업에 사용되는 반면, 인터셉터는 `프레임워크` 수준의 작업에, AOP는 `애플리케이션 전반`의 공통된 작업에 사용됩니다.

2. **적용 지점**:<br/>
	필터는 `HTTP 요청/응답` 수준에서 작동하고, 인터셉터는 `프레임워크` 내 특정 액션 또는 라우트 수준에서 작동하며, AOP는 `애플리케이션 코드`의 특정 지점(EX:메서드 호출 전후)에서 작동합니다.

3. **복잡성**:<br/>
	필터와 인터셉터는 `비교적 간단한 작업`을 위해 설계되었으나, AOP는 더 `복잡한 공통 로직`을 애플리케이션 전반에 걸쳐 적용하기 위해 설계되었습니다.

![Filter,Interceptor,AOP](./image/filter_interceptor_aop.png)