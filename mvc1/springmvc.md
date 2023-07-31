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
- @RestController : Http메시지 바디에 바로 입력 <br><br>

- HttpEntity : HTTP header, body정보를 편리하게 조회, view조회하지 않음
- 비동기 통신 : 웹에서 화면전환 없이 이루어지는 동작들
- Model객체 : Modelrorcpsms Controller에서 생성된 데이터를 담아 view로 전달할 때 사용하는 객체
- @ModelAttribute : HTTP Body내용과 HTTP파라미터 값들을 Getter, Setter, 생성자를 통해 주입하기 위해 사용
- @RequestBody : HTTP 요청의 본문이 그대로 전달, 자바객체로 변환
- @ResponseBody : 자바객체를 HTTP요청의 바디내용으로 매핑하여 클라이언트로 전송

