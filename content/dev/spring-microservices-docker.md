+++ 
date = "2022-08-25"
title = "Microservices with Spring Boot and Spring Cloud chap04 Docker"
tags = ["spring","docker" ]
+++

Page 105 when running docker build, there's an error: `Docker: failed to export image: failed to create image: failed to get layer`.

```
cd microservices/product-service
docker build -t product-service .
```
After adding 'RUN true' between each COPY, problem solved.

```docker
FROM adoptopenjdk:16_36-jre-hotspot as builder
WORKDIR extracted
ADD ./build/libs/*.jar app.jar
RUN java -Djarmode=layertools -jar app.jar extract

FROM adoptopenjdk:16_36-jre-hotspot
WORKDIR application
COPY --from=builder extracted/dependencies/ ./
RUN true
COPY --from=builder extracted/spring-boot-loader/ ./
RUN true
COPY --from=builder extracted/snapshot-dependencies/ ./
RUN true
COPY --from=builder extracted/application/ ./

EXPOSE 8080

ENTRYPOINT ["java", "org.springframework.boot.loader.JarLauncher"]

```


[Reference](https://stackoverflow.com/questions/51115856/docker-failed-to-export-image-failed-to-create-image-failed-to-get-layer)
