# pom坐标

当前最新版：3.5.3.1

```xml
<dependency>
  <groupId>com.baomidou</groupId>
  <artifactId>mybatis-plus-boot-starter</artifactId>
  <version>3.5.3.1</version>
</dependency>
```

# 扫描mapper

启动类添加`@MapperScan`注解

```java
@SpringBootApplication
@MapperScan("com.baomidou.mybatisplus.samples.quickstart.mapper")
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

如果不在启动类加`MapperScan`扫描的话，就要在每个Mapper接口上加`@Mapper`注解

# BaseMapper

```java
import com.baomidou.mybatisplus.core.mapper.BaseMapper;
import com.example.demo.pojo.User;

@Repository
public interface UserMapper extends BaseMapper<User> {

}
```

新建mapper接口继承BaseMapper，mybatis-plus会自动提供实现类。

`@Repository`注解用来告诉spring，把这个类注册成一个Bean，`@Component`注解是更通用的注解，包含`@Repository`,`@Service`



```java
@SpringBootTest
public class SampleTest {

    @Autowired
    private UserMapper userMapper;

    @Test
    public void testSelect() {
        System.out.println(("----- selectAll method test ------"));
        List<User> userList = userMapper.selectList(null);
        Assert.assertEquals(5, userList.size());
        userList.forEach(System.out::println);
    }

}
```

