# Spring boot Logging
提供Java Util Logging、Log4J2和Logback，每一種方式都已經有初始設定了。  

**Default**  
1. 若使用Starters，default會使用Logback。
2. file output - 到console
3. logging level - INFO

**Simple Logging Facade for Java (SLF4J)**  
Log API，支援許多logging框架，例如java.util.logging, logback, log4。

# 設定Logging
在application.properties中設定log
https://howtodoinjava.com/spring-boot2/logging/spring-boot-logging-configurations/

# 使用log
使用slf4j框架取得Logger
```java
import org.junit.jupiter.api.Test;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class CocalendarApplicationTests {
	
	private static final Logger LOGGER = LoggerFactory.getLogger(CocalendarApplicationTests.class);

	@Test
	void contextLoads() {
		LOGGER.info("Logging Test");
	}

}
```

# 使用@Slf4j

## Eclipse 安裝
1. 下載Lombok Jar File，隨便在一個專案放入，讓本地的maven儲存庫有Lombok Jar File
```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.22</version>
    <scope>provided</scope>
</dependency>
```

2. Installing Lombok
執行lombok-1.18.22.jar，並指定安裝路徑為eclipse.exe路徑
```
java -jar lombok-1.18.22.jar
```
  


### 使用
1. maven
```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.22</version>
    <scope>provided</scope>
</dependency>
```

2. java
```java
@Slf4j
@RestController
public class MyBatisController {
	@GetMapping("/query/{primarykey}")
	public Blog queryMybatis(@PathVariable("primarykey") int primarykey) {
		log.info("testxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx");
		return blogMapper.selectByPrimaryKey(primarykey).orElse(new com.example.mybatis.spring.model.Blog());
	}
}
```

### 參考
https://howtodoinjava.com/lombok/lombok-eclipse-installation-examples/