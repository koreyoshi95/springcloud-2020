# SpringCloud

# 一、介绍

## （一）cloud和boot之间的依赖关系

https://spring.io/projects/spring-cloud#overview

- Finchley 是基于 Spring Boot 2.0.x 构建的不再 Boot 1.5.x
- Dalston 和 Edgware 是基于 Spring Boot 1.5.x 构建的，不支持 Spring Boot 2.0.x
- Camden 构建于 Spring Boot 1.4.x，但依然能支持 Spring Boot 1.5.x

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123024227971.png" alt="image-20220123024227971" style="zoom: 80%;" />

更详细的版本对应查看方法：https://start.spring.io/actuator/info

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123024323186.png" alt="image-20220123024323186" style="zoom: 80%;" />

## （二）课程所用软件版本

1. cloud：Hoxton.SR1
2. boot：2.2.2.RELEASE
3. cloud alibaba：2.1.0.RELEASE
4. Java：Java8
5. Maven：3.5及以上
6. Mysql：5.7及以上
   
   

题外话：boot版已经到2.2.4为最新，为什么选2.2.2？

1. 如果项目中只用到 boot，直接用最新
2. 同时用boot和cloud，需要照顾cloud，由cloud决定boot版本

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123024608286.png" alt="image-20220123024608286" style="zoom: 80%;" />

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123024911535.png" alt="image-20220123024911535" style="zoom: 80%;" />

SpringCloud和SpringBoot版本对应关系

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123024939313.png" alt="image-20220123024939313" style="zoom: 80%;" />

## （三）Cloud各种组件的停更/升级/替换

以前：

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123025134516.png" alt="image-20220123025134516" style="zoom: 80%;" />

现在（2020年）：



![1641811794746](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/1641811794746.png)

# 二、微服务架构编码构建

约定 > 配置 > 编码

## （一）IDEA新建project工作空间

### 1、微服务cloud整体聚合父工程Project

#### （1）New Project

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220118235307862.png" alt="image-20220118235307862" style="zoom: 80%;" />

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220119000150639.png" alt="image-20220119000150639" style="zoom: 80%;" />

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220118235822453.png" alt="image-20220118235822453" style="zoom: 80%;" />

#### （2）字符编码

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220119000408237.png" alt="image-20220119000408237" style="zoom: 80%;" />

#### （3）注解生效激活

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/1641812377112.png" alt="1641812377112" style="zoom: 80%;" />

#### （4）java编译版本选8

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/1641809624397.png" alt="1641809624397" style="zoom: 80%;" />

#### （5）File Type过滤

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220119000546392.png" alt="image-20220119000546392" style="zoom: 80%;" />

### 2、父工程POM

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.atguigu.springcloud</groupId>
    <artifactId>mscloud</artifactId>
    <version>1.0-SNAPSHOT</version>
    <modules>
        <module>cloud-provider-payment8001</module>
    </modules>
    <packaging>pom</packaging>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
        <junit.version>4.12</junit.version>
        <log4j.version>1.2.17</log4j.version>
        <lombok.version>1.16.18</lombok.version>
        <mysql.version>5.1.47</mysql.version>
        <druid.version>1.1.16</druid.version>
        <mybatis.spring.boot.version>1.3.0</mybatis.spring.boot.version>
    </properties>

    <!-- 子模块继承之后，提供作用：锁定版本+子modlue不用写groupId和version  -->
    <dependencyManagement>
        <dependencies>
            <!--spring boot 2.2.2-->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.2.2.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <!--spring cloud Hoxton.SR1-->
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>Hoxton.SR1</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <!--spring cloud alibaba 2.1.0.RELEASE-->
            <dependency>
                <groupId>com.alibaba.cloud</groupId>
                <artifactId>spring-cloud-alibaba-dependencies</artifactId>
                <version>2.1.0.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
            <dependency>
                <groupId>mysql</groupId>
                <artifactId>mysql-connector-java</artifactId>
                <version>${mysql.version}</version>
            </dependency>
            <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>druid</artifactId>
                <version>${druid.version}</version>
            </dependency>
            <dependency>
                <groupId>org.mybatis.spring.boot</groupId>
                <artifactId>mybatis-spring-boot-starter</artifactId>
                <version>${mybatis.spring.boot.version}</version>
            </dependency>
            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>${junit.version}</version>
            </dependency>
            <dependency>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
                <version>${log4j.version}</version>
            </dependency>
            <dependency>
                <groupId>org.projectlombok</groupId>
                <artifactId>lombok</artifactId>
                <version>${lombok.version}</version>
                <optional>true</optional>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <finalName>mscloud</finalName>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>2.3.5.RELEASE</version>
                <configuration>
                    <fork>true</fork>
                    <addResources>true</addResources>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

如果有依赖下载不下来就先把 pom 文件中的`<dependencyManagement>` 注释掉，等下载完成后在取消注释即可



### 3、Maven工程落地细节复习

**Maven中的DependencyManagement和Dependencies**

dependencyManagement：

Maven 使用dependencyManagement 元素来提供了一种管理依赖版本号的方式。通常会在一个组织或者项目的最顶层的父POM 中看到dependencyManagement 元素。

使用pom.xml 中的dependencyManagement 元素能让所有在子项目中引用一个依赖而不用显式的列出版本号。

Maven 会沿着父子层次向上走，直到找到一个拥有dependencyManagement 元素的项目，然后它就会使用这个
dependencyManagement 元素中指定的版本号。

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/1641813022727.png" alt="1641813022727" style="zoom:80%;" />

这样做的好处就是：如果有多个子项目都引用同一样依赖，则可以避免在每个使用的子项目里都声明一个版本号，这样当想升级或切换到另一个版本时，只需要在顶层父容器里更新，而不需要一个一个子项目的修改；另外如果某个子项目需要另外的一个版本，只需要声明version就可。

*  dependencyManagement 里只是声明依赖，并不实现引入，因此子项目需要显示的声明需要用的依赖

*  如果不在子项目中声明依赖，是不会从父项目中继承下来的；只有在子项目中写了该依赖项，并且没有指定具体版本，才会从父项目中继承该项，并且version和scope都读取自父pom

*  如果子项目中指定了版本号，那么会使用子项目中指定的jar版本
  
  

**maven中跳过单元测试**

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220119001152702.png" alt="image-20220119001152702" style="zoom:80%;" />

**父工程创建完成执行mvn:install将父工程发布到仓库方便子工程继承**



## （二）Rest微服务工程构建

### 1、支付模块8001

cloud-provider-payment8001 微服务提供者支付Module模块

建 cloud-provider-payment8001

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220119221007002.png" alt="image-20220119221007002" style="zoom: 80%;" />

创建完成后请回到父工程查看pom文件变化

![image-20220119221119247](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220119221119247.png)

#### （1）改POM

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-provider-payment8001</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <!--mysql-connector-java-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
        <!--jdbc-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```

#### （2）写YML

application.yml

```yaml
server:
  port: 8001

spring:
  application:
    name: cloud-payment-service
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource            # 当前数据源操作类型
    driver-class-name: org.gjt.mm.mysql.Driver              # mysql驱动包 com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/springcloud2021?useUnicode=true&characterEncoding=utf-8&useSSL=false
    username: root
    password: root

mybatis:
  mapperLocations: classpath:mapper/*.xml
  type-aliases-package: com.atguigu.springcloud.entities    # 所有Entity别名类所在包
```



#### （3）主启动

```java
package com.atguigu.springcloud;

@SpringBootApplication
public class PaymentMain8001 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain8001.class,args);
    }
}
```



#### （4）建表

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220119222549864.png" alt="image-20220119222549864" style="zoom: 80%;" />

```mysql
CREATE TABLE `payment` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT 'ID',
  `serial` varchar(200) DEFAULT '',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8
```



#### （5）entities

主实体 Payment

```java
package com.atguigu.springcloud.entities;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class Payment implements Serializable {
    private Long id;
    private String serial;
}
```



Json封装体CommonResult

这个类是传递给前端的，前端不管什么 payment，它只要响应状态码、message...

```java
package com.atguigu.springcloud.entities;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class CommonResult<T> {
    private Integer code;
    private String message;
    private T data;

    public CommonResult(Integer code, String message) {
        this(code, message, null);
    }
}
```



#### （6）controller

```java
package com.atguigu.springcloud.controller;

@RestController
@Slf4j
@RequestMapping("/payment")
public class PaymentController {

    @Resource
    private PaymentService paymentService;

    @PostMapping("/create")
    public CommonResult create(Payment payment) {
        return paymentService.create(payment);
    }

    @GetMapping("/get/{id}")
    public CommonResult getPaymentById(@PathVariable("id") Long id){
        return paymentService.getPaymentById(id);
    }
}
```

public CommonResult create(Payment payment)这里加@RequestBody测试的时候会报405



#### （7）service

PaymentService

```java
package com.atguigu.springcloud.service;

public interface PaymentService {

    /**
     * 创建一个 payment
     * @param payment
     * @return
     */
    CommonResult create(Payment payment);

    /**
     * 根据 id 查询 payment
     * @param id
     * @return
     */
    CommonResult getPaymentById(Long id);
}
```



PaymentServiceImpl

```java
@Service
@Slf4j
public class PaymentServiceImpl implements PaymentService {

    @Resource
    private PaymentDao paymentDao;

    @Override
    public CommonResult create(Payment payment) {
        int result = paymentDao.create(payment);
        log.info("*****插入操作返回结果:{}",result);
        if (result > 0) {
            return new CommonResult(200, "插入数据库成功", result);
        } else {
            return new CommonResult(444, "插入数据库失败", null);
        }
    }

    @Override
    public CommonResult getPaymentById(Long id) {
        Payment payment = paymentDao.getPaymentById(id);
        log.info("*****查询结果:{}", payment);
        if (payment != null) {
            return new CommonResult(200, "查询成功", payment);
        } else {
            return new CommonResult(444, "没有对应记录,查询ID: " + id, null);
        }
    }
}
```



#### （8）dao

PaymentDao

```java
package com.atguigu.springcloud.dao;

@Mapper
public interface PaymentDao {

    /**
     * 创建一个 payment
     *
     * @param payment
     * @return
     */
    int create(Payment payment);

    /**
     * 根据 id 查询 payment
     *
     * @param id
     * @return
     */
    Payment getPaymentById(@Param("id") Long id);
}
```



PaymentMapper.xml

src\main\resources\mapper\PaymentMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >

<mapper namespace="com.atguigu.springcloud.dao.PaymentDao">
    <resultMap id="BaseResultMap" type="com.atguigu.springcloud.entities.Payment">
        <id column="id" property="id" jdbcType="BIGINT"/>
        <result column="serial" property="serial" jdbcType="VARCHAR"/>
    </resultMap>

    <insert id="create" parameterType="Payment" useGeneratedKeys="true" keyColumn="id">
        insert into payment(serial)
        values (#{serial})
    </insert>

    <select id="getPaymentById" parameterType="Long" resultMap="BaseResultMap">
        select id, serial
        from payment
        where id = #{id}
    </select>
</mapper>
```



#### （9）测试

postman模拟post

http://localhost:8001/payment/create?serial=‘111’

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220120001120241.png" alt="image-20220120001120241" style="zoom: 80%;" />

http://localhost:8001/payment/get/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220120001038440.png" alt="image-20220120001038440" style="zoom:80%;" />

#### （10）一些设置

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220120233020908.png" alt="image-20220120233020908" style="zoom: 80%;" />

### 2、热部署Devtools

#### （1）8001的pom

之前已经添加了

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
    <optional>true</optional>
</dependency>
```



#### （2）父工程的pom

之前已经添加了

```xml
<build>
    <finalName>mscloud</finalName>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <version>2.3.5.RELEASE</version>
            <configuration>
                <fork>true</fork>
                <addResources>true</addResources>
            </configuration>
        </plugin>
    </plugins>
</build>
```



#### （3）自动编译

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220121000836843.png" alt="image-20220121000836843" style="zoom: 80%;" />

#### （4）Update the value of

快捷键：`ctrl+shift+alt+/`

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220121001028891.png" alt="image-20220121001028891" style="zoom: 80%;" />

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220121001151946.png" alt="image-20220121001151946" style="zoom: 80%;" />

然后重启 IDEA

注意：开发阶段开启热部署，生产阶段必须关闭



### 3、订单模块80

cloud-consumer-order80 微服务消费者订单Module模块

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220121002413787.png" alt="image-20220121002413787" style="zoom: 80%;" />

#### （1）改POM

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-consumer-order80</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



#### （2）写YML

application.yml

```yaml
server:
  port: 80
```



#### （3）主启动

```java
package com.atguigu.springcloud;

@SpringBootApplication
public class MainApp80 {
    public static void main(String[] args) {
        SpringApplication.run(MainApp80.class, args);
    }
}
```



#### （4）entities

主实体 Payment

```java
package com.atguigu.springcloud.entities;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class Payment implements Serializable {
    private Long id;
    private String serial;
}
```



Json封装体CommonResult

这个类是传递给前端的，前端不管什么 payment，它只要响应状态码、message...

```java
package com.atguigu.springcloud.entities;

@Data
@AllArgsConstructor
@NoArgsConstructor
public class CommonResult<T> {
    private Integer code;
    private String message;
    private T data;

    public CommonResult(Integer code, String message) {
        this(code, message, null);
    }
}
```



#### （5）首说RestTemplate

是什么：

RestTemplate提供了多种便捷访问远程Http服务的方法， 是一种简单便捷的访问restful服务模板类，是Spring提供的用于访问Rest服务的客户端模板工具集



官网地址：

https://docs.spring.io/spring-framework/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html



使用：

使用restTemplate访问restful接口非常的简单粗暴无脑

- url：REST请求地址
- requestMap：请求参数
- ResponseBean.class：HTTP响应转换被转换成的对象类型
  
  

#### （6）config配置类

ApplicationContextConfig

```java
package com.atguigu.springcloud.config;

@Configuration
public class ApplicationContextConfig {

    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```



#### （7）controller

```java
@RestController
@Slf4j
@RequestMapping("/consumer")
public class OrderController {

    public static final String PaymentSrv_URL = "http://localhost:8001";

    @Resource
    private RestTemplate restTemplate;

    /**
     * 客户端用浏览器是get请求，但是底层实质发送post调用服务端8001
     *
     * @param payment
     * @return
     */
    @GetMapping("/payment/create")
    public CommonResult<Payment> create(Payment payment) {
        return restTemplate.postForObject(PaymentSrv_URL + "/payment/create", payment, CommonResult.class);
    }

    @GetMapping("/payment/get/{id}")
    public CommonResult<Payment> getPayment(@PathVariable("id") Long id) {
        return restTemplate.getForObject(PaymentSrv_URL + "/payment/get/" + id,CommonResult.class,id);
    }
}
```

注意：`/payment/get/`路径中 get 后面的 / 不要忘了加，否则会一直报错

![image-20220121005326776](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220121005326776.png)

![image-20220121005418027](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220121005418027.png)



#### （8）测试

http://localhost/consumer/payment/get/1

http://localhost/consumer/payment/create?serial=aaaaa1



<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220122235915781.png" alt="image-20220122235915781" style="zoom: 80%;" />

但是数据库中只有主键并没有数据

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123000016123.png" alt="image-20220123000016123" style="zoom: 80%;" />

8001中的 create 不要忘记@RequestBody注解

```java
@PostMapping("/create")
public CommonResult create(@RequestBody Payment payment) {
    return paymentService.create(payment);
}
```



插入成功

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123000203509.png" alt="image-20220123000203509" style="zoom: 80%;" />

### 4、工程重构

#### （1）观察问题

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123020257709.png" alt="image-20220123020257709" style="zoom: 80%;" />

系统中有重复部分，重构



#### （2）cloud-api-commons

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123021053758.png" alt="image-20220123021053758" style="zoom: 80%;" />

pom.xml

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>cn.hutool</groupId>
        <artifactId>hutool-all</artifactId>
        <version>5.1.0</version>
    </dependency>
</dependencies>
```



把 8001 和 80 的 entities 移到 commons 中

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123021533643.png" alt="image-20220123021533643" style="zoom: 80%;" />

maven命令clean install

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123022241845.png" alt="image-20220123022241845" style="zoom: 80%;" />

订单80和支付8001分别改造

- 删除各自的原先有过的entities文件夹

- 各自粘贴POM内容
  
  - ```xml
    <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <groupId>com.atguigu.springcloud</groupId>
        <artifactId>cloud-api-commons</artifactId>
        <version>${project.version}</version>
    </dependency>
    ```
    
    

# 三、SpringCloud Eureka 服务注册与发现

## （一）Eureka基础知识

### 1、什么是服务治理

Spring Cloud 封装了 Netflix 公司开发的 Eureka 模块来实现服务治理

在传统的rpc远程调用框架中，管理每个服务与服务之间依赖关系比较复杂，管理比较复杂，所以需要使用服务治理，管理服务于服务之间依赖关系，可以实现服务调用、负载均衡、容错等，实现服务发现与注册。



### 2、什么是服务注册

Eureka采用了CS的设计架构，Eureka Server 作为服务注册功能的服务器，它是服务注册中心。而系统中的其他微服务，使用 Eureka的客户端连接到 Eureka Server并维持心跳连接。这样系统的维护人员就可以通过 Eureka Server 来监控系统中各个微服务是否正常运行。

在服务注册与发现中，有一个注册中心。当服务器启动的时候，会把当前自己服务器的信息 比如 服务地址通讯地址等以别名方式注册到注册中心上。另一方（消费者|服务提供者），以该别名的方式去注册中心上获取到实际的服务通讯地址，然后再实现本地RPC调用RPC远程调用框架核心设计思想：在于注册中心，因为使用注册中心管理每个服务与服务之间的一个依赖关系(服务治理概念)。在任何rpc远程框架中，都会有一个注册中心(存放服务地址相关信息(接口地址))

下左图是Eureka系统架构，右图是Dubbo的架构，请对比：

![image-20220123025941829](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123025941829.png)



### 3、Eureka两组件

Eureka包含两个组件：Eureka Server和Eureka Client

- Eureka Server 提供服务注册服务

各个微服务节点通过配置启动后，会在EurekaServer中进行注册，这样EurekaServer中的服务注册表中将会存储所有可用服务节点的信息，服务节点的信息可以在界面中直观看到

- EurekaClient 通过注册中心进行访问

是一个Java客户端，用于简化Eureka Server的交互，客户端同时也具备一个内置的、使用轮询(round-robin)负载算法的负载均衡器。在应用启动后，将会向Eureka Server发送心跳(默认周期为30秒)。如果Eureka Server在多个心跳周期内没有接收到某个节点的心跳，EurekaServer将会从服务注册表中把这个服务节点移除（默认90秒）



## （二）单机Eureka构建步骤

### 1、eurekaServer端服务注册中心

IDEA生成eurekaServer端服务注册中心类似物业公司

#### （1）建Module

cloud-eureka-server7001

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123030402591.png" alt="image-20220123030402591" style="zoom: 80%;" />

#### （2）改POM

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-eureka-server7001</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <!--eureka-server-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        </dependency>
        <!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <!--boot web actuator-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!--图形监控，以后的swagger和Hystrix要用的-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--一般通用配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
        </dependency>
    </dependencies>
</project>
```



1.X和2.X的对比说明：

```xml
以前的老版本（当前使用2018）
<dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-eureka</artifactId>
</dependency>
```

```xml
现在新版本（当前使用2020.2）
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```



#### （3）写YML

```yaml
server:
  port: 7001

eureka:
  instance:
    hostname: localhost #eureka服务端的实例名称
  client:
    #false表示不向注册中心注册自己。
    register-with-eureka: false
    #false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去检索服务
    fetch-registry: false
    service-url:
    #设置与Eureka Server交互的地址查询服务和注册服务都需要依赖这个地址。
      defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka/
```



#### （4）主启动

```java
package com.atguigu.springcloud;

@SpringBootApplication
@EnableEurekaServer
public class EurekaMain7001 {
    public static void main(String[] args) {
        SpringApplication.run(EurekaMain7001.class, args);
    }
}
```



#### （5）测试

http://localhost:7001/

![image-20220123031503669](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123031503669.png)

No application available 没有服务被发现，因为没有注册服务进来当然不可能有服务被发现



### 2、8001注册进Eureka成为提供者

EurekaClient 端 cloud-provider-payment8001 将注册进 EurekaServer 成为服务提供者 provider，类似尚硅谷学校对外提供授课服务

#### （1）改POM

```xml
<!--eureka-client-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```



#### （2）写YML

application.yml

```yaml
eureka:
  client:
    #表示是否将自己注册进EurekaServer默认为true。
    register-with-eureka: true
    #是否从EurekaServer抓取已有的注册信息，默认为true。单节点无所谓，集群必须设置为true才能配合ribbon使用负载均衡
    fetchRegistry: true
    service-url:
      defaultZone: http://localhost:7001/eureka
```



#### （3）主启动

```java
@EnableEurekaClient
```

```java
package com.atguigu.springcloud;

@SpringBootApplication
@EnableEurekaClient
public class PaymentMain8001 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain8001.class,args);
    }
}
```



#### （4）测试

先要启动EurekaServer，http://localhost:7001/

![image-20220123120903795](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123120903795.png)



微服务注册名配置说明

![image-20220123121142942](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123121142942.png)



#### （5）自我保护机制

![image-20220123121247649](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123121247649.png)



### 3、80注册进Eureka成为消费者

EurekaClient 端 cloud-consumer-order80 将注册进 EurekaServer 成为服务消费者 consumer，类似来尚硅谷上课消费的各位同学

#### （1）改POM

```xml
<!--eureka-client-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```



#### （2）写YML

application.yml

```yaml
server:
  port: 80

spring:
  application:
    name: cloud-order-service

eureka:
  client:
    #表示是否将自己注册进EurekaServer默认为true。
    register-with-eureka: true
    #是否从EurekaServer抓取已有的注册信息，默认为true。单节点无所谓，集群必须设置为true才能配合ribbon使用负载均衡
    fetchRegistry: true
    service-url:
      defaultZone: http://localhost:7001/eureka
```



#### （3）主启动

```java
@EnableEurekaClient
```

```java
package com.atguigu.springcloud;

@SpringBootApplication
@EnableEurekaClient
public class MainApp80 {
    public static void main(String[] args) {
        SpringApplication.run(MainApp80.class, args);
    }
}
```



#### （4）测试

先要启动EurekaServer——7001服务，再要启动服务提供者provider——8001服务

![image-20220123122247426](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123122247426.png)



http://localhost/consumer/payment/get/31

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123122320920.png" alt="image-20220123122320920" style="zoom: 80%;" />

### 4、bug

Failed to bind properties under 'eureka.client.service-url' to java.util.Map<java.lang.String, java.lang.String>

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123122714466.png" alt="image-20220123122714466" style="zoom: 80%;" />

## （二）集群Eureka构建步骤

### 1、Eureka集群原理说明

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123123020106.png" alt="image-20220123123020106" style="zoom: 80%;" />

问题：微服务RPC远程服务调用最核心的是什么？

高可用，试想你的注册中心只有一个only one， 它出故障了那就呵呵(￣▽￣)"了，会导致整个为服务环境不可用，所以解决办法：搭建Eureka注册中心集群 ，实现负载均衡+故障容错



### 2、EurekaServer集群环境构建步骤

#### （1）新建cloud-eureka-server7002

参考cloud-eureka-server7001，新建cloud-eureka-server7002



#### （2）改POM

```xml
<artifactId>cloud-eureka-server7002</artifactId>
```



父工程 mscloud 的 POM

```xml
<module>cloud-eureka-server7002</module>
```



#### （3）修改映射配置

找到C:\Windows\System32\drivers\etc路径下的hosts文件，修改映射配置添加进hosts文件

- 127.0.0.1  eureka7001.com
- 127.0.0.1  eureka7002.com

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123125019978.png" alt="image-20220123125019978" style="zoom:80%;" />

#### （4）写YML

以前单机版：

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123125614973.png" alt="image-20220123125614973" style="zoom: 80%;" />

7001：

```yaml
server:
  port: 7001

eureka:
  instance:
    hostname: eureka7001.com  #eureka服务端的实例名称
  client:
    register-with-eureka: false #false表示不向注册中心注册自己。
    fetch-registry: false #false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去检索服务
    service-url:
      defaultZone: http://eureka7002.com:7002/eureka/
```



7002：

```yaml
server:
  port: 7002

eureka:
  instance:
    hostname: eureka7002.com  #eureka服务端的实例名称
  client:
    register-with-eureka: false #false表示不向注册中心注册自己。
    fetch-registry: false #false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去检索服务
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/
```



#### （5）主启动

```java
package com.atguigu.springcloud;

@SpringBootApplication
@EnableEurekaServer
public class EurekaMain7002 {
    public static void main(String[] args) {
        SpringApplication.run(EurekaMain7002.class, args);
    }
}
```



#### （6）测试

![image-20220123175252624](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123175252624.png)



<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123130850066.png" alt="image-20220123130850066" style="zoom: 80%;" />

### 3、8001发布到2台Eureka集群

application.yml

```yaml
# 集群版
defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka  
```



```yaml
server:
  port: 8001

spring:
  application:
    name: cloud-payment-service
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource            # 当前数据源操作类型
    driver-class-name: org.gjt.mm.mysql.Driver              # mysql驱动包 com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/springcloud2021?useUnicode=true&characterEncoding=utf-8&useSSL=false
    username: root
    password: root

eureka:
  client:
    #表示是否将自己注册进EurekaServer默认为true。
    register-with-eureka: true
    #是否从EurekaServer抓取已有的注册信息，默认为true。单节点无所谓，集群必须设置为true才能配合ribbon使用负载均衡
    fetchRegistry: true
    service-url:
      #defaultZone: http://localhost:7001/eureka
      defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka  # 集群版

