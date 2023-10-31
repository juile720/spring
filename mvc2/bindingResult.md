### BindingResult

- Spring에서 제공하는 Field Type, 프로그래머가 직접 작성한 FieldError, ObjectError를 한데 묶어(List) Model에 주입시켜주는 통합 인터페이스
- Model에 주입이 되어 Thymeleaf 같은 뷰 템플릿에 넘겨주어서 사용할 수 있으며, addError 메서드를 통해 프로그래머가 직접 작성한 에러 메시지를 넣을 수 있게 기능을 지원

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
