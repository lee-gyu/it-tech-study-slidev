---
layout: cover
background: none
---

# innorules.xml

이노룰스 7.3 룰 시스템 Configuration (빌더 + 룰 엔진)\
이규철

---
layout: default
---

# 룰 시스템 구성

룰 시스템의 기본 구성요소는 아래로 구성되어 있다.

- 룰 빌더 클라이언트
- 룰 빌더 서버
- 룰 저장소 (DB)
- 룰 서버
- 룰 애플리케이션 / 룰 API

![Rule Architecture](/lee-gyu/img/rule.png)

---
layout: default
---

# 룰 빌더 클라이언트 - 룰 빌더 서버

- HTTP, HTTPS 또는 TCP 통신으로 연결
- 웹 버전의 경우 HTTP/HTTPS로만 통신
- TCP를 이용하는 경우 연결은 유지되지만, HTTP/HTTPS의 경우 연결이 맺고 끊어짐

---
layout: default
---

# 룰 빌더 서버 - 룰 DB

- 빌더 서버는 JDBC를 이용하여 룰 DB에 접속 (Read/Write)
- 데이터베이스 연결은 데이터소스(커넥션 풀)로부터 획득
- 통신 프로토콜은 설정된 JDBC 드라이버의 프로토콜을 따름

---
layout: default
---

# 룰 서버 - 룰 DB

- 룰 서버는 룰 처리를 위해 룰 DB에 접속 (Read Only)
  - 룰 DB는 개발계 빌더를 통해서 Write가 가능하며, 검증계, 운영계는 이관을 통해 변경된다.
- 룰 서버는 룰 데이터의 일부 또는 전부를 캐시하여 메모리에 보관
- 룰 DB 동기화를 위한 메시지는 모니터 서버를 통해 수신 받는다.

---
layout: default
---

# 룰 빌더 서버 - 룰 서버

- 룰 서버는 빌더 서버와 연결하여 변경된 사항을 반영 (모니터 서버 연결)
- 빌더 서버는 룰 데이터 변경을, 모니터 연결을 이용하여 변경 내역 통지
- 룰 서버는 변경 내역을 이용하여 룰 저장소 캐시 갱신

---
layout: default
---

# 룰 애플리케이션 - 룰 서버

- 룰룰 애플리케이션은 룰 API의 메소드를 이용하여 룰 서비스 호출
- 직접 룰 API 라이브러리를 통해 호출하거나, TCP 등의 원격 호출을 통해 호출

---
layout: default
---

# 다단계 룰 시스템

- 개발 > 검증 > 운영과 같이 다단계로 룰 시스템을 구성할 수 있음
- 이관 작업을 통해 룰 시스템의 요소(항목, 룰)를 다음 단위 룰 시스템으로 이행
- 이관 시, 연관된 단위 시스템 DB에 모두 접근 가능해야 함.
- 이관의 제약
  - 한번에 하나의 단위 시스템만 이관 가능
  - 단위 시스템은 순환 참조 불가능 (예: 개발 → 운영 → 개발)
  - 단위 시스템의 변경(룰 저장, 이관)하는 빌더 서버는 하나여야 함

---
layout: default
---

# J2EE

룰 시스템은 J2EE 기반 아키텍처에서 동작한다.\
J2EE는 확장성, 보안성, 신뢰성, 분산형 컴포넌트 기반의 멀티 티어 애플리케이션 개발을 위한 플랫폼이다.

- Servlet: HTTP 요청을 처리하는 서버 사이드 컴포넌트
- JSP: 동적 웹 페이지를 생성하기 위한 기술. JSP 페이지는 서블릿으로 변환되어 실행.
- EJB: 확장가능한 분산형 기업용 애플리케이션을 위한 컴포넌트 기반 아키텍처
  - Session Bean: 클라이언트와 상호작용하는 비지니스 로직을 포함
  - Entity Bean: 데이터베이스와 상호작용하는 비지니스 로직을 포함
  - Message Driven Bean: 비동기 메시지를 처리하는 비지니스 로직을 포함
- JMS: 비동기 메시지를 생성, 소비, 전달하는 기술
- JTA: 트랜잭션 처리를 위한 API
- JNDI: 이름과 디렉터리를 이용하여 내부 자원을 찾는 기술
- JPA: 자바 개체와 관계형 데이터베이스를 매핑하는 기술

---
layout: default
---

# J2EE Application 배포

J2EE 애플리케이션은 일반적으로 J2EE 명세를 구현한 WAS(Web Application Server)에 배포된다.\
해당 명세를 구현한 WAS는 아래와 같은 종류가 있다.

- Oracle WebLogic
- IBM WebSphere
- Apache Tomcat
- TMAX JEUS

---
layout: default
---

# J2EE 룰 시스템 서블릿 설정

1. 웹 애플이케이션 배포 (`.war` 파일 또는 디렉터리 )
2. 배포된 디렉터리의 WEB-INF 디렉터리의 `web.xml` 파싱 (서블릿 기반 Deployment Descriptor)
3. `<servlet/>` 요소 정의된 서블릿 초기화 (`<load-on-startup/>` 요소의 우선 순위 순)
4. 기본적으로 아래와 같은 XML을 구성함

- 아래 `web.xml` 예제는 WAS 홈 디렉터리의 /{context-path}/WEB-INF/conf/innorules.xml 파일을 읽어들임

