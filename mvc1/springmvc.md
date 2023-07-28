### war VS jar
- war : 톰캣을 별도 설치할 때, JSP사용시
- jar : 내장 톰캣 사용, 'webapp'경로 사용하지 않음

### 로깅
- 운영에서는 system.out.println() 사용하지 않음
- SLF4J의 logback
```
log.trace
log.debug (개발 server)
log.info (운영 server)
log.warn
log.error
```
-> 설정은 application.properties에서
- private Logger log = LoggerFactory.getLogger(getClass()); = (lombok사용시) @SLF4J

### @Controller VS @RestController
- @Controller : 반환값이 String이면 뷰 이름으로 인식, 뷰를 찾고 뷰가 렌더링됨
- @RestController : Http메시지 바디에 바로 입력