mybatis:
  mapperLocations: classpath:mapper/*.xml
  type-aliases-package: com.atguigu.springcloud.entities    # 所有Entity别名类所在包
```



### 4、80发布到2台Eureka集群

application.yml

```yaml
defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka  # 集群版
```



```yaml
server:
  port: 80

spring:
  application:
    name: cloud-order-service

eureka:
  client:
    #表示是否将自己注册进EurekaServer默认为true。
    register-with-eureka: true
    #是否从EurekaServer抓取已有的注册信息，默认为true。单节点无所谓，集群必须设置为true才能配合ribbon使用负载均衡
    fetchRegistry: true
    service-url:
      #defaultZone: http://localhost:7001/eureka
      defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka  # 集群版
```



### 5、测试01

先要启动EurekaServer，7001/7002服务，再要启动服务提供者provide——8001，最后再启动消费者——80

http://localhost/consumer/payment/get/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123134613385.png" alt="image-20220123134613385" style="zoom: 80%;" />

### 6、支付服务提供者8001集群环境构建

#### （1）新建cloud-provider-payment8002

参考cloud-provider-payment8001



pom.xml

```xml
<artifactId>cloud-provider-payment8002</artifactId>
```



application.yml

```yaml
server:
  port: 8002
```



主启动

```java
package com.atguigu.springcloud;

@SpringBootApplication
@EnableEurekaClient
public class PaymentMain8002 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain8002.class,args);
    }
}
```



#### （2）修改8001/8002的PaymentServiceImpl

8001：

```java
@Value("${server.port}")
private String serverPort;
```



```java
package com.atguigu.springcloud.service.impl;

@Service
@Slf4j
public class PaymentServiceImpl implements PaymentService {

    @Resource
    private PaymentDao paymentDao;

    @Value("${server.port}")
    private String serverPort;

    @Override
    public CommonResult create(Payment payment) {
        int result = paymentDao.create(payment);
        log.info("*****插入操作返回结果:{}", result);
        if (result > 0) {
            return new CommonResult(200, "插入数据库成功，serverPort：" + serverPort, result);
        } else {
            return new CommonResult(444, "插入数据库失败", null);
        }
    }

    @Override
    public CommonResult getPaymentById(Long id) {
        Payment payment = paymentDao.getPaymentById(id);
        log.info("*****查询结果:{}", payment);
        if (payment != null) {
            return new CommonResult(200, "查询成功，serverPort：" + serverPort, payment);
        } else {
            return new CommonResult(444, "没有对应记录,查询ID: " + id, null);
        }
    }
}
```



8002：

同理

```java
@Value("${server.port}")
private String serverPort;
```



#### （3）测试

http://eureka7001.com:7001/

![image-20220123175603467](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123175603467.png)



http://eureka7002.com:7002/

![image-20220123175621348](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123175621348.png)



http://localhost:8001/payment/get/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123181118488.png" alt="image-20220123181118488" style="zoom: 80%;" />

http://localhost:8002/payment/get/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123181145608.png" alt="image-20220123181145608" style="zoom: 80%;" />

http://localhost/consumer/payment/get/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123181246895.png" alt="image-20220123181246895" style="zoom: 80%;" />

#### （4）bug

我们发现不管怎么刷新请求，请求的端口号一直是8001，原因是我们在80的controller中写死了

![image-20220123182702982](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123182702982.png)



OrderController：

```java
///不要把地址写死
//public static final String PaymentSrv_URL = "http://localhost:8001";
// 通过在eureka上注册过的微服务名称调用
public static final String PAYMENT_SRV = "http://CLOUD-PAYMENT-SERVICE";
```



此时再测试

![image-20220123201948548](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123201948548.png)

这又是什么情况？

现在注册中心不再是暴露出具体的端口号，而是微服务名称 CLOUD-PAYMENT-SERVICE，但是这个微服务名称代表的集群中有很多个，比如8001、8002......用哪个，它并不知道

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123202535357.png" alt="image-20220123202535357" style="zoom: 80%;" />

我们需要再配置一下负载均衡



### 7、负载均衡

#### （1）@LoadBalanced

使用 @LoadBalanced 注解赋予 RestTemplate 负载均衡的能力

cloud-consumer-order80

ApplicationContextConfig

```java
@LoadBalanced //使用@LoadBalanced注解赋予RestTemplate负载均衡的能力
```

```java
package com.atguigu.springcloud.config;

@Configuration
public class ApplicationContextConfig {

    @Bean
    @LoadBalanced //使用@LoadBalanced注解赋予RestTemplate负载均衡的能力
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```



#### （2）测试

第一次

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123203629529.png" alt="image-20220123203629529" style="zoom: 80%;" />

第二次

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123203723079.png" alt="image-20220123203723079" style="zoom: 80%;" />

负载均衡效果达到，8001/8002端口交替出现



提前剧透：Ribbon和Eureka整合后Consumer可以直接调用服务而不用再关心地址和端口号，且该服务还有负载功能了。O(∩_∩)O



## （三）actuator微服务信息完善

### 1、主机名称:服务名称修改

#### （1）当前问题

含有主机名称

![image-20220123204237614](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123204237614.png)



#### （2）修改8001和8002

8001：

application.yml

```yaml
instance:
  instance-id: payment8001
```

```yaml
server:
  port: 8001

spring:
  application:
    name: cloud-payment-service
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource            # 当前数据源操作类型
    driver-class-name: org.gjt.mm.mysql.Driver              # mysql驱动包 com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/springcloud2021?useUnicode=true&characterEncoding=utf-8&useSSL=false
    username: root
    password: root

eureka:
  client:
    #表示是否将自己注册进EurekaServer默认为true。
    register-with-eureka: true
    #是否从EurekaServer抓取已有的注册信息，默认为true。单节点无所谓，集群必须设置为true才能配合ribbon使用负载均衡
    fetchRegistry: true
    service-url:
      #defaultZone: http://localhost:7001/eureka
      defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka  # 集群版
  instance:
    instance-id: payment8001

mybatis:
  mapperLocations: classpath:mapper/*.xml
  type-aliases-package: com.atguigu.springcloud.entities    # 所有Entity别名类所在包
```



同理，8002：

```yaml
instance:
  instance-id: payment8002
```



再测试

![image-20220123211341196](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123211341196.png)



![image-20220123211536534](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123211536534.png)



### 2、访问信息有IP信息提示

#### （1）当前问题

没有IP提示

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123204651752.png" alt="image-20220123204651752" style="zoom:67%;" />

#### （2）修改8001和8002

application.yml

```yaml
prefer-ip-address: true     #访问路径可以显示IP地址
```



```yaml
eureka:
  client:
    #表示是否将自己注册进EurekaServer默认为true。
    register-with-eureka: true
    #是否从EurekaServer抓取已有的注册信息，默认为true。单节点无所谓，集群必须设置为true才能配合ribbon使用负载均衡
    fetchRegistry: true
    service-url:
      #defaultZone: http://localhost:7001/eureka
      defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka  # 集群版
  instance:
    instance-id: payment8001
    prefer-ip-address: true     #访问路径可以显示IP地址
```



![image-20220123211851786](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123211851786.png)



![image-20220123211909332](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123211909332.png)



## （四）服务发现Discovery

对于注册进eureka里面的微服务，可以通过服务发现来获得该服务的信息

### 1、修改8001和8002的Controller

加上

```java
@Resource
private DiscoveryClient discoveryClient;

@GetMapping(value = "/discovery")
public Object discovery() {
    List<String> services = discoveryClient.getServices();
    for (String service : services) {
        log.info("service:{}", service);
    }
    List<ServiceInstance> instances = discoveryClient.getInstances("CLOUD-PAYMENT-SERVICE");
    for (ServiceInstance instance : instances) {
        log.info(instance.getServiceId() + "\t" + instance.getHost() + "\t" + instance.getPort() + "\t"
                 + instance.getUri());
    }
    return this.discoveryClient;
}
```



```java
package com.atguigu.springcloud.controller;

import org.springframework.cloud.client.discovery.DiscoveryClient;

@RestController
@Slf4j
@RequestMapping("/payment")
public class PaymentController {

    @Resource
    private PaymentService paymentService;

    @Resource
    private DiscoveryClient discoveryClient;

    @PostMapping("/create")
    public CommonResult create(@RequestBody Payment payment) {
        return paymentService.create(payment);
    }

    @GetMapping("/get/{id}")
    public CommonResult getPaymentById(@PathVariable("id") Long id) {
        return paymentService.getPaymentById(id);
    }

    @GetMapping(value = "/discovery")
    public Object discovery() {
        List<String> services = discoveryClient.getServices();
        for (String service : services) {
            log.info("service:{}", service);
        }
        List<ServiceInstance> instances = discoveryClient.getInstances("CLOUD-PAYMENT-SERVICE");
        for (ServiceInstance instance : instances) {
            log.info(instance.getServiceId() + "\t" + instance.getHost() + "\t" + instance.getPort() + "\t"
                    + instance.getUri());
        }
        return this.discoveryClient;
    }
}
```



### 2、主启动类

```java
@EnableDiscoveryClient //服务发现
```



8001：

```java
@SpringBootApplication
@EnableEurekaClient
@EnableDiscoveryClient //服务发现
public class PaymentMain8001 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain8001.class,args);
    }
}
```



8002同理



### 3、测试

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123214547168.png" alt="image-20220123214547168" style="zoom: 80%;" />

![image-20220123214535831](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123214535831.png)



## （五）Eureka自我保护

### 1、故障现象

概述：保护模式主要用于一组客户端和Eureka Server之间存在网络分区场景下的保护。一旦进入保护模式，Eureka Server将会尝试保护其服务注册表中的信息，不再删除服务注册表中的数据，也就是不会注销任何微服务。

如果在Eureka Server的首页看到以下这段提示，则说明Eureka进入了保护模式

![image-20220123215516917](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123215516917.png)



### 2、导致原因

为什么会产生Eureka自我保护机制？

为了防止EurekaClient可以正常运行，但是 与 EurekaServer网络不通情况下，EurekaServer不会立刻将EurekaClient服务剔除



什么是自我保护模式？

默认情况下，如果EurekaServer在一定时间内没有接收到某个微服务实例的心跳，EurekaServer将会注销该实例（默认90秒）。但是当网络分区故障发生(延时、卡顿、拥挤)时，微服务与EurekaServer之间无法正常通信，以上行为可能变得非常危险了——因为微服务本身其实是健康的，此时本不应该注销这个微服务。Eureka通过“自我保护模式”来解决这个问题——当EurekaServer节点在短时间内丢失过多客户端时（可能发生了网络分区故障），那么这个节点就会进入自我保护模式。



<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123215611742.png" style="zoom: 80%;" />

在自我保护模式中，Eureka Server会保护服务注册表中的信息，不再注销任何服务实例。

它的设计哲学就是宁可保留错误的服务注册信息，也不盲目注销任何可能健康的服务实例。一句话讲解：好死不如赖活着

综上，自我保护模式是一种应对网络异常的安全保护措施。它的架构哲学是宁可同时保留所有微服务（健康的微服务和不健康的微服务都会保留）也不盲目注销任何健康的微服务。使用自我保护模式，可以让Eureka集群更加的健壮、稳定。



一句话：某时刻某一个微服务不可用了，Eureka不会立刻清理，依旧会对该微服务的信息进行保存

属于CAP里面的AP分支



### 3、怎么禁止自我保护

现在可以不用集群版了，只用开一个，在 application.yml 中把集群配置改为单机版

#### （1）注册中心eureakeServer端7001

出厂默认，自我保护机制是开启的 eureka.server.enable-self-preservation=true，使用eureka.server.enable-self-preservation = false 可以禁用自我保护模式

application.yml：

```yaml
server:
  #关闭自我保护机制，保证不可用服务被及时踢除
  enable-self-preservation: false
  eviction-interval-timer-in-ms: 2000
```



```yaml
server:
  port: 7001

eureka:
  instance:
    hostname: eureka7001.com  #eureka服务端的实例名称
  client:
    register-with-eureka: false #false表示不向注册中心注册自己。
    fetch-registry: false #false表示自己端就是注册中心，我的职责就是维护服务实例，并不需要去检索服务
    service-url:
      defaultZone: http://eureka7002.com:7002/eureka/
  server:
    #关闭自我保护机制，保证不可用服务被及时踢除
    enable-self-preservation: false
    eviction-interval-timer-in-ms: 2000
```



关闭效果：

![image-20220123221232971](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123221232971.png)



#### （2）生产者客户端eureakeClient端8001

默认配置：

```yaml
eureka.instance.lease-renewal-interval-in-seconds=30 #单位为秒(默认是30秒)
eureka.instance.lease-expiration-duration-in-seconds=90 #单位为秒(默认是90秒)
```



配置：

```yaml
#Eureka客户端向服务端发送心跳的时间间隔，单位为秒(默认是30秒)
lease-renewal-interval-in-seconds: 1
#Eureka服务端在收到最后一次心跳后等待时间上限，单位为秒(默认是90秒)，超时将剔除服务
lease-expiration-duration-in-seconds: 2
```



```yaml
server:
  port: 8001

spring:
  application:
    name: cloud-payment-service
  datasource:
    type: com.alibaba.druid.pool.DruidDataSource            # 当前数据源操作类型
    driver-class-name: org.gjt.mm.mysql.Driver              # mysql驱动包 com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/springcloud2021?useUnicode=true&characterEncoding=utf-8&useSSL=false
    username: root
    password: root

eureka:
  client:
    #表示是否将自己注册进EurekaServer默认为true。
    register-with-eureka: true
    #是否从EurekaServer抓取已有的注册信息，默认为true。单节点无所谓，集群必须设置为true才能配合ribbon使用负载均衡
    fetchRegistry: true
    service-url:
      defaultZone: http://localhost:7001/eureka
      #defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka  # 集群版
  instance:
    instance-id: payment8001
    #访问路径可以显示IP地址
    prefer-ip-address: true
    #Eureka客户端向服务端发送心跳的时间间隔，单位为秒(默认是30秒)
    lease-renewal-interval-in-seconds: 1
    #Eureka服务端在收到最后一次心跳后等待时间上限，单位为秒(默认是90秒)，超时将剔除服务
    lease-expiration-duration-in-seconds: 2

mybatis:
  mapperLocations: classpath:mapper/*.xml
  type-aliases-package: com.atguigu.springcloud.entities    # 所有Entity别名类所在包
```



测试：

7001和8001都配置完成，先启动7001再启动8001

http://eureka7001.com:7001/

![image-20220123222603823](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123222603823.png)



模拟8001出现了故障关闭了，以前7001还会保留，但是现在：

![image-20220123222749492](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123222749492.png)



# 四、Zookeeper服务注册与发现

## （一）Eureka停止更新了你怎么办

https://github.com/Netflix/eureka/wiki

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123223011220.png" alt="image-20220123223011220" style="zoom: 80%;" />

## （二）SpringCloud整合Zookeeper代替Eureka

### 1、注册中心Zookeeper



zookeeper 暂时跳过，虚拟机没有装 zookeeper 





# 五、SpringCloud Consul 服务注册与发现

## （一）Consul简介

### 1、是什么

https://www.consul.io/intro/index.html

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123230251771.png" alt="image-20220123230251771" style="zoom: 80%;" />

Consul 是一套开源的分布式服务发现和配置管理系统，由 HashiCorp 公司用 Go 语言开发

提供了微服务系统中的服务治理、配置中心、控制总线等功能。这些功能中的每一个都可以根据需要单独使用，也可以一起使用以构建全方位的服务网格，总之Consul提供了一种完整的服务网格解决方案

它具有很多优点。包括： 基于 raft 协议，比较简洁； 支持健康检查, 同时支持 HTTP 和 DNS 协议 支持跨数据中心的 WAN 集群 提供图形界面 跨平台，支持 Linux、Mac、Windows



### 2、能干嘛

Spring Cloud Consul 具有如下特性：

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123230402725.png" alt="image-20220123230402725" style="zoom: 80%;" />

- 服务发现：提供HTTP和DNS两种发现方式
- 健康监测：支持多种方式，HTTP、TCP、Docker、Shell脚本定制化监控
- KV存储：Key、Value的存储方式
- 多数据中心：Consul支持多数据中心
- 可视化Web界面
  
  

### 3、去哪下

https://www.consul.io/downloads.html



### 4、怎么玩

https://www.springcloud.cc/spring-cloud-consul.html



## （二）安装并运行Consul

### 1、官网安装说明

https://learn.hashicorp.com/consul/getting-started/install.html



### 2、下载和安装

下载完成后只有一个consul.exe文件，硬盘路径下双击运行，查看版本号信息



直接在软件目录中输入 cmd 进入命令控制台

![image-20220123231219542](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123231219542.png)



consul --version：查看 consul 版本号

```sh
Microsoft Windows [版本 10.0.17763.1637]
(c) 2018 Microsoft Corporation。保留所有权利。

D:\Java学习资料\03、微服务生态\SpringCloud\安装包>consul --version
Consul v1.8.3
Revision a9322b9c7
Protocol 2 spoken by default, understands 2 to 3 (agent will automatically use protocol >2 when speaking to compatible agents)
```



使用开发模式启动

consul agent -dev

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123231554989.png" alt="image-20220123231554989" style="zoom:80%;" />

通过以下地址可以访问Consul的首页：http://localhost:8500

![image-20220123231638608](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220123231638608.png)



## （三）服务提供者

### 1、新建Module支付服务provider8006

cloud-providerconsul-payment8006

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220212170922437.png" alt="image-20220212170922437" style="zoom: 80%;" />

### 2、改POM

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-providerconsul-payment8006</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>
    <dependencies>
        <!--SpringCloud consul-server -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-consul-discovery</artifactId>
        </dependency>
        <!-- SpringBoot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



### 3、改 YML

```yaml
###consul服务端口号
server:
  port: 8006

spring:
  application:
    name: consul-provider-payment
  ####consul注册中心地址
  cloud:
    consul:
      host: localhost
      port: 8500
      discovery:
        #hostname: 127.0.0.1
        service-name: ${spring.application.name}
```





### 4、主启动类

```java
@SpringBootApplication
@EnableDiscoveryClient
public class PaymentMain8006 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain8006.class,args);
    }
}
```



### 5、业务类Controller

```java
package com.atguigu.springcloud.controller;

import lombok.extern.slf4j.Slf4j;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.UUID;

@RestController
@Slf4j
public class PaymentController {
    @Value("${server.port}")
    private String serverPort;

    @GetMapping("/payment/consul")
    public String paymentInfo() {
        return "springcloud with consul: " + serverPort + "\t\t" + UUID.randomUUID().toString();
    }
}
```



### 6、验证测试

http://localhost:8500

![image-20220212172722364](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220212172722364.png)



http://localhost:8006/payment/consul

![image-20220212173652460](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220212173652460.png)



## （四）服务消费者

### 1、新建Module消费服务order80

cloud-consumerconsul-order80

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220212174058132.png" alt="image-20220212174058132" style="zoom: 80%;" />

### 2、改POM

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-consumerconsul-order80</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <!--SpringCloud consul-server -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-consul-discovery</artifactId>
        </dependency>
        <!-- SpringBoot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



### 3、建 YML

application.yml

```yaml
###consul服务端口号
server:
  port: 80

spring:
  application:
    name: cloud-consumer-order
  ####consul注册中心地址
  cloud:
    consul:
      host: localhost
      port: 8500
      discovery:
        #hostname: 127.0.0.1
        service-name: ${spring.application.name}
```



### 4、主启动类

```java
package com.atguigu.springcloud;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;

/**
 * @author 杨帆
 * @date 2022/2/12 17:45
 */
@SpringBootApplication
@EnableDiscoveryClient //该注解用于向使用consul或者zookeeper作为注册中心时注册服务
public class OrderConsulMain80 {
    public static void main(String[] args) {
        SpringApplication.run(OrderConsulMain80.class, args);
    }
}
```



### 5、配置Bean

```java
package com.atguigu.springcloud.config;

import org.springframework.cloud.client.loadbalancer.LoadBalanced;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.client.RestTemplate;

@Configuration
public class ApplicationContextBean {
    @Bean
    @LoadBalanced
    public RestTemplate getRestTemplate() {
        return new RestTemplate();
    }
}
```



### 6、Controller

```java
package com.atguigu.springcloud.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.client.RestTemplate;

/**
 * @author 杨帆
 * @date 2022/2/12 17:51
 */
@RestController
public class OrderConsulController {
    public static final String INVOKE_URL = "http://consul-provider-payment";

    @Resource
    private RestTemplate restTemplate;

    @GetMapping(value = "/consumer/payment/consul")
    public String paymentInfo() {
        String result = restTemplate.getForObject(INVOKE_URL + "/payment/consul", String.class);
        System.out.println("消费者调用支付服务(consule)--->result:" + result);
        return result;
    }
}
```



### 7、验证测试

http://localhost:8500

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220212234711187.png" alt="image-20220212234711187"  />

### 8、访问测试地址

http://localhost/consumer/payment/consul

![image-20220214003444635](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220214003444635.png)



## （五）三个注册中心异同点

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220214004021036.png" alt="image-20220214004021036" style="zoom:80%;" />

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220214004056095.png" alt="image-20220214004056095" style="zoom: 80%;" />

### 1、CAP

C：Consistency（强一致性）

A：Availability（可用性）

P：Partition tolerance（分区容错性）

CAP理论关注粒度是数据，而不是整体系统设计的策略



### 2、经典CAP图

最多只能同时较好的满足两个。

CAP理论的核心是：一个分布式系统不可能同时很好的满足一致性，可用性和分区容错性这三个需求，因此，根据 CAP 原理将 NoSQL 数据库分成了满足 CA 原则、满足 CP 原则和满足 AP 原则三大类：

- CA - 单点集群，满足一致性，可用性的系统，通常在可扩展性上不太强大
- CP - 满足一致性，分区容忍必的系统，通常性能不是特别高
- AP - 满足可用性，分区容忍性的系统，通常可能对一致性要求低一些

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220214004251390.png" alt="image-20220214004251390" style="zoom: 80%;" />

AP(Eureka)：

AP架构：

当网络分区出现后，为了保证可用性，系统B可以返回旧值，保证系统的可用性。

结论：违背了一致性C的要求，只满足可用性和分区容错，即AP

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220214004658986.png" alt="image-20220214004658986" style="zoom:80%;" />

CP(Zookeeper/Consul)

CP架构：

当网络分区出现后，为了保证一致性，就必须拒接请求，否则无法保证一致性

结论：违背了可用性A的要求，只满足一致性和分区容错，即CP

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220214004731063.png" alt="image-20220214004731063" style="zoom:80%;" />

# 六、SpringCloud Ribbon 负载均衡服务调用

## （一）概述

### 1、是什么

Spring Cloud Ribbon是基于Netflix Ribbon实现的一套客户端负载均衡的工具。

简单的说，Ribbon是Netflix发布的开源项目，主要功能是提供客户端的软件负载均衡算法和服务调用。Ribbon客户端组件提供一系列完善的配置项如连接超时，重试等。简单的说，就是在配置文件中列出Load Balancer（简称LB）后面所有的机器，Ribbon会自动的帮助你基于某种规则（如简单轮询，随机连接等）去连接这些机器。我们很容易使用Ribbon实现自定义的负载均衡算法。



### 2、官网资料

https://github.com/Netflix/ribbon/wiki/Getting-Started



Ribbon目前也进入维护模式 https://github.com/Netflix/ribbon

![image-20220215004143873](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220215004143873.png)



未来替换方案

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220215004232887.png" alt="image-20220215004232887" style="zoom:80%;" />

### 3、能干吗

#### （1）LB（负载均衡）

LB负载均衡(Load Balance)是什么？

- 简单的说就是将用户的请求平摊的分配到多个服务上，从而达到系统的HA（高可用），常见的负载均衡有软件Nginx，LVS，硬件 F5等
  
  

Ribbon本地负载均衡客户端 VS Nginx服务端负载均衡区别？

- Nginx是服务器负载均衡，客户端所有请求都会交给nginx，然后由nginx实现转发请求。即负载均衡是由服务端实现的
- Ribbon本地负载均衡，在调用微服务接口时候，会在注册中心上获取注册信息服务列表之后缓存到JVM本地，从而在本地实现RPC远程服务调用技术
  
  

以下理解来自哔哩哔哩弹幕：

> 举个例子，nginx的负载均衡是针对服务器的，但是ribbon负载均衡是针对微服务的



> 我是这样理解的：nginx负责转发客户的请求，这是转发的负载均衡（可轮询转发、可xxx转发）。Ribbon是获取微服务注册信息的负载均衡（因为一个服务名可以集群，多个IP。可轮询获取、可xxx获取）。



> 最简单的例子，淘宝服务器可以在上海，北京，成都，ng做负载均衡决定你的请求分在哪个地区，ribbon负载均衡决定你在具体地区的某个微服务上



**集中式LB：**

即在服务的消费方和提供方之间使用独立的LB设施(可以是硬件，如F5, 也可以是软件，如nginx), 由该设施负责把访问请求通过某种策略转发至服务的提供方；



**进程内LB：**

将LB逻辑集成到消费方，消费方从服务注册中心获知有哪些地址可用，然后自己再从这些地址中选择出一个合适的服务器

Ribbon就属于进程内LB，它只是一个类库，集成于消费方进程，消费方通过它来获取到服务提供方的地址



#### （2）举例

前面我们讲解过了80通过轮询负载访问8001/8002【详情见eureka】

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220215233600609.png" alt="image-20220215233600609" style="zoom: 80%;" />

刷新后（负载均衡）：

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220215233702323.png" alt="image-20220215233702323" style="zoom:80%;" />

#### （3）一句话

负载均衡+RestTemplate调用



## （二）Ribbon负载均衡演示

### 1、架构说明

Ribbon在工作时分成两步：

第一步先选择 EurekaServer ,它优先选择在同一个区域内负载较少的server

第二步再根据用户指定的策略，在从server取到的服务注册列表中选择一个地址；其中Ribbon提供了多种策略：比如轮询、随机和根据响应时间加权

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220215005852821.png" alt="image-20220215005852821" style="zoom:80%;" />

总结：Ribbon其实就是一个软负载均衡的客户端组件，他可以和其他所需请求的客户端结合使用，和eureka结合只是其中的一个实例。



### 2、POM

之前写样例时候没有引入spring-cloud-starter-ribbon也可以使用ribbon

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-ribbon</artifactId>
</dependency>
```

猜测spring-cloud-starter-netflix-eureka-client自带了spring-cloud-starter-ribbon引用，证明如下： 可以看到spring-cloud-starter-netflix-eureka-client 确实引入了Ribbon

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220215231232368.png" alt="image-20220215231232368" style="zoom:80%;" />

以上：POM 中既可以加 ribbon 的依赖也可以不用加，因为 eureka 已经集成了 ribbon



### 3、二说RestTemplate的使用

#### （1）官网

https://docs.spring.io/spring-framework/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220215234118408.png" alt="image-20220215234118408" style="zoom:80%;" />

#### （2）getForObject方法/getForEntity方法

getForObject方法：

返回对象为响应体中数据转化成的对象，基本上可以理解为Json

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220215234243699.png" alt="image-20220215234243699" style="zoom:80%;" />

getForEntity方法：

返回对象为ResponseEntity对象，包含了响应中的一些重要信息，比如响应头、响应状态码、响应体等

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220216003557349.png" alt="image-20220216003557349" style="zoom: 80%;" />

OrderController：

com.atguigu.springcloud.controller.OrderController

```java
@GetMapping("/payment/getForEntity/{id}")
public CommonResult<Payment> getForEntity(@PathVariable("id") Long id) {
    ResponseEntity<CommonResult> entity = restTemplate.getForEntity(PAYMENT_SRV + "/payment/get/" + id, CommonResult.class);
    if (entity.getStatusCode().is2xxSuccessful()) {
        return entity.getBody();
    } else {
        return new CommonResult<>(444, "操作失败");
    }
}
```



```java
@RestController
@Slf4j
@RequestMapping("/consumer")
public class OrderController {

    ///不要把地址写死
    //public static final String PAYMENT_SRV = "http://localhost:8001";
    // 通过在eureka上注册过的微服务名称调用
    public static final String PAYMENT_SRV = "http://CLOUD-PAYMENT-SERVICE";

    @Resource
    private RestTemplate restTemplate;

    /**
     * 客户端用浏览器是get请求，但是底层实质发送post调用服务端8001
     *
     * @param payment
     * @return
     */
    @GetMapping("/payment/create")
    public CommonResult<Payment> create(Payment payment) {
        return restTemplate.postForObject(PAYMENT_SRV + "/payment/create", payment, CommonResult.class);
    }

    @GetMapping("/payment/get/{id}")
    public CommonResult<Payment> getPayment(@PathVariable("id") Long id) {
        return restTemplate.getForObject(PAYMENT_SRV + "/payment/get/" + id, CommonResult.class);
    }

    @GetMapping("/payment/getForEntity/{id}")
    public CommonResult<Payment> getForEntity(@PathVariable("id") Long id) {
        ResponseEntity<CommonResult> entity = restTemplate.getForEntity(PAYMENT_SRV + "/payment/get/" + id, CommonResult.class);
        if (entity.getStatusCode().is2xxSuccessful()) {
            return entity.getBody();
        } else {
            return new CommonResult<>(444, "操作失败");
        }
    }
}
```



测试：http://localhost/consumer/payment/getForEntity/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220216003724293.png" alt="image-20220216003724293" style="zoom:80%;" />

刷新后：

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220216003743058.png" alt="image-20220216003743058" style="zoom:80%;" />

#### （3）postForObject方法/postForEntity方法

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220215235507700.png" alt="image-20220215235507700" style="zoom:80%;" />

#### （4）GET请求方法

```java
<T> T getForObject(String url, Class<T> responseType, Object... uriVariables);

<T> T getForObject(String url, Class<T> responseType, Map<String, ?> uriVariables);

<T> T getForObject(URI url, Class<T> responseType);

<T> ResponseEntity<T> getForEntity(String url, Class<T> responseType, Object... uriVariables);

<T> ResponseEntity<T> getForEntity(String url, Class<T> responseType, Map<String, ?> uriVariables);

<T> ResponseEntity<T> getForEntity(URI var1, Class<T> responseType);
```



#### （5）POST请求方法

```java
<T> T postForObject(String url, @Nullable Object request, Class<T> responseType, Object... uriVariables);

<T> T postForObject(String url, @Nullable Object request, Class<T> responseType, Map<String, ?> uriVariables);

<T> T postForObject(URI url, @Nullable Object request, Class<T> responseType);

<T> ResponseEntity<T> postForEntity(String url, @Nullable Object request, Class<T> responseType, Object... uriVariables);

<T> ResponseEntity<T> postForEntity(String url, @Nullable Object request, Class<T> responseType, Map<String, ?> uriVariables);

<T> ResponseEntity<T> postForEntity(URI url, @Nullable Object request, Class<T> responseType);
```



## （三）Ribbon核心组件IRule

### 1、IRule

IRule：根据特定算法中从服务列表中选取一个要访问的服务

AbstractLoadBalancerRule——快捷键：ctrl+alt+shift+u

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220216004228419.png" alt="image-20220216004228419" style="zoom:80%;" />

1. com.netflix.loadbalancer.RoundRobinRule：轮询
2. com.netflix.loadbalancer.RandomRule：随机
3. com.netflix.loadbalancer.RetryRule：先按照RoundRobinRule的策略获取服务，如果获取服务失败则在指定时间内会进行重试，获取可用的服务
4. WeightedResponseTimeRule：对RoundRobinRule的扩展，响应速度越快的实例选择权重越大，越容易被选择
5. BestAvailableRule：会先过滤掉由于多次访问故障而处于断路器跳闸状态的服务，然后选择一个并发量最小的服务
6. AvailabilityFilteringRule：先过滤掉故障实例，再选择并发较小的实例
7. ZoneAvoidanceRule：默认规则,复合判断server所在区域的性能和server的可用性选择服务器
   
   

### 2、如何替换

#### （1）修改cloud-consumer-order80



#### （2）注意配置细节

官方文档明确给出了警告：

> 这个自定义配置类不能放在@ComponentScan所扫描的当前包下以及子包下，否则我们自定义的这个配置类就会被所有的Ribbon客户端所共享，达不到特殊化定制的目的了。

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220216004850261.png" alt="image-20220216004850261" style="zoom:80%;" />

即不能放在主启动类所在的包下，因为@SpringBootApplication包含了@ComponentScan，它会扫描这个类所在的包及其子包



#### （3）新建package

com.atguigu.myrule

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220216005609454.png" alt="image-20220216005609454" style="zoom:80%;" />

#### （4）MySelfRule规则类

上面包下新建MySelfRule规则类

```java
@Configuration
public class MySelfRule {
    @Bean
    public IRule myRule() {
        // 定义为随机
        return new RandomRule();
    }
}
```



#### （5）主启动类添加@RibbonClient

```java
@RibbonClient(name = "CLOUD-PAYMENT-SERVICE", configuration = MySelfRule.class)
```



```java
@SpringBootApplication
@EnableEurekaClient
@RibbonClient(name = "CLOUD-PAYMENT-SERVICE", configuration = MySelfRule.class)
public class MainApp80 {
    public static void main(String[] args) {
        SpringApplication.run(MainApp80.class, args);
    }
}
```



**问题？？？**

这里的 CLOUD-PAYMENT-SERVICE 如果是大写就是我们定义的随机访问规则；

如果是小写 cloud-payment-service 则我们定义的不生效，它还是轮询访问



如果是小写，但是把 MySelfRule 放在 @ComponentScan 可以扫描的包下时则又可以随机访问了

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220216011602360.png" alt="image-20220216011602360" style="zoom:80%;" />

#### （6）测试

http://localhost/consumer/payment/get/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220216010211882.png" alt="image-20220216010211882" style="zoom:80%;" />

刷新后就不再是轮询了，而是随机负载均衡了



## （四）Ribbon负载均衡算法

### 1、原理

负载均衡算法：rest接口第几次请求数 % 服务器集群总数量 = 实际调用服务器位置下标  ，每次服务重启动后rest接口计数从1开始

```java
List<ServiceInstance> instances = discoveryClient.getInstances("CLOUD-PAYMENT-SERVICE");
```

```java
如：    List [0] instances = 127.0.0.1:8002
     List [1] instances = 127.0.0.1:8001
```

8001+ 8002 组合成为集群，它们共计2台机器，集群总数为2， 按照轮询算法原理：

当总请求数为1时：1 % 2 =1 对应下标位置为1 ，则获得服务地址为127.0.0.1:8001

当总请求数位2时：2 % 2 =0 对应下标位置为0 ，则获得服务地址为127.0.0.1:8002

当总请求数位3时：3 % 2 =1 对应下标位置为1 ，则获得服务地址为127.0.0.1:8001

当总请求数位4时：4 % 2 =0 对应下标位置为0 ，则获得服务地址为127.0.0.1:8002

如此类推......



### 2、RoundRobinRule源码

见哔哩哔哩尚硅谷视频：https://www.bilibili.com/video/BV18E411x7eT?p=41&spm_id_from=pageDriver



### 3、手写

自己试着写一个本地负载均衡器试试

7001/7002集群启动

8001/8002微服务改造



# 七、SpringCloud  OpenFeign 服务接口调用

## （一）概述

### 1、OpenFeign是什么

官网解释：
https://cloud.spring.io/spring-cloud-static/Hoxton.SR1/reference/htmlsingle/#spring-cloud-openfeign

Feign是一个声明式WebService客户端，使用Feign能让编写Web Service客户端更加简单，它的使用方法是定义一个服务接口然后在上面添加注解，Feign也支持可拔插式的编码器和解码器，Spring Cloud对Feign进行了封装，使其支持了Spring MVC标准注解和HttpMessageConverters，Feign可以与Eureka和Ribbon组合使用以支持负载均衡



Feign是一个声明式的Web服务客户端，让编写Web服务客户端变得非常容易，只需创建一个接口并在接口上添加注解即可



GitHub：https://github.com/spring-cloud/spring-cloud-openfeign



### 2、能干嘛

Feign旨在使编写Java Http客户端变得更容易，前面在使用Ribbon+RestTemplate时，利用RestTemplate对http请求的封装处理，形成了一套模版化的调用方法。但是在实际开发中，由于对服务依赖的调用可能不止一处，往往一个接口会被多处调用，所以通常都会针对每个微服务自行封装一些客户端类来包装这些依赖服务的调用。所以，Feign在此基础上做了进一步封装，由他来帮助我们定义和实现依赖服务接口的定义。在Feign的实现下，我们只需创建一个接口并使用注解的方式来配置它(以前是Dao接口上面标注Mapper注解，现在是一个微服务接口上面标注一个Feign注解即可)，即可完成对服务提供方的接口绑定，简化了使用Spring cloud Ribbon时，自动封装服务调用客户端的开发量。

Feign集成了Ribbon，利用Ribbon维护了Payment的服务列表信息，并且通过轮询实现了客户端的负载均衡。而与Ribbon不同的是，通过feign只需要定义服务绑定接口且以声明式的方法，优雅而简单的实现了服务调用



### 3、Feign和OpenFeign两者区别

Feign：

- Feign是Spring Cloud组件中的一个轻量级RESTful的HTTP服务客户端
- Feign内置了Ribbon，用来做客户端负载均衡，去调用服务注册中心的服务
- Feign的使用方式是：使用Feign的注解定义接口，调用这个接口，就可以调用服务注册中心的服务

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-feign</artifactId>
</dependency>
```



OpenFeign：

- OpenFeign是Spring Cloud 在Feign的基础上支持了SpringMVC的注解，如@RequesMapping等等
- OpenFeign的@FeignClient可以解析SpringMVC的@RequestMapping注解下的接口，并通过动态代理的方式产生实现类，实现类中做负载均衡并调用其他服务

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```



## （二）OpenFeign使用步骤

接口+注解：微服务调用接口+@FeignClient

### 1、新建cloud-consumer-feign-order80

Feign在消费端使用



### 2、pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-consumer-feign-order80</artifactId>

    <dependencies>
        <!--openfeign-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
        <!--eureka client-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <!--web-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--一般基础通用配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



### 3、application.yml

```yaml
server:
  port: 80

eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/,http://eureka7002.com:7002/eureka/
```



### 4、主启动

com.atguigu.springcloud.OrderFeignMain80

```java
@EnableFeignClients
```

```java
@SpringBootApplication
@EnableFeignClients
public class OrderFeignMain80 {
    public static void main(String[] args) {
        SpringApplication.run(OrderFeignMain80.class, args);
    }
}
```



### 5、业务类

业务逻辑接口+@FeignClient配置调用provider服务

新建PaymentFeignService接口并新增注解@FeignClient

com.atguigu.springcloud.service.PaymentFeignService

```java
@FeignClient(value = "CLOUD-PAYMENT-SERVICE")
public interface PaymentFeignService {
    @GetMapping("/payment/get/{id}")
    CommonResult getPaymentById(@PathVariable("id") Long id);
}
```



@FeignClient value 的内容就是 Eureka 中要调用的微服务的名

![image-20220306115624149](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306115624149.png)



Service 中的内容是复制的 8001 的 Controller 的方法头



控制层Controller

com.atguigu.springcloud.controller.OrderFeignController

```java
@RestController
public class OrderFeignController {
    @Resource
    private PaymentFeignService paymentFeignService;

    @GetMapping(value = "/consumer/payment/get/{id}")
    public CommonResult<Payment> getPaymentById(@PathVariable("id") Long id) {
        return paymentFeignService.getPaymentById(id);
    }
}
```



### 6、测试

说明：如果是单机版就停一个，不用开俩

1. 先启动2个eureka集群7001/7002
2. 再启动2个微服务8001/8002
3. 启动OpenFeign启动
4. http://localhost/consumer/payment/get/1
5. Feign自带负载均衡配置项
   
   

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306121254815.png" alt="image-20220306121254815"  />

### 7、小总结

![image-20220306121623012](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306121623012.png)



这里能调到和方法名无关，只和路径有关，只是路径！路径！！



## （三）OpenFeign超时控制

### 1、模拟超时

超时设置，故意设置超时演示出错情况

服务提供方8001和8002故意写暂停程序

```java
@Value("${server.port}")
private String serverPort;

@GetMapping(value = "/feign/timeout")
public String paymentFeignTimeOut() {
    System.out.println("*****paymentFeignTimeOut from port: " + serverPort);
    //暂停几秒钟线程
    try {
        TimeUnit.SECONDS.sleep(3);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    return serverPort;
}
```



服务消费方80添加超时方法，PaymentFeignService

```java
@GetMapping(value = "/payment/feign/timeout")
String paymentFeignTimeOut();
```



服务消费方80添加超时方法，OrderFeignController

```java
@GetMapping(value = "/consumer/payment/feign/timeout")
public String paymentFeignTimeOut() {
    return paymentFeignService.paymentFeignTimeOut();
}
```



先自测8001：http://localhost:8001/payment/feign/timeout

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306134101402.png" alt="image-20220306134101402" style="zoom:80%;" />

测试：http://localhost/consumer/payment/feign/timeout

![image-20220306134607785](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306134607785.png)



### 2、分析

为什么自测的8001不报错，而80调用报错了呢？

- OpenFeign默认等待1秒钟，超过后报错 
  
  

OpenFeign超时控制是什么？

- 默认Feign客户端只等待一秒钟，但是服务端处理需要超过1秒钟，导致Feign客户端不想等待了，直接返回报错。为了避免这样的情况，有时候我们需要设置Feign客户端的超时控制
  
  

OpenFeign默认支持Ribbon

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306140057567.png" alt="image-20220306140057567" style="zoom:80%;" />

YML文件里需要开启OpenFeign客户端超时控制

80的yaml文件中

```yaml
#设置feign客户端超时时间(OpenFeign默认支持ribbon)
ribbon:
  #指的是建立连接后从服务器读取到可用资源所用的时间
  ReadTimeout: 5000
  #指的是建立连接所用的时间，适用于网络状况正常的情况下,两端连接所用的时间
  ConnectTimeout: 5000
```



<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306140834581.png" alt="image-20220306140834581" style="zoom:80%;" />

### 3、OpenFeign日志打印功能

Feign 提供了日志打印功能，我们可以通过配置来调整日志级别，从而了解 Feign 中 Http 请求的细节。
说白了就是对Feign接口的调用情况进行监控和输出



日志级别

- NONE：默认的，不显示任何日志

- BASIC：仅记录请求方法、URL、响应状态码及执行时间

- HEADERS：除了 BASIC 中定义的信息之外，还有请求和响应的头信息

- FULL：除了 HEADERS 中定义的信息之外，还有请求和响应的正文及元数据
  
  