```xml {*} {maxHeight:'260px'}
<servlet>
  <servlet-name>InnoRulesConfigurator</servlet-name>
  <!-- 서블릿 초기화 클래스 -->
  <servlet-class>com.innoexpert.utility.initializer.InitializerChainServlet</servlet-class>
  <init-param>
    <!-- 설정파일 경로 -->
    <param-name>config-path</param-name>
    <param-value>/WEB-INF/conf</param-value>
  </init-param>
  <init-param>
    <!-- 설정파일 이름 -->
    <param-name>config-name</param-name>
    <param-value>innorules</param-value>
  </init-param>
  <!-- 서블릿 초기화 우선 순위 -->
  <load-on-startup>10</load-on-startup>
</servlet>

<servlet-mapping>
  <!-- <servlet/>에 정의된 servlet-name 매핑 -->
  <servlet-name>InnoRulesConfigurator</servlet-name>
  <!-- 서블릿 매핑 url 패턴-->
  <url-pattern>/services/*</url-pattern>
</servlet-mapping>
```

---
layout: default
---

# config xml 로드

- 룰 `InitializerChainServlet`에 파라미터로 정의된 `config-name` 요소 이름의 xml 파일을 읽음
- 해당 파일의 디렉터리 경로는 `config-path` 요소로 정의됨
- 빌더, 룰 엔진 등의 서비스 초기화를 위한 핵심 설정 정의
- 가장 root 요소는 `<innorules-server>` 요소로 정의됨.

---
layout: default
---

# config xml 구성 계층 요소

초기화 과정은 `com.innoexpert.utility.initializer.InitializerChainServlet` 서블릿 클래스에서 호출되며,\
실제 초기화 로직은 `com.innoexpert.utility.initializer.InitializerChainForWebapp` 클래스의 `initialize(configPath, configName, env, appctx)` 메소드에서 수행된다.
※ `innoutils` 프로젝트에서 확인 가능

- `<innorules-server/>`: 룰 서버의 root 요소
  - `<initializers/>`: 룰 시스템에서 사용되는 초기화 클래스를 정의 (각 Initializer에 xml 공유)
  - `<license/>`: 룰 서버의 라이센스 정보 (Seed256 암호화)
  - `<management/>`: `ManagementInitializer` 클래스
  - `<logging/>`: `LoggingInitializer` 클래스
  - `<jndi/>`: `JndiInitializer` 클래스
  - `<ruledb-validator/>`: `RuleDbValidator` 클래스
  - `<dbinfo-managers/>`: `DBInfoInitializer` 클래스
  - `<builder-service/>`: `BuilderServiceInitializer` 클래스
  - `<repositories/>`: `RepositoryInitializer` 클래스
  - `<irclient-clusters/>`: `RuleInterfaceClusterInitializer` 클래스

---
layout: default
---

# InitializerChainForWebapp.initialize()

서블릿에서 지정한 xml 경로의 내용을 파싱하여 JVM에 이노룰스 룰 서비스 클래스들을 초기화한다.\
configName이 null인 경우, `innorules`를 파일 이름으로 사용한다.\
만약 configName이 `classpath:`로 시작한다면 내부 클래스 로더 내 리소스 영역에서 xml 파일을 찾는다.

xml 파일은 `org.apache.axiom.om.OMXMLBuilderFactory`으로 파싱한다.\
초기화 과정은 아래 순서를 따른다.

1. 라이선스 확인
2. initializers 로드 (<intializers/> 요소에 정의된 순서대로 초기화)
3. 서비스 기동

---
layout: default
---

# `<management/>` innoutils/ManagementInitializer

J2EE의 MBean을 생성하여 WAS의 MBean 서버에 등록\
자바 기능을 모니터링하고 관리하기 위한 기능을 제공

※ 자세한 내용은 JMX 관련 문서 참고

---
layout: default
---

# `<logging/>` innoutils/LoggingInitializer

어떤 Logger를 사용할지 설정하는 요소\
log4j2를 이용한다면 `com.innorules.log.impl.log4j2.Log4jLogManager`를 class로 지정한다.\
내부에 정의된 `<configuration/>` 요소를 전달 받아 log4j2 설정을 수행한다. (log4j의 공식 문서의 설정과 동일)

---
layout: default
---

# `<jndi/>` innoutils/JndiInitializer

요소에 정의된 각 `<resource/>`를 jndi Context에 저장한다.\
`provider-urls`를 ","로 분할하여 각 요소에 저장한다.\
예: `DEV,@builder`라고 정의된 경우 `DEV`와 `@builder` 각각 저장한다.

기본적으로 `java.naming.factory.initial`과 `java.naming.provider.url`이 설정되며, 나머지는 `<resource/>`에 정의된 내용을 저장한다.

---
layout: default
---

# `<ruledb-validator/>` configuration-wizard/RuleDbValidator

현재 룰 DB 구성이 룰 시스템 DB에 올바른지 확인한다.\
`RULES010`테이블의 `R01_1`이 `SYSTEM`으로 지정된 `R01_2` 컬럼을 확인한다.\
여기서 시스템 ID가 `<ruledb-validator/>`에서 정의한 id와 동일하여야 한다.

---
layout: default
---

# `<dbinfo-managers>` innorulesj/DBInfoInitializer



---
layout: default
---
# 참고 자료

- 룰 시스템 컨셉 6.8
- 룰 시스템 아키텍트
- 이노룰스 7.3 기준 소스 분석