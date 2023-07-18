- Http 요청 -> FrontController(매핑정보 확인) -> Controller -> JSP -> HTML응답
- controller interface 생성, interface를 구현하는 controller구현체들을 Override로 생성,
FrontController에서 어떤 url을 받는지 확인 후 매핑되는 controller구현체로 보내줌
