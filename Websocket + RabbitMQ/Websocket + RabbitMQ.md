# Websocket + RabbitMQ

## RabbitMQ STOMP server設定和啟動
建立image，使用此資料夾下的dockerfile建立能夠傳送STOMP的image。   
Dockerfile內容
```Dockerfile
FROM rabbitmq:management
RUN rabbitmq-plugins enable rabbitmq_stomp --offline
EXPOSE 61613
```
指令
```
docker build -t rabbitmq-stop .
```
並執行以下指令:
```
docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 -p 61613:61613 rabbitmq-stop
```
### RabbitMQ server資訊能夠到以下網址查看
http://localhost:15672/
  

## Spring boot maven 設定
使用spring-rabbit
```xml
<!-- RabbitMQ -->
<dependency>
    <groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

Spring websocket若要使用外部的Messge Broker如RabbitMQ需要多放io.projectreactor.netty:reactor-netty和io.netty:netty-all，用來管理TCP connection。
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-reactor-netty</artifactId>
</dependency>
```
[參考來源1: 官網](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#websocket-stomp-handle-broker-relay)  
[參考來源2: stackoverflow](https://stackoverflow.com/questions/55762527/failed-to-start-bean-stompbrokerrelaymessagehandler-nested-exception-is-java)

## Spring boot WebSocketMessageBrokerConfigurer設定
在spring boot中，需要設定Message Broker的相關資訊:
```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

	@Override
	public void configureMessageBroker(MessageBrokerRegistry config) {
		config.setApplicationDestinationPrefixes("/app")
			.enableStompBrokerRelay("/topic", "/queue")
			.setRelayHost("localhost")
			.setRelayPort(61613)
			.setClientLogin("guest")
			.setClientPasscode("guest");
	}
	
	/**
	 * 建立連線位置
	 */
	@Override
	public void registerStompEndpoints(StompEndpointRegistry registry) {
		registry.addEndpoint("/websocket-app")
				.withSockJS();
	}

}
```
前端則能用SockJS與Websocket建立連線和傳送訊息。