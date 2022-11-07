# .class

获取类的class对象

```java
SpringApplication.run(MaidApplication.class, args);
```

# 数组初始化

```java
int[] arr = new int[]{1, 2, 3};
String[] arr1 = new String[]{"1", "2", "3"};
int[] arr2 = {1, 2, 3};
String[] arr3 = {"1", "2", "3"};
Student[] arr4 = new Student[]{new Student(), new Student()};
Student[] arr5 = {new Student(), new Student()};
```

# 自定义404返回信息

```properties
spring.mvc.throw-exception-if-no-handler-found=true
spring.web.resources.add-mappings=false
```

```java
@RestControllerAdvice
public class GlobalExceptionHandler {
  @ExceptionHandler(NoHandlerFoundException.class)
  public String noHandlerFoundException(NoHandlerFoundException e, HttpServletRequest request) {
    System.out.println(e);
    System.out.println(request);
    return "胜多负少";
  }
}
```

