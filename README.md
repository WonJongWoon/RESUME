# 프로필

- 이름: 원종운
- 생일: 1996.07.15
- 지역: 서울

저의 개발 모토는 "Make it Work, Make it Right, Make it Fast" 입니다. 고민을 하는 것은 좋은 행동이지만, 많은 고민만 하게 되면 전진할 수 없습니다. 빠르게 시도하여 동작하게 만들고, 그것이 올바르게 동작하도록 만들고, 빠르게 동작하게 만듭니다. 

저는 트러블 슈팅에 강하며, 동료에게 Geek 하다는 이야기를 많이 듣습니다. 문제가 발생하였을 때, 끊임없이 파고 들며, 원인을 찾아 정답이 아니더라도 해답을 제시하고자합니다.
애플리케이션 레벨의 개발뿐만 아니라, 애플리케이션이 동작하는 클라우드와 같은 인프라에도 관심이 많습니다.

# 기술

## 언어

- Java, Kotlin, Gradle
- Golang
- TypeScript

## 인프라

- Linux
- Docker
- Vector
- AWS, K8S

## 기타

- Spring Boot, JPA(Hibernate), Jenkins
- MySQL
- Git
- React
- 학습한 내용을 기록합니다.
  - <https://jongwoon.tistory.com/>
  - <https://woony.hashnode.dev/>

# 학력

## 부경대학교

- 부산
- 주전공: 컴퓨터공학과
- 2016.03 ~ 2022.02
- 누적 평점 4.16/4.5
- 전공 평점 4.27/4.5
  - [관련 수업 이수 내역](./COURSE.md)

# 경력

## [버킷플레이스](https://www.bucketplace.com/) 정규직

- 2022.05 ~ 재직 중
- Core Platform Engineer
- 전사 엔지니어링 조직이 공통적으로 사용해야 하는 인프라 플랫폼 및 서비스(라이브러리) 개발

### 로깅 파이프라인 플랫폼 개발

- 사용 기술 : Kotlin, Quarkus, Kafka(Schema Registry), Vector
- 시스템 로그 및 전사 서비스 애플리케이션에서 발생하는 로그를 수집 및 분류하는 로깅 파이프라인 플랫폼을 개발하였습니다.
- K8s 환경에서 동작하는 전사 서비스 애플리케이션에서 발생하는 로그를 수집하기 위한 전사 로깅 에이전트(Vector)를 배포하고 파이프라인을 개발 및 운영하였습니다.
   - Vector Agent 를 이용하여 K8s 환경에서 각 Pod 에서 발생하는 로그들을 수집하고, 수집 대상이 되는 로그를 검사하여, 전사 로그 수집 Kafka Topic 으로 전달하는 파이프라인을 구성하였습니다.
   - 전반적인 K8s 로깅 아키텍처 및 전사 로그의 수집 경로 등의 지식을 사내 전파를 위한 발표도 진행하였습니다.
- 위 단계에서, 수집된 로그들이 유효한 스키마를 가지는지 검증하고, 로그 소비자들을 위하여 특정 토픽으로 분류하여 주는 컨슈머 애플리케이션을 개발하였습니다.
   - 수집된 로그를 소비하여, 해당 로그가 정해진 스키마를 준수(Schema Evoluation) 하는지, 해당 로그의 프로퍼티를 기준으로 소비자를 확인하여 특정 규칙에 맞게 다른 토픽으로 분류하여 줍니다.
   - 사용자 입장에서 어떻게 로그를 발생하고, 어떻게 원하는 토픽으로 수집할 수 있는지 개발자들을 대상으로 Demo Day 및 발표도 진행하였습니다.
- 전사 서비스 애플리케이션에서 남기는 로그가 플랫폼의 수집 대상이 되기 위하여 필요한 Logging SDK를 개발하였습니다.
   - Slf4j, Logback 을 이용하여 Logger 와 Appdender를 개발하여, 사용자가 남기는 로그를 구조화하고, 플랫폼에 필요한 정보를 쉽게 추가할 수 있도록 제공하였습니다.

### Feature Flag 라이브러리 개발