配置日志bean

com.atguigu.springcloud.config.FeignConfig

```java
@Configuration
public class FeignConfig {
    @Bean
    Logger.Level feignLoggerLevel() {
        return Logger.Level.FULL;
    }
}
```



YML文件里需要开启日志的Feign客户端

```yaml
logging:
  level:
    # feign日志以什么级别监控哪个接口
    com.atguigu.springcloud.service.PaymentFeignService: debug
```



测试：http://localhost/consumer/payment/get/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306142900755.png" alt="image-20220306142900755" style="zoom:80%;" />

后台日志查看

![image-20220306143550197](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306143550197.png)



也可以直接在yaml中配置：feign.client.config.default.loggerLevel: FULL，其中"default”可以换成FeignClient中配置的name属性，也可以直接用default，对应的是FeignClientProperties类中的config属性。该类为Feign自动配置类引入的配置项类



# 八、SpringCloud Hystrix 断路器

## （一）概述

### 1、分布式系统面临的问题

复杂分布式体系结构中的应用程序有数十个依赖关系，每个依赖关系在某些时候将不可避免地失败

![image-20220306144150599](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306144150599.png)



服务雪崩：

多个微服务之间调用的时候，假设微服务A调用微服务B和微服务C，微服务B和微服务C又调用其它的微服务，这就是所谓的“扇出”，如果扇出的链路上某个微服务的调用响应时间过长或者不可用，对微服务A的调用就会占用越来越多的系统资源，进而引起系统崩溃，所谓的“雪崩效应”

对于高流量的应用来说，单一的后端依赖可能会导致所有服务器上的所有资源都在几秒钟内饱和，比失败更糟糕的是，这些应用程序还可能导致服务之间的延迟增加、备份队列、线程和其他系统资源紧张，导致整个系统发生更多的级联故障，这些都表示需要对故障和延迟进行隔离和管理，以便单个依赖关系的失败，不能取消整个应用程序或系统，所以，通常当你发现一个模块下的某个实例失败后，这时候这个模块依然还会接收流量，然后这个有问题的模块还调用了其他的模块，这样就会发生级联故障，或者叫雪崩



### 2、Hystrix 是什么

Hystrix是一个用于处理分布式系统的延迟和容错的开源库，在分布式系统里，许多依赖不可避免的会调用失败，比如超时、异常等，Hystrix能够保证在一个依赖出问题的情况下，不会导致整体服务失败，避免级联故障，以提高分布式系统的弹性。

“断路器”本身是一种开关装置，当某个服务单元发生故障之后，通过断路器的故障监控（类似熔断保险丝），向调用方返回一个符合预期的、可处理的备选响应（FallBack），而不是长时间的等待或者抛出调用方无法处理的异常，这样就保证了服务调用方的线程不会被长时间、不必要地占用，从而避免了故障在分布式系统中的蔓延，乃至雪崩。



### 3、Hystrix能干嘛

服务降级、服务熔断、接近实时的监控······



官网资料：https://github.com/Netflix/Hystrix/wiki/How-To-Use

Hystrix官宣，停更进维：https://github.com/Netflix/Hystrix

被动修复bugs、不再接受合并请求、不再发布新版本



## （二）Hystrix重要概念

### 1、服务降级

服务器忙，请稍后再试，不让客户端等待并立刻返回一个友好提示，fallback



哪些情况会出发降级？

- 程序运行异常
- 超时
- 服务熔断触发服务降级
- 线程池/信号量打满也会导致服务降级
  
  

### 2、服务熔断

类比保险丝达到最大服务访问后，直接拒绝访问，拉闸限电，然后调用服务降级的方法并返回友好提示

就是保险丝：服务的降级->进而熔断->恢复调用链路



### 3、服务限流

秒杀高并发等操作，严禁一窝蜂的过来拥挤，大家排队，一秒钟N个，有序进行



## （三）hystrix案例

### 1、构建 hystrix-payment8001

新建cloud-provider-hystrix-payment8001

pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-provider-hystrix-payment8001</artifactId>

    <dependencies>
        <!--hystrix-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
        </dependency>
        <!--eureka client-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <!--web-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```



application.yml

```yaml
server:
  port: 8001

spring:
  application:
    name: cloud-provider-hystrix-payment
  main:
    allow-bean-definition-overriding: true #当遇到同样名字的时候，是否允许覆盖注册

eureka:
  client:
    register-with-eureka: true
    fetch-registry: true
    service-url:
      #defaultZone: http://eureka7001.com:7001/eureka,http://eureka7002.com:7002/eureka
      defaultZone: http://eureka7001.com:7001/eureka
```



主启动：com.atguigu.springcloud.PaymentHystrixMain8001

```java
@SpringBootApplication
@EnableEurekaClient //本服务启动后会自动注册进eureka服务中
public class PaymentHystrixMain8001 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentHystrixMain8001.class, args);
    }
}
```



业务类

Service：com.atguigu.springcloud.service.PaymentService

```java
public interface PaymentService {
    /**
     * 正常访问一切 OK
     *
     * @param id
     * @return
     */
    String paymentInfoOk(Integer id);

    /**
     * 超时访问，演示降级
     *
     * @param id
     * @return
     */
    String paymentInfoTimeOut(Integer id);
}
```



ServiceImpl：com.atguigu.springcloud.service.Impl.PaymentServiceImpl

```java
@Service
public class PaymentServiceImpl implements PaymentService {
    @Override
    public String paymentInfoOk(Integer id) {
        return "线程池:" + Thread.currentThread().getName() + "paymentInfo_OK,id: " + id + "\t" + "O(∩_∩)O";
    }

    @Override
    public String paymentInfoTimeOut(Integer id) {
        try {
            TimeUnit.SECONDS.sleep(5);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        return "线程池:" + Thread.currentThread().getName() + "paymentInfo_TimeOut,id: " + id + "\t" + "O(∩_∩)O，耗费3秒";

    }
}
```



Controller：com.atguigu.springcloud.controller.PaymentController

```java
@RestController
@Slf4j
public class PaymentController {
    @Autowired
    private PaymentService paymentService;

    @Value("${server.port}")
    private String serverPort;


    @GetMapping("/payment/hystrix/ok/{id}")
    public String paymentInfoOk(@PathVariable("id") Integer id) {
        String result = paymentService.paymentInfoOk(id);
        log.info("****result: " + result);
        return result;
    }

    @GetMapping("/payment/hystrix/timeout/{id}")
    public String paymentInfoTimeOut(@PathVariable("id") Integer id) throws InterruptedException {
        String result = paymentService.paymentInfoTimeOut(id);
        log.info("****result: " + result);
        return result;
    }
}
```



正常测试

- 启动eureka7001
- 启动cloud-provider-hystrix-payment8001
- 访问
  - success的方法：http://localhost:8001/payment/hystrix/ok/1
  - 每次调用耗费5秒钟：http://localhost:8001/payment/hystrix/timeout/1
    
    

上述module均OK，以上述为根基平台，从正确->错误->降级熔断->恢复



<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306155438769.png" alt="image-20220306155438769" style="zoom:80%;" />

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306155511986.png" alt="image-20220306155511986" style="zoom:80%;" />

### 2、高并发测试

上述在非高并发情形下，还能勉强满足



Jmeter压测测试：

开启Jmeter，来20000个并发压死8001，20000个请求都去访问paymentInfo_TimeOut服务

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306160306575.png" alt="image-20220306160306575" style="zoom:67%;" />

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306162945296.png" alt="image-20220306162945296" style="zoom:67%;" />

再来一个访问：http://localhost:8001/payment/hystrix/ok/1



看演示结果：两个都在自己转圈圈，为什么会被卡死？

- tomcat的默认的工作线程数被打满了，没有多余的线程来分解压力和处理
  
  

Jmeter压测结论：

上面还是服务提供者8001自己测试，假如此时外部的消费者80也来访问，那消费者只能干等，最终导致消费端80不满意，服务端8001直接被拖死

看热闹不嫌弃事大，80新建加入



### 3、构建 hystrix-order80 再压测

cloud-consumer-feign-hystrix-order80

pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-consumer-feign-hystrix-order80</artifactId>

    <dependencies>
        <!--openfeign-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
        <!--hystrix-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
        </dependency>
        <!--eureka client-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <!--web-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--一般基础通用配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



application.yml

```yaml
server:
  port: 80

spring:
  application:
    name: cloud-consumer-feign-hystrix-order
  main:
    allow-bean-definition-overriding: true #当遇到同样名字的时候，是否允许覆盖注册

eureka:
  client:
    register-with-eureka: false
    service-url:
      defaultZone: http://eureka7001.com:7001/eureka/
```



主启动：com.atguigu.springcloud.OrderHystrixMain80

```java
@SpringBootApplication
@EnableFeignClients
public class OrderHystrixMain80 {
    public static void main(String[] args) {
        SpringApplication.run(OrderHystrixMain80.class, args);
    }
}
```



业务类

PaymentHystrixService

com.atguigu.springcloud.service.PaymentHystrixService

```java
@Component
@FeignClient(value = "CLOUD-PROVIDER-HYSTRIX-PAYMENT")
public interface PaymentHystrixService {
    @GetMapping("/payment/hystrix/ok/{id}")
    String paymentInfoOk(@PathVariable("id") Integer id);

    @GetMapping("/payment/hystrix/timeout/{id}")
    String paymentInfoTimeOut(@PathVariable("id") Integer id);
}
```



OrderHystrixController

com.atguigu.springcloud.controller.OrderHystrixController

```java
@RestController
@Slf4j
public class OrderHystrixController {
    @Resource
    private PaymentHystrixService paymentHystrixService;

    @GetMapping("/consumer/payment/hystrix/ok/{id}")
    public String paymentInfoOk(@PathVariable("id") Integer id) {
        String result = paymentHystrixService.paymentInfoOk(id);
        return result;
    }

    @GetMapping("/consumer/payment/hystrix/timeout/{id}")
    public String paymentInfoTimeOut(@PathVariable("id") Integer id) {
        String result = paymentHystrixService.paymentInfoTimeOut(id);
        return result;
    }
}
```



正常测试：http://localhost/consumer/payment/hystrix/ok/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306165045615.png" alt="image-20220306165045615" style="zoom:67%;" />

高并发测试：

- 2W个线程压8001
- 消费端80微服务再去访问正常的Ok微服务8001地址
- http://localhost/consumer/payment/hystrix/ok/1
- 消费者80，o(╥﹏╥)o
  - 要么转圈圈等待
  - 要么消费端报超时错误

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306165228402.png" alt="image-20220306165228402" style="zoom:67%;" />

### 4、故障现象和导致原因

- 8001同一层次的其它接口服务被困死，因为tomcat线程池里面的工作线程已经被挤占完毕
- 80此时调用8001，客户端访问响应缓慢，转圈圈
  
  

上诉结论：正因为有上述故障或不佳表现，才有我们的降级/容错/限流等技术诞生



### 5、如何解决？解决的要求

超时导致服务器变慢(转圈)：超时不再等待

出错(宕机或程序运行出错)：出错要有兜底



解决：

- 对方服务(8001)超时了，调用者(80)不能一直卡死等待，必须有服务降级
- 对方服务(8001)宕机了，调用者(80)不能一直卡死等待，必须有服务降级
- 对方服务(8001)OK，调用者(80)自己出故障或有自我要求（自己的等待时间小于服务提供者）自己处理降级
  
  

## （四）服务降级

降级配置：@HystrixCommand



8001先从自身找问题：设置自身调用超时时间的峰值，峰值内可以正常运行，超过了需要有兜底的方法处理，作服务降级fallback



### 1、8001fallback

#### （1）业务类启用

```java
@Service
public class PaymentServiceImpl implements PaymentService {


    /**
     * 正常访问一切 OK
     *
     * @param id
     * @return
     */
    @Override
    public String paymentInfoOk(Integer id) {
        return "线程池:" + Thread.currentThread().getName() + "paymentInfo_OK,id: " + id + "\t" + "O(∩_∩)O";
    }

    /**
     * 超时访问，演示降级
     *
     * @param id
     * @return
     */
    @Override
    @HystrixCommand(fallbackMethod = "paymentInfoTimeOutHandler", commandProperties = {
            @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds", value = "3000")
    })
    public String paymentInfoTimeOut(Integer id) {
        try {
            TimeUnit.SECONDS.sleep(5);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        return "线程池:" + Thread.currentThread().getName() + "paymentInfo_TimeOut,id: " + id + "\t" + "O(∩_∩)O，耗费3秒";

    }

    /**
     * 超时访问的降级方法
     *
     * @param id
     * @return
     */
    public String paymentInfoTimeOutHandler(Integer id) {
        return "/(ㄒoㄒ)/调用支付接口超时或异常：\t" + "\t当前线程池名字" + Thread.currentThread().getName();
    }
}
```



@HystrixCommand报异常后如何处理？

一旦调用服务方法失败并抛出了错误信息后，会自动调用@HystrixCommand标注好的fallbackMethod调用类中的指定方法



图示：

![image-20220306172830815](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306172830815.png)



上图故意制造两个异常：

- int age = 10/0; 计算异常
- 我们能接受3秒钟，它运行5秒钟，超时异常

当前服务不可用了，做服务降级，兜底的方案都是 paymentInfo_TimeOutHandler



#### （2）主启动类激活

添加新注解@EnableCircuitBreaker



测试：http://localhost:8001/payment/hystrix/timeout/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306173930649.png" alt="image-20220306173930649" style="zoom:80%;" />

### 2、80fallback

80订单微服务，也可以更好的保护自己，自己也依样画葫芦进行客户端降级保护

题外话，切记：我们自己配置过的热部署方式对java代码的改动明显，但对@HystrixCommand内属性的修改建议重启微服务



#### （1）主启动：OrderHystrixMain80

```java
@EnableHystrix
```



#### （2）application.yml

```yaml
feign:
  hystrix:
    enabled: true

hystrix:
  command:
    default:
      execution:
        isolation:
          thread:
            timeoutInMilliseconds: 5000

#设置feign客户端超时时间(OpenFeign默认支持ribbon)
ribbon:
  #指的是建立连接后从服务器读取到可用资源所用的时间
  ReadTimeout: 5000
  #指的是建立连接所用的时间，适用于网络状况正常的情况下,两端连接所用的时间
  ConnectTimeout: 5000
```



#### （3）OrderHystrixController

```java
@RestController
@Slf4j
public class OrderHystrixController {
    @Resource
    private PaymentHystrixService paymentHystrixService;

    @GetMapping("/consumer/payment/hystrix/ok/{id}")
    public String paymentInfoOk(@PathVariable("id") Integer id) {
        String result = paymentHystrixService.paymentInfoOk(id);
        return result;
    }

    @GetMapping("/consumer/payment/hystrix/timeout/{id}")
    @HystrixCommand(fallbackMethod = "paymentTimeOutFallbackMethod", commandProperties = {
            @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds", value = "1500")
    })
    public String paymentInfoTimeOut(@PathVariable("id") Integer id) {
        String result = paymentHystrixService.paymentInfoTimeOut(id);
        return result;
    }

    public String paymentTimeOutFallbackMethod(@PathVariable("id") Integer id) {
        return "我是消费者80,对方支付系统繁忙请10秒钟后再试或者自己运行出错请检查自己,o(╥﹏╥)o";
    }
}
```



测试之前先把8001的超时时间和睡眠时间调整：

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306191819490.png" alt="image-20220306191819490"  />

测试：http://localhost/consumer/payment/hystrix/timeout/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306191646137.png" alt="image-20220306191646137" style="zoom: 80%;" />

把80客户端的超时时间换成4s

```java
@GetMapping("/consumer/payment/hystrix/timeout/{id}")
@HystrixCommand(fallbackMethod = "paymentTimeOutFallbackMethod", commandProperties = {
        @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds", value = "4000")
})
```

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306193125214.png" alt="image-20220306193125214" style="zoom:80%;" />

#### （4）说明

是否调用兜底fallback方法是取决于 `@HystrixProperty 中的 value = "4000"`，只要这个value的值大于服务端8001的睡眠时间或进来就直接异常，比如说 10/0 就会走80的fallback方法，与application.yml中配置的ribbon的那个feign的超时时间以及hystrix的时间无关



以下来自B站网友fan9833在视频https://www.bilibili.com/video/BV18E411x7eT下的回复评论

> p55，controller中超时时间配置不生效原因：
>        关键在于feign:hystrix:enabled: true的作用，官网解释“Feign将使用断路器包装所有方法”，也就是将@FeignClient标记的那个service接口下所有的方法进行了hystrix包装（类似于在这些方法上加了一个@HystrixCommand），这些方法会应用一个默认的超时时间为1s，所以你的service方法也有一个1s的超时时间，service1s就会报异常，controller立马进入备用方法，controller上那个3秒那超时时间就没有效果了。
> 改变这个默认超时时间方法：
> 
> ```yaml
> hystrix:
>   command:
>     default:
>       execution:
>         isolation:
>           thread:
>             timeoutInMilliseconds: 3000
> ```
> 
> 然后ribbon的超时时间也需加上
> 
> ```yaml
> ribbon:
>   ReadTimeout: 5000
>   ConnectTimeout: 5000
> ```



### 3、问题和解决方案

#### （1）目前问题

- 每个业务方法对应一个兜底的方法，代码膨胀
- 统一和自定义的分开
  
  

#### （2）解决方案一

- 每个方法配置一个？？？膨胀
  - feign接口系列
  - @DefaultProperties(defaultFallback = "")
  - <img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306190859060.png" alt="image-20220306190859060" style="zoom:67%;" />

说明：@DefaultProperties(defaultFallback = "")

1. 每个方法配置一个服务降级方法，技术上可以，实际上傻X

2. N 除了个别重要核心业务有专属，其它普通的可以通过@DefaultProperties(defaultFallback = "")  统一跳转到统一处理结果页面

通用的和独享的各自分开，避免了代码膨胀，合理减少了代码量，O(∩_∩)O哈哈~ 



controller配置：

```java
@DefaultProperties(defaultFallback = "paymentGlobalFallbackMethod")
public class OrderHystrixController {
    // ···

    //@HystrixCommand(fallbackMethod = "paymentTimeOutFallbackMethod", commandProperties = {
    //@HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds", value = "4000")
    //})
    @HystrixCommand //加了@DefaultProperties属性注解，并且没有写具体方法名字，就用统一全局的
    public String paymentInfoTimeOut(@PathVariable("id") Integer id) {
        String result = paymentHystrixService.paymentInfoTimeOut(id);
        return result;
    }

    /**
     * 全局fallback方法
     *
     * @return
     */
    public String paymentGlobalFallbackMethod() {
        return "Global异常处理信息，请稍后再试，/(ㄒoㄒ)/~~";
    }
}
```



<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306212437297.png" alt="image-20220306212437297" style="zoom:80%;" />

#### （3）解决方案二

和业务逻辑混一起？？？混乱

- 服务降级，客户端去调用服务端，碰上服务端宕机或关闭

- 本次案例服务降级处理是在客户端80实现完成的，与服务端8001没有关系，只需要为Feign客户端定义的接口添加一个服务降级处理的实现类即可实现解耦
- 未来我们要面对的异常
  - 运行
  - 超时
  - 宕机
- 再看我们的业务类PaymentController【混合在一块 ，每个业务方法都要提供一个】

![image-20220306210727062](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306210727062.png)



##### ① 修改 feign-hystrix-order80

根据cloud-consumer-feign-hystrix-order80已经有的PaymentHystrixService接口，重新新建一个类(PaymentFallbackServiceImpl)实现该接口，统一为接口里面的方法进行异常处理

PaymentFallbackServiceImpl类实现PaymentHystrixService接口



<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307000700182.png" alt="image-20220307000700182" style="zoom: 67%;" />

##### ② 兜底fallback类

新建com.atguigu.springcloud.service.fallback.PaymentFallbackServiceImpl

```java
@Component //必须加 //必须加 //必须加
public class PaymentFallbackServiceImpl implements PaymentHystrixService {

    @Override
    public String paymentInfoOk(Integer id) {
        return "====PaymentHystrixService fall back paymentInfoOk，o(╥﹏╥)o====";
    }

