---
title: SpringBoot基础配置
categories: Java
tags:
  - Java
  - Spring
  - SpringBoot
keywords: SpringBoot基础配置
abbrlink: f066a429
date: 2020-01-12 12:17:12
---

## 定制Banner
Spring Boot项目在启动的时候会有一个默认的启动图案：
```

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.2.2.RELEASE)
```

我们可以把这个图案修改为自己想要的。在src/main/resources目录下新建banner.txt文件，然后将自己的图案黏贴进去即可。ASCII图案可通过网站[http://www.network-science.de/ascii/](http://www.network-science.de/ascii/)一键生成，比如输入perye生成图案后复制到banner.txt，启动项目，控制台输出如下：
```
 _____      __   _ __   __  __     __
/\ '__`\  /'__`\/\`'__\/\ \/\ \  /'__`\
\ \ \L\ \/\  __/\ \ \/ \ \ \_\ \/\  __/
 \ \ ,__/\ \____\\ \_\  \/`____ \ \____\
  \ \ \/  \/____/ \/_/   `/___/> \/____/
   \ \_\                    /\___/
    \/_/                    \/__/
:: Spring Boot ::        (v2.2.2.RELEASE)
```

banner也可以关闭，在main方法中：
```java
public static void main(String[] args) {
    SpringApplication app = new SpringApplication(DemoApplication.class);
    app.setBannerMode(Banner.Mode.OFF);
    app.run(args);
}
```

## 全局配置文件
在src/main/resources目录下，Spring Boot提供了一个名为application.properties的全局配置文件，可对一些默认配置的配置值进行修改。

附:[application.properties中可配置所有官方属性](https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-application-properties.html)

### 自定义属性值
Spring Boot允许我们在application.properties下自定义一些属性，比如：
```
# 自定义属性
perye.blog.name = perye's Blog
perye.blog.title = SpringBoot
```
定义一个BlogProperties Bean，通过`@Value("${属性名}")`来加载配置文件中的属性值：
```java
import lombok.Data;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

/**
 * @author perye
 * @email peryedev@gmail.com
 * @date 2020/1/12
 */
@Data
@Component
public class BlogProperties {

    @Value("${perye.blog.name}")
    private String name;

    @Value("${perye.blog.title}")
    private String title;
}

```

编写IndexController，注入该Bean：

```java
@RestController
public class IndexController {

    @Autowired
    private BlogProperties blogProperties;

    @RequestMapping("/")
    String index() {
        return blogProperties.getName()+"——"+blogProperties.getTitle();
    }

}
```

启动项目访问http://localhost:8080
