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