- 사용 기술 : Kotlin, Gradle, ETCD
- 코드의 변경 없이 동적으로 기능을 변경할 수 있는 [Feature Flag](https://martinfowler.com/articles/feature-toggles.html) 라이브러리를 개발하였습니다.
  - 준 실시간으로 Feature Flag의 값을 라이브러리 내에서 제공하기 위하여 ETCD Storage의 Watch를 사용한, 로컬 캐시를 구현하여, 빠른 응답성을 제공하고자 노력하였습니다.
- Kotlin에서 Feature Flag를 쉽게 제어하고 사용할 수 있도록 하는 라이브러리 및 Gradle Plugin 을 개발하였습니다.
  - Gradle Plugin 을 통하여, 사용자가 문자열 기반으로 플래깅(일반적인 오픈 소스들의 사용 방법)을 제어하는 휴먼 에러 등을 방지할 수 있도록 컴파일 타임에 사용하고자 하는 Feature에 대한 정보를 바탕으로 클래스를 생성하여 사용성 및 생산성을 개선하였습니다.
- 사용자에게 노출되는 API는 최소한으로 공개하는 형태로 접근하되, 확장성 있는 기능 추가를 주로 고려하여 개발을 진행하였습니다.

### 사내 표준 메타데이터 전파 라이브러리 개발

- 사용 기술 : Kotlin, Spring WebFlux(WebMvc), gRPC(Armeria, gRPC-Kotlin)
- MSA 환경에서 여러 마이크로서비스간의 컨텍스트(정보) 전파를 위한 라이브러리 개발하였습니다.
- 기존에는 여러 채널(HTTP Header, HTTP Cookie, HTTP Request Body, HTTP Query)로 파편화되어 전달되어, 이전 서비스가 어떠한 채널을 통하여 정보를 전달하였는지에 따라 컨텍스트 정보를 조회하는데 어려움이 발생하거나 유실이 발생하였습니다. 이를 하나의 채널(HTTP Header)로 통일하여 전파함으로써 해결하였고, 어느 요청 지점 내에서도 동일한 채널을 통하여 관련 컨텍스트 정보를 조회할 수 있도록 보장하였습니다.
- 또한, 기존 Thread Per Request 모델(WebMvc)에서는 하나의 요청이 모두 하나의 Thread에서 처리되는 형태이지만, WebFlux 및 gRPC의 경우 Reactive Stream 스펙을 준수하며, 해당 모델은 하나의 요청이 여러 Thread를 옮겨가면서 처리될 수 있습니다. 이 경우 관습적인 방법(ThreadLocal)으로 많은 컨텍스트 정보가 유실될 수 있습니다. 이러한 Thread Switching 을 고려하여 여러 Thread 간의 Switching 이 일어나더라도 컨텍스트 정보가 유실되지 않도록 Request Scoping 처리하였습니다.
   - 또한 이러한 Request Scoping 을 위하여 각 기술 스택에서는 각기 다른 자료구조와 방법을 사용하기 때문에 동일한 인터페이스를 통하여 접근하기 어렵다는 Pain Point 가 존재하였고, 이 부분을 모든 기술 스택에서 동일한 자료구조와 동일한 인터페이스를 사용할 수 있도록 추상화하여 제공하여 해결하였고, 따라 사용자는 기술 스택과 상관없이 동일하게 사용할 수 있게 되었습니다.
      - WebFlux는 Project Reactor를 사용하며, 해당 Project Reactor에서 제공하는 Hook 기능을 통하여, Request Scoping 처리를 하였습니다.

## [버킷플레이스](https://www.bucketplace.com/) 인턴

- 2022.02 ~ 2022.05
- Core Platform Engineer

### 안심번호 서비스 개발

- 사용 기술 : Kotlin, Spring Boot, Redis, MySQL, React
- 사용자의 사생활/개인정보 보호를 위한 050 안심번호 발급 API 서버를 개발하였습니다.
- 사용자들이 동일한 안심번호 발급을 받지 않도록 Redis를 큐형태로 사용 및 원자적 연산을 이용하여 동시성을 제어하였습니다.
- 로컬 트랜잭션과 외부 API 연동에서 발생할 수 있는 롤백 문제 및 커넥션 고갈 등의 이슈를 해소하기 위하여 트랜잭션을 분리하여 처리하였습니다.
- VoC 처리를 위하여 안심번호 발급/해지 등의 히스토리를 MySQL에 기록하고, 관련 내용을 쉽게 조회할 수 있도록 사내 어드민을 개발하였습니다.


# 프로젝트

## Gogooma

- 2021.01 ~ 2021.02
- Kotlin, Spring Boot, Spring Security, Spring Data JPA
- 현대인들의 연애 고민을 공유하여 이야기함으로서 해소를 도와주는 커뮤니티
- 팀장 및 백엔드 파트 전체를 맡아 프로젝트를 진행하였습니다.
- [발표 동영상](https://youtu.be/shzG5MkYtOM?t=2651)

# 언어

- 한국어

# 링크

- email: <wolfram_alpha@naver.com>
- [Blog](https://jongwoon.tistory.com/)
- [GitHub](https://github.com/WonJongWoon)
- [LinkedIn](https://www.linkedin.com/in/woony-won/)
