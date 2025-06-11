# Spring AI MCP (Model Context Protocol) 문서 정리

## 목차
1. [MCP Client Boot Starter](#mcp-client-boot-starter)
2. [MCP Server Boot Starter](#mcp-server-boot-starter)
3. [MCP Helpers](#mcp-helpers)

---

## MCP Client Boot Starter

### 개요
- MCP(Model Context Protocol) Client Boot Starter는 Spring Boot 애플리케이션에서 MCP 클라이언트 기능을 위한 자동 구성을 제공합니다
- 동기 및 비동기 클라이언트 구현을 지원합니다
- 다양한 전송 옵션과 클라이언트 관리 기능을 제공합니다

### 주요 스타터

#### 1. 표준 MCP 클라이언트
- **의존성**: `spring-ai-starter-mcp-client`
- STDIO 및/또는 SSE 전송을 통해 MCP 서버에 연결

#### 2. WebFlux 클라이언트
- **의존성**: `spring-ai-starter-mcp-client-webflux`
- WebFlux 기반 SSE 전송 구현 사용

### 구성 속성
- 공통 속성 접두사: `spring.ai.mcp.client`
- 구성 가능한 설정:
  - 클라이언트 활성화/비활성화 상태
  - 클라이언트 이름 및 버전
  - 요청 타임아웃
  - 클라이언트 타입 (SYNC 또는 ASYNC)
  - 전송별 구성

### 주요 기능
- 동기 및 비동기 클라이언트 타입 지원
- 콜백 인터페이스를 통한 광범위한 클라이언트 커스터마이징
- 다중 전송 지원 (Stdio, SSE HTTP, SSE WebFlux)
- Spring AI의 도구 실행 프레임워크와의 통합

### 예제 구성
```yaml
spring:
  ai:
    mcp:
      client:
        enabled: true
        name: my-mcp-client
        type: SYNC
        sse:
          connections:
            server1:
              url: http://localhost:8080
```

### 커스터마이징 옵션
- `McpSyncClientCustomizer` 또는 `McpAsyncClientCustomizer` 구현
- 커스터마이징 가능한 항목:
  - 요청 타임아웃
  - 루트 액세스
  - 샘플링 핸들러
  - 이벤트 핸들러
  - 로깅 핸들러

---

## MCP Server Boot Starter

### 개요
- MCP(Model Context Protocol) Server Boot Starter는 Spring Boot 애플리케이션에서 MCP 서버 설정을 위한 자동 구성을 제공합니다
- 동기 및 비동기 작동 모드를 지원합니다
- 다양한 전송 계층 옵션을 제공합니다

### 스타터 옵션

#### 1. 표준 MCP 서버 (STDIO 전송)
- **의존성**: `spring-ai-mcp-server-spring-boot-starter`
- 커맨드라인 및 데스크톱 도구에 적합

#### 2. WebMVC 서버 전송 (Spring MVC를 사용한 SSE)
- **의존성**: `spring-ai-starter-mcp-server-webmvc`
- Server-Sent Events를 사용한 HTTP 기반 전송 제공

#### 3. WebFlux 서버 전송 (반응형 SSE)
- **의존성**: `spring-ai-starter-mcp-server-webflux`
- Spring WebFlux를 사용한 반응형 전송 제공

### 주요 기능
- 도구 관리
- 리소스 관리
- 프롬프트 관리
- 완성 관리
- 변경 알림 지원

### 구성 속성
- 접두사: `spring.ai.mcp.server`
- 구성 가능한 옵션:
  - 서버 활성화/비활성화
  - 전송 모드
  - 서버 이름 및 버전
  - 기능 토글
  - 타임아웃 설정

### 서버 타입
- 동기 (기본값)
- 비동기 (논블로킹 작업용)

### 예제 구성
```yaml
spring:
  ai:
    mcp:
      server:
        name: webmvc-mcp-server
        version: 1.0.0
        type: SYNC
        instructions: "날씨 정보를 제공하는 서버"
```

### 사용 예제
```java
@SpringBootApplication
public class McpServerApplication {
    @Bean
    public ToolCallbackProvider weatherTools(WeatherService weatherService) {
        return MethodToolCallbackProvider.builder()
            .toolObjects(weatherService)
            .build();
    }
}
```

---

## MCP Helpers

### 개요
- Spring AI 애플리케이션과 Model Context Protocol 통합을 위한 기초 지원 제공
- Spring AI의 도구 시스템과 MCP 서버 간의 통신 활성화
- 동기 및 비동기 작업 모두 지원

### 주요 컴포넌트

#### 1. ToolCallback 유틸리티
- MCP 도구를 Spring AI의 도구 인터페이스에 적응시킴
- 동기 및 비동기 실행 모두 지원
- 제공하는 메서드:
  - 도구 콜백을 도구 명세로 변환
  - MCP 클라이언트에서 도구 콜백 검색

#### 2. McpToolUtils
- 도구 콜백을 도구 명세로 변환
- 동기 및 비동기 도구 명세 모두 지원
- MCP 클라이언트에서 도구 콜백 추출 가능

#### 3. Native Image 지원
- `McpHints` 클래스가 GraalVM native image 힌트 제공
- MCP 스키마 클래스에 대한 리플렉션 힌트 자동 등록

### 코드 예제

#### 동기 도구 콜백 생성:
```java
McpSyncClient mcpClient = // MCP 클라이언트 획득
Tool mcpTool = // MCP 도구 정의 획득
ToolCallback callback = new SyncMcpToolCallback(mcpClient, mcpTool);
```

#### 비동기 도구 콜백 생성:
```java
McpAsyncClient mcpClient = // MCP 클라이언트 획득
Tool mcpTool = // MCP 도구 정의 획득
ToolCallback callback = new AsyncMcpToolCallback(mcpClient, mcpTool);
```

### 요약
유틸리티는 Spring AI 애플리케이션에서 통합을 단순화하고 유연한 도구 관리를 제공하도록 설계되었습니다.

---

## 전체 요약

Spring AI MCP는 Model Context Protocol을 Spring Boot 애플리케이션에 통합하기 위한 포괄적인 솔루션을 제공합니다. 클라이언트와 서버 모두를 위한 자동 구성, 다양한 전송 옵션, 그리고 Spring AI의 기존 도구 시스템과의 원활한 통합을 제공합니다. 이 문서는 동기 및 비동기 작업, 다양한 전송 메커니즘, 그리고 광범위한 커스터마이징 옵션을 지원하여 개발자가 강력한 AI 기반 애플리케이션을 구축할 수 있도록 합니다.