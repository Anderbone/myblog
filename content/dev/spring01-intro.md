+++ 
date = "2020-02-07"
title = "Spring In Action 01 - Intro"
tags = ["spring", "java", "spring-in-action" ]
+++

Follow the book: Spring in Action fifth version.
Code repo: [github](https://github.com/Anderbone/spring-in-action-5-samples)

## 1.1 What is Spring?
At its core, Spring offers a container, often referred to as the Spring application context, that creates and manages application components. These components, or beans, are wired together inside the Spring application context to make a complete application, much like bricks, mortar, timber, nails, plumbing, and wiring are bound together to make a house.

The act of wiring beans together is based on a pattern known as dependency injection (DI). Rather than have components create and maintain the lifecycle of other beans that they depend on, a dependency-injected application relies on a separate entity (the container) to create and maintain all components and inject those into the beans that need them. This is done typically through constructor arguments or property accessor methods.
![](https://i.imgur.com/HmrlIsd.png)

## 1.2 Initializing a spring application (Testing)

- From the web application at http://start.spring.io 
- From the command line using the curl command 
- From the command line using the Spring Boot command-line interface 
- When creating a new project with Spring Tool Suite 
- When creating a new project with IntelliJ IDEA 
- When creating a new project with NetBeans

![](https://i.imgur.com/wTApSQv.png)
The @Configuration annotation indicates to Spring that this is a configuration class that will provide beans to the Spring application context. The configuration’s class methods are annotated with @Bean, indicating that the objects they return should be added as beans in the application context (where, by default, their respective bean IDs will be the same as the names of the methods that define them).

@SpringBootApplication annotation clearly signifies that this is a Spring Boot application. But there’s more to @SpringBootApplication than meets the eye. @SpringBootApplication is a composite application that combines three other annotations: 
    -  @SpringBootConfiguration—Designates this class as a configuration class. Although there’s not much configuration in the class yet, you can add Javabased Spring Framework configuration to this class if you need to. This annotation is, in fact, a specialized form of the @Configuration annotation.
    -  @EnableAutoConfiguration—Enables Spring Boot automatic configuration. We’ll talk more about autoconfiguration later. For now, know that this annotation tells Spring Boot to automatically configure any components that it thinks you’ll need.
    - @ComponentScan—Enables component scanning. This lets you declare other classes with annotations like @Component, @Controller, @Service, and others, to have Spring automatically discover them and register them as components in the Spring application context


## 1.3 Writing a Spring application (Controller, view template)

- You created an initial project structure using Spring Initializr. 
- You wrote a controller class to handle the homepage request. 
- You defined a view template to render the homepage. 
- You wrote a simple test class to prove out your work.

## 1.4 Surveying the Spring landscape

- The core Spring framework: Spring MVC, REST APIs, template-based JDBC, reactive-style programming
- Spring Boot
- Spring Data
- Spring security
- Spring Integration and Spring Batch
- Spring Cloud

## Summary

- Spring aims to make developer challenges easy, like creating web applications, working with databases, securing applications, and microservices.
- Spring Boot builds on top of Spring to make Spring even easier with simplified dependency management, automatic configuration, and runtime insights.
- Spring applications can be initialized using the Spring Initializr, which is webbased and supported natively in most Java development environments.
- The components, commonly referred to as beans, in a Spring application context can be declared explicitly with Java or XML, discovered by component scanning, or automatically configured with Spring Boot autoconfiguration

## Code
If port 8080 is in used, add `server.port=8090` in your application.properties.