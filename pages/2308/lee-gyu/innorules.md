---
layout: cover
background: none
---

# innorules.xml

룰 시스템 Configuration\
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
- TCP를 이용하는 경우 연결은 유지되지만, HTTP/HTTPS의 경우 연결이 맺조 끊어짐

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
- 룰 서버는 룰 데이터의 일부 또는 전부를 캐시하여 메모리에 보관

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

# J2EE 룰 시스템 초기화

1. 웹 애플이케이션 배포 (`.war` 파일 또는 디렉터리 )
2. 배포된 디렉터리의 WEB-INF 디렉터리의 `web.xml` 파싱 (서블릿 기반 Deployment Descriptor)
3. `<servlet/>` 요소 정의된 서블릿 초기화 (`<load-on-startup/>` 요소의 우선 순위 순)
4. 기본적으로 아래와 같은 XML을 구성함

```xml
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
  <servlet-name>InnoRulesConfigurator</servlet-name>
  <url-pattern>/services/*</url-pattern>
</servlet-mapping>
```

---
layout: default
---

# innorules.xml 로드

- 룰 `InitializerChainServlet`에 파라미터로 정의된 `config-name` 요소 이름의 xml 파일을 읽음
- 해당 파일의 디렉터리 경로는 `config-path` 요소로 정의됨
- 빌더, 룰 엔진 등의 서비스 초기화를 위한 핵심 설정 정의

---
layout: default
---

# DataSource (JDBC)

---
layout: default
---
# 참고 자료

- 룰 시스템 컨셉 6.8
- 룰 시스템 아키텍트