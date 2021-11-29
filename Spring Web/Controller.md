步驟
1. 引進maven檔案
2. 設定java config: @Configuration


###2. 設定java config: @Configuration 
spring的設定檔
```java
package com.luv2code.springdemo.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
@EnableWebMvc
@ComponentScan("com.luv2code.springdemo") // 要掃描的地方
public class DemoAppConfig implements WebMvcConfigurer {

}
```
###3. 設定Dispatcher Servlate Initializer
spring本身提供一個方法，可以對Dispatcher Servlate進行初始化，這裡和spring MVC沒有甚麼分別
```java
package com.luv2code.springdemo.config;

import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;

public class MySpringMvcDispatcherServletInitializer extends AbstractAnnotationConfigDispatcherServletInitializer {

	@Override
	protected Class<?>[] getRootConfigClasses() {
		// TODO Auto-generated method stub
		return null;
	}

    // spring的設定檔
	@Override
	protected Class<?>[] getServletConfigClasses() {
		return new Class[] { DemoAppConfig.class };
	}

    // 路徑
	@Override
	protected String[] getServletMappings() {
		return new String[] { "/" };
	}

}
```

### 3. 創建REST Controller
```java
package com.luv2code.springdemo.rest;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/test")
public class DemoRestController {

	// add code for the "/hello" endpoint
	
	@GetMapping("/hello")
	public String sayHello() {
		return "Hello World!";
	}
	
}


```