    @Override
    public String paymentInfoTimeOut(Integer id) {
        return "====PaymentHystrixService fall back paymentInfoTimeOut，o(╥﹏╥)o====";
    }
}
```



改造 PaymentHystrixService：com.atguigu.springcloud.service.PaymentHystrixService

```java
@FeignClient(value = "CLOUD-PROVIDER-HYSTRIX-PAYMENT",fallback = PaymentFallbackServiceImpl.class)
```



#### （4）测试

依次启动7001、8001、80

正常访问测试：http://localhost/consumer/payment/hystrix/ok/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307000556413.png" alt="image-20220307000556413" style="zoom:80%;" />

故意关闭微服务8001，客户端自己调用提示，此时服务端provider已经down了，但是我们做了服务降级处理，
让客户端在服务端不可用时也会获得提示信息而不会挂起耗死服务器

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307001003524.png" alt="image-20220307001003524" style="zoom: 67%;" />

tips：服务端宕机会调用这个兜底的实现类中的方法，但是客户端中的方法出错还是会调用方法头上那个注解



## （五）服务熔断

断路器：一句话就是家里的保险丝



### 1、熔断是什么

熔断机制概述：

熔断机制是应对雪崩效应的一种微服务链路保护机制，当扇出链路的某个微服务出错不可用或者响应时间太长时，
会进行服务的降级，进而熔断该节点微服务的调用，快速返回错误的响应信息，当检测到该节点微服务调用响应正常后，恢复调用链路

在Spring Cloud框架里，熔断机制通过Hystrix实现。Hystrix会监控微服务间调用的状况，当失败的调用到一定阈值，缺省是5秒内20次调用失败，就会启动熔断机制。熔断机制的注解是@HystrixCommand



大神论文：https://martinfowler.com/bliki/CircuitBreaker.html



总结：降解是思想，熔断是对降解的具体实现，但是降解的实现并不止熔断这一种

1. 调用失败会触发降级，而降级会调用fallback方法
2. 但无论如何降级的流程一定会先调用正常方法再调用fallback方法
3. 假如单位时间内调用失败次数过多，也就是降级次数过多，则触发熔断
4. 熔断以后就会跳过正常方法直接调用fallback方法
5. 所谓“熔断后服务不可用”就是因为跳过了正常方法直接执行fallback
   
   

### 2、实操

修改：cloud-provider-hystrix-payment8001

PaymentService：com.atguigu.springcloud.service.PaymentService

```java
String paymentCircuitBreaker(@PathVariable("id") Integer id);
```



PaymentServiceImpl：com.atguigu.springcloud.service.Impl.PaymentServiceImpl

```java
// =====服务熔断=====
@Override
@HystrixCommand(fallbackMethod = "paymentCircuitBreaker_fallback", commandProperties = {
        @HystrixProperty(name = "circuitBreaker.enabled", value = "true"),// 是否开启断路器
        @HystrixProperty(name = "circuitBreaker.requestVolumeThreshold", value = "10"),// 请求次数
        @HystrixProperty(name = "circuitBreaker.sleepWindowInMilliseconds", value = "10000"),// 时间窗口期
        @HystrixProperty(name = "circuitBreaker.errorThresholdPercentage", value = "60"),// 失败率达到多少后跳闸
})
public String paymentCircuitBreaker(@PathVariable("id") Integer id) {
    if (id < 0) {
        throw new RuntimeException("******id 不能负数");
    }
    String serialNumber = IdUtil.simpleUUID();

    return Thread.currentThread().getName() + "\t" + "调用成功，流水号: " + serialNumber;
}

public String paymentCircuitBreaker_fallback(@PathVariable("id") Integer id) {
    return "id 不能负数，请稍后再试，/(ㄒoㄒ)/~~   id: " + id;
}
```



> 1. 这个时间窗口期是打开短路器之后到尝试恢复，期间拒绝请求的时间
> 2. 时间窗口期是指保险丝开启后经过的一段时间再转换为半开状态的时间



why配置这些参数？

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307004353733.png" alt="image-20220307004353733" style="zoom: 80%;" />

PaymentController：com.atguigu.springcloud.controller.PaymentController

```java
// ====服务熔断=====
@GetMapping("/payment/circuit/{id}")
public String paymentCircuitBreaker(@PathVariable("id") Integer id) {
    String result = paymentService.paymentCircuitBreaker(id);
    log.info("****result: " + result);
    return result;
}
```



### 3、测试

自测cloud-provider-hystrix-payment8001：http://localhost:8001/payment/circuit/1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307004921881.png" alt="image-20220307004921881" style="zoom:80%;" />

http://localhost:8001/payment/circuit/-31

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307005001104.png" alt="image-20220307005001104" style="zoom:80%;" />

一次正确一次错误trytry



重点测试，多次错误，然后慢慢正确，发现刚开始不满足条件，就算是正确的访问地址也不能进行

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307005411645.png" alt="image-20220307005411645" style="zoom:80%;" />

### 4、原理(小总结)

#### （1）大神结论

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307005614863.png" alt="image-20220307005614863" style="zoom:80%;" />

#### （2）熔断类型

- 熔断打开
  - 请求不再进行调用当前服务，内部设置时钟一般为MTTR（平均故障处理时间)，当打开时长达到所设时钟则进入半熔断状态
- 熔断关闭
  - 熔断关闭不会对服务进行熔断
- 熔断半开
  - 部分请求根据规则调用当前服务，如果请求成功且符合规则则认为当前服务恢复正常，关闭熔断
    
    

#### （3）官网断路器流程图

![image-20220307005806670](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307005806670.png)



#### （4）官网步骤

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307005832881.png" alt="image-20220307005832881" style="zoom:80%;" />

#### （5）断路器在什么情况下开始起作用

![image-20220307005849631](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307005849631.png)



涉及到断路器的三个重要参数：请求总数阈值、快照时间窗、错误百分比阈值

- 请求总数阈值：在快照时间窗内，必须满足请求总数阀值才有资格熔断。默认为20，意味着在10秒内，如果该hystrix命令的调用次数不足20次，即使所有的请求都超时或其他原因失败，断路器都不会打开

- 快照时间窗：断路器确定是否打开需要统计一些请求和错误数据，而统计的时间范围就是快照时间窗，默认为最近的10秒【这个时间窗口期是打开短路器之后到尝试恢复，期间拒绝请求的时间】

- 错误百分比阈值：当请求总数在快照时间窗内超过了阀值，比如发生了30次调用，如果在这30次调用中，有15次发生了超时异常，也就是超过50%的错误百分比，在默认设定50%阀值情况下，这时候就会将断路器打开
  
  

#### （6）断路器开启或者关闭的条件

1. 当满足一定的阀值的时候（默认10秒内超过20个请求次数）
2. 当失败率达到一定的时候（默认10秒内超过50%的请求失败）
3. 到达以上阀值，断路器将会开启
4. 当开启的时候，所有请求都不会进行转发
5. 一段时间之后（默认是5秒），这个时候断路器是半开状态，会让其中一个请求进行转发；如果成功，断路器会关闭；若失败，继续开启。重复4和5
   
   

#### （7）断路器打开之后

再有请求调用的时候，将不会调用主逻辑，而是直接调用降级fallback，通过断路器，实现了自动地发现错误并将降级逻辑切换为主逻辑，减少响应延迟的效果



#### （8）原来的主逻辑如何恢复

对于这一问题，hystrix也为我们实现了自动恢复功能。当断路器打开，对主逻辑进行熔断之后，hystrix会启动一个休眠时间窗，在这个时间窗内，降级逻辑是临时的成为主逻辑，当休眠时间窗到期，断路器将进入半开状态，释放一次请求到原来的主逻辑上，如果此次请求正常返回，那么断路器将继续闭合，主逻辑恢复；如果这次请求依然有问题，断路器继续进入打开状态，休眠时间窗重新计时



#### （9）All配置

```java
//========================All
@HystrixCommand(fallbackMethod = "str_fallbackMethod",
        groupKey = "strGroupCommand",
        commandKey = "strCommand",
        threadPoolKey = "strThreadPool",

        commandProperties = {
                // 设置隔离策略，THREAD 表示线程池 SEMAPHORE：信号池隔离
                @HystrixProperty(name = "execution.isolation.strategy", value = "THREAD"),
                // 当隔离策略选择信号池隔离的时候，用来设置信号池的大小（最大并发数）
                @HystrixProperty(name = "execution.isolation.semaphore.maxConcurrentRequests", value = "10"),
                // 配置命令执行的超时时间
                @HystrixProperty(name = "execution.isolation.thread.timeoutinMilliseconds", value = "10"),
                // 是否启用超时时间
                @HystrixProperty(name = "execution.timeout.enabled", value = "true"),
                // 执行超时的时候是否中断
                @HystrixProperty(name = "execution.isolation.thread.interruptOnTimeout", value = "true"),
                // 执行被取消的时候是否中断
                @HystrixProperty(name = "execution.isolation.thread.interruptOnCancel", value = "true"),
                // 允许回调方法执行的最大并发数
                @HystrixProperty(name = "fallback.isolation.semaphore.maxConcurrentRequests", value = "10"),
                // 服务降级是否启用，是否执行回调函数
                @HystrixProperty(name = "fallback.enabled", value = "true"),
                // 是否启用断路器
                @HystrixProperty(name = "circuitBreaker.enabled", value = "true"),
                // 该属性用来设置在滚动时间窗中，断路器熔断的最小请求数。例如，默认该值为 20 的时候，
                // 如果滚动时间窗（默认10秒）内仅收到了19个请求， 即使这19个请求都失败了，断路器也不会打开。
                @HystrixProperty(name = "circuitBreaker.requestVolumeThreshold", value = "20"),
                // 该属性用来设置在滚动时间窗中，表示在滚动时间窗中，在请求数量超过
                // circuitBreaker.requestVolumeThreshold 的情况下，如果错误请求数的百分比超过50,
                // 就把断路器设置为 "打开" 状态，否则就设置为 "关闭" 状态。
                @HystrixProperty(name = "circuitBreaker.errorThresholdPercentage", value = "50"),
                // 该属性用来设置当断路器打开之后的休眠时间窗。 休眠时间窗结束之后，
                // 会将断路器置为 "半开" 状态，尝试熔断的请求命令，如果依然失败就将断路器继续设置为 "打开" 状态，
                // 如果成功就设置为 "关闭" 状态。
                @HystrixProperty(name = "circuitBreaker.sleepWindowinMilliseconds", value = "5000"),
                // 断路器强制打开
                @HystrixProperty(name = "circuitBreaker.forceOpen", value = "false"),
                // 断路器强制关闭
                @HystrixProperty(name = "circuitBreaker.forceClosed", value = "false"),
                // 滚动时间窗设置，该时间用于断路器判断健康度时需要收集信息的持续时间
                @HystrixProperty(name = "metrics.rollingStats.timeinMilliseconds", value = "10000"),
                // 该属性用来设置滚动时间窗统计指标信息时划分"桶"的数量，断路器在收集指标信息的时候会根据
                // 设置的时间窗长度拆分成多个 "桶" 来累计各度量值，每个"桶"记录了一段时间内的采集指标。
                // 比如 10 秒内拆分成 10 个"桶"收集这样，所以 timeinMilliseconds 必须能被 numBuckets 整除。否则会抛异常
                @HystrixProperty(name = "metrics.rollingStats.numBuckets", value = "10"),
                // 该属性用来设置对命令执行的延迟是否使用百分位数来跟踪和计算。如果设置为 false, 那么所有的概要统计都将返回 -1。
                @HystrixProperty(name = "metrics.rollingPercentile.enabled", value = "false"),
                // 该属性用来设置百分位统计的滚动窗口的持续时间，单位为毫秒。
                @HystrixProperty(name = "metrics.rollingPercentile.timeInMilliseconds", value = "60000"),
                // 该属性用来设置百分位统计滚动窗口中使用 “ 桶 ”的数量。
                @HystrixProperty(name = "metrics.rollingPercentile.numBuckets", value = "60000"),
                // 该属性用来设置在执行过程中每个 “桶” 中保留的最大执行次数。如果在滚动时间窗内发生超过该设定值的执行次数，
                // 就从最初的位置开始重写。例如，将该值设置为100, 滚动窗口为10秒，若在10秒内一个 “桶 ”中发生了500次执行，
                // 那么该 “桶” 中只保留 最后的100次执行的统计。另外，增加该值的大小将会增加内存量的消耗，并增加排序百分位数所需的计算时间。
                @HystrixProperty(name = "metrics.rollingPercentile.bucketSize", value = "100"),
                // 该属性用来设置采集影响断路器状态的健康快照（请求的成功、 错误百分比）的间隔等待时间。
                @HystrixProperty(name = "metrics.healthSnapshot.intervalinMilliseconds", value = "500"),
                // 是否开启请求缓存
                @HystrixProperty(name = "requestCache.enabled", value = "true"),
                // HystrixCommand的执行和事件是否打印日志到 HystrixRequestLog 中
                @HystrixProperty(name = "requestLog.enabled", value = "true"),
        },
        threadPoolProperties = {
                // 该参数用来设置执行命令线程池的核心线程数，该值也就是命令执行的最大并发量
                @HystrixProperty(name = "coreSize", value = "10"),
                // 该参数用来设置线程池的最大队列大小。当设置为 -1 时，线程池将使用 SynchronousQueue 实现的队列，
                // 否则将使用 LinkedBlockingQueue 实现的队列。
                @HystrixProperty(name = "maxQueueSize", value = "-1"),
                // 该参数用来为队列设置拒绝阈值。 通过该参数， 即使队列没有达到最大值也能拒绝请求。
                // 该参数主要是对 LinkedBlockingQueue 队列的补充,因为 LinkedBlockingQueue
                // 队列不能动态修改它的对象大小，而通过该属性就可以调整拒绝请求的队列大小了。
                @HystrixProperty(name = "queueSizeRejectionThreshold", value = "5"),
        }
)
public String strConsumer() {
    return "hello 2020";
}
public String str_fallbackMethod()
{
    return "*****fall back str_fallbackMethod";
}
```



## （六）服务限流

后面高级篇讲解alibaba的Sentinel说明



## （七）hystrix工作流程

Hystrix工作流程：https://github.com/Netflix/Hystrix/wiki/How-it-Works



官网图例：

![image-20220306170007240](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220306170007240.png)



步骤说明：

1. 创建 HystrixCommand（用在依赖的服务返回单个操作结果的时候） 或 HystrixObserableCommand（用在依赖的服务返回多个操作结果的时候） 对象
2. 命令执行。其中 HystrixComand 实现了下面前两种执行方式；而 HystrixObservableCommand 实现了后两种执行方式：execute()：同步执行，从依赖的服务返回一个单一的结果对象， 或是在发生错误的时候抛出异常。queue()：异步执行， 直接返回 一个Future对象， 其中包含了服务执行结束时要返回的单一结果对象。observe()：返回 Observable 对象，它代表了操作的多个结果，它是一个 Hot Obserable（不论 "事件源" 是否有 "订阅者"，都会在创建后对事件进行发布，所以对于 Hot Observable 的每一个 "订阅者" 都有可能是从 "事件源" 的中途开始的，并可能只是看到了整个操作的局部过程）。toObservable()： 同样会返回 Observable 对象，也代表了操作的多个结果，但它返回的是一个Cold Observable（没有 "订阅者" 的时候并不会发布事件，而是进行等待，直到有 "订阅者" 之后才发布事件，所以对于 Cold Observable 的订阅者，它可以保证从一开始看到整个操作的全部过程）
3. 若当前命令的请求缓存功能是被启用的， 并且该命令缓存命中， 那么缓存的结果会立即以 Observable 对象的形式返回
4. 检查断路器是否为打开状态。如果断路器是打开的，那么Hystrix不会执行命令，而是转接到 fallback 处理逻辑（第 8 步）；如果断路器是关闭的，检查是否有可用资源来执行命令（第 5 步）
5. 线程池/请求队列/信号量是否占满。如果命令依赖服务的专有线程池和请求队列，或者信号量（不使用线程池的时候）已经被占满， 那么 Hystrix 也不会执行命令， 而是转接到 fallback 处理逻辑（第8步）
6. Hystrix 会根据我们编写的方法来决定采取什么样的方式去请求依赖服务。HystrixCommand.run() ：返回一个单一的结果，或者抛出异常。HystrixObservableCommand.construct()： 返回一个Observable 对象来发射多个结果，或通过 onError 发送错误通知
7. Hystrix会将 "成功"、"失败"、"拒绝"、"超时" 等信息报告给断路器， 而断路器会维护一组计数器来统计这些数据。断路器会使用这些统计数据来决定是否要将断路器打开，来对某个依赖服务的请求进行 "熔断/短路"
8. 当命令执行失败的时候， Hystrix 会进入 fallback 尝试回退处理， 我们通常也称该操作为 "服务降级"。而能够引起服务降级处理的情况有下面几种：第4步： 当前命令处于"熔断/短路"状态，断路器是打开的时候。第5步： 当前命令的线程池、 请求队列或 者信号量被占满的时候。第6步：HystrixObservableCommand.construct() 或 HystrixCommand.run() 抛出异常的时候
9. 当Hystrix命令执行成功之后， 它会将处理结果直接返回或是以Observable 的形式返回
   
   

tips：如果我们没有为命令实现降级逻辑或者在降级处理逻辑中抛出了异常， Hystrix 依然会返回一个 Observable 对象， 但是它不会发射任何结果数据， 而是通过 onError 方法通知命令立即中断请求，并通过onError()方法将引起命令失败的异常发送给调用者



## （八）服务监控hystrixDashboard

### 1、概述

除了隔离依赖服务的调用以外，Hystrix还提供了准实时的调用监控（Hystrix Dashboard），Hystrix会持续地记录所有通过Hystrix发起的请求的执行信息，并以统计报表和图形的形式展示给用户，包括每秒执行多少请求多少成功，多少失败等。Netflix通过hystrix-metrics-event-stream项目实现了对以上指标的监控。Spring Cloud也提供了Hystrix Dashboard的整合，对监控内容转化成可视化界面。



### 2、仪表盘9001

新建cloud-consumer-hystrix-dashboard9001



#### （1）pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-consumer-hystrix-dashboard9001</artifactId>

    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-hystrix-dashboard</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



#### （2）application.yml

```yaml
server:
  port: 9001
```



#### （3）主启动

com.atguigu.springcloud.HystrixDashboardMain9001

HystrixDashboardMain9001+新注解@EnableHystrixDashboard

```java
@SpringBootApplication
@EnableHystrixDashboard
public class HystrixDashboardMain9001 {
    public static void main(String[] args) {
        SpringApplication.run(HystrixDashboardMain9001.class, args);
    }
}
```



所有Provider微服务提供类(8001/8002/8003)都需要监控依赖配置

```xml
<!-- actuator监控信息完善 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```



启动cloud-consumer-hystrix-dashboard9001该微服务后续将监控微服务8001 http://localhost:9001/hystrix

![image-20220307013239017](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307013239017.png)



### 3、断路器演示

服务监控hystrixDashboard

#### （1）修改hystrix-payment8001

注意:新版本Hystrix需要在主启动类PaymentHystrixMain8001中指定监控路径

```java
@SpringBootApplication
@EnableCircuitBreaker
@EnableEurekaClient //本服务启动后会自动注册进eureka服务中
public class PaymentHystrixMain8001 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentHystrixMain8001.class, args);
    }

    /**
     * 此配置是为了服务监控而配置，与服务容错本身无关，springcloud升级后的坑
     * ServletRegistrationBean因为springboot的默认路径不是"/hystrix.stream"，
     * 只要在自己的项目里配置上下面的servlet就可以了
     */
    @Bean
    public ServletRegistrationBean getServlet() {
        HystrixMetricsStreamServlet streamServlet = new HystrixMetricsStreamServlet();
        ServletRegistrationBean registrationBean = new ServletRegistrationBean(streamServlet);
        registrationBean.setLoadOnStartup(1);
        registrationBean.addUrlMappings("/hystrix.stream");
        registrationBean.setName("HystrixMetricsStreamServlet");
        return registrationBean;
    }
}
```



#### （2）监控测试

启动1个eureka或者3个eureka集群均可



观察监控窗口

9001监控8001，填写监控地址：http://localhost:8001/hystrix.stream

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307014043228.png" alt="image-20220307014043228"  />

测试地址：

http://localhost:8001/payment/circuit/1

http://localhost:8001/payment/circuit/-1



上述测试通过



先访问正确地址，再访问错误地址，再正确地址，会发现图示断路器都是慢慢放开的



监控结果，成功

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307014330855.png" alt="image-20220307014330855" style="zoom:80%;" />

监控结果，失败

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307014406583.png" alt="image-20220307014406583" style="zoom:80%;" />

#### （3）如何看？

7色、1圈、1线



1圈：

实心圆：共有两种含义，它通过颜色的变化代表了实例的健康程度，它的健康度从绿色<黄色<橙色<红色递减。该实心圆除了颜色的变化之外，它的大小也会根据实例的请求流量发生变化，流量越大该实心圆就越大。所以通过该实心圆的展示，就可以在大量的实例中快速的发现故障实例和高压力实例



1线：

曲线：用来记录2分钟内流量的相对变化，可以通过它来观察到流量的上升和下降趋势。



整图说明：

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307014628981.png" alt="image-20220307014628981" style="zoom:80%;" />

整图说明2：

![image-20220307014712408](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307014712408.png)



搞懂一个才能看懂复杂的：

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307014733165.png" alt="image-20220307014733165" style="zoom:120%;" />

## 九、SpringCloud Gateway 网关

## （一）概述简介

### 1、官网

上一代zuul 1.X：https://github.com/Netflix/zuul/wiki

当前gateway：https://cloud.spring.io/spring-cloud-static/spring-cloud-gateway/2.2.1.RELEASE/reference/html/



### 2、是什么

Cloud全家桶中有个很重要的组件就是网关，在1.x版本中都是采用的Zuul网关；但在2.x版本中，zuul的升级一直跳票，SpringCloud最后自己研发了一个网关替代Zuul，那就是SpringCloud Gateway一句话：gateway是原zuul1.x版的替代

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307204503225.png" alt="image-20220307204503225"  />

Gateway是在Spring生态系统之上构建的API网关服务，基于Spring 5，Spring Boot 2和 Project Reactor等技术。Gateway旨在提供一种简单而有效的方式来对API进行路由，以及提供一些强大的过滤器功能， 例如：熔断、限流、重试等

![image-20220307204750225](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307204750225.png)



SpringCloud Gateway 是 Spring Cloud 的一个全新项目，基于 Spring 5.0+Spring Boot 2.0 和 Project Reactor 等技术开发的网关，它旨在为微服务架构提供一种简单有效的统一的 API 路由管理方式。

SpringCloud Gateway 作为 Spring Cloud 生态系统中的网关，目标是替代 Zuul，在Spring Cloud 2.0以上版本中，没有对新版本的Zuul 2.0以上最新高性能版本进行集成，仍然还是使用的Zuul 1.x非Reactor模式的老版本。而为了提升网关的性能，SpringCloud Gateway是基于WebFlux框架实现的，而WebFlux框架底层则使用了高性能的Reactor模式通信框架Netty。

Spring Cloud Gateway的目标提供统一的路由方式且基于 Filter 链的方式提供了网关基本的功能，例如：安全，监控/指标，和限流。



SpringCloud Gateway 使用的Webflux中的reactor-netty响应式编程组件，底层使用了Netty通讯框架。



源码架构：

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307205401061.png" alt="image-20220307205401061" style="zoom:80%;" />

### 3、能干嘛

- 反向代理
- 鉴权
- 流量控制
- 熔断
- 日志监控
  
  

微服务架构中网关在哪里？

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307222826280.png" alt="image-20220307222826280" style="zoom:80%;" />

### 4、有Zuul了怎么又出来了gateway

neflix不太靠谱，zuul2.0一直跳票，迟迟不发布，一方面因为Zuul1.0已经进入了维护阶段，而且Gateway是SpringCloud团队研发的，是亲儿子产品，值得信赖。而且很多功能Zuul都没有用起来也非常的简单便捷。Gateway是基于异步非阻塞模型上进行开发的，性能方面不需要担心。虽然Netflix早就发布了最新的 Zuul 2.x，但 Spring Cloud 貌似没有整合计划。而且Netflix相关组件都宣布进入维护期；不知前景如何？多方面综合考虑Gateway是很理想的网关选择。



### 5、Gateway特征

- 基于Spring Framework 5, Project Reactor 和 Spring Boot 2.0 进行构建
- 动态路由：能够匹配任何请求属性
- 可以对路由指定 Predicate（断言）和 Filter（过滤器）
- 集成Hystrix的断路器功能
- 集成 Spring Cloud 服务发现功能
- 易于编写的 Predicate（断言）和 Filter（过滤器）
- 请求限流功能
- 支持路径重写
  
  

### 6、Gateway与Zuul的区别

在SpringCloud Finchley 正式版之前，Spring Cloud 推荐的网关是 Netflix 提供的Zuul：

- Zuul 1.x，是一个基于阻塞 I/ O 的 API Gateway

- Zuul 1.x 基于Servlet 2. 5使用阻塞架构它不支持任何长连接(如 WebSocket) Zuul 的设计模式和Nginx较像，每次 I/ O 操作都是从工作线程中选择一个执行，请求线程被阻塞到工作线程完成，但是差别是Nginx 用C++ 实现，Zuul 用 Java 实现，而 JVM 本身会有第一次加载较慢的情况，使得Zuul 的性能相对较差。

- Zuul 2.x理念更先进，想基于Netty非阻塞和支持长连接，但SpringCloud目前还没有整合。 Zuul 2.x的性能较 Zuul 1.x 有较大提升。在性能方面，根据官方提供的基准测试， Spring Cloud Gateway 的 RPS（每秒请求数）是Zuul 的 1. 6 倍。

- Spring Cloud Gateway 建立 在 Spring Framework 5、 Project Reactor 和 Spring Boot 2 之上， 使用非阻塞 API。

- Spring Cloud Gateway 还 支持 WebSocket， 并且与Spring紧密集成拥有更好的开发体验
  
  

### 7、Zuul1.x模型

Springcloud中所集成的Zuul版本，采用的是Tomcat容器，使用的是传统的Servlet IO处理模型



学过尚硅谷web中期课程都知道一个题目，Servlet的生命周期？

servlet由servlet container进行生命周期管理，container启动时构造servlet对象并调用servlet init()进行初始化；container运行时接受请求，并为每个请求分配一个线程（一般从线程池中获取空闲线程）然后调用service()
container关闭时调用servlet destory()销毁servlet



上述模式的缺点：

servlet是一个简单的网络IO模型，当请求进入servlet container时，servlet container就会为其绑定一个线程，在并发不高的场景下这种模型是适用的。但是一旦高并发(比如抽风用jemeter压)，线程数量就会上涨，而线程资源代价是昂贵的（上线文切换，内存消耗大）严重影响请求的处理时间。在一些简单业务场景下，不希望为每个request分配一个线程，只需要1个或几个线程就能应对极大并发的请求，这种业务场景下servlet模型没有优势



所以Zuul 1.X是基于servlet之上的一个阻塞式处理模型，即spring实现了处理所有request请求的一个servlet（DispatcherServlet）并由该servlet阻塞式处理处理。所以Springcloud Zuul无法摆脱servlet模型的弊端



### 8、GateWay模型

![image-20220307223911740](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307223911740.png)



![image-20220307223927752](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307223927752.png)



WebFlux是什么

https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html#webflux-new-framework



传统的Web框架，比如说：struts2，springmvc等都是基于Servlet API与Servlet容器基础之上运行的。但是
在Servlet3.1之后有了异步非阻塞的支持。而WebFlux是一个典型非阻塞异步的框架，它的核心是基于Reactor的相关API实现的。相对于传统的web框架来说，它可以运行在诸如Netty，Undertow及支持Servlet3.1的容器上。非阻塞式+函数式编程（Spring5必须让你使用java8）

Spring WebFlux 是 Spring 5.0 引入的新的响应式框架，区别于 Spring MVC，它不需要依赖Servlet API，它是完全异步非阻塞的，并且基于 Reactor 来实现响应式流规范。



## （二）三大核心概念

### 1、Route(路由)

路由是构建网关的基本模块，它由ID，目标URI，一系列的断言和过滤器组成，如果断言为true则匹配该路由



### 2、Predicate(断言)

参考的是Java8的java.util.function.Predicate，开发人员可以匹配HTTP请求中的所有内容(例如请求头或请求参数)，如果请求与断言相匹配则进行路由



### 3、Filter(过滤)

指的是Spring框架中GatewayFilter的实例，使用过滤器，可以在请求被路由前或者之后对请求进行修改。



web请求，通过一些匹配条件，定位到真正的服务节点。并在这个转发过程的前后，进行一些精细化控制。
predicate就是我们的匹配条件；而filter，就可以理解为一个无所不能的拦截器。有了这两个元素，再加上目标uri，就可以实现一个具体的路由了

![image-20220307225907461](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307225907461.png)



## （三）Gateway工作流程

官网总结

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307230245126.png" alt="image-20220307230245126" style="zoom:80%;" />

![image-20220307230255413](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307230255413.png)

客户端向 Spring Cloud Gateway 发出请求。然后在 Gateway Handler Mapping 中找到与请求相匹配的路由，将其发送到 Gateway Web Handler；Handler 再通过指定的过滤器链来将请求发送到我们实际的服务执行业务逻辑，然后返回；过滤器之间用虚线分开是因为过滤器可能会在发送代理请求之前（“pre”）或之后（“post”）执行业务逻辑；Filter在“pre”类型的过滤器可以做参数校验、权限校验、流量监控、日志输出、协议转换等，在“post”类型的过滤器中可以做响应内容、响应头的修改，日志的输出，流量监控等有着非常重要的作用



核心逻辑：路由转发+执行过滤器链



## （四）入门配置

### 1、新建 gateway9527

新建Module：cloud-gateway-gateway9527



### 2、pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-gateway-gateway9527</artifactId>

    <dependencies>
        <!--gateway-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-gateway</artifactId>
        </dependency>
        <!--eureka-client-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <!--一般基础配置类-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



### 3、application.yml

```yml
server:
  port: 9527

spring:
  application:
    name: cloud-gateway

eureka:
  instance:
    hostname: cloud-gateway-service
  client: #服务提供者provider注册进eureka服务列表内
    service-url:
      register-with-eureka: true
      fetch-registry: true
      defaultZone: http://eureka7001.com:7001/eureka
```



### 4、业务类

无



### 5、主启动类

com.atguigu.springcloud.GateWayMain9527

```java
@SpringBootApplication
@EnableEurekaClient
public class GateWayMain9527 {
    public static void main(String[] args) {
        SpringApplication.run(GateWayMain9527.class, args);
    }
}
```



### 6、9527网关如何做路由映射呢？

cloud-provider-payment8001看看controller的访问地址

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307233400797.png" alt="image-20220307233400797"  />

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307233459397.png" alt="image-20220307233459397"  />

我们目前不想暴露8001端口，希望在8001外面套一层9527



### 7、YML新增网关配置

```yaml
server:
  port: 9527

spring:
  application:
    name: cloud-gateway
  cloud:
    gateway:
      routes:
        - id: payment_routh #payment_route    #路由的ID，没有固定规则但要求唯一，建议配合服务名
          uri: http://localhost:8001          #匹配后提供服务的路由地址
          predicates:
            - Path=/payment/get/**         # 断言，路径相匹配的进行路由

        - id: payment_routh2 #payment_route    #路由的ID，没有固定规则但要求唯一，建议配合服务名
          uri: http://localhost:8001          #匹配后提供服务的路由地址
          predicates:
            - Path=/payment/lb/**         # 断言，路径相匹配的进行路由

eureka:
  instance:
    hostname: cloud-gateway-service
  client: #服务提供者provider注册进eureka服务列表内
    service-url:
      register-with-eureka: true
      fetch-registry: true
      defaultZone: http://eureka7001.com:7001/eureka
```



### 8、测试

1. 启动7001
2. 启动8001：cloud-provider-payment8001
3. 启动9527网关
   
   

访问说明

![image-20220307234550952](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307234550952.png)



![image-20220307235910439](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307235910439.png)



添加网关前：http://localhost:8001/payment/get/1

添加网关后：http://localhost:9527/payment/get/1



<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308000003795.png" alt="image-20220308000003795" style="zoom: 67%;" />

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308000023170.png" alt="image-20220308000023170" style="zoom:67%;" />

### 9、YML配置说明

Gateway网关路由有两种配置方式：

1. 在配置文件yml中配置：见前面的步骤
2. 代码中注入RouteLocator的Bean

官网案例：

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220307234807137.png" alt="image-20220307234807137" style="zoom:80%;" />

啥玩意儿？？？



自己写一个案例：

通过9527网关访问到外网的百度新闻网址：http://news.baidu.com/guonei



编码：cloud-gateway-gateway9527



业务实现

com.atguigu.springcloud.config.GateWayConfig



```java
@Configuration
public class GateWayConfig {
    /**
     * 配置了一个id为route-name的路由规则，
     * 当访问地址 http://localhost:9527/guonei时会自动转发到地址：http://news.baidu.com/guonei
     *
     * @param builder
     * @return
     */
    @Bean
    public RouteLocator customRouteLocator(RouteLocatorBuilder builder) {
        RouteLocatorBuilder.Builder routes = builder.routes();

        routes.route("path_route_atguigu",
                r -> r.path("/guonei")
                        .uri("http://news.baidu.com/guonei")).build();

        return routes.build();
    }

    @Bean
    public RouteLocator customRouteLocator2(RouteLocatorBuilder builder) {
        RouteLocatorBuilder.Builder routes = builder.routes();
        routes.route("path_route_atguigu2", 
                r -> r.path("/guoji")
                        .uri("http://news.baidu.com/guoji")).build();
        return routes.build();
    }
}
```



http://localhost:9527/guonei

![image-20220308005244674](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308005244674.png)



## （五）通过微服务名实现动态路由

### 1、以前的配置

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308010109458.png" alt="image-20220308010109458" style="zoom: 50%;" />

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308010012311.png" alt="image-20220308010012311" style="zoom: 33%;" />

默认情况下Gateway会根据注册中心注册的服务列表，以注册中心上微服务名为路径创建动态路由进行转发，从而实现动态路由的功能



启动：一个eureka7001 + 两个服务提供者8001/8002

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```



### 2、application.yml

需要注意的是uri的协议为lb，表示启用Gateway的负载均衡功能

lb://serviceName是spring cloud gateway在微服务中自动为我们创建的负载均衡uri

```yaml
server:
  port: 9527

spring:
  application:
    name: cloud-gateway
  cloud:
    gateway:
      discovery:
        locator:
          enabled: true #开启从注册中心动态创建路由的功能，利用微服务名进行路由
      routes:
        - id: payment_routh #payment_route    #路由的ID，没有固定规则但要求唯一，建议配合服务名
          # uri: http://localhost:8001          #匹配后提供服务的路由地址
          uri: lb://cloud-payment-service #匹配后提供服务的路由地址
          predicates:
            - Path=/payment/get/**         # 断言，路径相匹配的进行路由

        - id: payment_routh2 #payment_route    #路由的ID，没有固定规则但要求唯一，建议配合服务名
          # uri: http://localhost:8001          #匹配后提供服务的路由地址
          uri: lb://cloud-payment-service #匹配后提供服务的路由地址
          predicates:
            - Path=/payment/lb/**         # 断言，路径相匹配的进行路由

eureka:
  instance:
    hostname: cloud-gateway-service
  client: #服务提供者provider注册进eureka服务列表内
    service-url:
      register-with-eureka: true
      fetch-registry: true
      defaultZone: http://eureka7001.com:7001/eureka
```



测试：http://localhost:9527/payment/lb

8001/8002两个端口切换



<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308011540617.png" alt="image-20220308011540617" style="zoom:80%;" />

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308011551828.png" alt="image-20220308011551828" style="zoom: 80%;" />

## （六）Predicate的使用

### 1、是什么

启动我们的gateway9527

![image-20220308011649518](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308011649518.png)



Route Predicate Factories这个是什么东东?

![image-20220308011716452](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308011716452.png)



Spring Cloud Gateway将路由匹配作为Spring WebFlux HandlerMapping基础架构的一部分，Spring Cloud Gateway包括许多内置的Route Predicate工厂，所有这些Predicate都与HTTP请求的不同属性匹配，多个Route Predicate工厂可以进行组合

Spring Cloud Gateway 创建 Route 对象时，使用 RoutePredicateFactory 创建 Predicate 对象，Predicate 对象可以赋值给 Route。 Spring Cloud Gateway 包含许多内置的Route Predicate Factories。所有这些谓词都匹配HTTP请求的不同属性。多种谓词工厂可以组合，并通过逻辑and。



### 2、常用的Route Predicate

![image-20220308012113647](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308012113647.png)



#### （1）After Route Predicate

![image-20220308225327935](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308225327935.png)

我们的问题是：上述这个After好懂，这个时间串串？？？



ZonedDateTimeDemo：com.atguigu.springcloud.test.ZonedDateTimeDemo

```java
public class ZonedDateTimeDemo {
    public static void main(String[] args) {
        ZonedDateTime zbj = ZonedDateTime.now(); // 默认时区
        System.out.println("zbj = " + zbj);

        ZonedDateTime zny = ZonedDateTime.now(ZoneId.of("America/New_York")); // 用指定时区获取当前时间
        System.out.println("zny = " + zny);
    }
}
```

```java
zbj = 2022-03-08T23:04:51.718+08:00[Asia/Shanghai]
zny = 2022-03-08T10:04:51.723-05:00[America/New_York]
```



application.yml

把时间调到当前时间之后，未到设置时间之后就无法访问

```yaml
- After=2022-03-08T23:21:51.718+08:00[Asia/Shanghai]         # 断言，路径相匹配的进行路由
```

```yaml
server:
  port: 9527

spring:
  application:
    name: cloud-gateway
  cloud:
    gateway:
      discovery:
        locator:
          enabled: true #开启从注册中心动态创建路由的功能，利用微服务名进行路由
      routes:
        - id: payment_routh #payment_route    #路由的ID，没有固定规则但要求唯一，建议配合服务名
          # uri: http://localhost:8001          #匹配后提供服务的路由地址
          uri: lb://cloud-payment-service #匹配后提供服务的路由地址
          predicates:
            - Path=/payment/get/**         # 断言，路径相匹配的进行路由

        - id: payment_routh2 #payment_route    #路由的ID，没有固定规则但要求唯一，建议配合服务名
          # uri: http://localhost:8001          #匹配后提供服务的路由地址
          uri: lb://cloud-payment-service #匹配后提供服务的路由地址
          predicates:
            - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
            - After=2022-03-08T23:14:51.718+08:00[Asia/Shanghai]         # 断言，路径相匹配的进行路由

eureka:
  instance:
    hostname: cloud-gateway-service
  client: #服务提供者provider注册进eureka服务列表内
    service-url:
      register-with-eureka: true
      fetch-registry: true
      defaultZone: http://eureka7001.com:7001/eureka
```



http://localhost:9527/payment/lb

![image-20220308232054328](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308232054328.png)



![image-20220308232241106](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308232241106.png)



用途：项目上线定时开启访问时间可以用、秒杀



#### （2）Before Route Predicate

![image-20220308233150949](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308233150949.png)



application.yml

```yaml
predicates:
  - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
  - Before=2023-03-08T24:21:51.718+08:00[Asia/Shanghai]         # 断言，路径相匹配的进行路由
```



#### （3）Between Route Predicate

application.yml

```yaml
predicates:
  - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
  - Between=2022-02-02T17:45:06.206+08:00[Asia/Shanghai],2023-03-25T18:59:06.206+08:00[Asia/Shanghai]
```



#### （4）Cookie Route Predicate

![image-20220308233626966](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308233626966.png)



Cookie Route Predicate需要两个参数，一个是 Cookie name，一个是正则表达式

路由规则会通过获取对应的 Cookie name 值和正则表达式去匹配，如果匹配上就会执行路由；如果没有匹配上则不执行



application.yml

```yaml
predicates:
  - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
  - Cookie=username,yfstart
```



不带cookie访问：curl http://localhost:9527/payment/lb

![image-20220308235018750](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308235018750.png)



带上cookies访问：curl http://localhost:9527/payment/lb --cookie "username=yfstart"

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220308235954148.png" alt="image-20220308235954148"  />

如果加入curl返回中文乱码：https://blog.csdn.net/leedee/article/details/82685636



#### （5）Header Route Predicate

![image-20220309000456321](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309000456321.png)



两个参数：一个是属性名称和一个正则表达式，这个属性值和正则表达式匹配则执行



application.yml

```yaml
predicates:
  - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
  - Header=X-Request-Id, \d+  # 请求头要有X-Request-Id属性并且值为整数的正则表达式
```



curl http://localhost:9527/payment/lb -H "X-Request-Id:123"

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309000754839.png" alt="image-20220309000754839" style="zoom: 67%;" />

curl http://localhost:9527/payment/lb -H "X-Request-Id:-123"

![image-20220309000841103](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309000841103.png)



#### （6）Host Route Predicate

![image-20220309000930459](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309000930459.png)



Host Route Predicate 接收一组参数，一组匹配的域名列表，这个模板是一个 ant 分隔的模板，用.号作为分隔符

它通过参数中的主机地址作为匹配规则



application.yml

```yaml
predicates:
  - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
  - Host=**.atguigu.com
```



正确：

curl http://localhost:9527/payment/lb -H "Host: www.atguigu.com"

curl http://localhost:9527/payment/lb -H "Host: java.atguigu.com"

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309001448401.png" alt="image-20220309001448401" style="zoom: 67%;" />

错误：

curl http://localhost:9527/payment/lb -H "Host: java.atguigu.net"

![image-20220309001526638](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309001526638.png)



#### （7）Method Route Predicate

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309001551777.png" alt="image-20220309001551777" style="zoom:80%;" />

application.yml

```yaml
predicates:
  - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
  - Method=GET
```



![image-20220309001711494](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309001711494.png)



#### （8）Path Route Predicate

![image-20220309001739385](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309001739385.png)



application.yml

```yaml
predicates:
  - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
```



#### （9）Query Route Predicate

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309001857631.png" alt="image-20220309001857631" style="zoom:80%;" />

支持传入两个参数，一个是属性名，一个为属性值，属性值可以是正则表达式



application.yml

```yaml
predicates:
  - Path=/payment/lb/**         # 断言，路径相匹配的进行路由
  - Query=username, \d+  # 要有参数名username并且值还要是整数才能路由
```





正确：http://localhost:9527/payment/lb?username=1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309002142766.png" alt="image-20220309002142766" style="zoom:80%;" />

错误：http://localhost:9527/payment/lb?username=-1

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309002200482.png" alt="image-20220309002200482" style="zoom: 50%;" />

小总结：说白了，Predicate就是为了实现一组匹配规则，让请求过来找到对应的Route进行处理



## （七）Filter的使用

### 1、是什么

![image-20220309002320817](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309002320817.png)



路由过滤器可用于修改进入的HTTP请求和返回的HTTP响应，路由过滤器只能指定路由进行使用

Spring Cloud Gateway 内置了多种路由过滤器，他们都由GatewayFilter的工厂类来产生



### 2、Spring Cloud Gateway的Filter

生命周期，Only Two

- pre
- post
  
  

种类，Only Two

- GatewayFilter 
- GlobalFilter
  
  

GatewayFilter：https://cloud.spring.io/spring-cloud-static/spring-cloud-gateway/2.2.1.RELEASE/reference/html/#the-addrequestparameter-gatewayfilter-factory

31种之多：

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309002724244.png" alt="image-20220309002724244" style="zoom:80%;" />

GlobalFilter：

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309002734294.png" alt="image-20220309002734294" style="zoom:80%;" />

### 3、常用的GatewayFilter

AddRequestParameter

```yaml
filters:
  - AddRequestParameter=X-Request-Id,1024 #过滤器工厂会在匹配的请求头加上一对请求头，名称为X-Request-Id值为1024
```

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309003009248.png" alt="image-20220309003009248"  />

### 4、自定义过滤器

自定义全局GlobalFilter



两个主要接口介绍：

```java
implements GlobalFilter,Ordered
```



能干嘛？

- 全局日志记录
- 统一网关鉴权
  
  

案例代码

MyLogGateWayFilter：com.atguigu.springcloud.filter.MyLogGateWayFilter

```java
@Component //必须加，必须加，必须加
public class MyLogGateWayFilter implements GlobalFilter, Ordered {
    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        System.out.println("time:" + new Date() + "\t 执行了自定义的全局过滤器: " + "MyLogGateWayFilter" + "hello");

        String uname = exchange.getRequest().getQueryParams().getFirst("uname");
        if (uname == null) {
            System.out.println("****用户名为null，无法登录");
            exchange.getResponse().setStatusCode(HttpStatus.NOT_ACCEPTABLE);
            return exchange.getResponse().setComplete();
        }
        return chain.filter(exchange);
    }

    /**
     * 这个返回的数值越小，上面的filter优先级就越高
     *
     * @return
     */
    @Override
    public int getOrder() {
        return 0;
    }
}
```



Ordered 的源码

```java
package org.springframework.core;

public interface Ordered {
    int HIGHEST_PRECEDENCE = -2147483648;
    int LOWEST_PRECEDENCE = 2147483647;

    int getOrder();
}
```



### 5、测试

启动7001、8001、8002、9527

正确：http://localhost:9527/payment/lb?uname=zhang3

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309004200471.png" alt="image-20220309004200471" style="zoom:80%;" />

错误：没有参数uname：http://localhost:9527/payment/lb

<img src="https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309004244182.png" alt="image-20220309004244182" style="zoom:50%;" />

![image-20220309004352415](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/image-20220309004352415.png)



# 十、SpringCloud Config 分布式配置中心

## （一）概述

分布式系统面临的---配置问题

微服务意味着要将单体应用中的业务拆分成一个个子服务，每个服务的粒度相对较小，因此系统中会出现大量的服务。由于每个服务都需要必要的配置信息才能运行，所以一套集中式的、动态的配置管理设施是必不可少的。

SpringCloud提供了ConfigServer来解决这个问题，我们每一个微服务自己带着一个application.yml，上百个配置文件的管理....../(ㄒoㄒ)/~~



### 1、是什么

SpringCloud Config为微服务架构中的微服务提供集中化的外部配置支持，配置服务器为各个不同微服务应用的所有环境提供了一个中心化的外部配置。

![image-20220322005035706](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203220058069.png)



### 2、怎么玩

SpringCloud Config分为服务端和客户端两部分。

服务端也称为分布式配置中心，它是一个独立的微服务应用，用来连接配置服务器并为客户端提供获取配置信息，加密/解密信息等访问接口

客户端则是通过指定的配置中心来管理应用资源，以及与业务相关的配置内容，并在启动的时候从配置中心获取和加载配置信息配置服务器默认采用git来存储配置信息，这样就有助于对环境配置进行版本管理，并且可以通过git客户端工具来方便的管理和访问配置内容。



### 3、能干嘛

- 集中管理配置文件

- 不同环境不同配置，动态化的配置更新，分环境部署比如dev/test/prod/beta/release

- 运行期间动态调整配置，不再需要在每个服务部署的机器上编写配置文件，服务会向配置中心统一拉取配置自己的信息

- 当配置发生变动时，服务不需要重启即可感知到配置的变化并应用新的配置

- 将配置信息以REST接口的形式暴露：post、curl访问刷新均可......
  
  

### 4、与GitHub整合配置

由于SpringCloud Config默认使用Git来存储配置文件(也有其它方式，比如支持SVN和本地文件)，但最推荐的还是Git，而且使用的是http/https访问的形式

官网：https://cloud.spring.io/spring-cloud-static/spring-cloud-config/2.2.1.RELEASE/reference/html/

![image-20220322010132874](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203220101007.png)



## （二）Config服务端配置与测试

### 1、服务端配置

- 用你自己的账号在Gitee上新建一个名为springcloud-config的新Repository

- 由上一步获得刚新建的git地址
  
  - SSH：git@gitee.com:yangfan1814012468/springcloud-config.git
  
  - HTTPS：https://gitee.com/yangfan1814012468/springcloud-config.git

- 本地硬盘目录上新建git仓库并clone
  
  - 例：E:\临时文件夹\SpringCloud2020
  - git clone https://gitee.com/yangfan1814012468/springcloud-config.git

