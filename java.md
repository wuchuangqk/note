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

# 日期格式化SimpleDateFormat

| yyyy：年                                           |
| -------------------------------------------------- |
| MM：月                                             |
| dd：日                                             |
| hh：12小时制(0-11)                                 |
| HH：24小时制(0-23)                                 |
| mm：分                                             |
| ss：秒                                             |
| S：毫秒                                            |
| E：星期几                                          |
| D：一年中的第几天                                  |
| F：一月中的第几个星期(会把这个月总共过的天数除以7) |
| w：一年中的第几个星期                              |
| W：一月中的第几星期(会根据实际情况来算)            |
| a：上下午标识                                      |
| k：和HH差不多，表示一天24小时制(1-24)。            |
| K：和hh差不多，表示一天12小时制(0-11)。            |
| z：表示时区                                        |

```java
Date d = new Date();
System.out.println(d);
// 要转换的格式
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
SimpleDateFormat sdf1 = new SimpleDateFormat(
  "一年中的第 D 天 一年中第w个星期 一月中第W个星期 E a 在一天中K时 z时区");
// 格式化日期，日期->字符串
String formatDate = sdf.format(d);
String formatDate1 = sdf1.format(d);
System.out.println(formatDate);
System.out.println(formatDate1);

String s = "2022-07-13 15:12:34 000";
try {
  Date date = sdf.parse(s);//格式化日期，字符串->日期
  System.out.println(date);
} catch (ParseException e) {
  e.printStackTrace();
}

```

# idea快捷键

| 快捷键         | 作用                               |
| -------------- | ---------------------------------- |
| ctrl + enter   | 自动补全变量名                     |
| sout           | System.out.print()                 |
| ctrl + o       | 实现接口的方法，或者覆盖父类的方法 |
| ctrl + enter   | 自动补全变量名                     |
| ctrl + alt + t | try-catch快捷键                    |
|                |                                    |
|                |                                    |
|                |                                    |
|                |                                    |

 

# javax

java和javax都是Java的API(Application Programming Interface)包，java是核心包，javax的x是extension的意思，也就是扩展包。java类库是java发布之初就确定了的基础库，而javax类库则是在上面增加的一层东西，就是为了保持版本兼容要保存原来的，但有些东西有了更好的解决方案，所以，就加上些，典型的就是awt(Abstract Windowing ToolKit) 和swing。

# 注解

## @WebServlet

```java
import javax.servlet.annotation.WebServlet;
```

```xml
<dependency>
  <groupId>javax.servlet</groupId>
  <artifactId>javax.servlet-api</artifactId>
  <version>3.0.1</version>
  <scope>provided</scope>
</dependency>
```

# IO流

IO流分字节流和字符流，字节流适合读写文件、二进制数据等；字符流适合读写文本文件

## 字节流

字节流基类（抽象类）：

- 输入流：InputStream，把数据从文件读到内存
- 输出流：OutputStream，把内存里的数据写入到文件

InputStream常用子类

- FileInputStream 

OutputStream常用子类

- FileOutputStream 



## 字符流

字节流基类（抽象类）：

- 输入流：Reader，把数据从文件读到内存
- 输出流：Write，把内存里的数据写入到文件



# 字符串

## StringBuffer和StringBuilder的区别

StringBuffer：可变字符串、效率低、线程安全；

StringBuilder：可变字符序列、效率高、线程不安全；
