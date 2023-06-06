# spring
```yaml
server:
	# 端口号
  port: 8080
spring:
	# 数据库
  datasource:
  	# 连接池(新版springboot自带hikari连接池)
    type: com.zaxxer.hikari.HikariDataSource
    # 驱动
    driver-class-name: com.mysql.cj.jdbc.Driver
    # 地址
    url: jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=UTF-8
    # 用户名
    username: root
    # 密码
    password: mysql
 	mvc:
 		# 自定义404错误信息
    throw-exception-if-no-handler-found: true
  web:
    resources:
      add-mappings: false


```

spring.datasource.url 可选参数（常用）：

- `useUnicode`：指定是否使用 Unicode 编码。
- `characterEncoding`：指定连接使用的字符编码。
- `serverTimezone`：指定连接使用的时区。



# mybatis-plus

```yaml
mybatis-plus:
  # mapper.xml
  mapper-locations: classpath:mappers/*.xml
  # 实体类别名
  type-aliases-package: com.banciyuan.pojo
  configuration:
    # 自动映射级别
    auto-mapping-behavior: full
    # 下划线转驼峰
    map-underscore-to-camel-case: true
```

自动映射级别：

- NONE：不进行自动映射，需要手动指定对象属性和表字段的映射关系。
- PARTIAL：只进行部分自动映射，自动映射对象属性名和表字段名相同的部分，需要手动指定其他映射关系。
- FULL：完全自动映射，自动映射对象属性名和表字段名相同的部分，并且自动映射驼峰式命名和下划线命名之间的映射关系。