- 此时在本地E盘符下E:\临时文件夹\SpringCloud2020\springcloud-config
  
  - 表示多个环境的配置文件例如：config-test.yml、config-dev.yml、config-master.yml
  - 保存格式必须为UTF-8
  - 如果需要修改，此处模拟运维人员操作git和github
    - git add .
    - git commit -m "init yml"
    - git push origin master

![image-20220322135209282](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281425277.png)



config-test.yml

```yaml
spring:
  application:
    name: springcloud-config-test
  profiles:
    active: test
```



config-dev.yml

```yaml
spring:
  application:
    name: springcloud-config-dev
  profiles:
    active: dev
```



config-master.yml

```yaml
spring:
  application:
    name: springcloud-config-master
  profiles:
    active: master
```



### 2、配置模块 cloud-config-center-3344

新建Module模块cloud-config-center-3344，它即为Cloud的配置中心模块cloudConfig Center



#### （1）pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-config-center-3344</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-config-server</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```



#### （2）application.yml

```yaml
server:
  port: 3344

spring:
  application:
    name: cloud-config-center #注册进Eureka服务器的微服务名
  cloud:
    config:
      server:
        git:
          uri: https://gitee.com/yangfan1814012468/springcloud-config.git #Gitee上面的git仓库名字
          ####搜索目录
          search-paths:
            - springcloud-config
      ####读取分支
      label: master

#服务注册到eureka地址
eureka:
  client:
    service-url:
      defaultZone: http://localhost:7001/eureka
```



#### （3）主启动类

com.atguigu.springcloud.ConfigCenterMain3344

```java
@EnableConfigServer
```

```java
@SpringBootApplication
@EnableConfigServer
public class ConfigCenterMain3344 {
    public static void main(String[] args) {
        SpringApplication.run(ConfigCenterMain3344.class, args);
    }
}
```



#### （4）映射

windows下修改hosts文件，增加映射：127.0.0.1  config-3344.com



#### （5）测试

测试通过Config微服务是否可以从Gitee上获取配置内容

先启动7001、再启动微服务3344：http://config-3344.com:3344/master/config-dev.yml

![image-20220322140639573](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281425678.png)



### 3、配置读取规则

1. {application} 就是应用名称，对应到配置文件上来，就是配置文件的名称部分，例如我上面创建的配置文件

2. {profile} 就是配置文件的版本，我们的项目有开发版本、测试环境版本、生产环境版本，对应到配置文件上来就是以 application-{profile}.yml 加以区分，例如application-dev.yml、application-sit.yml、application-prod.yml

3. {label} 表示 git 分支，默认是 master 分支，如果项目是以分支做区分也是可以的，那就可以通过不同的 label 来控制访问不同的配置文件了
   
   

官网：

![](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281425337.png)



#### （1）/{label}/{application}-{profile}.yml

- master分支
  - http://config-3344.com:3344/master/config-dev.yml
  - http://config-3344.com:3344/master/config-test.yml
  - http://config-3344.com:3344/master/config-prod.yml
- dev分支
  - http://config-3344.com:3344/dev/config-dev.yml
  - http://config-3344.com:3344/dev/config-test.yml
  - http://config-3344.com:3344/dev/config-prod.yml
    
    

#### （2）/{application}-{profile}.yml

- http://config-3344.com:3344/config-dev.yml
- http://config-3344.com:3344/config-test.yml
- http://config-3344.com:3344/config-prod.yml
- http://config-3344.com:3344/config-xxxx.yml(不存在的配置)
  
  

#### （3）/{application}/{profile}[/{label}]

- http://config-3344.com:3344/config/dev/master
- http://config-3344.com:3344/config/test/master
- http://config-3344.com:3344/config/test/dev
  
  

## （三）Config客户端配置与测试

新建cloud-config-client-3355

### 1、pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-config-client-3355</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```



### 2、bootstrap.yml

#### （1）是什么

applicaiton.yml是用户级的资源配置项；bootstrap.yml是系统级的，优先级更加高

Spring Cloud会创建一个“Bootstrap Context”，作为Spring应用的`Application Context`的父上下文。初始化的时候，`Bootstrap Context`负责从外部源加载配置属性并解析配置。这两个上下文共享一个从外部获取的`Environment`。

`Bootstrap`属性有高优先级，默认情况下，它们不会被本地配置覆盖。 `Bootstrap context`和`Application Context`有着不同的约定，所以新增了一个`bootstrap.yml`文件，保证`Bootstrap Context`和`Application Context`配置的分离。

要将Client模块下的application.yml文件改为bootstrap.yml，这是很关键的，因为bootstrap.yml是比application.yml先加载的。bootstrap.yml优先级高于application.yml



#### （2）内容

```yaml
server:
  port: 3355

spring:
  application:
    name: config-client
  cloud:
    #Config客户端配置
    config:
      label: master #分支名称
      name: config #配置文件名称
      profile: dev #读取后缀名称   上述3个综合：master分支上config-dev.yml的配置文件被读取http://config-3344.com:3344/master/config-dev.yml
      uri: http://localhost:3344 #配置中心地址

#服务注册到eureka地址
eureka:
  client:
    service-url:
      defaultZone: http://localhost:7001/eureka
```



#### （3）说明

![image-20220322134709767](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281425452.png)



修改config-dev.yml配置并提交到GitHub中，比如加个变量age或者版本号version



### 3、主启动

com.atguigu.springcloud.ConfigClientMain3355

```java
@EnableEurekaClient
@SpringBootApplication
public class ConfigClientMain3355 {
    public static void main(String[] args) {
        SpringApplication.run(ConfigClientMain3355.class, args);
    }
}
```



### 4、业务类

com.atguigu.springcloud.controller.ConfigClientController

```java
@RestController
public class ConfigClientController {
    @Value("${spring.cloud.config.info}")
    private String configInfo;

    @GetMapping("/configInfo")
    public String getConfigInfo() {
        return configInfo;
    }
}
```



### 5、测试

启动Config配置中心3344微服务并自测：

http://config-3344.com:3344/master/config-dev.yml

![image-20220322162426573](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281425452.png)



启动3355作为Client准备访问：http://localhost:3355/configInfo

![image-20220322162408629](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281425132.png)



获取成功，从3355访问3344,3344再去访问gitee，当gitee变化的时候，3344和3355都要变，3344变了，但是3355必须要重启才可以更新，所以还是存在问题

修改 gitee 上的配置：把 version 改为2

![image-20220322162638710](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281425492.png)

刷新3344：

![image-20220322162654685](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281425747.png)



刷新3355，发现没有变化



### 6、分布式配置的动态刷新问题

- Linux运维修改Gitee上的配置文件内容做调整
- 刷新3344，发现ConfigServer配置中心立刻响应
- 刷新3355，发现ConfigClient客户端没有任何响应
- 3355没有变化除非自己重启或者重新加载
- 难到每次运维修改配置文件，客户端都需要重启？？噩梦
  
  

## （四）Config客户端之动态刷新

避免每次更新配置都要重启客户端微服务3355，我们需要它能动态刷新，下面来修改3355模块

### 1、POM引入actuator监控

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```



### 2、修改YML，暴露监控端口

```yaml
# 暴露监控端点
management:
  endpoints:
    web:
      exposure:
        include: "*"
```



### 3、@RefreshScope业务类Controller修改

```java
@RefreshScope
```

```java
@RestController
@RefreshScope
public class ConfigClientController {
    @Value("${spring.cloud.config.info}")
    private String configInfo;

    @GetMapping("/configInfo")
    public String getConfigInfo() {
        return configInfo;
    }
}
```



### 4、问题和解决

此时修改gitee，再测：http://localhost:3355/configInfo，发现3355还是没有变化

需要运维人员发送Post请求刷新3355

```
curl -X POST "http://localhost:3355/actuator/refresh"
```

![image-20220322162851252](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281426382.png)



再次请求：http://localhost:3355/configInfo，成功实现了客户端3355刷新到最新配置内容，避免了服务重启

![image-20220322162910328](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281426699.png)



### 5、思考

想想还有什么问题？

- 假如有多个微服务客户端3355/3366/3377。。。。。。
- 每个微服务都要执行一次post请求，手动刷新？
- 可否广播，一次通知，处处生效？
- 我们想大范围的自动刷新，求方法
  
  

# 十一、SpringCloud Bus 消息总线

## （一）概述

上一讲解的加深和扩充，一言以蔽之，分布式自动刷新配置功能

Spring Cloud Bus 配合 Spring Cloud Config 使用可以实现配置的动态刷新

### 1、是什么

![image-20220322143600397](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281426650.png)

Spring Cloud Bus是用来将分布式系统的节点与轻量级消息系统链接起来的框架，它整合了Java的事件处理机制和消息中间件的功能。Spring Clud Bus目前支持RabbitMQ和Kafka。



### 2、能干嘛

Spring Cloud Bus能管理和传播分布式系统间的消息，就像一个分布式执行器，可用于广播状态更改、事件推送等，也可以当作微服务间的通信通道。

![image-20220322143735703](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281426242.png)



### 3、总线

什么是总线

在微服务架构的系统中，通常会使用轻量级的消息代理来构建一个共用的消息主题，并让系统中所有微服务实例都连接上来。由于该主题中产生的消息会被所有实例监听和消费，所以称它为消息总线。在总线上的各个实例，都可以方便地广播一些需要让其他连接在该主题上的实例都知道的消息。

基本原理

ConfigClient实例都监听MQ中同一个topic(默认是springCloudBus)。当一个服务刷新数据的时候，它会把这个信息放入到Topic中，这样其它监听同一Topic的服务就能得到通知，然后去更新自身的配置。

https://www.bilibili.com/video/av55976700?from=search&seid=15010075915728605208



## （二）RabbitMQ环境配置

安装Erlang，下载地址：http://erlang.org/download/otp_win64_21.3.exe

安装RabbitMQ，下载地址：https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.14/rabbitmq-server-3.7.14.exe

进入RabbitMQ安装目录下的sbin目录，输入以下命令启动管理功能

![image-20220322145326480](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281426316.png)

```shell
rabbitmq-plugins enable rabbitmq_management
```

![image-20220322145432077](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281426986.png)



可视化插件：

![image-20220322145538610](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281426498.png)



访问地址查看是否安装成功：http://localhost:15672/

tips：如果访问不到重启一下电脑就好了

输入账号密码并登录：guest guest

![image-20220322152540977](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281450111.png)



## （三）动态刷新全局广播

### 1、搭建客户端微服务3366

必须先具备良好的RabbitMQ环境先，演示广播效果，增加复杂度，再以3355为模板再制作一个3366

新建 cloud-config-client-3366

#### （1）pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-config-client-3366</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```



#### （2）bootstrap.yml

```yaml
server:
  port: 3366

spring:
  application:
    name: config-client
  cloud:
    #Config客户端配置
    config:
      label: master #分支名称
      name: config #配置文件名称
      profile: dev #读取后缀名称   上述3个综合：master分支上config-dev.yml的配置文件被读取http://config-3344.com:3344/master/config-dev.yml
      uri: http://localhost:3344 #配置中心地址

#服务注册到eureka地址
eureka:
  client:
    service-url:
      defaultZone: http://localhost:7001/eureka

# 暴露监控端点
management:
  endpoints:
    web:
      exposure:
        include: "*"
```



#### （3）主启动

com.atguigu.springcloud.ConfigClientMain3366

```java
@EnableEurekaClient
@SpringBootApplication
public class ConfigClientMain3366 {
    public static void main(String[] args) {
        SpringApplication.run(ConfigClientMain3366.class, args);
    }
}
```



#### （4）controller

com.atguigu.springcloud.controller.ConfigClientController

```java
@RestController
@RefreshScope
public class ConfigClientController {
    @Value("${spring.cloud.config.info}")
    private String configInfo;

    @GetMapping("/configInfo")
    public String getConfigInfo() {
        return configInfo;
    }
}
```



### 2、设计思想

（1）利用消息总线触发一个客户端/bus/refresh,而刷新所有客户端的配置

![image-20220322153035534](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281450731.png)



（2）利用消息总线触发一个服务端ConfigServer的/bus/refresh端点，而刷新所有客户端的配置

![image-20220322153135164](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281450538.png)



图二的架构显然更加适合，图一不适合的原因如下：

1. 打破了微服务的职责单一性，因为微服务本身是业务模块，它本不应该承担配置刷新的职责
2. 破坏了微服务各节点的对等性
3. 有一定的局限性。例如，微服务在迁移时，它的网络地址常常会发生变化，此时如果想要做到自动刷新，那就会增加更多的修改
   
   

### 3、配置中心3344添加消息总线支持

给cloud-config-center-3344配置中心服务端添加消息总线支持

#### （1）pom.xml

```xml
<!--添加消息总线RabbitMQ支持-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bus-amqp</artifactId>
</dependency>
```



#### （2）application.yml

```yaml
##rabbitmq相关配置,暴露bus刷新配置的端点
management:
  endpoints: #暴露bus刷新配置的端点
    web:
      exposure:
        include: 'bus-refresh'
```



### 4、客户端3355添加消息总线支持

给cloud-config-client-3355客户端添加消息总线支持

#### （1）pom.xml

```xml
<!--添加消息总线RabbitMQ支持-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bus-amqp</artifactId>
</dependency>
```



#### （2）bootstrap.yml

```yaml
#rabbitmq相关配置 15672是Web管理界面的端口；5672是MQ访问的端口
rabbitmq:
  host: localhost
  port: 5672
  username: guest
  password: guest
```

```yaml
server:
  port: 3355

spring:
  application:
    name: config-client
  cloud:
    #Config客户端配置
    config:
      label: master #分支名称
      name: config #配置文件名称
      profile: dev #读取后缀名称   上述3个综合：master分支上config-dev.yml的配置文件被读取http://config-3344.com:3344/master/config-dev.yml
      uri: http://localhost:3344 #配置中心地址
  #rabbitmq相关配置 15672是Web管理界面的端口；5672是MQ访问的端口
  rabbitmq:
    host: localhost
    port: 5672
    username: guest
    password: guest

#服务注册到eureka地址
eureka:
  client:
    service-url:
      defaultZone: http://localhost:7001/eureka

# 暴露监控端点
management:
  endpoints:
    web:
      exposure:
        include: "*"
```



### 5、客户端3366添加消息总线支持

给cloud-config-client-3366客户端添加消息总线支持

#### （1）pom.xml

```xml
<!--添加消息总线RabbitMQ支持-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-bus-amqp</artifactId>
</dependency>
```



#### （2）bootstrap.yml

```yaml
#rabbitmq相关配置 15672是Web管理界面的端口；5672是MQ访问的端口
rabbitmq:
  host: localhost
  port: 5672
  username: guest
  password: guest
```

```yaml
server:
  port: 3366

spring:
  application:
    name: config-client
  cloud:
    #Config客户端配置
    config:
      label: master #分支名称
      name: config #配置文件名称
      profile: dev #读取后缀名称   上述3个综合：master分支上config-dev.yml的配置文件被读取http://config-3344.com:3344/master/config-dev.yml
      uri: http://localhost:3344 #配置中心地址
  #rabbitmq相关配置 15672是Web管理界面的端口；5672是MQ访问的端口
  rabbitmq:
    host: localhost
    port: 5672
    username: guest
    password: guest

#服务注册到eureka地址
eureka:
  client:
    service-url:
      defaultZone: http://localhost:7001/eureka

# 暴露监控端点
management:
  endpoints:
    web:
      exposure:
        include: "*"
```



### 6、测试

#### （1）运维工程师

修改Gitee上配置文件增加版本号

![image-20220322163211923](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281450918.png)

发送POST请求

```shell
curl -X POST "http://localhost:3344/actuator/bus-refresh"
```

一次发送，处处生效



#### （2）配置中心

http://config-3344.com:3344/master/config-dev.yml

![image-20220322163726386](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281450109.png)



#### （3）客户端

http://localhost:3355/configInfo

![image-20220322163830669](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281450062.png)



http://localhost:3366/configInfo

![image-20220322163840087](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281450620.png)

一次修改，广播通知，处处生效



## （四）动态刷新定点通知

不想全部通知，只想定点通知：只通知3355，不通知3366

简单一句话：指定具体某一个实例生效而不是全部

公式：http://localhost:配置中心的端口号/actuator/bus-refresh/{destination}

/bus/refresh请求不再发送到具体的服务实例上，而是发给config server并通过destination参数类指定需要更新配置的服务或实例

案例：

我们这里以刷新运行在3355端口上的config-client为例：只通知3355，不通知3366

```shell
curl -X POST "http://localhost:3344/actuator/bus-refresh/config-client:3355"
```



通知总结All

![image-20220322164834859](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281551617.png)



# 十二、SpringCloud Stream 消息驱动

## （一）消息驱动概述

### 1、是什么

屏蔽底层消息中间件的差异,降低切换成本，统一消息的编程模型



### 2、官网

https://spring.io/projects/spring-cloud-stream#overview

Spring Cloud Stream是用于构建与共享消息传递系统连接的高度可伸缩的事件驱动微服务框架，该框架提供了一个灵活的编程模型，它建立在已经建立和熟悉的Spring熟语和最佳实践上，包括支持持久化的发布/订阅、消费组以及消息分区这三个核心概念

![image-20220322165759792](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281552759.png)



https://cloud.spring.io/spring-cloud-static/spring-cloud-stream/3.0.1.RELEASE/reference/html/



Spring Cloud Stream中文指导手册：https://m.wang1314.com/doc/webapp/topic/20971999.html



### 3、设计思想

#### （1）标准MQ

- 生产者/消费者之间靠消息媒介传递信息内容——Message
- 消息必须走特定的通道——消息通道MessageChannel
- 消息通道里的消息如何被消费呢，谁负责收发处理——消息通道MessageChannel的子接口SubscribableChannel，由MessageHandler消息处理器所订阅

![image-20220322165851999](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281552814.png)



#### （2）为什么用Cloud Stream

问题：为什么要引入SpringCloud Stream

举例：对于我们Java程序员来说，可能有时要使用ActiveMQ,有时要使用RabbitMQ,甚至还有RocketMQ以及Kafka，这之间的切换似乎很麻烦，我们很难，也没有太多时间去精通每一门技术，那有没有一种新技术的诞生，让我们不再关注具体MQ的细节，自动的给我们在各种MQ内切换。

简介：Spring Cloud Stream 是一个用来为微服务应用构建消息驱动能力的框架。它可以基于 Spring Boot 来创建独立的、可用于生产的 Spring 应用程序。Spring Cloud Stream 为一些供应商的消息中间件产品提供了个性化的自动化配置实现，并引入了发布-订阅、消费组、分区这三个核心概念。通过使用 Spring Cloud Stream，可以有效简化开发人员对消息中间件的使用复杂度，让系统开发人员可以有更多的精力关注于核心业务逻辑的处理。但是目前 Spring Cloud Stream 只支持 RabbitMQ 和 Kafka 的自动化配置。

一句话：屏蔽底层消息中间件的差异，降低切换成本，统一消息的编程模型。



#### （3）Binder

在没有绑定器这个概念的情况下，我们的SpringBoot应用要直接与消息中间件进行信息交互的时候，由于各消息中间件构建的初衷不同，它们的实现细节上会有较大的差异性，通过定义绑定器作为中间层，完美地实现了应用程序与消息中间件细节之间的隔离。Stream对消息中间件的进一步封装，可以做到代码层面对中间件的无感知，甚至于动态的切换中间件(rabbitmq切换为kafka)，使得微服务开发的高度解耦，服务可以关注更多自己的业务流程

![image-20220322170240853](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281450320.png)

通过定义绑定器Binder作为中间层，实现了应用程序与消息中间件细节之间的隔离。

Binder可以生成Binding，Binding用来绑定消息容器的生产者和消费者，它有两种类型，INPUT和OUTPUT，INPUT对应于消费者，OUTPUT对应于生产者。



#### （4）Stream中的消息通信方式遵循了发布-订阅模式

Topic主题进行广播：在RabbitMQ就是Exchange，在Kakfa中就是Topic



### 4、Stream标准流程套路

Binder：很方便的连接中间件，屏蔽差异

Channel：通道，是队列Queue的一种抽象，在消息通讯系统中就是实现存储和转发的媒介，通过Channel对队列进行配置

Source和Sink：简单的可理解为参照对象是Spring Cloud Stream自身，从Stream发布消息就是输出，接受消息就是输入

![image-20220322170624180](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281451981.png)



### 5、编码API和常用注解

![image-20220328145156313](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281451638.png)

![image-20220322170827789](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281451634.png)



## （二）案例说明

RabbitMQ环境已经OK，工程中新建三个子模块

- cloud-stream-rabbitmq-provider8801，作为生产者进行发消息模块
- cloud-stream-rabbitmq-consumer8802，作为消息接收模块
- cloud-stream-rabbitmq-consumer8803  作为消息接收模块
  
  

### 1、消息驱动之生产者 provider8801

cloud-stream-rabbitmq-provider8801

#### （1）pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-stream-rabbitmq-provider8801</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-stream-rabbit</artifactId>
        </dependency>
        <!--基础配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



#### （2）application.yml

```yaml
server:
  port: 8801

spring:
  application:
    name: cloud-stream-provider
  cloud:
    stream:
      binders: # 在此处配置要绑定的rabbitmq的服务信息；
        defaultRabbit: # 表示定义的名称，用于于binding整合
          type: rabbit # 消息组件类型
          environment: # 设置rabbitmq的相关的环境配置
            spring:
              rabbitmq:
                host: localhost
                port: 5672
                username: guest
                password: guest
      bindings: # 服务的整合处理
        output: # 这个名字是一个通道的名称
          destination: studyExchange # 表示要使用的Exchange名称定义
          content-type: application/json # 设置消息类型，本次为json，文本则设置“text/plain”
          binder: defaultRabbit # 设置要绑定的消息服务的具体设置

eureka:
  client: # 客户端进行Eureka注册的配置
    service-url:
      defaultZone: http://localhost:7001/eureka
  instance:
    lease-renewal-interval-in-seconds: 2 # 设置心跳的时间间隔（默认是30秒）
    lease-expiration-duration-in-seconds: 5 # 如果现在超过了5秒的间隔（默认是90秒）
    instance-id: send-8801.com  # 在信息列表时显示主机名称
    prefer-ip-address: true     # 访问的路径变为IP地址
```



#### （3）主启动类StreamMQMain8801

com.atguigu.springcloud.StreamMQMain8801

```java
@SpringBootApplication
public class StreamMQMain8801 {
    public static void main(String[] args) {
        SpringApplication.run(StreamMQMain8801.class, args);
    }
}
```



#### （4）业务类

发送消息接口：com.atguigu.springcloud.service.IMessageProvider

```java
public interface IMessageProvider {
    String send();
}
```



发送消息接口实现类：com.atguigu.springcloud.service.impl.MessageProviderImpl

```java
package com.atguigu.springcloud.service.impl;

import com.atguigu.springcloud.service.IMessageProvider;
import org.springframework.cloud.stream.annotation.EnableBinding;
import org.springframework.cloud.stream.messaging.Source;
import org.springframework.integration.support.MessageBuilder;
import org.springframework.messaging.MessageChannel;

import javax.annotation.Resource;
import java.util.UUID;

/**
 * @EnableBinding(Source.class) :可以理解为是一个消息的发送管道的定义
 * @author: yangfan
 * @Description:
 * @create: 2022-03-22 17:19
 */
@EnableBinding(Source.class)
public class MessageProviderImpl implements IMessageProvider {

    /**
     * 消息的发送管道
     */
    @Resource
    private MessageChannel output;

    @Override
    public String send() {
        String serial = UUID.randomUUID().toString();
        // 创建并发送消息
        this.output.send(MessageBuilder.withPayload(serial).build());
        System.out.println("***serial: " + serial);

        return serial;
    }
}
```



Controller：com.atguigu.springcloud.controller.SendMessageController

```java
@RestController
public class SendMessageController {
    @Resource
    private IMessageProvider messageProvider;

    @GetMapping(value = "/sendMessage")
    public String sendMessage() {
        return messageProvider.send();
    }
}
```



#### （5）测试

- 启动7001eureka
- 启动rabbitmq
  - rabbitmq-plugins enable rabbitmq_management
  - http://localhost:15672/
- 启动8801
- 访问：http://localhost:8801/sendMessage

![image-20220322172947229](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281452118.png)



![image-20220322173031694](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281452617.png)



### 2、消息驱动之消费者 consumer8802

cloud-stream-rabbitmq-consumer8802

#### （1）pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloud-stream-rabbitmq-consumer8802</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-stream-rabbit</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--基础配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



#### （2）application.yml

```yaml
server:
  port: 8802

spring:
  application:
    name: cloud-stream-consumer
  cloud:
    stream:
      binders: # 在此处配置要绑定的rabbitmq的服务信息；
        defaultRabbit: # 表示定义的名称，用于于binding整合
          type: rabbit # 消息组件类型
          environment: # 设置rabbitmq的相关的环境配置
            spring:
              rabbitmq:
                host: localhost
                port: 5672
                username: guest
                password: guest
      bindings: # 服务的整合处理
        input: # 这个名字是一个通道的名称
          destination: studyExchange # 表示要使用的Exchange名称定义
          content-type: application/json # 设置消息类型，本次为对象json，如果是文本则设置“text/plain”
          binder: defaultRabbit # 设置要绑定的消息服务的具体设置

eureka:
  client: # 客户端进行Eureka注册的配置
    service-url:
      defaultZone: http://localhost:7001/eureka
  instance:
    lease-renewal-interval-in-seconds: 2 # 设置心跳的时间间隔（默认是30秒）
    lease-expiration-duration-in-seconds: 5 # 如果现在超过了5秒的间隔（默认是90秒）
    instance-id: receive-8802.com  # 在信息列表时显示主机名称
    prefer-ip-address: true     # 访问的路径变为IP地址
```



#### （3）主启动类StreamMQMain8802

com.atguigu.springcloud.StreamMQMain8802

```java
@SpringBootApplication
public class StreamMQMain8802 {
    public static void main(String[] args) {
        SpringApplication.run(StreamMQMain8802.class, args);
    }
}
```



#### （4）业务类

com.atguigu.springcloud.service.ReceiveMessageListener

```java
@Component
@EnableBinding(Sink.class)
public class ReceiveMessageListener {
    @Value("${server.port}")
    private String serverPort;

    @StreamListener(Sink.INPUT)
    public void input(Message<String> message) {
        System.out.println("消费者1号，------->接收到的消息：" + message.getPayload() + "\t port: " + serverPort);
    }
}
```



#### （5）测试8801发送8802接收消息

http://localhost:8801/sendMessage

![image-20220322174156447](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281452140.png)



8802控制台：

![image-20220328145300608](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281453839.png)



### 3、分组消费与持久化 consumer8803

cloud-stream-rabbitmq-consumer8803

依照8802，clone出来一份运行8803



### 4、分组消费

#### （1）启动

- RabbitMQ
- 7001：服务注册
- 8801：消息生产
- 8802：消息消费
- 8803：消息消费

运行后有两个问题：

- 有重复消费问题
- 消息持久化问题
  
  

#### （2）消费

http://localhost:8801/sendMessage

目前是8802/8803同时都收到了，存在重复消费问题

![image-20220322175049804](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281453625.png)

![image-20220322175100443](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281453259.png)



如何解决？分组和持久化属性group



生产实际案例：

比如在如下场景中，订单系统我们做集群部署，都会从RabbitMQ中获取订单信息，那如果一个订单同时被两个服务获取到，那么就会造成数据错误，我们得避免这种情况。这时我们就可以使用Stream中的消息分组来解决

![image-20220322175234895](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281453518.png)

注意在Stream中处于同一个group中的多个消费者是竞争关系，就能够保证消息只会被其中一个应用消费一次

不同组是可以全面消费的(重复消费)，同一组内会发生竞争关系，只有其中一个可以消费



#### （3）分组

原理：微服务应用放置于同一个group中，就能够保证消息只会被其中一个应用消费一次。不同的组是可以消费的，同一个组内会发生竞争关系，只有其中一个可以消费。

##### ① 不同组

8802/8803都变成不同组，group两个不同

8802修改YML：

```yaml
group: atguiguA
```

![image-20220322175518532](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281454565.png)



8803修改YML：

```yaml
group: atguiguB
```

![image-20220322175605202](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281455270.png)



我们自己配置：

![image-20220322175755621](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281454576.png)

分布式微服务应用为了实现高可用和负载均衡，实际上都会部署多个实例，本例阳哥启动了两个消费微服务(8802/8803)，多数情况，生产者发送消息给某个具体微服务时只希望被消费一次，按照上面我们启动两个应用的例子，虽然它们同属一个应用，但是这个消息出现了被重复消费两次的情况。为了解决这个问题，在Spring Cloud Stream中提供了消费组的概念



结论：还是重复消费

8802/8803实现了轮询分组，每次只有一个消费者，8801模块的发的消息只能被8802或8803其中一个接收到，这样避免了重复消费



##### ② 同组

8802/8803都变成相同组，group两个相同，都变成 atguiguA

```yaml
group: atguiguA
```



结论：同一个组的多个微服务实例，每次只会有一个拿到



### 5、持久化

通过上述，解决了重复消费问题，再看看持久化

- 停止8802/8803并去除掉8802的分组group: atguiguA，8803的分组group: atguiguA没有去掉
- 8801先发送4条消息到rabbitmq
- 先启动8802，无分组属性配置，后台没有打出来消息
- 再启动8803，有分组属性配置，后台打出来了MQ上的消息

8802控制台：

![image-20220322180553889](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281455689.png)



8803控制台：

![image-20220322180645114](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281552245.png)



# 十三、SpringCloud Sleuth 分布式请求链路跟踪

## （一）概述

为什么会出现这个技术？需要解决哪些问题？

在微服务框架中，一个由客户端发起的请求在后端系统中会经过多个不同的的服务节点调用来协同产生最后的请求结果，每一个前段请求都会形成一条复杂的分布式服务调用链路，链路中的任何一环出现高延时或错误都会引起整个请求最后的失败



是什么

官网：https://github.com/spring-cloud/spring-cloud-sleuth

Spring Cloud Sleuth提供了一套完整的服务跟踪的解决方案，在分布式系统中提供追踪解决方案并且兼容支持了zipkin

![image-20220322180945364](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281457290.png)



## （二）搭建链路监控步骤

### 1、zipkin

SpringCloud从F版起已不需要自己构建Zipkin Server了，只需调用jar包即可

https://dl.bintray.com/openzipkin/maven/io/zipkin/java/zipkin-server/

zipkin-server-2.12.9-exec.jar

```shell
java -jar zipkin-server-2.12.9-exec.jar
```

![image-20220322181520318](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281458479.png)



运行控制台：http://localhost:9411/zipkin/



术语—完整的调用链路： 表示一请求链路，一条链路通过Trace Id唯一标识，Span标识发起的请求信息，各span通过parent id 关联起来

![image-20220322181811124](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281458765.png)



一条链路通过Trace Id唯一标识，Span标识发起的请求信息，各span通过parent id 关联起来

![image-20220322181859871](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281458609.png)



![image-20220322181913301](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281458407.png)



名词解释：

- Trace：类似于树结构的Span集合，表示一条调用链路，存在唯一标识
- span：表示调用链路来源，通俗的理解span就是一次请求信息
  
  

### 2、服务提供者 cloud-provider-payment8001

cloud-provider-payment8001

#### （1）改 pom.xml

增加：

```xml
<!--包含了sleuth+zipkin-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-zipkin</artifactId>
</dependency>
```



#### （2）改 application.yml

增加：

```yaml
zipkin:
  base-url: http://localhost:9411
sleuth:
  sampler:
    #采样率值介于 0 到 1 之间，1 则表示全部采集
    probability: 1
```

![image-20220322182412645](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281458938.png)



#### （3）改业务类 PaymentController

增加：

```java
@GetMapping("/payment/zipkin")
public String paymentZipkin() {
    return "hi ,i'am paymentzipkin server fall back，welcome to atguigu，O(∩_∩)O哈哈~";
}
```



### 3、服务消费者（调用方）cloud-consumer-order80

cloud-consumer-order80

#### （1）改 pom.xml

增加：

```xml
<!--包含了sleuth+zipkin-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-zipkin</artifactId>
</dependency>
```



#### （2）改 application.yml

增加：

```yaml
zipkin:
  base-url: http://localhost:9411
sleuth:
  sampler:
    #采样率值介于 0 到 1 之间，1 则表示全部采集
    probability: 1
```

![image-20220322183125316](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281458022.png)



#### （3）改业务类 PaymentController

增加：

```java
/**
 * zipkin+sleuth
 *
 * @return
 */
@GetMapping("/consumer/payment/zipkin")
public String paymentZipkin() {
    String result = restTemplate.getForObject("http://localhost:8001" + "/payment/zipkin/", String.class);
    return result;
}
```



### 4、测试

- 依次启动eureka7001/8001/80
- 80调用8001几次测试下：http://localhost/consumer/payment/get/2
- 打开浏览器访问：http://localhost:9411

![image-20220328150003315](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281500646.png)



![image-20220322190255772](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281459683.png)



查看依赖关系

![image-20220322190519137](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281500835.png)



#### 5、原理

![image-20220322181811124](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281500759.png)



# 十四、SpringCloud Alibaba 入门简介

## （一）why会出现SpringCloud alibaba

Spring Cloud Netflix项目进入维护模式：https://spring.io/blog/2018/12/12/spring-cloud-greenwich-rc1-available-now

![image-20220322190917289](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281500501.png)



Spring Cloud Netflix Projects Entering Maintenance Mode

什么是维护模式？

![image-20220322190943840](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281501316.png)

将模块置于维护模式，意味着 Spring Cloud 团队将不会再向模块添加新功能。我们将修复 block 级别的 bug 以及安全问题，我们也会考虑并审查社区的小型 pull request



进入维护模式意味着什么呢？

进入维护模式意味着 Spring Cloud Netflix 将不再开发新的组件，我们都知道Spring Cloud 版本迭代算是比较快的，因而出现了很多重大ISSUE都还来不及Fix就又推另一个Release了。进入维护模式意思就是目前一直以后一段时间Spring Cloud Netflix提供的服务和功能就这么多了，不在开发新的组件和功能了。以后将以维护和Merge分支Full Request为主

