- getInstance() 메소드 -> 싱글톤 방식으로 객체를 관리
: 앱이 시작될 때 최초 한번만 메모리를 할당한 후 그 메모리에 인스턴스를 만들어 사용하는 디자인 패턴
 ->매번 새롭게 DB를 인스턴스화해서 가져오는 것이 아님

- JSP, timeleaf : 템플릿 엔진, HTML문서에 동적으로 변경해야하는 부분만 자바코드 넣음
- HttpServletRequest에 request는 내부에 데이터 저장소가 있음 -> setRequest, getRequest 사용 가능
- dispatcher.forward : JSP로 이동할 수 있는 기능, 서버 내부에서 호출 발생
- WEB-INF : 외부에서 호출되지 않음, 항상 controller를 거쳐서 호출이 됨
- redicect VS forward : redirect는 실제 클라이언트(웹 브라우저)에 응답이 나갔다가, 클라이언트가 redirect경로로 다시 요청, URL경로도 실제로 ㄹ변경, 호출이 두번 일어남 / forward는 서버 내부에서 일어나는 호출(서버->서블릿->뷰), 클라이언트가 인지하지 못함
- Model은 HttpServletRequest객체
