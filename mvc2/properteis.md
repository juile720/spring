### 메시지

messages.properties파일에 메시지 관리 내용을 입력
item.itemName=상품명

HTML파일에서 아래와 같이 사용
<label for="itemName" th:text="#{item.itemName}"></label>

### 국제화

messages_en.properties
item.itemName=Item Name

스프링 부트를 사용하면 스프링 부트가 MessageSource 를 자동으로 스프링 빈으로 등록한다.