新组件功能将以其他替代平代替的方式实现

![image-20220322191038903](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281501570.png)



## （二）SpringCloud alibaba带来了什么

### 1、是什么

官网：https://github.com/alibaba/spring-cloud-alibaba/blob/master/README-zh.md

诞生：2018.10.31，Spring Cloud Alibaba 正式入驻了 Spring Cloud 官方孵化器，并在 Maven 中央库发布了第一个版本

![image-20220322191128049](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281501379.png)



### 2、能干嘛

服务限流降级：默认支持 Servlet、Feign、RestTemplate、Dubbo 和 RocketMQ 限流降级功能的接入，可以在运行时通过控制台实时修改限流降级规则，还支持查看限流降级 Metrics 监控

服务注册与发现：适配 Spring Cloud 服务注册与发现标准，默认集成了 Ribbon 的支持

分布式配置管理：支持分布式系统中的外部化配置，配置更改时自动刷新

消息驱动能力：基于 Spring Cloud Stream 为微服务应用构建消息驱动能力

阿里云对象存储：阿里云提供的海量、安全、低成本、高可靠的云存储服务。支持在任何应用、任何时间、任何地点存储和访问任意类型的数据

分布式任务调度：提供秒级、精准、高可靠、高可用的定时（基于 Cron 表达式）任务调度服务。同时提供分布式的任务执行模型，如网格任务。网格任务支持海量子任务均匀分配到所有 Worker（schedulerx-client）上执行



### 3、去哪下

https://github.com/alibaba/spring-cloud-alibaba/blob/master/README-zh.md



### 4、怎么玩

![image-20220322191240304](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281501422.png)



## （三）SpringCloud alibaba学习资料获取

官网：https://spring.io/projects/spring-cloud-alibaba#overview

![image-20220322191431284](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281501826.png)

Spring Cloud Alibaba 致力于提供微服务开发的一站式解决方案。此项目包含开发分布式应用微服务的必需组件，方便开发者通过 Spring Cloud 编程模型轻松使用这些组件来开发分布式应用服务。依托 Spring Cloud Alibaba，您只需要添加一些注解和少量配置，就可以将 Spring Cloud 应用接入阿里微服务解决方案，通过阿里中间件来迅速搭建分布式应用系统。

SpringCloud Alibaba进入了SpringCloud官方孵化器，而且毕业了



英文：

- https://github.com/alibaba/spring-cloud-alibaba
- https://spring-cloud-alibaba-group.github.io/github-pages/greenwich/spring-cloud-alibaba.html
  
  

中文：https://github.com/alibaba/spring-cloud-alibaba/blob/master/README-zh.md



# 十五、SpringCloud Alibaba Nacos服务注册和配置中心



## （一）Nacos简介

### 1、为什么叫Nacos

前四个字母分别为Naming和Configuration的前两个字母，最后的s为Service



### 2、是什么

Nacos: Dynamic Naming and Configuration Service 一个更易于构建云原生应用的动态服务发现、配置管理和服务管理平台

Nacos 就是注册中心 + 配置中心的组合    Nacos = Eureka+Config +Bus



### 3、能干嘛

1. 替代Eureka做服务注册中心
2. 替代Config做服务配置中心
   
   

### 4、去哪下

https://github.com/alibaba/Nacos

官网文档：

- https://nacos.io/zh-cn/index.html
- https://spring-cloud-alibaba-group.github.io/github-pages/greenwich/spring-cloud-alibaba.html#_spring_cloud_alibaba_nacos_discovery
  
  

### 5、各种注册中心比较

![image-20220322192116429](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281503417.png)

据说 Nacos 在阿里巴巴内部有超过 10 万的实例运行，已经过了类似双十一等各种大型流量的考验



## （二）安装并运行Nacos

本地Java8+Maven环境已经OK

先从官网下载Nacos：https://github.com/alibaba/nacos/releases

解压安装包，直接运行bin目录下的startup.cmd

```shell
startup.cmd -m standalone
```

![image-20220322193218894](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281504004.png)



命令运行成功后直接访问：http://localhost:8848/nacos    默认账号密码都是nacos

![image-20220328150425520](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281504884.png)



## （三）Nacos作为服务注册中心演示

官网文档：https://spring-cloud-alibaba-group.github.io/github-pages/greenwich/spring-cloud-alibaba.html#_spring_cloud_alibaba_nacos_config

### 1、基于Nacos的服务提供者9001

新建Module：cloudalibaba-provider-payment9001

#### （1）父 pom.xml

增加：

```xml
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-alibaba-dependencies</artifactId>
    <version>2.1.0.RELEASE</version>
    <type>pom</type>
    <scope>import</scope>
</dependency>
```



#### （2）本模块 pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloudalibaba-provider-payment9001</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <!--SpringCloud ailibaba nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!-- SpringBoot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```



#### （3）application.yml

```yaml
server:
  port: 9001

spring:
  application:
    name: nacos-payment-provider
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848 #配置Nacos地址

management:
  endpoints:
    web:
      exposure:
        include: '*'
```



#### （4）主启动

com.atgugu.cloudalibaba.PaymentMain9001

```java
@EnableDiscoveryClient
@SpringBootApplication
public class PaymentMain9001 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain9001.class, args);
    }
}
```



#### （5）业务类

com.atgugu.cloudalibaba.controller.PaymentController

```java
@RestController
public class PaymentController {
    @Value("${server.port}")
    private String serverPort;

    @GetMapping(value = "/payment/nacos/{id}")
    public String getPayment(@PathVariable("id") Integer id) {
        return "nacos registry, serverPort: " + serverPort + "\t id" + id;
    }
}
```



#### （6）测试

http://localhost:9001/payment/nacos/1

nacos控制台：

![image-20220328150458424](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281504688.png)

nacos服务注册中心+服务提供者9001都OK了



为了下一章节演示nacos的负载均衡，参照9001新建9002

新建cloudalibaba-provider-payment9002



或者取巧不想新建重复体力劳动，直接拷贝虚拟端口映射

![image-20220322194841578](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281506748.png)



```shell
-DServer.port=9002
```

![image-20220322201838021](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281506447.png)

![image-20220322201858346](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281506989.png)



### 2、基于Nacos的服务消费者83

新建Module：cloudalibaba-consumer-nacos-order83

#### （1）pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloudalibaba-consumer-nacos-order83</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <!--SpringCloud ailibaba nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <!-- SpringBoot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



为什么nacos支持负载均衡？

![image-20220322195454778](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281507656.png)



#### （2）application.yml

```yaml
server:
  port: 83

spring:
  application:
    name: nacos-order-consumer
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848

#消费者将要去访问的微服务名称(注册成功进nacos的微服务提供者)
service-url:
  nacos-user-service: http://nacos-payment-provider
```



#### （3）主启动

com.atguigu.springcloud.alibaba.OrderNacosMain83

```java
@EnableDiscoveryClient
@SpringBootApplication
public class OrderNacosMain83 {
    public static void main(String[] args) {
        SpringApplication.run(OrderNacosMain83.class, args);
    }
} 
```



#### （4）业务类

##### ① ApplicationContextBean

com.atguigu.springcloud.alibaba.config.ApplicationContextBean

```java
@Configuration
public class ApplicationContextBean {
    @Bean
    @LoadBalanced
    public RestTemplate getRestTemplate() {
        return new RestTemplate();
    }
}
```



##### ② OrderNacosController

com.atguigu.springcloud.alibaba.controller.OrderNacosController

```java
@RestController
public class OrderNacosController {
    @Resource
    private RestTemplate restTemplate;

    @Value("${service-url.nacos-user-service}")
    private String serverURL;

    @GetMapping("/consumer/payment/nacos/{id}")
    public String paymentInfo(@PathVariable("id") Long id) {
        return restTemplate.getForObject(serverURL + "/payment/nacos/" + id, String.class);
    }

}
```



#### （5）测试

nacos控制台：

![image-20220322201922973](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281507584.png)



http://localhost:83/consumer/payment/nacos/1

![image-20220322201957740](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281507962.png)

![image-20220322202015749](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281507261.png)

83访问9001/9002，轮询负载OK



### 3、服务注册中心对比

Nacos全景图所示：

![image-20220323100012376](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281507890.png)



Nacos和CAP：

![image-20220323100126191](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281507364.png)

![image-20220323100140809](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281507961.png)



Nacos 支持AP和CP模式的切换：

C是所有节点在同一时间看到的数据是一致的；而A的定义是所有的请求都会收到响应

何时选择使用何种模式？

一般来说，如果不需要存储服务级别的信息且服务实例是通过nacos-client注册，并能够保持心跳上报，那么就可以选择AP模式。当前主流的服务如 Spring cloud 和 Dubbo 服务，都适用于AP模式，AP模式为了服务的可能性而减弱了一致性，因此AP模式下只支持注册临时实例。

如果需要在服务级别编辑或者存储配置信息，那么 CP 是必须，K8S服务和DNS服务则适用于CP模式。CP模式下则支持注册持久化实例，此时则是以 Raft 协议为集群运行模式，该模式下注册实例之前必须先注册服务，如果服务不存在，则会返回错误。

```shell
curl -X PUT '$NACOS_SERVER:8848/nacos/v1/ns/operator/switches?entry=serverMode&value=CP'
```



## （四）Nacos作为服务配置中心演示

### 1、Nacos作为配置中心3377-基础配置

新建 cloudalibaba-config-nacos-client3377

#### （1）pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloudalibaba-config-nacos-client3377</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <!--nacos-config-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
        </dependency>
        <!--nacos-discovery-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--web + actuator-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--一般基础配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



#### （2）两个 yml

why配置两个？

Nacos 同 springcloud-config 一样，在项目初始化时，要保证先从配置中心进行配置拉取，拉取配置之后，才能保证项目的正常启动。

springboot 中配置文件的加载是存在优先级顺序的，bootstrap 优先级高于application



bootstrap.yml

```yaml
# nacos配置
server:
  port: 3377

spring:
  application:
    name: nacos-config-client
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848 #Nacos服务注册中心地址
      config:
        server-addr: localhost:8848 #Nacos作为配置中心地址
        file-extension: yaml #指定yaml格式的配置


# ${spring.application.name}-${spring.profile.active}.${spring.cloud.nacos.config.file-extension}
```



application.yml

```yaml
spring:
  profiles:
    active: dev # 表示开发环境
```



#### （3）主启动

com.atguigu.springcloud.alibaba.NacosConfigClientMain3377

```java
@EnableDiscoveryClient
@SpringBootApplication
public class NacosConfigClientMain3377 {
    public static void main(String[] args) {
        SpringApplication.run(NacosConfigClientMain3377.class, args);
    }
}
```



#### （4）业务类

ConfigClientController：com.atguigu.springcloud.alibaba.controller.ConfigClientController

```java
@RestController
@RefreshScope //在控制器类加入@RefreshScope注解使当前类下的配置支持Nacos的动态刷新功能。
public class ConfigClientController {
    @Value("${config.info}")
    private String configInfo;

    @GetMapping("/config/info")
    public String getConfigInfo() {
        return configInfo;
    }
}
```



#### （5）在Nacos中添加配置信息

##### ① 理论

Nacos中的dataid的组成格式及与SpringBoot配置文件中的匹配规则

官网：https://nacos.io/zh-cn/docs/quick-start-spring-cloud.html

说明：之所以要配置 `spring.application.name`，是因为它是构成 Nacos 配置管理 `dataId`字段的一部分

在 Nacos Spring Cloud 中，dataId 的完整格式如下：（就是说在nacos端我们怎么命名文件的）

```yaml
${prefix}-${spring.profiles.active}.${file-extension}
```

- prefix 默认为 spring.application.name 的值，也可以通过配置项 spring.cloud.nacos.config.prefix 来配置
- spring.profiles.active 即为当前环境对应的 profile，详情可以参考 Spring Boot文档。 注意：当 spring.profiles.active 为空时，对应的连接符 - 也将不存在，dataId的拼接格式变成 `${prefix}.${file-extension}`
- file-exetension 为配置内容的数据格式，可以通过配置项 spring.cloud.nacos.config.file-extension 来配置。目前只支持 properties 和 yaml类型（注意nacos里必须使用yaml）
- 通过 Spring Cloud 原生注解 `@RefreshScope` 实现配置自动刷新
  
  

最后公式：

```yaml
${spring.application.name}-${spring.profiles.active}.${spring.cloud.nacos.config.file-extension}
```



综合以上说明，和下面的截图，Nacos 的 dataid（类似文件名）应为： nacos-config-client-dev.yaml (必须是yaml)

![image-20220323103313360](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281507754.png)



##### ② 实操

配置新增：nacos-config-client-dev.yaml

tips：不要掉了 `.yaml`

```yaml
config:
  info: "config info for dev,from nacos config center."
```

![image-20220323110431533](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281507991.png)

![image-20220323110448780](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281508635.png)



小总结：

![](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281508803.png)



历史配置：Nacos会记录配置文件的历史版本默认保留30天，此外还有一键回滚功能，回滚操作将会触发配置更新

回滚：

![image-20220323110528581](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281508838.png)



#### （6）测试

- 启动前需要在 nacos 客户端-配置管理-配置管理栏目下有对应的 yaml 配置文件
- 运行cloud-config-nacos-client3377的主启动类
- 调用接口查看配置信息：http://localhost:3377/config/info

![image-20220323110744293](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281508315.png)



自带动态刷新：修改下Nacos中的yaml配置文件，再次调用查看配置的接口，就会发现配置已经刷新

![image-20220323110853107](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281508303.png)



刷新：

![image-20220323110916166](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281508102.png)



### 2、Nacos作为配置中心-分类配置

#### （1）问题——多环境多项目管理

问题1：

实际开发中，通常一个系统会准备：dev开发环境、test测试环境、prod生产环境，如何保证指定环境启动时服务能正确读取到Nacos上相应环境的配置文件呢？

问题2：

一个大型分布式微服务系统会有很多微服务子项目，每个微服务项目又都会有相应的开发环境、测试环境、预发环境、正式环境......那怎么对这些微服务配置进行管理呢？



#### （2）Nacos的图形化管理界面

配置管理：

![image-20220323111251204](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281508787.png)



命名空间：

![image-20220323111325623](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281508678.png)



#### （3）Namespace+Group+Data ID三者关系？

思考：为什么这么设计？

① 是什么？

类似Java里面的package名和类名，最外层的namespace是可以用于区分部署环境的，Group和DataID逻辑上区分两个目标对象



② 三者情况

![image-20220323111515475](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281508937.png)



③ 默认情况

Namespace=public，Group=DEFAULT_GROUP，默认Cluster是DEFAULT

Nacos默认的命名空间是public；Namespace主要用来实现隔离，比方说我们现在有三个环境：开发、测试、生产环境，我们就可以创建三个Namespace，不同的Namespace之间是隔离的

Group默认是DEFAULT_GROUP，Group可以把不同的微服务划分到同一个分组里面去

Service就是微服务；一个Service可以包含多个Cluster（集群），Nacos默认Cluster是DEFAULT，Cluster是对指定微服务的一个虚拟划分。比方说为了容灾，将Service微服务分别部署在了杭州机房和广州机房，这时就可以给杭州机房的Service微服务起一个集群名称（HZ），给广州机房的Service微服务起一个集群名称（GZ），还可以尽量让同一个机房的微服务互相调用，以提升性能

最后是Instance，就是微服务的实例



#### （4）三种方案加载配置 Case

##### ① DataID方案

指定spring.profile.active和配置文件的DataID来使不同环境下读取不同的配置

默认空间+默认分组+新建dev和test两个DataID

新建test配置DataID：nacos-config-client-test.yaml

```yaml
config:
  info: "config info for test,from nacos config center."
```

![image-20220323112114934](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281508941.png)



通过spring.profile.active属性就能进行多环境下配置文件的读取：

![image-20220323112358412](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281508920.png)



测试：http://localhost:3377/config/info

配置是什么就加载什么——test

![image-20220323112518141](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281508796.png)



##### ② Group方案

通过Group实现环境区分，新建Group

**Data ID：**nacos-config-client-info.yaml

**Group：**TEST_GROUP

```yaml
config:
  info: "nacos-config-client-info.yaml,TEST_GROUP,version = v1.0."
```

![image-20220323112959609](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509462.png)



**Data ID：**nacos-config-client-info.yaml

**Group：**DEV_GROUP

```yaml
config:
  info: "nacos-config-client-info.yaml,DEV_GROUP,version = v1.0."
```

![image-20220323113236868](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509201.png)



![image-20220323113342091](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509655.png)



bootstrap+application

![image-20220323113616914](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509491.png)



刷新：http://localhost:3377/config/info

![image-20220323113658336](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509765.png)



##### ③ Namespace方案

新建dev/test的Namespace

注意下面的命名空间ID：

![image-20220323113855550](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509399.png)



回到服务管理-服务列表查看

![image-20220323113939684](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509448.png)



按照域名配置填写：

**Data ID：**nacos-config-client-dev.yaml

**Group：**DEFAULT_GROUP

```yaml
config:
  info: "nacos-config-client-dev.yaml,DEFAULT_GROUP,version = v1.0."
```



**Data ID：**nacos-config-client-dev.yaml

**Group：**DEV_GROUP

```yaml
config:
  info: "nacos-config-client-dev.yaml,DEV_GROUP,version = v1.0."
```



**Data ID：**nacos-config-client-dev.yaml

**Group：**TEST_GROUP

```yaml
config:
  info: "nacos-config-client-dev.yaml,TEST_GROUP,version = v1.0."
```



![image-20220323115847249](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509873.png)



bootstrap+application：

![image-20220323115258486](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509908.png)



刷新：http://localhost:3377/config/info

![image-20220323133320733](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509425.png)



## （五）Nacos集群和持久化配置

### 1、官网说明

https://nacos.io/zh-cn/docs/cluster-mode-quick-start.html

![image-20220323133720484](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509032.png)



上图官网翻译，真实情况

![image-20220323133755904](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509065.png)



说明：

默认Nacos使用嵌入式数据库实现数据的存储。所以，如果启动多个默认配置下的Nacos节点，数据存储是存在一致性问题的。为了解决这个问题，Nacos采用了集中式存储的方式来支持集群化部署，目前只支持MySQL的存储



按照上述，我们需要mysql数据库

官网说明：https://nacos.io/zh-cn/docs/deployment.html

重点说明：

![image-20220323134716536](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281509768.png)

![image-20220323134436168](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510409.png)



### 2、Nacos持久化配置解释

Nacos默认自带的是嵌入式数据库derby：https://github.com/alibaba/nacos/blob/develop/config/pom.xml

derby到mysql切换配置步骤：

- nacos-server-1.1.4\nacos\conf目录下找到sql脚本，执行 nacos-mysql.sql

```mysql
# 先创建数据库
CREATE DATABASE nacos_config;
USE nacos_config;
```

![image-20220323140136905](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510411.png)

- 修改nacos/conf/application.properties文件(切换数据库)，增加支持mysql数据源配置（目前只支持mysql），添加mysql数据源的url、用户名和密码

![image-20220323135619249](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510060.png)

```properties
# 切换数据库
spring.datasource.platform=mysql

db.num=1
db.url.0=jdbc:mysql://localhost:3306/nacos_devtest?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
db.user=root
db.password=root
```

- 访问：http://localhost:8848/nacos，可以看到是个全新的空记录界面，以前是记录进derby

![image-20220323141300144](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510950.png)



### 3、Linux版Nacos+MySQL生产环境配置

预计需要，1个Nginx+3个nacos注册中心+1个mysql

#### （1）Nacos下载Linux版

![image-20220323141343546](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510421.png)

https://github.com/alibaba/nacos/releases/tag/1.1.4

nacos-server-1.1.4.tar.gz

解压后安装：

![image-20220323141408633](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510617.png)



#### （2）集群配置步骤（重点）

##### ① Linux服务器上mysql数据库配置

SQL脚本在哪里

![image-20220323141549792](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510242.png)

sql语句源文件：nacos-mysql.sql

自己Linux机器上的Mysql数据库粘贴

![image-20220323141618679](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510393.png)



##### ② application.properties 配置

位置：

![image-20220323141653784](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510514.png)

![image-20220323141704028](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510211.png)



内容：

application.properties 文件打开后的最后面，配置如下内容：

```properties
spring.datasource.platform=mysql

db.num=1
db.url.0=jdbc:mysql://127.0.0.1:3306/nacos_config?characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true
db.user=root
db.password=root
```

![image-20220323141753696](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510121.png)



##### ③ Linux服务器上nacos的集群配置cluster.conf

梳理出3台nacos集器的不同服务端口号

复制出cluster.conf

![image-20220323141837927](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510638.png)

![image-20220323141906906](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281510398.png)

![image-20220323141932345](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511403.png)



内容：

![image-20220323141947891](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511371.png)



这个IP不能写127.0.0.1，必须是Linux命令hostname -i能够识别的IP

![image-20220323142008034](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511993.png)



##### ④ 编辑Nacos的启动脚本startup.sh，使它能够接受不同的启动端口

/mynacos/nacos/bin 目录下有startup.sh

在什么地方，修改什么，怎么修改？

/mynacos/nacos/bin 目录下有startup.sh，平时单机版的启动，都是./startup.sh即可。但是集群启动，我们希望可以类似其它软件的shell命令，传递不同的端口号启动不同的nacos实例

命令：./startup.sh -p 3333 表示启动端口号为3333的nacos服务器实例，和上一步的cluster.conf配置的一致



修改内容：

![image-20220323142133647](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511892.png)

修改前：

![image-20220323142155402](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511522.png)

![image-20220323142227641](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511542.png)

修改后：

![image-20220323142206985](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511850.png)

![image-20220323142232345](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511879.png)



执行方式：

![image-20220323142248748](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511673.png)



##### ⑤ Nginx的配置，由它作为负载均衡器

修改nginx的配置文件：

![](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511211.png)



nginx.conf：

```shell
upstream cluster{
        server 127.0.0.1:3333;
        server 127.0.0.1:4444;
        server 127.0.0.1:5555;
    }
```

```shell
server {
        listen       1111;
        server_name  localhost;
        #charset koi8-r;
        #access_log  logs/host.access.log  main;
        location / {
            #root   html;
            #index  index.html index.htm;
            proxy_pass http://cluster;
        }
.......省略
```

![image-20220323142437877](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511949.png)



按照指定启动：

![image-20220323142517545](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511003.png)



##### ⑥ 截止到此处，1个Nginx+3个nacos注册中心+1个mysql

测试通过nginx访问nacos：http://192.168.111.144:1111/nacos/#/login



新建一个配置测试：

![image-20220323142601613](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281511420.png)



linux服务器的mysql插入一条记录：

![image-20220323142620678](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281512270.png)



#### （3）测试

微服务cloudalibaba-provider-payment9002启动注册进nacos集群

```yaml
server:
  port: 9002

spring:
  application:
    name: nacos-payment-provider
  cloud:
    nacos:
      discovery:
        #配置Nacos地址
        #server-addr: localhost:8848
        # 换成nginx的1111端口，做集群
        server-addr: 192.168.111.144:1111


management:
  endpoints:
    web:
      exposure:
        include: '*'
```



结果：

![image-20220323142809485](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281512638.png)



### 4、高可用小总结

![image-20220323142830346](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281512359.png)



# 十六、SpringCloud Alibaba Sentinel 实现熔断与限流

## （一）概述

官网：https://github.com/alibaba/Sentinel

中文：https://github.com/alibaba/Sentinel/wiki/%E4%BB%8B%E7%BB%8D

### 1、是什么

一句话解释，之前我们讲解过的Hystrix

![image-20220323143025709](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281512048.png)



### 2、去哪下

https://github.com/alibaba/Sentinel/releases

![image-20220323143055298](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281512464.png)



### 3、能干嘛

![image-20220323143105095](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281512558.png)



### 4、怎么玩

https://spring-cloud-alibaba-group.github.io/github-pages/greenwich/spring-cloud-alibaba.html#_spring_cloud_alibaba_sentinel

服务使用中的各种问题：

- 服务雪崩
- 服务降级
- 服务熔断
- 服务限流
  
  

## （二）安装Sentinel控制台

sentinel组件由两部分构成：

1. 核心库（Java 客户端）不依赖任何框架/库，能够运行于所有 Java 运行时环境，同时对 Dubbo / Spring Cloud 等框架也有较好的支持
2. 控制台（Dashboard）基于 Spring Boot 开发，打包后可以直接运行，不需要额外的 Tomcat 等应用容器

后台 + 前台8080



安装步骤：

下载：https://github.com/alibaba/Sentinel/releases，下载到本地 sentinel-dashboard-1.7.1.jar

前提：java8环境OK + 8080端口不能被占用

运行命令：java -jar sentinel-dashboard-1.7.1.jar

![image-20220323143710437](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281512831.png)



访问sentinel管理界面：http://localhost:8080，登录账号密码均为sentinel

![image-20220323143825731](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281512234.png)



## （三）初始化演示工程

启动Nacos8848成功：http://localhost:8848/nacos/#/login



新建 cloudalibaba-sentinel-service8401

### 1、pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloudalibaba-sentinel-service8401</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <!--SpringCloud ailibaba nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--SpringCloud ailibaba sentinel-datasource-nacos 后续做持久化用到-->
        <dependency>
            <groupId>com.alibaba.csp</groupId>
            <artifactId>sentinel-datasource-nacos</artifactId>
        </dependency>
        <!--SpringCloud ailibaba sentinel -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
        </dependency>
        <!--openfeign-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
        <!-- SpringBoot整合Web组件+actuator -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>cn.hutool</groupId>
            <artifactId>hutool-all</artifactId>
            <version>4.6.3</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

    </dependencies>
</project>
```



### 2、application.yml

```yaml
server:
  port: 8401

spring:
  application:
    name: cloudalibaba-sentinel-service
  cloud:
    nacos:
      discovery:
        #Nacos服务注册中心地址
        server-addr: localhost:8848
    sentinel:
      transport:
        #配置Sentinel dashboard地址
        dashboard: localhost:8080
        #默认8719端口，假如被占用会自动从8719开始依次+1扫描,直至找到未被占用的端口
        port: 8719

management:
  endpoints:
    web:
      exposure:
        include: '*'
```



### 3、主启动

com.atguigu.springcloud.alibaba.SentinelMainApp8401

```java
@EnableDiscoveryClient
@SpringBootApplication
public class SentinelMainApp8401 {
    public static void main(String[] args) {
        SpringApplication.run(SentinelMainApp8401.class, args);
    }
}
```



### 4、业务类FlowLimitController

com.atguigu.springcloud.alibaba.controller.FlowLimitController

```java
@RestController
public class FlowLimitController {

    @GetMapping("/testA")
    public String testA() {
        return "------testA";
    }

    @GetMapping("/testB")
    public String testB() {
        return "------testB";
    }
}
```



### 5、测试

- 启动Sentinel8080：java -jar sentinel-dashboard-1.7.0.jar
- 启动微服务8401
- 启动8401微服务后查看sentienl控制台

空空如也，啥都没有

Sentinel采用的懒加载说明：

执行一次访问即可：http://localhost:8401/testA、http://localhost:8401/testB

![image-20220323145628467](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281512409.png)



结论：sentinel8080正在监控微服务8401



## （四）流控规则

### 1、基本介绍

![image-20220323145829338](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281512754.png)



解释说明：

- 资源名：唯一名称，默认请求路径
- 针对来源：sentinel可以针对调用者进行限流，填写微服务名，默认default（不区分来源）
- 阈值类型/单机值：
  - QPS（每秒钟的请求数量）：当调用该api就QPS达到阈值的时候，进行限流
  - 线程数．当调用该api的线程数达到阈值的时候，进行限流
- 是否集群：不需要集群
- 流控模式：
  - 直接：api达到限流条件时，直接限流。分为QPS和线程数
  - 关联：当关联的资到阈值时，就限流自己。别人惹事，自己买单
  - 链路：只记录指定链路上的流量（指定资源从入口资源进来的流量，如果达到阈值，就进行限流）【api级别的针对来源】
- 流控效果：
  - 快速失败：直接抛异常
  - warm up：根据codeFactor（冷加载因子，默认3）的值，从阈值codeFactor，经过预热时长，才达到设置的QPS阈值
  - 排队等待：匀速排毒，让请求以匀速通过，阈值类型必须设置为QPS，否则无效
    
    

QPS和线程数的区别：

- QPS 类似于银行的保安：所有的请求到Sentinel 后，他会根据阈值放行，超过报错
- 线程数类似于银行的窗口：所有的请求会被放进来，但如果阈值设置为1，那么其他的请求就会报错也就是，银行里只有一个窗口，一个人在办理业务中，其他人跑过来则会告诉你“现在不行，没到你”

![在这里插入图片描述](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281513871.png)



**重要属性：**

| Field           | 说明                                   | 默认值               |
| --------------- | ------------------------------------ | ----------------- |
| resource        | 资源名，资源名是限流规则的作用对象                    |                   |
| count           | 限流阈值                                 |                   |
| grade           | 限流阈值类型，QPS 模式（1）或并发线程数模式（0）          | QPS 模式            |
| limitApp        | 流控针对的调用来源                            | default，代表不区分调用来源 |
| strategy        | 调用关系限流策略：直接、链路、关联                    | 根据资源本身（直接）        |
| controlBehavior | 流控效果（直接拒绝/WarmUp/匀速+排队等待），不支持按调用关系限流 | 直接拒绝              |
| clusterMode     | 是否集群限流                               | 否                 |



### 2、流控模式

#### （1）直接（默认）

- 直接->快速失败：系统默认

- 配置及说明：表示1秒钟内查询1次就是OK，若超过次数1，就直接-快速失败，报默认错误
  ![image-20220323150201131](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281513197.png)

![image-20220323150409267](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281513807.png)

测试：快速点击访问：http://localhost:8401/testA

结果：Blocked by Sentinel (flow limiting)

![image-20220323150346997](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281513472.png)

思考？？？

直接调用默认报错信息，技术方面OK，但是否应该有我们自己的后续处理？类似有个fallback的兜底方法？



#### （2）关联

- 当关联的资源达到阈值时，就限流自己
- 当与A关联的资源B达到阀值后，就限流A自己
- B惹事，A挂了

配置A：设置效果，当关联资源/testB的qps阀值超过1时，就限流/testA的Rest访问地址，当关联资源到阈值后限制配置好的资源名

![image-20220323150636586](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281513005.png)



测试：

访问testB成功：

![image-20220323152120040](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281513780.png)



postman里新建多线程集合组：

![image-20220323152235062](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281513045.png)



将访问地址添加进新新线程组：

![image-20220323152333645](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281513608.png)



Run：

![image-20220323152427426](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281513298.png)

![image-20220323152530854](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281514108.png)



运行后发现testA挂了，点击访问：http://localhost:8401/testA，结果：Blocked by Sentinel (flow limiting)



#### （3）链路【尝试失败】

链路模式：只针对从指定链路访问到本资源的请求做统计，判断是否超过阈值

例如有两条请求链路：

- /test1      /common
- /test2      /common

如果只希望统计从/test2进入到/common的请求，对/test2 进行限流，则可以这样配置：

![image-20220323171559605](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281514648.png)



注意有个大坑：https://blog.csdn.net/qq_31155349/article/details/108478190

> 从1.6.3 版本开始，Sentinel Web filter默认收敛所有URL的入口context，因此链路限流不生效。1.7.0 版本开始（对应SCA的2.1.1.RELEASE)，官方在CommonFilter 引入了WEB_CONTEXT_UNIFY 参数，用于控制是否收敛context。将其配置为 false 即可根据不同的URL 进行链路限流。SCA 2.1.1.RELEASE之后的版本，可以通过配置spring.cloud.sentinel.web-context-unify=false即可关闭收敛，我们当前使用的版本是SpringCloud Alibaba 2.1.0.RELEASE，无法实现链路限流。目前官方还未发布SCA 2.1.2.RELEASE，所以我们只能使用2.1.1.RELEASE，需要写代码的形式实现

我们使用的版本：

![image-20220323175347809](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281514276.png)

上面这段是从百度down下来的，经过测试，SCA换成最新版本2.2.1.RELEASE仍然无效：配置spring.cloud.sentinel.web-context-unify=false无效！！！

推荐做法仍然是关闭官方的CommonFilter实例化，自己手动实例化CommonFilter，设置WEB_CONTEXT_UNIFY=false

```yaml
spring:
    cloud:
        sentinel:
            filter:
                enabled: false
```

【未解决】



**案例：流控模式-链路**

需求：有查询订单和创建订单业务，两者都需要查询商品。针对从查询订单进入到查询商品的请求统计，并设置限流

步骤：

1. 在OrderService中添加一个queryGoods方法，不用实现业务
2. 在OrderController中，创建/order/query端点，调用OrderService中的queryGoods方法(/order/query -> queryGoods)
3. 在OrderController中，创建/order/save端点，调用OrderService的queryGoods方法(/order/save -> queryGoods)
4. 给queryGoods设置限流规则，从/order/query进入queryGoods的方法限制QPS必须小于2**（设置/order/query qqs<2）**

Sentinel默认只标记Controller中的方法为资源，如果要标记其它方法，需要利用@SentinelResource注解，示例：

```java
@SentinelResource("goods")
public void queryGoods(){
    System.err.println("查询商品");
}
```



Sentinel默认会将Controller方法做context整合，导致链路模式的流控失效，需要修改application.yml，添加配置：

```yaml
spring:
  cloud:
    sentinel:
      transport:
        dashboard: localhost:8080 # sentinel控制台地址
      web-context-unify: false # 关闭context整合
