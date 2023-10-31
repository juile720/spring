### BindingResult

Spring에서 제공하는 Field Type, 프로그래머가 직접 작성한 FieldError, ObjectError를 한데 묶어(List) Model에 주입시켜주는 통합 인터페이스이다.

Model에 주입이 되어 Thymeleaf 같은 뷰 템플릿에 넘겨주어서 사용할 수 있으며, addError 메서드를 통해 프로그래머가 직접 작성한 에러 메시지를 넣을 수 있게 기능을 지원한다.

Spring에서 기본적으로 사용하는 구현체는 BeanPropertyBindingResult이다.

### BindingResult Interface

```
package org.springframework.validation;

public interface BindingResult extends Errors {
    // ...
    private final List<ObjectError> errors = new ArrayList<>();
    // ...
    void addError(ObjectError error);
    // ...
}
```
- Errors 인터페이스를 상속받은 인터페이스이다.
- Errors 인터페이스는 단순히 에러의 저장과 조회 기능을 제공하는데,
  BindingResult는 addError() 등, 추가적인 기능을 제공한다.
- Spring에서 코드를 작성할 때는 BindingResult를 사용하며,
  컴파일때 BeanPropertyBindingResult 구현체를 기본으로 주입한다.
- @RequestParam, @ModelAttribute에서 바인딩 에러가 발생하는 경우,
  BindingResult에 해당 에러의 내용이 담긴다.
- Controller의 Argument로 BindingResult를 넘길 수 있다.

### ObjectError

```
public class ObjectError extends DefaultMessageSourceResolvable {

    public ObjectError(
            String objectName, 
            String defaultMessage
    ) {
        this(objectName, null, null, defaultMessage);
    }

    public ObjectError(
            String objectName, 
            @Nullable String[] codes, 
            @Nullable Object[] arguments, 
            @Nullable String defaultMessage
    ) {
        super(codes, arguments, defaultMessage);
        Assert.notNull(objectName, "Object name must not be null");
        this.objectName = objectName;
    }

}
```
- String objectName
    에러 이름을 작성한다.
    여기에 작성된 값이 Model에 key 값으로 전달된다.
    ${objectName}
- @Nullable String defaultMessage
    에러가 났을 경우, 출력되는 기본 메시지
    여기에 작성된 값이 Model에 value 값으로 전달된다.
- @Nullable String[] codes
    메시지 기능을 이용할 때 사용하는 값이다.
    errors.properties에서 key 값를 찾는다.
    만약 key도 없고 errors.properties도 없는 경우, defaultMessage를 출력한다.
    defaultMessage도 없는 경우, ObjectError에서 제공되는 기본 메시지를 보여준다.
- @Nullable Object[] arguments
    메시지 기능을 이용할 때 사용하는 값이다.
    errors.properties에서 찾은 value 값의 인자({0}, {1})를 전달한다.

### FieldError

```
public class FieldError extends ObjectError {

    public FieldError(
            String objectName, 
            String field, 
            String defaultMessage
    ) {
        this(objectName, field, null, false, null, null, defaultMessage);
    }

    public FieldError(
            String objectName, 
            String field, 
            @Nullable Object rejectedValue, 
            boolean bindingFailure,
            @Nullable String[] codes, 
            @Nullable Object[] arguments, 
            @Nullable String defaultMessage
    ) {
        super(objectName, codes, arguments, defaultMessage);
        Assert.notNull(field, "Field must not be null");
        this.field = field;
        this.rejectedValue = rejectedValue;
        this.bindingFailure = bindingFailure;
    }
}
```
- ObjectError를 상속받은 구현체이다.
- objectName, codes, arguments, defaultMessage는 ObjectError의 설명과 같다.
- String field
    오류가 발생한 field(변수 명)의 이름을 작성한다.
    objectName에 입력했던 Model Key 값의 하위 Field로 들어간다.
    ${objectName.field}
- @Nullable Object rejectedValue
    어떤 값을 시도해서 실패했는지 작성해야 할 때 사용.
- boolean bindingFailure
    현재 이 오류가 바인딩 실패(Type 불일치)인지 나타낼 때 사용.
