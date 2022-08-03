+++ 
date = "2022-07-31"
title = "Spring In Action 07 - RESTful API"
tags = ["spring", "java", "spring-in-action" ]
toc = true
+++

Based on [Spring in action 6th version github repo](https://github.com/habuma/spring-in-action-6-samples). 

## RESTful controllers

### return a 404 status
Here we can return `Optional<Taco>` directly, but it will return `null` if id doesn't exist with status code 200.
If we want to return a 404 status code appropriately, as shown here:
```java
	@GetMapping("/{id}")
	public ResponseEntity<Taco> tacoById(@PathVariable("id") Long id) {
		return tacoRepo.findById(id).map(taco -> new ResponseEntity<>(taco, HttpStatus.OK))
				.orElseGet(() -> new ResponseEntity<>(null, HttpStatus.NOT_FOUND));
	}

```

### IngredientController and rest client

I added `IngredientById` here, it's in the rest client test but not in the codebase.
```java
package tacos.web.api;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import tacos.Ingredient;
import tacos.Taco;
import tacos.data.IngredientRepository;

@RestController
@RequestMapping(path="/api/ingredients", produces="application/json")
@CrossOrigin(origins="http://localhost:8080")
public class IngredientController {

	private IngredientRepository repo;

	@Autowired
	public IngredientController(IngredientRepository repo) {
		this.repo = repo;
	}

	@GetMapping
	public Iterable<Ingredient> allIngredients() {
		return repo.findAll();
	}

	@GetMapping("/{id}")
	public ResponseEntity<Ingredient> IngredientById(@PathVariable("id") String id) {
		return repo.findById(id).map(ingredient -> new ResponseEntity<>(ingredient, HttpStatus.OK))
				.orElseGet(() -> new ResponseEntity<>(null, HttpStatus.NOT_FOUND));
	}

}

```
Code of rest client

```java
package tacos.restclient;

import java.util.Collection;
import java.util.List;

import org.springframework.core.ParameterizedTypeReference;
import org.springframework.hateoas.CollectionModel;
import org.springframework.hateoas.client.Traverson;
import org.springframework.http.HttpMethod;
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

import lombok.extern.slf4j.Slf4j;
import tacos.Ingredient;
import tacos.Taco;

@Service
@Slf4j
public class TacoCloudClient {

  private RestTemplate rest;
  private Traverson traverson;

  public TacoCloudClient(RestTemplate rest, Traverson traverson) {
    this.rest = rest;
    this.traverson = traverson;
  }

  //
  // GET examples
  //

  /*
   * Specify parameter as varargs argument
   */
  public Ingredient getIngredientById(String ingredientId) {
    return rest.getForObject("http://localhost:8080/api/ingredients/{id}",
                             Ingredient.class, ingredientId);
  }
  public List<Ingredient> getAllIngredients() {
    return rest.exchange("http://localhost:8080/api/ingredients",
            HttpMethod.GET, null, new ParameterizedTypeReference<List<Ingredient>>() {})
        .getBody();
  }
}
```

Rest examples
```java

import java.net.URI;
import java.util.List;

import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.SpringBootConfiguration;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.hateoas.MediaTypes;
import org.springframework.hateoas.client.Traverson;
import org.springframework.web.client.RestTemplate;

import lombok.extern.slf4j.Slf4j;
import tacos.Ingredient;
import tacos.Taco;

@SpringBootConfiguration
@ComponentScan
@Slf4j
public class RestExamples {

  public static void main(String[] args) {
    SpringApplication.run(RestExamples.class, args);
  }

  @Bean
  public RestTemplate restTemplate() {
    return new RestTemplate();
  }

  @Bean
  public CommandLineRunner fetchIngredients(TacoCloudClient tacoCloudClient) {
    return args -> {
      log.info("----------------------- GET -------------------------");
      log.info("GETTING INGREDIENT BY IDE");
      log.info("Ingredient:  " + tacoCloudClient.getIngredientById("CHED"));
      log.info("GETTING ALL INGREDIENTS");
      List<Ingredient> ingredients = tacoCloudClient.getAllIngredients();
      log.info("All ingredients:");
      for (Ingredient ingredient : ingredients) {
        log.info("   - " + ingredient);
      }
    };
  }

  @Bean
  public CommandLineRunner putAnIngredient(TacoCloudClient tacoCloudClient) {
    return args -> {
      log.info("----------------------- PUT -------------------------");
      Ingredient before = tacoCloudClient.getIngredientById("LETC");
      log.info("BEFORE:  " + before);
//      tacoCloudClient.updateIngredient(new Ingredient("LETC", "Shredded Lettuce", Ingredient.Type.VEGGIES));
      Ingredient after = tacoCloudClient.getIngredientById("LETC");
      log.info("AFTER:  " + after);
    };
  }
}
```


## HATEOAS: links embedded
Hypermedia as the Engine of Application State
### overview
creating self-describing APIs wherein resources returned from an API contain links to related resources. This enables clients to navigate an API with minimal understanding of the API’s URLs. Instead, it understands relationships between the resources served by the API and uses its understanding of those relationships to discover the API’s URLs as it traverses those relationships.
### linkTo, methodOn
call linkTo() by giving it a method on the controller to have ControllerLinkBuilder derive the base URL from both the controller’s base path and the method’s mapped path. 
- code
```java
Resources<Resource<Taco>> recentResources = Resources.wrap(tacos); recentResources.add(
linkTo(methodOn(DesignTacoController.class).recentTacos()) .withRel("recents"));
```
statically include the linkTo() and methodOn() methods (both from ControllerLinkBuilder) to keep the code easier to read. The methodOn() method takes the controller class and lets you make a call to the recentTacos() method, which is intercepted by ControllerLinkBuilder and used to determine not only the controller’s base path, but also the path mapped to recentTacos(). Now the entire URL is derived from the controller’s mappings, and absolutely no portion is hardcoded. Sweet!
- code
```java
public static String getFailedLabJobOperationQualityLink(Integer jobOperationLabQualityId) {
 return ControllerLinkBuilder.linkTo(ControllerLinkBuilder.methodOn(JobOperationQualityController.class)
   .getFailedLabJobOperationQuality(jobOperationLabQualityId)).withSelfRel().getHref();
}

```
### ResourceProcessor
The ResourceProcessor shown in listing 6.8 is defined as an anonymous inner class and declared as a bean to be created in the Spring application context. Spring HATEOAS will discover this bean (as well as any other beans of type ResourceProcessor) automatically and will apply them to the appropriate resources. In this case, if a PagedResources<Resource<Taco>> is returned from a controller, it will receive a link for the most recently created tacos. This includes the response for requests for /api/tacos.
#### SpringDataRestConfiguration
- code
```java
@Configuration
public class SpringDataRestConfiguration {

  @Bean
  public ResourceProcessor<PagedResources<Resource<Taco>>>
    tacoProcessor(EntityLinks links) {

    return new ResourceProcessor<PagedResources<Resource<Taco>>>() {
      @Override
      public PagedResources<Resource<Taco>> process(
                          PagedResources<Resource<Taco>> resource) {
        resource.add(
            links.linkFor(Taco.class)
                 .slash("recent")
                 .withRel("recents"));
        return resource;
      }
    };
  }
  
}


```

## Http methods
uniform interface, verbs
### request/response
#### request 
HEAD /psts/1 HTTP/1.1
Accept: text/html, ..
Connection: keep-alive
Host: blog.eg.com
#### response
Content-Type: text/html; charset=UTF-8
Date: ..GMT
Server: Apache
<!DOCTYPE..> <html>..
### methods
- get
- read
- post (create)
unlike put, doesn't need to knokw the URL of the resource
put
update
- delete
- head
only retrieve meta data. check resource exists or newer version



## Archived for Spring in Action 5th version bug fix

Set [project](https://github.com/habuma/spring-in-action-5-samples/tree/master/ch06) to java 8. 

1. In ch06 folder, run `./mvnw clean package`.

Error:
```log
[ERROR] Failed to execute goal com.github.eirslett:frontend-maven-plugin:1.4:install-node-and-npm (install node and npm) on project tacocloud-ui: Could not install Node: Unable to delete file: C:\Users\yanch\g
itProject\spring-in-action-5-samples\ch06\tacocloud-ui\node\tmp\node-v6.9.1-win-x64\node_modules\npm\node_modules\columnify\node_modules\wcwidth\node_modules\defaults\node_modules\clone\LICENSE -> [Help 1]
[ERROR]
```
This is what [found](https://stackoverflow.com/questions/19489720/maven-failed-to-clean-project-failed-to-delete-org-ow2-util-asm-asm-tree) about this error.
I exited my apps that possibly scan my system, like listary, and it works.

Error:
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:2.21.0:test (default-test) on project taco-cloud: There are test failures.

Add this dependency to in ch06/pom.xml then run `./mvnw clean package`.
```
    <dependencies>
        <dependency>
            <groupId>javax.xml.bind</groupId>
            <artifactId>jaxb-api</artifactId>
            <version>2.3.0</version>
        </dependency>
        <dependency>
            <groupId>org.javassist</groupId>
            <artifactId>javassist</artifactId>
            <version>3.25.0-GA</version>
        </dependency>
    </dependencies>
```

2. Run `java -jar tacos/target/taco-cloud-0.0.6-SNAPSHOT.jar`
3. Open 'http://localhost:8080/'  
