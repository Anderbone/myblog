+++ 
date = "2020-02-19"
title = "Spring In Action 03 - Data"
tags = ["spring", "java", "spring-in-action" ]
draft = true
+++

JDBC at first and JPA later.
## 3.1 Reading and writing data with JDBC
Spring JDBC support is rooted in the JdbcTemplate class. JdbcTemplate provides a means by which developers can perform SQL operations against a relational database without all the ceremony and boilerplate typically required when working with JDBC.

![](https://i.imgur.com/Vf418s1.png)

![](https://i.imgur.com/u0ksD8N.png)

## 3.2 Persisting data with Spring Data JPA

![](https://i.imgur.com/VLM1NMe.png)


## Summary
- Spring’s JdbcTemplate greatly simplifies working with JDBC. 
- PreparedStatementCreator and KeyHolder can be used together when you need to know the value of a database-generated ID.
- For easy execution of data inserts, use SimpleJdbcInsert. 
- Spring Data JPA makes JPA persistence as easy as writing a repository interface.

## Code
When running the JPA example code:

applicaton.yml
```yml
spring:
  datasource:
    username: sa
    password: sa
    url: jdbc:h2:mem:default
    driver-class-name: org.h2.Driver
    schema:
      - classpath:data.sql
    initialization-mode: always
```
![](https://i.imgur.com/kpJEBfx.png)

Then there's an error:
```log
Error creating bean with name 'entityManagerFactory' defined in class path resource [org/springframework/boot/autoconfigure/orm/jpa/HibernateJpaConfiguration.class]: Invocation of init method failed; nested exception is javax.persistence.PersistenceException: [PersistenceUnit: default] Unable to build Hibernate SessionFactory; nested exception is org.hibernate.MappingException: Could not get constructor for org.hibernate.persister.entity.SingleTableEntityPersister
```

It's mainly because you copied schema.sql, you don't need to use it in JPA project. A quick fix is to add a new dependency.
```xml
        <dependency>
            <groupId>org.javassist</groupId>
            <artifactId>javassist</artifactId>
            <version>3.27.0-GA</version>
        </dependency>
```

A better solution:

Remove schema.sql and then there's another error,
```log
"org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'entityManagerFactory' defined in class path resource [org/springframework/boot/autoconfigure/orm/jpa/HibernateJpaConfiguration.class]: Initialization of bean failed; nested exception is org.springframework.jdbc.datasource.init.ScriptStatementFailedException: Failed to execute SQL script statement #6 of URL [file:/home/zhu/NetBeansProjects/Jpa-Taco-cloud-chapter3/target/classes/data.sql]: insert into Ingredient (id, name, type) values ('FLTO', 'Flour Tortilla', 'WRAP'); nested exception is org.h2.jdbc.JdbcSQLDataException: Data conversion error converting "'WRAP' (INGREDIENT: ""TYPE"" INTEGER)"; SQL statement:"
```
After I annotated Type type with @Enumerated(EnumType.STRING) in Ingredient class, it worked.
```java
@Data
@RequiredArgsConstructor
@NoArgsConstructor(access=AccessLevel.PRIVATE, force=true)
@Entity
public class Ingredient {
  
  @Id
  private final String id;
  private final String name;
  @Enumerated(EnumType.STRING)
  private final Type type;

  public static enum Type {
    WRAP, PROTEIN, VEGGIES, CHEESE, SAUCE
  }

}
```