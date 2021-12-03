# SpringWebSocket

Запустится веб-сервер, и можно переходить по адресу http://localhost:8080 и наслаждаться работающим чатом.

## Использование брокера RabbitMQ

##### Если вы не хотите пользоваться встроенным брокером, а хотите подключить полноценный, то в зависимости Maven надо добавить:

```xml
<!-- RabbitMQ Starter Dependency -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>

<!-- Following additional dependency is required for Full Featured STOMP Broker Relay -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-reactor-netty</artifactId>
</dependency>
```

##### Далее надо включить RabbitMQ в классе конфигурации WebSocketConfig.java таким образом:

```java
public void configureMessageBroker(MessageBrokerRegistry registry) {
    registry.setApplicationDestinationPrefixes("/app");

    // Use this for enabling a Full featured broker like RabbitMQ
    registry.enableStompBrokerRelay("/topic")
            .setRelayHost("localhost")
            .setRelayPort(61613)
            .setClientLogin("guest")
            .setClientPasscode("guest");
}
```