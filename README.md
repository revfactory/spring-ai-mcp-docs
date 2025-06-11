# Spring AI MCP 한글 문서

Spring AI MCP(Model Context Protocol)에 대한 한국어 문서화 프로젝트입니다.

## 📖 프로젝트 소개

이 프로젝트는 Spring AI의 Model Context Protocol(MCP) 기능을 한국어로 문서화하여 한국 개발자들이 쉽게 이해하고 활용할 수 있도록 돕습니다.

## 📁 프로젝트 구조

```
├── README.md                    # 프로젝트 설명 (이 파일)
├── spring-ai-mcp-정리.md        # MCP 한글 문서 (마크다운)
├── index.html                   # MCP 한글 문서 (웹 페이지)
└── urls.txt                     # 공식 문서 참조 링크
```

## 🚀 문서 보기

### 웹 페이지 버전
`index.html` 파일을 브라우저에서 열어 아름다운 핑크 테마의 웹 문서를 확인할 수 있습니다.

### 마크다운 버전
`spring-ai-mcp-정리.md` 파일에서 마크다운 형식의 문서를 확인할 수 있습니다.

## 📋 문서 내용

### MCP Client Boot Starter
- Spring Boot 애플리케이션에서 MCP 클라이언트 기능을 위한 자동 구성
- 동기 및 비동기 클라이언트 지원
- 다양한 전송 옵션 (STDIO, SSE)

### MCP Server Boot Starter  
- Spring Boot 애플리케이션에서 MCP 서버 설정을 위한 자동 구성
- STDIO, WebMVC, WebFlux 전송 지원
- 도구, 리소스, 프롬프트 관리 기능

### MCP Helpers
- Spring AI와 MCP 통합을 위한 유틸리티
- ToolCallback 및 McpToolUtils 제공
- GraalVM Native Image 지원

## 🔗 공식 문서 링크

- [MCP Client Boot Starter 공식 문서](https://docs.spring.io/spring-ai/reference/api/mcp/mcp-client-boot-starter-docs.html)
- [MCP Server Boot Starter 공식 문서](https://docs.spring.io/spring-ai/reference/api/mcp/mcp-server-boot-starter-docs.html)
- [MCP Helpers 공식 문서](https://docs.spring.io/spring-ai/reference/api/mcp/mcp-helpers.html)

## 🤝 기여하기

이 문서에 오타나 개선 사항이 있다면 언제든지 이슈를 생성하거나 풀 리퀘스트를 보내주세요.

## 📄 라이선스

이 프로젝트는 [MIT 라이선스](LICENSE) 하에 배포됩니다.

---

**Spring AI MCP**는 Model Context Protocol을 Spring Boot 애플리케이션에 통합하기 위한 포괄적인 솔루션을 제공합니다. 🚀