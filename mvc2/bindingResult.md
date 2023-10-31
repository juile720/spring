### BindingResult

- Spring에서 제공하는 Field Type, 프로그래머가 직접 작성한 FieldError, ObjectError를 한데 묶어(List) Model에 주입시켜주는 통합 인터페이스
- Model에 주입이 되어 Thymeleaf 같은 뷰 템플릿에 넘겨주어서 사용할 수 있으며, addError 메서드를 통해 프로그래머가 직접 작성한 에러 메시지를 넣을 수 있게 기능을 지원
