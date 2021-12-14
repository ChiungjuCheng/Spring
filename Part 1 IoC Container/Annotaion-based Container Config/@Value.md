# 讀取properties或xml的資料
當想使用class讀取properties或yml檔案的時候可以使用@Value annotation。如下:   

application.xml
```xml
demo.name=test
```
讀取的class
```java
public class PropertiesDemoService {

	@Value(value = "${demo.name}")
	private String name1;
		
	public void printName1() {
		System.out.println(name1); // test
	}
}
```
## 1. 設定value resolver
Spring在Default的設定中，若找不到對應的value，就會直接注入當初設定value的字串，例如上述會印出${demo.name}字串。若想要在找不到value的情況下拋錯的話需要自己重新宣告一個PropertySourcesPlaceholderConfigurer Bean，但在Demo中不知道為什麼都抓不到properties的位置，都需要特別設定location，導致一定要自己定義...

* 使用xml設定PropertySourcesPlaceholderConfigurer
context schema裡頭包含property-placeholder，可以很方便的設定PropertyPlaceholderConfigurer
```xml
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">


	<context:annotation-config />
    <context:property-placeholder location="classpath:application.properties"/>

    <!-- 使用<bean>的方式 -->
	<!-- <bean
		class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
		<property name="locations"
			value="classpath:application.properties" />
	</bean> -->

</beans>
```

* 使用Annotation設定PropertySourcesPlaceholderConfigurer
1. 需要使用到@Configuration，因此必須要在xml增加coompont scan，這個步驟也可以使用@ComponentScan代替
```xml
<context:component-scan base-package="com" /> 
```
2. 設定PropertySourcesPlaceholderConfigurer Bean
```java
@Configuration
@PropertySource("classpath:application.properties")
public class PropertySourcesPlaceholderConfig {
	
	@Bean
	public static PropertySourcesPlaceholderConfigurer propertyPlaceholderConfigurer() {
		return new PropertySourcesPlaceholderConfigurer();
	}
}
```

# Spring boot
 Spring boot的default設定是application.xml或application.properties。


#### 備註
[1. Difference between context:annotation-config and context:component-scan](/https://stackoverflow.com/questions/7414794/difference-between-contextannotation-config-and-contextcomponent-scan)