```



![image-20220323174132581](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281514876.png)

访问/order/query、/order/save资源

- http://localhost:8088/order/query：##触发链路限流
- http://localhost:8088/order/save：不会触发链路限流
  
  

### 3、流控效果

#### （1）快速失败（默认的流控处理）

直接失败，抛出异常：Blocked by Sentinel (flow limiting)

源码：com.alibaba.csp.sentinel.slots.block.flow.controller.DefaultController



#### （2）预热

官网：https://github.com/alibaba/Sentinel/wiki/%E6%B5%81%E9%87%8F%E6%8E%A7%E5%88%B6

![image-20220323153241843](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281514287.png)



默认coldFactor为3，即请求 QPS 从 threshold / 3 开始，经预热时长逐渐升至设定的 QPS 阈值



限流冷启动：https://github.com/alibaba/Sentinel/wiki/%E9%99%90%E6%B5%81---%E5%86%B7%E5%90%AF%E5%8A%A8



源码：com.alibaba.csp.sentinel.slots.block.flow.controller.WarmUpController

![image-20220323153556079](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281514244.png)



WarmUp配置：

默认 coldFactor 为 3，即请求QPS从(threshold / 3) 开始，经多少预热时长才逐渐升至设定的 QPS 阈值

案例，阀值为10+预热时长设置5秒

系统初始化的阀值为10 / 3 约等于3，即阀值刚开始为3；然后过了5秒后阀值才慢慢升高恢复到10，效果为：开始访问[ http://localhost:8401/testB](http://localhost:8401/testB) 时每秒请求别超过10/3个才能正常访问，5秒后可以接受的请求可以达到每秒10次

![image-20220323153932479](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281514652.png)

多次点击：http://localhost:8401/testB

刚开始不行，后续慢慢OK



应用场景：

秒杀系统在开启的瞬间，会有很多流量上来，很有可能把系统打死，预热方式就是把为了保护系统，可慢慢的把流量放进来，慢慢的把阀值增长到设置的阀值



#### （3）排队等待

匀速排队，让请求以均匀的速度通过，阀值类型必须设成QPS，否则无效

设置含义：/testA每秒1次请求，超过的话就排队等待，等待的超时时间为20000毫秒

如下此设置的含义为：代表 1 秒匀速的通过 2 个请求，也就是每个请求平均间隔恒定为 1 / 2 = 0.5 s 也即 500 ms，每一个请求的最长等待时间为20s

同理，如果单机阈值为 1 时，每个请求的平均间隔恒定为 1000/1 = 10000 ms

![image-20220323192430204](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281514941.png)

说明：匀速排队，阈值必须设置为QPS



官网：https://github.com/alibaba/Sentinel/wiki/%E6%B5%81%E9%87%8F%E6%8E%A7%E5%88%B6

![image-20220323154314829](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281514530.png)



源码：com.alibaba.csp.sentinel.slots.block.flow.controller.RateLimiterController



测试：

![image-20220323193030705](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281514916.png)

阈值为2时：

![image-20220323192403691](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281514841.png)



阈值为1时：

![image-20220323192847700](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281514867.png)



## （五）降级规则

官网：https://github.com/alibaba/Sentinel/wiki/%E7%86%94%E6%96%AD%E9%99%8D%E7%BA%A7

### 1、介绍

![image-20220323155804020](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515155.png)

RT（平均响应时间，秒级）

- 平均响应时间**超出阈值**且**在时间窗口内通过的请求>=5**，两个条件同时满足后触发降级
- 窗口期过后关闭断路器
- RT最大4900（更大的需要通过-Dcsp.sentinel.statistic.max.rt=XXXX才能生效）

异常比列（秒级）

- **QPS >= 5**且**异常比例（秒级统计）超过阈值时**，触发降级；时间窗口结束后，关闭降级

异常数（分钟级）

- 异常数（分钟统计）超过阈值时，触发降级；时间窗口结束后，关闭降级
  
  

进一步说明：

Sentinel 熔断降级会在调用链路中某个资源出现不稳定状态时（例如调用超时或异常比例升高），对这个资源的调用进行限制，让请求快速失败，避免影响到其它的资源而导致级联错误

当资源被降级后，在接下来的降级时间窗口之内，对该资源的调用都自动熔断（默认行为是抛出 DegradeException）



Sentinel 的断路器是没有半开状态的：

半开的状态系统自动去检测是否请求有异常，没有异常就关闭断路器恢复使用；有异常则继续打开断路器不可用。具体可以参考Hystrix



### 2、RT

#### （1）介绍

![image-20220323160241638](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515075.png)

![image-20220323160504510](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515377.png)

#### （2）实操

在controller中加入textC：

```java
@GetMapping("/testC")
public String testC() {
    //暂停几秒钟线程
    try {
        TimeUnit.SECONDS.sleep(1);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    log.info("testC 测试RT");
    return "------testC";
}
```



配置：

![image-20220323160920116](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515640.png)



jmeter压测：

![image-20220323161349348](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515705.png)

压测时再访问 /testC

![image-20220323193614484](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515953.png)



停止压测后：

![image-20220323193713925](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515369.png)



结论：

按照上述配置，永远一秒钟打进来10个线程（大于5个了）调用testC，我们希望200毫秒处理完本次任务，如果超过200毫秒还没处理完，在未来1秒钟的时间窗口内，断路器打开(保险丝跳闸)微服务不可用，保险丝跳闸断电了，后续我停止jmeter，没有这么大的访问量了，断路器关闭(保险丝恢复)，微服务恢复OK



### 3、异常比例

#### （1）介绍

![image-20220323161738085](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515484.png)

![image-20220323161743863](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515834.png)



#### （2）实操

在controller中加入textD：

```java
@GetMapping("/testD")
public String testD() {
    log.info("testD 测试RT");
    int age = 10 / 0;
    return "------testD";
}
```



配置

![image-20220323161939354](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515342.png)



单独一次访问：http://localhost:8401/testD

![image-20220323194543546](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515109.png)



开启 jmeter 压测后再次访问：

![image-20220323194532214](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515892.png)

此时的压测还未停止：

![image-20220323194515805](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281515145.png)

![image-20220323170720421](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281516069.png)



当停止压测后：

![](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281516730.png)



#### （3）结论

按照上述配置，单独访问一次，必然来一次报错一次(int age  = 10/0)，调一次错一次；开启jmeter后，直接高并发发送请求，多次调用达到我们的配置条件了。
断路器开启(保险丝跳闸)，微服务不可用了，不再报错error而是服务降级了



### 5、异常数

#### （1）介绍

**时间窗口一定要大于等于60秒、异常数是按照分钟统计的**

![image-20220323162208655](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281516284.png)

![image-20220323162249143](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281516586.png)



#### （2）实战

在controller中加入textE：

```java
@GetMapping("/testE")
public String testE() {
    log.info("testE 测试异常比例");
    int age = 10 / 0;
    return "------testE 测试异常比例";
}
```



配置：

![image-20220323162453116](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281516256.png)

访问：http://localhost:8401/testE，第一次访问绝对报错，因为除数不能为零，我们看到error窗口，但是达到5次报错后，进入熔断后降级



第一次访问：

![image-20220323194645532](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281516920.png)



jmeter压测：

![image-20220323162533138](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281516123.png)

此时再访问：

![image-20220323194745727](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281516953.png)



当压测停止后：

![image-20220323194645532](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281517233.png)



## （六）热点key限流

### 1、基本介绍

何为热点：热点即经常访问的数据，很多时候我们希望统计或者限制某个热点数据中访问频次最高的TopN数据，并对其访问进行限流或者其它操作

官网：https://github.com/alibaba/Sentinel/wiki/%E7%83%AD%E7%82%B9%E5%8F%82%E6%95%B0%E9%99%90%E6%B5%81



承上启下复习start：

兜底方法：分为系统默认和客户自定义两种

- 之前的case，限流出问题后，都是用sentinel系统默认的提示：Blocked by Sentinel (flow limiting)

- 我们能不能自定？类似hystrix，某个方法出问题了，就找对应的兜底降级方法？

结论：从 HystrixCommand 到 **@SentinelResource**



### 2、实操

在controller中加入：

```java
@GetMapping("/testHotKey")
@SentinelResource(value = "testHotKey", blockHandler = "dealHandlerTestHotKey")
public String testHotKey(@RequestParam(value = "p1", required = false) String p1,
                         @RequestParam(value = "p2", required = false) String p2) {
    return "------testHotKey";
}

public String dealHandlerTestHotKey(String p1, String p2, BlockException exception) {
    return "-----dealHandler_testHotKey";
}
```

说明：

- `@SentinelResource(value = "testHotKey")`异常打到了前台用户界面看到，不友好
- `@SentinelResource(value = "testHotKey",blockHandler = "dealHandlerTestHotKey")`方法 testHotKey 里面第一个参数只要QPS超过每秒1次，马上降级处理
  
  

配置：

![image-20220323195740604](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281517409.png)

![image-20220323200235304](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281517909.png)

限流模式只支持QPS模式，固定写死了。（这才叫热点）`@SentinelResource`注解的方法参数索引，0代表第一个参数，1代表第二个参数，以此类推，单机阀值以及统计窗口时长表示在此窗口时间超过阀值就限流。上面的抓图就是第一个参数有值的话，1秒的QPS为1，超过就限流，限流后调用dealHandler_testHotKey支持方法。



压力测试：

- error：
  - http://localhost:8401/testHotKey?p1=abc
  - http://localhost:8401/testHotKey?p1=abc&p2=33
- right：
  - http://localhost:8401/testHotKey?p2=abc
    
    

http://localhost:8401/testHotKey?p1=abc

![image-20220323195806578](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281517874.png)



http://localhost:8401/testHotKey?p1=abc&p2=33

![image-20220323195834169](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281517455.png)



http://localhost:8401/testHotKey?p2=abc

![image-20220323195906415](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281517530.png)



### 3、参数例外项

上述案例演示了第一个参数p1，当QPS超过1秒1次点击后马上被限流

特例情况：我们期望p1参数当它是某个特殊值时，它的限流值和平时不一样

特例：假如当p1的值等于5时，它的阈值可以达到200

热点参数的注意点，参数必须是基本类型或者String

![image-20220324114602998](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281517638.png)



测试：

http://localhost:8401/testHotKey?p1=5    当p1等于5的时候，阈值变为200



用 JMeter 压测：

这个线程数随便

![image-20220324142444965](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281517701.png)

要指定 QPS 为固定值：

![image-20220324142418091](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281517589.png)

![image-20220324142344690](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281517628.png)



压测时我们来访问

![image-20220324142912094](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281518306.png)

![image-20220324143007287](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281518307.png)



-----



如果指定 QPS 为 2000【已经远大于在 Sentinel 中的阈值 200 了】

![image-20220324142736396](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281518552.png)

![image-20220324142828200](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281518337.png)

![image-20220324142713630](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281525188.png)



http://localhost:8401/testHotKey?p1=3    当p1不等于5的时候，阈值就是平常的1

都不用压测，直接手动快速刷新

![image-20220324143113039](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281525310.png)



### 4、其它

手贱添加异常看看....../(ㄒoㄒ)/~~

@SentinelResource：处理的是Sentinel控制台配置的违规情况，有blockHandler方法配置的兜底处理；

RuntimeException：int age = 10/0,这个是java运行时报出的运行时异常RunTimeException，@SentinelResource不管

总结：@SentinelResource主管配置出错，运行出错该走异常走异常



## （七）系统规则

### 1、介绍

https://github.com/alibaba/Sentinel/wiki/%E7%B3%BB%E7%BB%9F%E8%87%AA%E9%80%82%E5%BA%94%E9%99%90%E6%B5%81



### 2、各项配置参数说明

![image-20220324143938881](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281525104.png)

![image-20220324144124506](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281525143.png)

可以配置全局QPS



### 3、@SentinelResource

#### （1）按资源名称限流+后续处理

- 启动Nacos成功：http://localhost:8848/nacos/#/login

- 启动Sentinel成功：http://localhost:8080/

- 修改 cloudalibaba-sentinel-service8401

##### ① pom.xml

增加

```xml
<dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
    <groupId>com.atguigu.springcloud</groupId>
    <artifactId>cloud-api-commons</artifactId>
    <version>${project.version}</version>
</dependency>
```



##### ② 新增业务类RateLimitController

```java
@RestController
public class RateLimitController {
    @GetMapping("/byResource")
    @SentinelResource(value = "byResource", blockHandler = "handleException")
    public CommonResult byResource() {
        return new CommonResult(200, "按资源名称限流测试OK", new Payment(2020L, "serial001"));
    }

    public CommonResult handleException(BlockException exception) {
        return new CommonResult(444, exception.getClass().getCanonicalName() + "\t 服务不可用");
    }
}
```



##### ③ 配置流控规则

先访问：http://localhost:8401/byResource

![image-20220324145436122](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281525595.png)

簇点链路：byResource 是资源

![image-20220324145412281](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281525195.png)

除了在流控规则中，还可以直接在资源这里设置流控：

![image-20220324145606669](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281525442.png)

![image-20220324150027892](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281525591.png)



图形配置和代码关系：

![image-20220324150130344](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281525565.png)

表示1秒钟内查询次数大于1，就跑到我们自定义的处流，限流



测试：

1秒钟点击1下，OK：

![image-20220324150240371](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281526068.png)



超过上述，疯狂点击，返回了自己定义的限流处理信息，限流发生：

![image-20220324150407659](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281526012.png)



##### ④ 额外问题

此时关闭问服务8401看看：Sentinel控制台，流控规则消失了？？？？？临时/持久？

![image-20220324150527714](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281526834.png)



#### （2）按照Url地址限流+后续处理

通过访问的URL来限流，会返回Sentinel自带默认的限流处理信息

##### ① 修改业务类RateLimitController

新增：

```java
@GetMapping("/rateLimit/byUrl")
@SentinelResource(value = "byUrl")
public CommonResult byUrl() {
    return new CommonResult(200, "按url限流测试OK", new Payment(2020L, "serial002"));
}
```

访问：http://localhost:8401/rateLimit/byUrl

![image-20220324150822137](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281526531.png)

簇点链路：

byUrl 是资源

![image-20220324150935954](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281526033.png)



##### ② Sentinel控制台配置

![image-20220324151021468](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281526603.png)



测试，疯狂点击 http://localhost:8401/rateLimit/byUrl

![image-20220324151102496](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281526928.png)



#### （3）上面兜底方案面临的问题

1. 系统默认的，没有体现我们自己的业务要求

2. 依照现有条件，我们自定义的处理方法又和业务代码耦合在一块，不直观

3. 每个业务方法都添加一个兜底的，那代码膨胀加剧

4. 全局统一的处理方法没有体现
   
   

#### （4）客户自定义限流处理逻辑

##### ① 新建 CustomerBlockHandler

创建 CustomerBlockHandler 类用于自定义限流处理逻辑

com.atguigu.springcloud.alibaba.myhandler.CustomerBlockHandler

```java
public class CustomerBlockHandler {
    public static CommonResult handleException(BlockException exception) {
        return new CommonResult(2020, "自定义的限流处理信息......CustomerBlockHandler");
    }

    public static CommonResult handleException2(BlockException exception) {
        return new CommonResult(2020, "自定义的限流处理信息2......CustomerBlockHandler2");
    }
}
```



##### ② 修改 RateLimitController

新增：

```java
/**
 * 自定义通用的限流处理逻辑
 * blockHandlerClass = CustomerBlockHandler.class
 * blockHandler = handleException2
 * 上述配置：找CustomerBlockHandler类里的handleException2方法进行兜底处理
 *
 * @return
 */
@GetMapping("/rateLimit/customerBlockHandler")
@SentinelResource(value = "customerBlockHandler",
        blockHandlerClass = CustomerBlockHandler.class, blockHandler = "handleException2")
public CommonResult customerBlockHandler() {
    return new CommonResult(200, "按客户自定义限流处理逻辑");
}
```



##### ③ 测试

启动微服务后先调用一次：http://localhost:8401/rateLimit/customerBlockHandler

![image-20220324152255800](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281526161.png)



簇点链路：

![image-20220324152321640](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281526587.png)



Sentinel控制台配置：

![image-20220324152419260](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281526130.png)



疯狂刷新：

![image-20220324152441008](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281526200.png)



#### （5）更多注解属性说明

@SentinelResource注解最主要的两个用法：限流控制和熔断降级的具体使用案例介绍完了。另外，该注解还有一些其他更精细化的配置，比如忽略某些异常的配置、默认降级函数等等，具体可见如下说明：

- value：资源名称，必需项（不能为空）
- entryType：entry类型，可选项（默认为 EntryType.OUT）
- fallback：fallback函数名称，可选项，用于在抛出异常的时候提供 fallback处理逻辑。fallback函数可以针对所有类型的异常（除了exceptionsToIgnore里面排除掉的异常类型）进行处理。fallback函数签名和位置要求： 返回值类型必须与原函数返回值类型一致；方法参数列表需要和原函数一致，或者可以额外多一个 Throwable类型的参数用于接收对应的异常。
- fallback函数默认需要和原方法在同一个类中。若希望使用其他类的函数，则可以指定 fallbackClass为对应的类的 Class 对象，注意对应的函数必需为 static函数，否则无法解析。 defaultFallback（since 1.6.0）：默认的 fallback函数名称，可选项，通常用于通用的 fallback逻辑（即可以用于很多服务或方法）。默认 fallback函数可以针对所有类型的异常（除了exceptionsToIgnore里面排除掉的异常类型）进行处理。若同时配置了 fallback和 defaultFallback，则只有 fallback会生效。defaultFallback函数签名要求：返回值类型必须与原函数返回值类型一致；
- 方法参数列表需要为空，或者可以额外多一个 Throwable 类型的参数用于接收对应的异常。
- defaultFallback函数默认需要和原方法在同一个类中。若希望使用其他类的函数，则可以指定 fallbackClass为对应的类的 Class 对象，注意对应的函数必需为 static 函数，否则无法解析。
- exceptionsToIgnore（since 1.6.0）：用于指定哪些异常被排除掉，不会计入异常统计中，也不会进入 fallback 逻辑中，而是会原样抛出。

这篇帖子也不错：https://blog.csdn.net/liuerchong/article/details/114534166



多说一句：所有的代码都要用try-catch-finally方式进行处理，o(╥﹏╥)o

![image-20220324153257572](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281526239.png)



Sentinel主要有三个核心Api：

- SphU定义资源
- Tracer定义统计
- ContextUtil定义了上下文
  
  

### 4、服务熔断功能

sentinel整合ribbon+openFeign+fallback

#### （1）Ribbon系列——提供者9003/9004

启动nacos和sentinel，新建cloudalibaba-provider-payment9003/9004两个一样的做法

##### ① pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloudalibaba-provider-payment9003</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <!--SpringCloud ailibaba nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <dependency><!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <!-- SpringBoot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



##### ② application.yml

记得修改不同的端口号

```yaml
server:
  port: 9003

spring:
  application:
    name: nacos-payment-provider
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848 #配置Nacos地址

management:
  endpoints:
    web:
      exposure:
        include: '*'
```



##### ③ 主启动

com.atguigu.springcloud.alibaba.PaymentMain9003

记得改名

```java
@SpringBootApplication
@EnableDiscoveryClient
public class PaymentMain9003 {
    public static void main(String[] args) {
        SpringApplication.run(PaymentMain9003.class, args);
    }
}
```



##### ④ 业务类

com.atguigu.springcloud.alibaba.controller.PaymentController

```java
@RestController
public class PaymentController {
    @Value("${server.port}")
    private String serverPort;

    public static HashMap<Long, Payment> hashMap = new HashMap<>();

    static {
        hashMap.put(1L, new Payment(1L, "28a8c1e3bc2742d8848569891fb42181"));
        hashMap.put(2L, new Payment(2L, "bba8c1e3bc2742d8848569891ac32182"));
        hashMap.put(3L, new Payment(3L, "6ua8c1e3bc2742d8848569891xt92183"));
    }

    @GetMapping(value = "/paymentSQL/{id}")
    public CommonResult<Payment> paymentSQL(@PathVariable("id") Long id) {
        Payment payment = hashMap.get(id);
        CommonResult<Payment> result = new CommonResult(200, "from mysql,serverPort:  " + serverPort, payment);
        return result;
    }
}
```



测试地址：http://localhost:9003/paymentSQL/1

![image-20220324155343937](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281527975.png)



#### （2）Ribbon系列——消费者84

新建cloudalibaba-consumer-nacos-order84

##### ① pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloudalibaba-consumer-nacos-order84</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <!--SpringCloud ailibaba nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--SpringCloud ailibaba sentinel -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
        </dependency>
        <!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <!-- SpringBoot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



##### ② application.yml

```yaml
server:
  port: 84

spring:
  application:
    name: nacos-order-consumer
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848
    sentinel:
      transport:
        #配置Sentinel dashboard地址
        dashboard: localhost:8080
        #默认8719端口，假如被占用会自动从8719开始依次+1扫描,直至找到未被占用的端口
        port: 8719


#消费者将要去访问的微服务名称(注册成功进nacos的微服务提供者)
service-url:
  nacos-user-service: http://nacos-payment-provider
```



##### ③ 主启动

com.atguigu.springcloud.alibaba.OrderNacosMain84

```java
@EnableDiscoveryClient
@SpringBootApplication
public class OrderNacosMain84 {
    public static void main(String[] args) {
        SpringApplication.run(OrderNacosMain84.class, args);
    }
}
```



##### ④ 业务类 ApplicationContextConfig

com.atguigu.springcloud.alibaba.config.ApplicationContextConfig

```java
@Configuration
public class ApplicationContextConfig {

    @Bean
    @LoadBalanced
    public RestTemplate getRestTemplate() {
        return new RestTemplate();
    }
}
```



##### ⑤ 业务类 CircleBreakerController

com.atguigu.springcloud.alibaba.controller.CircleBreakerController

```java
@RestController
@Slf4j
public class CircleBreakerController {
    public static final String SERVICE_URL = "http://nacos-payment-provider";

    @Resource
    private RestTemplate restTemplate;

    @RequestMapping("/consumer/fallback/{id}")
    @SentinelResource(value = "fallback")
    public CommonResult<Payment> fallback(@PathVariable Long id) {
        CommonResult<Payment> result = restTemplate.getForObject(SERVICE_URL + "/paymentSQL/" + id, CommonResult.class, id);

        if (id == 4) {
            throw new IllegalArgumentException("IllegalArgumentException,非法参数异常....");
        } else if (result.getData() == null) {
            throw new NullPointerException("NullPointerException,该ID没有对应记录,空指针异常");
        }

        return result;
    }
}
```

修改后请重启微服务：热部署对java代码级生效及时，对@SentinelResource注解内属性，有时效果不好

目的：fallback管运行异常、blockHandler管配置违规

测试地址：

http://localhost:84/consumer/fallback/1

![image-20220324161143250](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281527852.png)

http://localhost:84/consumer/fallback/4    给客户error页面，不友好

![image-20220324160515423](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281527257.png)

http://localhost:84/consumer/fallback/15645616165456

![image-20220324160709521](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281527461.png)



##### ⑥ 只配置fallback

本例sentinel无配置

```java
@RestController
@Slf4j
public class CircleBreakerController {
    public static final String SERVICE_URL = "http://nacos-payment-provider";

    @Resource
    private RestTemplate restTemplate;

    @RequestMapping("/consumer/fallback/{id}")
    @SentinelResource(value = "fallback", fallback = "handlerFallback")
    public CommonResult<Payment> fallback(@PathVariable Long id) {
        CommonResult<Payment> result = restTemplate.getForObject(SERVICE_URL + "/paymentSQL/" + id, CommonResult.class, id);

        if (id == 4) {
            throw new IllegalArgumentException("IllegalArgumentException,非法参数异常....");
        } else if (result.getData() == null) {
            throw new NullPointerException("NullPointerException,该ID没有对应记录,空指针异常");
        }

        return result;
    }

    public CommonResult handlerFallback(@PathVariable Long id, Throwable e) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(444, "兜底异常handlerFallback,exception内容  " + e.getMessage(), payment);
    }
}
```



测试：

http://localhost:84/consumer/fallback/4

![image-20220324161217507](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281527280.png)

http://localhost:84/consumer/fallback/15645616165456

![image-20220324161253947](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281527549.png)



##### ⑦ 只配置blockHandler

![image-20220324161503031](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281527607.png)

```java
@RestController
@Slf4j
public class CircleBreakerController {
    public static final String SERVICE_URL = "http://nacos-payment-provider";

    @Resource
    private RestTemplate restTemplate;

    @RequestMapping("/consumer/fallback/{id}")
//    @SentinelResource(value = "fallback", fallback = "handlerFallback")
    @SentinelResource(value = "fallback", blockHandler = "blockHandler")
    public CommonResult<Payment> fallback(@PathVariable Long id) {
        CommonResult<Payment> result = restTemplate.getForObject(SERVICE_URL + "/paymentSQL/" + id, CommonResult.class, id);

        if (id == 4) {
            throw new IllegalArgumentException("IllegalArgumentException,非法参数异常....");
        } else if (result.getData() == null) {
            throw new NullPointerException("NullPointerException,该ID没有对应记录,空指针异常");
        }

        return result;
    }

    public CommonResult handlerFallback(@PathVariable Long id, Throwable e) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(444, "兜底异常handlerFallback,exception内容  " + e.getMessage(), payment);
    }

    public CommonResult blockHandler(@PathVariable Long id, BlockException blockException) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(445, "blockHandler-sentinel限流,无此流水: blockException  " + blockException.getMessage(), payment);
    }
}
```



本例sentinel需配置：

簇点链路：

![image-20220324161928613](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281528112.png)

服务降级：

异常超过2次后，断路器打开，断电跳闸，系统被保护

![image-20220324162013617](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281528664.png)

第一次和第二次访问还是报异常：

![image-20220324162228438](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281531290.png)



第三、四次···访问：

![image-20220324162101918](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281531195.png)



时间窗口期70s过了之后：

![image-20220324162226665](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281531281.png)



##### ⑧ fallback和blockHandler都配置

![image-20220324162558106](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281531789.png)

![image-20220324162613489](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281531668.png)

```java
@RestController
@Slf4j
public class CircleBreakerController {
    public static final String SERVICE_URL = "http://nacos-payment-provider";

    @Resource
    private RestTemplate restTemplate;

    @RequestMapping("/consumer/fallback/{id}")
//    @SentinelResource(value = "fallback", fallback = "handlerFallback")
//    @SentinelResource(value = "fallback", blockHandler = "blockHandler")
    @SentinelResource(value = "fallback", fallback = "handlerFallback", blockHandler = "blockHandler")
    public CommonResult<Payment> fallback(@PathVariable Long id) {
        CommonResult<Payment> result = restTemplate.getForObject(SERVICE_URL + "/paymentSQL/" + id, CommonResult.class, id);

        if (id == 4) {
            throw new IllegalArgumentException("IllegalArgumentException,非法参数异常....");
        } else if (result.getData() == null) {
            throw new NullPointerException("NullPointerException,该ID没有对应记录,空指针异常");
        }

        return result;
    }

    public CommonResult handlerFallback(@PathVariable Long id, Throwable e) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(444, "fallback,无此流水,exception  " + e.getMessage(), payment);
    }

    public CommonResult blockHandler(@PathVariable Long id, BlockException blockException) {
        Payment payment = new Payment(id, "null");
        return new CommonResult<>(445, "blockHandler-sentinel限流,无此流水: blockException  " + blockException.getMessage(), payment);
    }
}
```



本例sentinel需配置：

http://localhost:84/consumer/fallback/4

![image-20220324162817089](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281531749.png)

第一、二次访问：

![image-20220324162739258](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281531602.png)

第三、四次访问【时间窗口期结束前】：

![image-20220324162905995](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281531593.png)

结论：若 blockHandler 和 fallback 都进行了配置，则被限流降级而抛出 BlockException 时只会进入 blockHandler 处理逻辑

##### ⑨ 忽略属性

```java
@SentinelResource(value = "fallback", fallback = "handlerFallback", blockHandler = "blockHandler", exceptionsToIgnore = {IllegalArgumentException.class})
```

![image-20220324163249295](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281552730.png)

本例sentinel无配置



测试：http://localhost:84/consumer/fallback/4

程序异常打到前台了，对用户不友好

![image-20220324163403563](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281531123.png)



#### （3）Feign系列

修改84模块

84消费者调用提供者9003，Feign组件一般是消费侧



##### ① 修改 pom.xml

新增：

```xml
<!--SpringCloud openfeign -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>cloudalibaba-consumer-nacos-order84</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <!--SpringCloud ailibaba nacos -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--SpringCloud ailibaba sentinel -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
        </dependency>
        <!--SpringCloud openfeign -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
        <!-- 引入自己定义的api通用包，可以使用Payment支付Entity -->
        <dependency>
            <groupId>com.atguigu.springcloud</groupId>
            <artifactId>cloud-api-commons</artifactId>
            <version>${project.version}</version>
        </dependency>
        <!-- SpringBoot整合Web组件 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--日常通用jar包配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <scope>runtime</scope>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```



##### ② 修改 application.yml

新增激活Sentinel对Feign的支持

```yaml
management:
  endpoints:
    web:
      exposure:
        include: '*'
# 激活Sentinel对Feign的支持
feign:
  sentinel:
    enabled: true
```

```yaml
server:
  port: 84

spring:
  application:
    name: nacos-order-consumer
  cloud:
    nacos:
      discovery:
        server-addr: localhost:8848
    sentinel:
      transport:
        #配置Sentinel dashboard地址
        dashboard: localhost:8080
        #默认8719端口，假如被占用会自动从8719开始依次+1扫描,直至找到未被占用的端口
        port: 8719


#消费者将要去访问的微服务名称(注册成功进nacos的微服务提供者)
service-url:
  nacos-user-service: http://nacos-payment-provider

management:
  endpoints:
    web:
      exposure:
        include: '*'
# 激活Sentinel对Feign的支持
feign:
  sentinel:
    enabled: true
```



##### ③ 新增业务类 PaymentService

带 @FeignClient注解的业务接口：com.atguigu.springcloud.alibaba.service.PaymentService

```java
/**
 * 使用 fallback 方式是无法获取异常信息的，
 * 如果想要获取异常信息，可以使用 fallbackFactory参数
 *
 * @author: yangfan
 * @Description:
 * @create: 2022-03-24 16:42
 */
@FeignClient(value = "nacos-payment-provider", fallback = PaymentFallbackService.class)//调用中关闭9003服务提供者
public interface PaymentService {
    @GetMapping(value = "/paymentSQL/{id}")
    CommonResult<Payment> paymentSQL(@PathVariable("id") Long id);
}
```

![image-20220324170334666](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281532585.png)



##### ④ 新增业务类 PaymentFallbackService

fallback = PaymentFallbackService.class：com.atguigu.springcloud.alibaba.service.fallback.PaymentFallbackService

```java
@Component
public class PaymentFallbackService implements PaymentService {
    @Override
    public CommonResult<Payment> paymentSQL(Long id) {
        return new CommonResult<>(444, "服务降级返回,没有该流水信息", new Payment(id, "errorSerial......"));
    }
}
```



##### ⑤ 修改业务类 CircleBreakerController

```java
@Resource
private PaymentService paymentService;

/**
 * OpenFeign
 *
 * @param id
 * @return
 */
@GetMapping(value = "/consumer/openfeign/{id}")
public CommonResult<Payment> paymentSQL(@PathVariable("id") Long id) {
    if (id == 4) {
        throw new RuntimeException("没有该id");
    }
    return paymentService.paymentSQL(id);
}
```



##### ⑥ 修改主启动

新增注解：

```java
@EnableFeignClients
```



##### ⑦ 测试

http://localhost:84/consumer/openfeign/1

![image-20220324170721213](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281534835.png)



测试84调用9003，此时故意关闭9003微服务提供者，看84消费侧自动降级，不会被耗死

![image-20220324170814473](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281534506.png)



#### （4）熔断框架比较

![image-20220324171043317](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281534215.png)



### 5、规则持久化

#### （1）是什么

一旦我们重启应用，sentinel规则将消失，生产环境需要将配置规则进行持久化



#### （2）怎么玩

将限流配置规则持久化进Nacos保存，只要刷新8401某个rest地址，sentinel控制台的流控规则就能看到，只要Nacos里面的配置不删除，针对8401上sentinel上的流控规则持续有效



#### （3）修改 cloudalibaba-sentinel-service8401

##### ① 修改 pom.xml

增加：

```xml
<!--SpringCloud ailibaba sentinel-datasource-nacos 后续做持久化用到-->
<dependency>
    <groupId>com.alibaba.csp</groupId>
    <artifactId>sentinel-datasource-nacos</artifactId>
</dependency>
```



##### ② 修改application.yml

增加：添加Nacos数据源配置

```yaml
#添加Nacos数据源配置
datasource:
  ds1:
    nacos:
      server-addr: localhost:8848
      dataId: cloudalibaba-sentinel-service
      groupId: DEFAULT_GROUP
      data-type: json
      rule-type: flow
```

```yaml
server:
  port: 8401

spring:
  application:
    name: cloudalibaba-sentinel-service
  cloud:
    nacos:
      discovery:
        #Nacos服务注册中心地址
        server-addr: localhost:8848
    sentinel:
      transport:
        #配置Sentinel dashboard地址
        dashboard: localhost:8080
        #默认8719端口，假如被占用会自动从8719开始依次+1扫描,直至找到未被占用的端口
        port: 8719
#      web-context-unify: false # 关闭context整合
      #添加Nacos数据源配置
      datasource:
        ds1:
          nacos:
            server-addr: localhost:8848
            dataId: cloudalibaba-sentinel-service
            groupId: DEFAULT_GROUP
            data-type: json
            rule-type: flow

management:
  endpoints:
    web:
      exposure:
        include: '*'
