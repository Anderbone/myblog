+++ 
date = "2024-01-11"
title = "Spring Start here 11 - 3 ways to consume RestAPI"
tags = ["spring"]
+++

We use 3 differnt ways to consume the payments service.

## Payments service to be consumed by 3 different clients
![](https://i.imgur.com/Xkc3PXb.png)

PaymentsController.java
```java
package com.example.controllers;

import com.example.model.Payment;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestHeader;
import org.springframework.web.bind.annotation.RestController;

import java.util.UUID;
import java.util.logging.Logger;

@RestController
public class PaymentsController {

  private static Logger logger = Logger.getLogger(PaymentsController.class.getName());

  @PostMapping("/payment")
  public ResponseEntity<Payment> createPayment(
      @RequestHeader String requestId,
      @RequestBody Payment payment
  ) {
    logger.info("Received request with ID " + requestId +
        " ;Payment Amount: " + payment.getAmount());

    payment.setId(UUID.randomUUID().toString());
    payment.setId("123");

    return ResponseEntity
        .status(HttpStatus.OK)
        .header("requestId", requestId)
        .body(payment);
  }

}

```
Payment.java
```java
package com.example.model;

public class Payment {

  private String id;
  private double amount;

  public String getId() {
    return id;
  }

  public void setId(String id) {
    this.id = id;
  }

  public double getAmount() {
    return amount;
  }

  public void setAmount(double amount) {
    this.amount = amount;
  }
}

```

## 1.Feign client

![](https://i.imgur.com/T9CfIG9.png)

ProjectConfig.java

```java
package com.example.config;

import org.springframework.cloud.openfeign.EnableFeignClients;
import org.springframework.context.annotation.Configuration;

@Configuration
@EnableFeignClients(basePackages = "com.example.proxy")
public class ProjectConfig {
}

```
PaymentsController.java
```java
package com.example.controllers;

import com.example.model.Payment;
import com.example.proxy.PaymentsProxy;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

import java.util.UUID;

@RestController
public class PaymentsController {

  private final PaymentsProxy paymentsProxy;

  public PaymentsController(PaymentsProxy paymentsProxy) {
    this.paymentsProxy = paymentsProxy;
  }

  @PostMapping("/payment")
  public Payment createPayment(
      @RequestBody Payment payment
      ) {
    String requestId = UUID.randomUUID().toString();
    return paymentsProxy.createPayment(requestId, payment);
  }
}

```

Payment.java
```java
package com.example.model;

public class Payment {

  private String id;
  private double amount;

  public String getId() {
    return id;
  }

  public void setId(String id) {
    this.id = id;
  }

  public double getAmount() {
    return amount;
  }

  public void setAmount(double amount) {
    this.amount = amount;
  }
}

```

PaymentsProxy.java
```java
package com.example.proxy;

import com.example.model.Payment;
import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestHeader;

@FeignClient(name = "payments", url = "${name.service.url}")
public interface PaymentsProxy {

  @PostMapping("/payment")
  Payment createPayment(
      @RequestHeader String requestId,
      @RequestBody Payment payment);

}

```

application.properties
```
server.port=9090

name.service.url=http://localhost:8080
```

## 2. RestTemplate
Outdated. Use 1 or 3 instead of new projects if possible.

Model Payment.java is the same as Feign, Controller is almost the same.

ProjectConfig.java
```java
package com.example.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.client.RestTemplate;

@Configuration
public class ProjectConfig {

  @Bean
  public RestTemplate restTemplate() {
    return new RestTemplate();
  }
}

```
PaymentsController.java

```java
package com.example.controllers;

import com.example.model.Payment;
import com.example.proxy.PaymentsProxy;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class PaymentsController {

  private final PaymentsProxy paymentsProxy;

  public PaymentsController(PaymentsProxy paymentsProxy) {
    this.paymentsProxy = paymentsProxy;
  }

  @PostMapping("/payment")
  public Payment createPayment(
      @RequestBody Payment payment
      ) {
    return paymentsProxy.createPayment(payment);
  }
}

```
PaymentsProxy.java
```java
package com.example.proxy;

import com.example.model.Payment;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.http.HttpEntity;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpMethod;
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Component;
import org.springframework.web.client.RestTemplate;

import java.util.UUID;

@Component
public class PaymentsProxy {

  private final RestTemplate rest;

  @Value("${name.service.url}")
  private String paymentsServiceUrl;

  public PaymentsProxy(RestTemplate rest) {
    this.rest = rest;
  }

  public Payment createPayment(Payment payment) {
    String uri = paymentsServiceUrl + "/payment";

    HttpHeaders headers = new HttpHeaders();
    headers.add("requestId", UUID.randomUUID().toString());

    HttpEntity<Payment> httpEntity = new HttpEntity<>(payment, headers);

    ResponseEntity<Payment> response =
        rest.exchange(uri,
            HttpMethod.POST,
            httpEntity,
            Payment.class);

    return response.getBody();
  }
}

```

## 3. WebClient
A reactive way. Model Payment.java is the same as above, PaymentsController.java is the same as Feign,  

ProjectConfig.java
```java
package com.example.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.reactive.function.client.WebClient;

@Configuration
public class ProjectConfig {

  @Bean
  public WebClient webClient() {
    return WebClient.builder().build();
  }
}

```

PaymentsProxy.java
```java
package com.example.proxy;

import com.example.model.Payment;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;
import org.springframework.web.reactive.function.client.WebClient;
import reactor.core.publisher.Mono;

@Component
public class PaymentsProxy {

  private final WebClient webClient;

  @Value("${name.service.url}")
  private String url;

  public PaymentsProxy(WebClient webClient) {
    this.webClient = webClient;
  }

  public Mono<Payment> createPayment(String requestId, Payment payment) {
    return webClient.post()
              .uri(url + "/payment")
              .header("requestId", requestId)
              .body(Mono.just(payment), Payment.class)
              .retrieve()
              .bodyToMono(Payment.class);
  }
}

```
