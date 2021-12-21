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