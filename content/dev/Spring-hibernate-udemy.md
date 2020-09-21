+++ 
date = "2020-09-21"
title = "Spring & Hibernate project on udemy: intellij setting up"
tags = ["spring","udemy","intellij" ]
+++

Udemy course [link](https://www.udemy.com/course/spring-hibernate-tutorial/)

In section 28, we start to build a real database web app. Here we use intellij with maven to set it up.

1. Download maven config, [link](https://drive.google.com/file/d/1v1mCDzeYFt5OV_crBjTv8wb0M_VT5PyQ/view)
2. Unzip and use intellij to open the inner folder, import as Maven project.
3. Suppose you set up the database correctly, update code in TestDbServlet.java if you use version 8+:
```java
		String jdbcUrl = "jdbc:mysql://localhost:3306/web_customer_tracker?useSSL=false&serverTimezone=UTC";
		String driver = "com.mysql.cj.jdbc.Driver";
```
4. Project settings as below:
![](https://i.imgur.com/jAZ3CY0.png)
![](https://i.imgur.com/KEmOMiQ.png)
![](https://i.imgur.com/yoX74o3.png)
![](https://i.imgur.com/E7w8Dqa.png)

5. Add your tomcat config and run it.
![](https://i.imgur.com/Griz7R0.png)
![](https://i.imgur.com/36vrRFC.png)