```



##### ③ 添加Nacos业务规则配置

Data ID：cloudalibaba-sentinel-service

Group：DEFAULT_GROUP

配置内容：

```json
[
    {
        "resource": "/rateLimit/byUrl",
        "limitApp": "default",
        "grade": 1,
        "count": 1,
        "strategy": 0,
        "controlBehavior": 0,
        "clusterMode": false
    }
]
```

内容解析：

- resource：资源名称；
- limitApp：来源应用；
- grade：阈值类型，0表示线程数，1表示QPS；
- count：单机阈值；
- strategy：流控模式，0表示直接，1表示关联，2表示链路；
- controlBehavior：流控效果，0表示快速失败，1表示Warm Up，2表示排队等待；
- clusterMode：是否集群；

![image-20220324173650508](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281534333.png)



启动8401后刷新sentinel发现业务规则有了

![image-20220324180206322](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281534430.png)

![image-20220324180227026](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281534708.png)



快速访问测试接口：http://localhost:8401/rateLimit/byUrl

![image-20220324180425006](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281534791.png)



停止8401再看sentinel，流控效果没有了

![image-20220324180526777](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281534994.png)



乍一看还是没有，稍等一会儿，重新启动8401再看sentinel

多次调用：http://localhost:8401/rateLimit/byUrl

重新配置出现了，持久化验证通过

![image-20220324180955416](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281535159.png)

![image-20220324181003135](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281535652.png)



# 十七、SpringCloud Alibaba Seata处理分布式事务

## （一）分布式事务问题

分布式前：单机单库没这个问题

分布式后：单体应用被拆分成微服务应用，原来的三个模块被拆分成三个独立的应用，分别使用三个独立的数据源，业务操作需要调用三个服务来完成。此时每个服务内部的数据一致性由本地事务来保证，但是全局的数据一致性问题没法保证

![image-20220324181213142](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281535645.png)

一句话：一次业务操作需要跨多个数据源或需要跨多个系统进行远程调用，就会产生分布式事务问题



## （二）Seata简介

### 1、是什么

Seata是一款开源的分布式事务解决方案，致力于在微服务架构下提供高性能和简单易用的分布式事务服务

官网地址：http://seata.io/zh-cn/



### 2、能干嘛

一个典型的分布式事务过程：

分布式事务处理过程的一ID+三组件模型

- Transaction ID XID：全局唯一的事务ID
- 3组件概念
  - Transaction Coordinator (TC)：事务协调器，维护全局事务的运行状态，负责协调并驱动全局事务的提交或回滚；
  - Transaction Manager (TM)：控制全局事务的边界，负责开启一个全局事务，并最终发起全局提交或全局回滚的决议；
  - Resource Manager (RM)：控制分支事务，负责分支注册、状态汇报，并接收事务协调器的指令，驱动分支（本地）事务的提交和回滚
    
    

处理过程：

- TM 向 TC 申请开启一个全局事务，全局事务创建成功并生成一个全局唯一的 XID；
- XID 在微服务调用链路的上下文中传播；
- RM 向 TC 注册分支事务，将其纳入 XID 对应全局事务的管辖；
- TM 向 TC 发起针对 XID 的全局提交或回滚决议；
- TC 调度 XID 下管辖的全部分支事务完成提交或回滚请求。

![image-20220324182141818](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281535793.png)



### 3、去哪下

发布说明：https://github.com/seata/seata/releases



### 4、怎么玩

- 本地：@Transactional
- 全局：@GlobalTransactional

SEATA 的分布式交易解决方案：

![image-20220324182410044](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281535257.png)



## （三）Seata-Server安装

### 1、官网地址

http://seata.io/zh-cn/



### 2、下载版本

https://github.com/seata/seata/releases

下载的是 seata-server-0.9.0.zip，本次截止2020.2月份后续是否升级自己决定



### 3、解压、修改 file.conf 配置文件

seata-server-0.9.0.zip 解压到指定目录并修改 conf 目录下的 file.conf 配置文件

先备份原始 file.conf 文件

主要修改：自定义事务组名称+事务日志存储模式为db+数据库连接信息

file.conf：

service模块：

红色标记为修改的

![image-20220324183945119](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281535595.png)



store模块：

![image-20220324184135492](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281536898.png)



### 4、mysql5.7数据库新建库seata

建表db_store.sql在\seata-server-0.9.0\seata\conf目录里面

![image-20220324184237966](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281536695.png)

![image-20220324184428268](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281536617.png)

### 5、修改 registry.conf 配置文件

修改seata-server-0.9.0\seata\conf目录下的registry.conf配置文件

目的是：指明注册中心为nacos，及修改nacos连接信息

![image-20220324184638394](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281536794.png)



### 6、启动测试

先启动Nacos端口号8848：softs\nacos-server-1.1.4\nacos\bin

```shell
startup.cmd -m standalone
```



再启动seata-server

![image-20220324184841356](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281536725.png)



## （四）订单/库存/账户业务数据库准备

以下演示都需要先启动Nacos后启动Seata，保证两个都OK

Seata没启动报错no available server to connect

### 1、分布式事务业务说明

这里我们会创建三个服务，一个订单服务，一个库存服务，一个账户服务

当用户下单时，会在订单服务中创建一个订单，然后通过远程调用库存服务来扣减下单商品的库存，再通过远程调用账户服务来扣减用户账户里面的余额，最后在订单服务中修改订单状态为已完成。

该操作跨越三个数据库，有两次远程调用，很明显会有分布式事务问题



下订单--->扣库存--->减账户(余额)



### 2、创建业务数据库和表

- seata_order：存储订单的数据库
- seata_storage：存储库存的数据库
- seata_account：存储账户信息的数据库

seata_order：

```mysql
CREATE DATABASE seata_order;
USE seata_order;
CREATE TABLE t_order(
    id BIGINT(11) NOT NULL AUTO_INCREMENT PRIMARY KEY ,
    user_id BIGINT(11) DEFAULT NULL COMMENT '用户id',
    product_id BIGINT(11) DEFAULT NULL COMMENT '产品id',
    count INT(11) DEFAULT NULL COMMENT '数量',
    money DECIMAL(11,0) DEFAULT NULL COMMENT '金额',
    status INT(1) DEFAULT NULL COMMENT '订单状态：0创建中，1已完结'
)ENGINE=InnoDB AUTO_INCREMENT=7 CHARSET=utf8;
```

seata_storage：

```mysql
CREATE DATABASE seata_storage;
USE seata_storage;
CREATE TABLE t_storage(
    id BIGINT(11) NOT NULL AUTO_INCREMENT PRIMARY KEY ,
    product_id BIGINT(11) DEFAULT NULL COMMENT '产品id',
    total INT(11) DEFAULT NULL COMMENT '总库存',
    used INT(11) DEFAULT NULL COMMENT '已用库存',
    residue INT(11) DEFAULT NULL COMMENT '剩余库存'
)ENGINE=InnoDB AUTO_INCREMENT=7 CHARSET=utf8;
INSERT INTO t_storage(id, product_id, total, used, residue) VALUES(1,1,100,0,100);
```

seata_account：

```mysql
CREATE DATABASE seata_account;
USE seata_account;
CREATE TABLE t_account(
    id BIGINT(11) NOT NULL AUTO_INCREMENT PRIMARY KEY ,
    user_id BIGINT(11) DEFAULT NULL COMMENT '用户id',
    total DECIMAL(10,0) DEFAULT NULL COMMENT '总额度',
    used DECIMAL(10,0) DEFAULT NULL COMMENT '已用额度',
    residue DECIMAL(10,0) DEFAULT 0 COMMENT '剩余可用额度'
)ENGINE=InnoDB AUTO_INCREMENT=7 CHARSET=utf8;
INSERT INTO t_account(id, user_id, total, used, residue) VALUES(1,1,1000,0,1000);
```

![image-20220324190054210](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281536504.png)



### 3、按照上述3库分别建对应的回滚日志表

订单-库存-账户3个库下都需要建各自的回滚日志表：\seata-server-0.9.0\seata\conf目录下的db_undo_log.sql

![image-20220324190340092](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281536391.png)

```mysql
-- the table to store seata xid data
-- 0.7.0+ add context
-- you must to init this sql for you business databese. the seata server not need it.
-- 此脚本必须初始化在你当前的业务数据库中，用于AT 模式XID记录。与server端无关（注：业务数据库）
-- 注意此处0.3.0+ 增加唯一索引 ux_undo_log
drop table `undo_log`;
CREATE TABLE `undo_log` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `branch_id` bigint(20) NOT NULL,
  `xid` varchar(100) NOT NULL,
  `context` varchar(128) NOT NULL,
  `rollback_info` longblob NOT NULL,
  `log_status` int(11) NOT NULL,
  `log_created` datetime NOT NULL,
  `log_modified` datetime NOT NULL,
  `ext` varchar(100) DEFAULT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `ux_undo_log` (`xid`,`branch_id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
```



最终效果：

![image-20220324190903696](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281536842.png)



## （五）订单/库存/账户业务微服务准备

业务需求：下订单->减库存->扣余额->改(订单)状态

### 1、新建订单 seata-order-service2001

#### （1）pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>seata-order-service2001</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>
    <dependencies>
        <!--nacos-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--seata-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
            <exclusions>
                <exclusion>
                    <artifactId>seata-all</artifactId>
                    <groupId>io.seata</groupId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>io.seata</groupId>
            <artifactId>seata-all</artifactId>
            <version>0.9.0</version>
        </dependency>
        <!--feign-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
        <!--web-actuator-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!--mysql-druid-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.37</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.0.0</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
    </dependencies>
</project>
```



#### （2）application.yml

```yaml
server:
  port: 2001

spring:
  application:
    name: seata-order-service
  cloud:
    alibaba:
      seata:
        #自定义事务组名称需要与seata-server中的对应
        tx-service-group: fsp_tx_group
    nacos:
      discovery:
        server-addr: localhost:8848
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/seata_order
    username: root
    password: root

feign:
  hystrix:
    enabled: false

logging:
  level:
    io:
      seata: info

mybatis:
  mapperLocations: classpath:mapper/*.xml
```



#### （3）file.conf

拷贝过来后修改 file.conf

原来的：

![image-20220325123055933](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281536641.png)



修改后：

```shell
service {

  vgroup_mapping.fsp_tx_group = "default" #修改自定义事务组名称

  default.grouplist = "127.0.0.1:8091"
  enableDegrade = false
  disable = false
  max.commit.retry.timeout = "-1"
  max.rollback.retry.timeout = "-1"
  disableGlobalTransaction = false
}
```

![image-20220325123202982](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281536574.png)



#### （4）registry.conf

把 registry.conf 拷贝到 resources 目录下

![image-20220324191802325](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281536296.png)



#### （5）domain

CommonResult：com.atguigu.springcloud.alibaba.domain.CommonResult

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class CommonResult<T> {
    private Integer code;
    private String message;
    private T data;

    public CommonResult(Integer code, String message) {
        this(code, message, null);
    }
}
```



Order：com.atguigu.springcloud.alibaba.domain.Order

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Order {
    private Long id;

    private Long userId;

    private Long productId;

    private Integer count;

    private BigDecimal money;

    /**
     * 订单状态：0：创建中；1：已完结
     */
    private Integer status;
}
```



#### （6）Dao接口及实现

OrderDao：com.atguigu.springcloud.alibaba.dao.OrderDao

```java
@Mapper
public interface OrderDao {

    /**
     * 创建订单
     *
     * @param order
     */
    void create(Order order);

    /**
     * 修改订单金额
     *
     * @param userId
     * @param status
     */
    void update(@Param("userId") Long userId, @Param("status") Integer status);
}
```



resources文件夹下新建mapper文件夹后添加：OrderDao.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >

<mapper namespace="com.atguigu.springcloud.alibaba.dao.OrderDao">

    <resultMap id="BaseResultMap" type="com.atguigu.springcloud.alibaba.domain.Order">
        <id column="id" property="id" jdbcType="BIGINT"/>
        <result column="user_id" property="userId" jdbcType="BIGINT"/>
        <result column="product_id" property="productId" jdbcType="BIGINT"/>
        <result column="count" property="count" jdbcType="INTEGER"/>
        <result column="money" property="money" jdbcType="DECIMAL"/>
        <result column="status" property="status" jdbcType="INTEGER"/>
    </resultMap>

    <insert id="create">
        INSERT INTO `t_order` (`id`, `user_id`, `product_id`, `count`, `money`, `status`)
        VALUES (NULL, #{userId}, #{productId}, #{count}, #{money}, 0);
    </insert>

    <update id="update">
        UPDATE `t_order`
        SET status = 1
        WHERE user_id = #{userId}
          AND status = #{status};
    </update>
</mapper>
```



#### （7）Service接口及实现

OrderService：com.atguigu.springcloud.alibaba.service.OrderService

```java
public interface OrderService {
    void create(Order order);
}
```



OrderServiceImpl：com.atguigu.springcloud.alibaba.service.impl.OrderServiceImpl

```java
@Service
@Slf4j
public class OrderServiceImpl implements OrderService {
    @Resource
    private OrderDao orderDao;

    @Resource
    private StorageService storageService;

    @Resource
    private AccountService accountService;

    /**
     * 创建订单->调用库存服务扣减库存->调用账户服务扣减账户余额->修改订单状态
     * 简单说：
     * 下订单->减库存->减余额->改状态
     *
     * @param order
     */
    @Override
    @GlobalTransactional(name = "fsp-create-order", rollbackFor = Exception.class)
    public void create(Order order) {
        log.info("------->下单开始");
        //本应用创建订单
        orderDao.create(order);

        //远程调用库存服务扣减库存
        log.info("------->order-service中扣减库存开始");
        storageService.decrease(order.getProductId(), order.getCount());
        log.info("------->order-service中扣减库存结束");

        //远程调用账户服务扣减余额
        log.info("------->order-service中扣减余额开始");
        accountService.decrease(order.getUserId(), order.getMoney());
        log.info("------->order-service中扣减余额结束");

        //修改订单状态为已完成
        log.info("------->order-service中修改订单状态开始");
        orderDao.update(order.getUserId(), 0);
        log.info("------->order-service中修改订单状态结束");

        log.info("------->下单结束");
    }
}
```



StorageService：com.atguigu.springcloud.alibaba.service.StorageService

```java
@FeignClient(value = "seata-storage-service")
public interface StorageService {

    /**
     * 扣减库存
     *
     * @param productId
     * @param count
     * @return
     */
    @PostMapping(value = "/storage/decrease")
    CommonResult decrease(@RequestParam("productId") Long productId, @RequestParam("count") Integer count);
}
```



AccountService：com.atguigu.springcloud.alibaba.service.AccountService

```java
@FeignClient(value = "seata-account-service")
public interface AccountService {

    /**
     * 扣减账户余额
     *
     * @param userId
     * @param money
     * @return
     */
    //@RequestMapping(value = "/account/decrease", method = RequestMethod.POST, produces = "application/json; charset=UTF-8")
    @PostMapping("/account/decrease")
    CommonResult decrease(@RequestParam("userId") Long userId, @RequestParam("money") BigDecimal money);
}
```



#### （8）Controller

OrderController：com.atguigu.springcloud.alibaba.controller.OrderController

```java
@RestController
public class OrderController {

    @Autowired
    private OrderService orderService;

    /**
     * 创建订单
     *
     * @param order
     * @return
     */
    @GetMapping("/order/create")
    public CommonResult create(Order order) {
        orderService.create(order);
        return new CommonResult(200, "订单创建成功!");
    }
}
```



#### （9）Config 配置

MyBatisConfig：com.atguigu.springcloud.alibaba.config.MyBatisConfig

```java
@Configuration
@MapperScan({"com.atguigu.springcloud.alibaba.dao"})
public class MyBatisConfig {
}
```



DataSourceProxyConfig：com.atguigu.springcloud.alibaba.config.DataSourceProxyConfig

```java
package com.atguigu.springcloud.alibaba.config;

import com.alibaba.druid.pool.DruidDataSource;
import io.seata.rm.datasource.DataSourceProxy;
import org.apache.ibatis.session.SqlSessionFactory;
import org.mybatis.spring.SqlSessionFactoryBean;
import org.mybatis.spring.transaction.SpringManagedTransactionFactory;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.io.support.PathMatchingResourcePatternResolver;

import javax.sql.DataSource;

/**
 * 使用Seata对数据源进行代理
 *
 * @author: yangfan
 * @Description:
 * @create: 2022-03-24 19:53
 */
@Configuration
public class DataSourceProxyConfig {

    @Value("${mybatis.mapperLocations}")
    private String mapperLocations;

    @Bean
    @ConfigurationProperties(prefix = "spring.datasource")
    public DataSource druidDataSource() {
        return new DruidDataSource();
    }

    @Bean
    public DataSourceProxy dataSourceProxy(DataSource dataSource) {
        return new DataSourceProxy(dataSource);
    }

    @Bean
    public SqlSessionFactory sqlSessionFactoryBean(DataSourceProxy dataSourceProxy) throws Exception {
        SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
        sqlSessionFactoryBean.setDataSource(dataSourceProxy);
        sqlSessionFactoryBean.setMapperLocations(new PathMatchingResourcePatternResolver().getResources(mapperLocations));
        sqlSessionFactoryBean.setTransactionFactory(new SpringManagedTransactionFactory());
        return sqlSessionFactoryBean.getObject();
    }
}
```



#### （10）主启动

SeataOrderMainApp2001：com.atguigu.springcloud.alibaba.SeataOrderMainApp2001

```java
@EnableDiscoveryClient
@EnableFeignClients
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)//取消数据源的自动创建
public class SeataOrderMainApp2001 {

    public static void main(String[] args) {
        SpringApplication.run(SeataOrderMainApp2001.class, args);
    }
}
```



### 2、新建库存 seata-storage-service2002

#### （1）pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>seata-storage-service2002</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>
    <dependencies>
        <!--nacos-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--seata-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
            <exclusions>
                <exclusion>
                    <artifactId>seata-all</artifactId>
                    <groupId>io.seata</groupId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>io.seata</groupId>
            <artifactId>seata-all</artifactId>
            <version>0.9.0</version>
        </dependency>
        <!--feign-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.0.0</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.37</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
    </dependencies>
</project>
```



#### （2）application.yml

```yaml
server:
  port: 2002

spring:
  application:
    name: seata-storage-service
  cloud:
    alibaba:
      seata:
        tx-service-group: fsp_tx_group
    nacos:
      discovery:
        server-addr: localhost:8848
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/seata_storage
    username: root
    password: root

logging:
  level:
    io:
      seata: info

mybatis:
  mapperLocations: classpath:mapper/*.xml
```



#### （3）file.conf

拷贝过来后修改 file.conf

原来的：

![image-20220325123055933](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281537554.png)



修改后：

```shell
service {

  vgroup_mapping.fsp_tx_group = "default" #修改自定义事务组名称

  default.grouplist = "127.0.0.1:8091"
  enableDegrade = false
  disable = false
  max.commit.retry.timeout = "-1"
  max.rollback.retry.timeout = "-1"
  disableGlobalTransaction = false
}
```

![image-20220325123202982](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281537903.png)



#### （4）registry.conf

把 registry.conf 拷贝到 resources 目录下

![image-20220324191802325](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281537032.png)



#### （5）domain

CommonResult：com.atguigu.springcloud.alibaba.domain.CommonResult

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class CommonResult<T> {
    private Integer code;
    private String message;
    private T data;

    public CommonResult(Integer code, String message) {
        this(code, message, null);
    }
}
```



Storage：com.atguigu.springcloud.alibaba.domain.Storage

```java
@Data
public class Storage {

    private Long id;

    /**
     * 产品id
     */
    private Long productId;

    /**
     * 总库存
     */
    private Integer total;

    /**
     * 已用库存
     */
    private Integer used;

    /**
     * 剩余库存
     */
    private Integer residue;
}
```



#### （6）Dao接口及实现

StorageDao：com.atguigu.springcloud.alibaba.dao.StorageDao

```java
@Mapper
public interface StorageDao {

    /**
     * 扣减库存
     */
    void decrease(@Param("productId") Long productId, @Param("count") Integer count);
}
```



resources文件夹下新建mapper文件夹后添加：StorageDao.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="com.atguigu.springcloud.alibaba.dao.StorageDao">

    <resultMap id="BaseResultMap" type="com.atguigu.springcloud.alibaba.domain.Storage">
        <id column="id" property="id" jdbcType="BIGINT"/>
        <result column="product_id" property="productId" jdbcType="BIGINT"/>
        <result column="total" property="total" jdbcType="INTEGER"/>
        <result column="used" property="used" jdbcType="INTEGER"/>
        <result column="residue" property="residue" jdbcType="INTEGER"/>
    </resultMap>

    <update id="decrease">
        UPDATE t_storage
        SET used    = used + #{count},
            residue = residue - #{count}
        WHERE product_id = #{productId}
    </update>

</mapper>
```



#### （7）Service接口及实现

StorageService：com.atguigu.springcloud.alibaba.service.StorageService

```java
public interface StorageService {
    /**
     * 扣减库存
     */
    void decrease(Long productId, Integer count);
}
```



StorageServiceImpl：com.atguigu.springcloud.alibaba.service.impl.StorageServiceImpl

```java
@Service
public class StorageServiceImpl implements StorageService {

    private static final Logger LOGGER = LoggerFactory.getLogger(StorageServiceImpl.class);

    @Resource
    private StorageDao storageDao;

    /**
     * 扣减库存
     */
    @Override
    public void decrease(Long productId, Integer count) {
        LOGGER.info("------->storage-service中扣减库存开始");
        storageDao.decrease(productId, count);
        LOGGER.info("------->storage-service中扣减库存结束");
    }
}
```



#### （8）Controller

StorageController：com.atguigu.springcloud.alibaba.controller.StorageController

```java
@RestController
public class StorageController {

    @Autowired
    private StorageService storageService;

    /**
     * 扣减库存
     */
    @RequestMapping("/storage/decrease")
    public CommonResult decrease(Long productId, Integer count) {
        storageService.decrease(productId, count);
        return new CommonResult(200, "扣减库存成功！");
    }
}
```



#### （9）Config 配置

MyBatisConfig：com.atguigu.springcloud.alibaba.config.MyBatisConfig

```java
@Configuration
@MapperScan({"com.atguigu.springcloud.alibaba.dao"})
public class MyBatisConfig {
}
```



DataSourceProxyConfig：com.atguigu.springcloud.alibaba.config.DataSourceProxyConfig

```java
package com.atguigu.springcloud.alibaba.config;

import com.alibaba.druid.pool.DruidDataSource;
import io.seata.rm.datasource.DataSourceProxy;
import org.apache.ibatis.session.SqlSessionFactory;
import org.mybatis.spring.SqlSessionFactoryBean;
import org.mybatis.spring.transaction.SpringManagedTransactionFactory;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.io.support.PathMatchingResourcePatternResolver;

import javax.sql.DataSource;

/**
 * 使用Seata对数据源进行代理
 *
 * @author: yangfan
 * @Description:
 * @create: 2022-03-24 19:53
 */
@Configuration
public class DataSourceProxyConfig {

    @Value("${mybatis.mapperLocations}")
    private String mapperLocations;

    @Bean
    @ConfigurationProperties(prefix = "spring.datasource")
    public DataSource druidDataSource(){
        return new DruidDataSource();
    }

    @Bean
    public DataSourceProxy dataSourceProxy(DataSource dataSource) {
        return new DataSourceProxy(dataSource);
    }

    @Bean
    public SqlSessionFactory sqlSessionFactoryBean(DataSourceProxy dataSourceProxy) throws Exception {
        SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
        sqlSessionFactoryBean.setDataSource(dataSourceProxy);
        sqlSessionFactoryBean.setMapperLocations(new PathMatchingResourcePatternResolver().getResources(mapperLocations));
        sqlSessionFactoryBean.setTransactionFactory(new SpringManagedTransactionFactory());
        return sqlSessionFactoryBean.getObject();
    }
}
```



#### （10）主启动

SeataStorageServiceApplication2002：com.atguigu.springcloud.alibaba.SeataStorageServiceApplication2002

```java
@EnableDiscoveryClient
@EnableFeignClients
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)//取消数据源的自动创建
public class SeataStorageServiceApplication2002 {

    public static void main(String[] args) {
        SpringApplication.run(SeataStorageServiceApplication2002.class, args);
    }
}
```



### 3、新建账户 seata-account-service2003

#### （1）pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>mscloud</artifactId>
        <groupId>com.atguigu.springcloud</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>seata-account-service2003</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>
    <dependencies>
        <!--nacos-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
        </dependency>
        <!--seata-->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
            <exclusions>
                <exclusion>
                    <artifactId>seata-all</artifactId>
                    <groupId>io.seata</groupId>
                </exclusion>
            </exclusions>
        </dependency>
        <dependency>
            <groupId>io.seata</groupId>
            <artifactId>seata-all</artifactId>
            <version>0.9.0</version>
        </dependency>
        <!--feign-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.0.0</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.37</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.10</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
    </dependencies>
</project>
```



#### （2）application.yml

```yaml
server:
  port: 2003

spring:
  application:
    name: seata-account-service
  cloud:
    alibaba:
      seata:
        tx-service-group: fsp_tx_group
    nacos:
      discovery:
        server-addr: localhost:8848
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/seata_account
    username: root
    password: root

feign:
  hystrix:
    enabled: false

logging:
  level:
    io:
      seata: info

mybatis:
  mapperLocations: classpath:mapper/*.xml
```



#### （3）file.conf

拷贝过来后修改 file.conf

原来的：

![image-20220325123055933](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281537791.png)



修改后：

```shell
service {

  vgroup_mapping.fsp_tx_group = "default" #修改自定义事务组名称

  default.grouplist = "127.0.0.1:8091"
  enableDegrade = false
  disable = false
  max.commit.retry.timeout = "-1"
  max.rollback.retry.timeout = "-1"
  disableGlobalTransaction = false
}
```

![image-20220325123202982](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281537011.png)



#### （4）registry.conf

把 registry.conf 拷贝到 resources 目录下

![image-20220324191802325](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281537506.png)



#### （5）domain

CommonResult：com.atguigu.springcloud.alibaba.domain.CommonResult

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class CommonResult<T> {
    private Integer code;
    private String message;
    private T data;

    public CommonResult(Integer code, String message) {
        this(code, message, null);
    }
}
```



Account：com.atguigu.springcloud.alibaba.domain.Account

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Account {

    private Long id;

    /**
     * 用户id
     */
    private Long userId;

    /**
     * 总额度
     */
    private BigDecimal total;

    /**
     * 已用额度
     */
    private BigDecimal used;

    /**
     * 剩余额度
     */
    private BigDecimal residue;
}
```



#### （6）Dao接口及实现

AccountDao：com.atguigu.springcloud.alibaba.dao.AccountDao

```java
@Mapper
public interface AccountDao {

    /**
     * 扣减账户余额
     */
    void decrease(@Param("userId") Long userId, @Param("money") BigDecimal money);
}
```



resources文件夹下新建mapper文件夹后添加：AccountMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<mapper namespace="com.atguigu.springcloud.alibaba.dao.StorageDao">

    <resultMap id="BaseResultMap" type="com.atguigu.springcloud.alibaba.domain.Storage">
        <id column="id" property="id" jdbcType="BIGINT"/>
        <result column="product_id" property="productId" jdbcType="BIGINT"/>
        <result column="total" property="total" jdbcType="INTEGER"/>
        <result column="used" property="used" jdbcType="INTEGER"/>
        <result column="residue" property="residue" jdbcType="INTEGER"/>
    </resultMap>

    <update id="decrease">
        UPDATE t_storage
        SET used    = used + #{count},
            residue = residue - #{count}
        WHERE product_id = #{productId}
    </update>

</mapper>
```



#### （7）Service接口及实现

AccountService：com.atguigu.springcloud.alibaba.service.AccountService

```java
public interface StorageService {
    /**
     * 扣减库存
     */
    void decrease(Long productId, Integer count);
}
```



AccountServiceImpl：com.atguigu.springcloud.alibaba.service.impl.AccountServiceImpl

```java
/**
 * 账户业务实现类
 *
 * @author: yangfan
 * @Description:
 * @create: 2022-03-24 20:35
 */
@Service
public class AccountServiceImpl implements AccountService {

    private static final Logger LOGGER = LoggerFactory.getLogger(AccountServiceImpl.class);


    @Resource
    AccountDao accountDao;

    /**
     * 扣减账户余额
     */
    @Override
    public void decrease(Long userId, BigDecimal money) {
        LOGGER.info("------->account-service中扣减账户余额开始");
        //模拟超时异常，全局事务回滚
        //暂停几秒钟线程
        //try { TimeUnit.SECONDS.sleep(30); } catch (InterruptedException e) { e.printStackTrace(); }
        accountDao.decrease(userId, money);
        LOGGER.info("------->account-service中扣减账户余额结束");
    }
}
```



#### （8）Controller

AccountController：com.atguigu.springcloud.alibaba.controller.AccountController

```java
@RestController
public class StorageController {

    @Autowired
    private StorageService storageService;

    /**
     * 扣减库存
     */
    @RequestMapping("/storage/decrease")
    public CommonResult decrease(Long productId, Integer count) {
        storageService.decrease(productId, count);
        return new CommonResult(200, "扣减库存成功！");
    }
}
```



#### （9）Config 配置

MyBatisConfig：com.atguigu.springcloud.alibaba.config.MyBatisConfig

```java
@Configuration
@MapperScan({"com.atguigu.springcloud.alibaba.dao"})
public class MyBatisConfig {
}
```



DataSourceProxyConfig：com.atguigu.springcloud.alibaba.config.DataSourceProxyConfig

```java
package com.atguigu.springcloud.alibaba.config;

import com.alibaba.druid.pool.DruidDataSource;
import io.seata.rm.datasource.DataSourceProxy;
import org.apache.ibatis.session.SqlSessionFactory;
import org.mybatis.spring.SqlSessionFactoryBean;
import org.mybatis.spring.transaction.SpringManagedTransactionFactory;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.io.support.PathMatchingResourcePatternResolver;

import javax.sql.DataSource;

/**
 * 使用Seata对数据源进行代理
 *
 * @author: yangfan
 * @Description:
 * @create: 2022-03-24 19:53
 */
@Configuration
public class DataSourceProxyConfig {

    @Value("${mybatis.mapperLocations}")
    private String mapperLocations;

    @Bean
    @ConfigurationProperties(prefix = "spring.datasource")
    public DataSource druidDataSource(){
        return new DruidDataSource();
    }

    @Bean
    public DataSourceProxy dataSourceProxy(DataSource dataSource) {
        return new DataSourceProxy(dataSource);
    }

    @Bean
    public SqlSessionFactory sqlSessionFactoryBean(DataSourceProxy dataSourceProxy) throws Exception {
        SqlSessionFactoryBean sqlSessionFactoryBean = new SqlSessionFactoryBean();
        sqlSessionFactoryBean.setDataSource(dataSourceProxy);
        sqlSessionFactoryBean.setMapperLocations(new PathMatchingResourcePatternResolver().getResources(mapperLocations));
        sqlSessionFactoryBean.setTransactionFactory(new SpringManagedTransactionFactory());
        return sqlSessionFactoryBean.getObject();
    }
}
```



#### （10）主启动

SeataAccountMainApp2003：com.atguigu.springcloud.alibaba.SeataAccountMainApp2003

```java
@EnableDiscoveryClient
@EnableFeignClients
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)//取消数据源的自动创建
public class SeataAccountMainApp2003 {

    public static void main(String[] args) {
        SpringApplication.run(SeataAccountMainApp2003.class, args);
    }
}
```



### 4、测试

下订单->减库存->扣余额->改(订单)状态

![image-20220324203834942](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281539430.png)



数据库初始情况：

t_order：

![image-20220325102443504](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281537891.png)



t_storage：

![image-20220325102508859](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281537829.png)



t_account：

![image-20220325102638271](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281537699.png)



#### （1）正常下单

http://localhost:2001/order/create?userId=1&productId=1&count=10&money=100

![image-20220325114525357](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281537656.png)



![image-20220325114551202](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281553317.png)



#### （2）超时异常，没加@GlobalTransactional

AccountServiceImpl添加超时

![image-20220325143147545](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281538343.png)

超时异常，没加@GlobalTransactional

![image-20220325143806884](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281538485.png)



数据库情况：

当库存和账户金额扣减后，订单状态并没有设置为已经完成，没有从零改为1，而且由于feign的重试机制，账户余额还有可能被多次扣减



t_order：

![image-20220325145212097](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281553814.png)



t_storage：

![image-20220325145251456](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281538633.png)



t_account：

![image-20220325145315549](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281550111.png)



#### （3）超时异常，添加@GlobalTransactional

AccountServiceImpl添加超时：

![image-20220325143147545](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281550604.png)



超时异常，加了@GlobalTransactional

![image-20220325145448391](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281550101.png)



下单后数据库数据并没有任何改变，记录都添加不进来

![image-20220325150054008](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281550898.png)



### 5、一部分补充

Seata：Simple Extensible Autonomous Transaction Architecture，简单可扩展自治事务框架

2019年1月份蚂蚁金服和阿里巴巴共同开源的分布式事务解决方案，2020起始，参加工作后用1.0以后的版本



再看TC/TM/RM三大组件：

![image-20220325151125333](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281550163.png)



#### （1）分布式事务的执行流程

- TM 开启分布式事务（TM 向 TC 注册全局事务记录）；
- 按业务场景，编排数据库、服务等事务内资源（RM 向 TC 汇报资源准备状态 ）；
- TM 结束分布式事务，事务一阶段结束（TM 通知 TC 提交/回滚分布式事务）；
- TC 汇总事务信息，决定分布式事务是提交还是回滚；
- TC 通知所有 RM 提交/回滚 资源，事务二阶段结束。
  
  

#### （2）AT模式如何做到对业务的无侵入

##### ① 是什么

![image-20220325151333736](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281550280.png)



##### ② 一阶段加载

在一阶段，Seata 会拦截“业务 SQL”

- 解析 SQL 语义，找到“业务 SQL”要更新的业务数据，在业务数据被更新前，将其保存成“before image”，
- 执行“业务 SQL”更新业务数据，在业务数据更新之后，
- 其保存成“after image”，最后生成行锁。

以上操作全部在一个数据库事务内完成，这样保证了一阶段操作的原子性。

![image-20220325151514577](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281550631.png)



##### ③ 二阶段提交

二阶段如是顺利提交的话，因为“业务 SQL”在一阶段已经提交至数据库，所以Seata框架只需将一阶段保存的快照数据和行锁删掉，完成数据清理即可

![image-20220325152015672](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281551620.png)



##### ④ 二阶段回滚

二阶段如果是回滚的话，Seata 就需要回滚一阶段已经执行的“业务 SQL”，还原业务数据。回滚方式便是用“before image”还原业务数据；但在还原前要首先要校验脏写，对比“数据库当前业务数据”和 “after image”，如果两份数据完全一致就说明没有脏写，可以还原业务数据，如果不一致就说明有脏写，出现脏写就需要转人工处理

![image-20220325152131982](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281551186.png)



![image-20220325152145713](https://yangfan-typroa.oss-cn-beijing.aliyuncs.com/202203281551981.png)
