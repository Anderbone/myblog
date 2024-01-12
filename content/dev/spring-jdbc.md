+++ 
date = "2024-01-12"
title = "Spring Start here 11 - DB connection"
tags = ["spring"]
+++

Here we show the 3 ways mentioned in chapter 11 of the book Spring Start Here. H2 in memory database, mysql database and mysql database with self defined data source.

## H2 in memory connection

![](https://i.imgur.com/C3CHDEA.png)

pom.xml
```xml
	<dependency>
		<groupId>com.h2database</groupId>
		<artifactId>h2</artifactId>
		<scope>runtime</scope>
	</dependency>
```

Controller `PurchaseController.java`
```java
package com.example.controllers;

import com.example.model.Purchase;
import com.example.repositories.PurchaseRepository;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
@RequestMapping("/purchase")
public class PurchaseController {

  private final PurchaseRepository purchaseRepository;

  public PurchaseController(PurchaseRepository purchaseRepository) {
    this.purchaseRepository = purchaseRepository;
  }

  @PostMapping
  public void storePurchase(@RequestBody Purchase purchase) {
    purchaseRepository.storePurchase(purchase);
  }

  @GetMapping
  public List<Purchase> findPurchases() {
    return purchaseRepository.findAllPurchases();
  }
}


```
Model `Purchase.java`
```java
package com.example.model;

import java.math.BigDecimal;
import java.util.Objects;

public class Purchase {

  private int id;
  private String product;
  private BigDecimal price;

  public int getId() {
    return id;
  }

  public void setId(int id) {
    this.id = id;
  }

  public String getProduct() {
    return product;
  }

  public void setProduct(String product) {
    this.product = product;
  }

  public BigDecimal getPrice() {
    return price;
  }

  public void setPrice(BigDecimal price) {
    this.price = price;
  }

  @Override
  public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    Purchase purchase = (Purchase) o;
    return id == purchase.id && Objects.equals(product, purchase.product) && Objects.equals(price, purchase.price);
  }

  @Override
  public int hashCode() {
    return Objects.hash(id, product, price);
  }
}


```

Repository `PurchaseRepository.java`
```java
package com.example.repositories;

import com.example.model.Purchase;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.RowMapper;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
public class PurchaseRepository {

  private final JdbcTemplate jdbc;

  public PurchaseRepository(JdbcTemplate jdbc) {
    this.jdbc = jdbc;
  }

  public void storePurchase(Purchase purchase) {
    String sql = "INSERT INTO purchase VALUES (NULL, ?, ?)";
    jdbc.update(sql, purchase.getProduct(), purchase.getPrice());
  }

  public List<Purchase> findAllPurchases() {
    String sql = "SELECT * FROM purchase";

    RowMapper<Purchase> purchaseRowMapper = (r, i) -> {
      Purchase rowObject = new Purchase();
      rowObject.setId(r.getInt("id"));
      rowObject.setProduct(r.getString("product"));
      rowObject.setPrice(r.getBigDecimal("price"));
      return rowObject;
    };

    return jdbc.query(sql, purchaseRowMapper);
  }
}

```
`schema.sql`
```sql
CREATE TABLE IF NOT EXISTS purchase (
    id INT AUTO_INCREMENT PRIMARY KEY,
    product varchar(50) NOT NULL,
    price double NOT NULL
);
```

## MySQL connection

```xml
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
```

application.properties
```
spring.datasource.url=jdbc:mysql://localhost/spring_quickly
spring.datasource.username=root
spring.datasource.password=
spring.datasource.initialization-mode=always
```


## self made datasource

One more ProjectConfig.java
```java
package com.example.config;

import com.zaxxer.hikari.HikariDataSource;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.sql.DataSource;

@Configuration
public class ProjectConfig {

  @Value("${custom.datasource.url}")
  private String datasourceUrl;

  @Value("${custom.datasource.username}")
  private String datasourceUsername;

  @Value("${custom.datasource.password}")
  private String datasourcePassword;

  @Bean
  public DataSource dataSource() {
    HikariDataSource dataSource = new HikariDataSource();
    dataSource.setJdbcUrl(datasourceUrl);
    dataSource.setUsername(datasourceUsername);
    dataSource.setPassword(datasourcePassword);
    dataSource.setConnectionTimeout(1000);
    return dataSource;
  }
}

```
application.properties
```
custom.datasource.url=jdbc:mysql://localhost/spring_quickly
custom.datasource.username=root
custom.datasource.password=
```