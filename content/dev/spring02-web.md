+++ 
date = "2020-02-19"
title = "Spring In Action 02 - Developing web app"
tags = ["spring", "java", "spring-in-action" ]
+++

This chapter focues on Spring web framework without database.

## 2.1 Displaying infomation

![](https://i.imgur.com/PeLvW5D.png)

### 2.1.1 Establishing the domain

```java
package tacos; 
import lombok.Data;
import lombok.RequiredArgsConstructor; 
@Data
@RequiredArgsConstructor 
public class Ingredient {
    private final String id; 
    private final String name; 
    private final Type type;

    public static enum Type { WRAP, PROTEIN, VEGGIES, CHEESE, SAUCE } 
}
```
### 2.1.2 Creating a controller class

Controllers are the major players in Spring’s MVC framework. Their primary job is to handle HTTP requests and either hand a request off to a view to render HTML (browser-displayed) or write data directly to the body of a response (RESTful). In this chapter, we’re focusing on the kinds of controllers that use views to produce content for web browsers. When we get to chapter 6, we’ll look at writing controllers that handle requests in a REST API.

-  Handle HTTP GET requests where the request path is /design 
-  Build a list of ingredients 
-  Hand the request and the ingredient data off to a view template to be rendered as HTML and sent to the requesting web browser
![](https://i.imgur.com/kiGks3L.png)


the @Data annotation at the class level is provided by Lombok and tells Lombok to generate all of those missing methods as well as a constructor that accepts all final properties as arguments. By using Lombok, you can keep the code for Ingredient slim and trim.

@GetMapping is just one member of a family of request-mapping annotations. Table 2.1 lists all of the request-mapping annotations available in Spring MVC.

![](https://i.imgur.com/zE6wqiw.png)

```java
	Type[] types = Ingredient.Type.values();
	for (Type type : types) {
	  model.addAttribute(type.toString().toLowerCase(),
	      filterByType(ingredients, type));
	}
```
Data placed in model attributes is copied into the servlet response attributes, where view can find them.

### 2.1.3 Designing the view
Spring offers several great options for defining views, including JavaServer Pages (JSP), Thymeleaf, FreeMarker, Mustache, and Groovy-based templates. For now, we’ll use Thymeleaf.

```html
<p th:text="${message}">placeholder message</p>
```
When the template is rendered into HTML, the body of the <p> element will be replaced with the value of the servlet request attribute whose key is "message". The th:text attribute is a Thymeleaf-namespaced attribute that performs the replacement. The ${} operator tells it to use the value of a request attribute ("message", in this case).


```html
    <h3>Designate your wrap:</h3>
    <div th:each="ingredient : ${wrap}">
    <input name="ingredients" type="checkbox" th:value="${ingredient.id}" />
    <span th:text="${ingredient.name}">INGREDIENT</span><br/>
    </div>
```
Here you use th:each attribute on the <div> tag to repeat rendering of the <div> once for each item in the collection found in the **wrap** request attribute. On each iteration, the ingredient item is bound to a Thymeleaf variable named ingredient. Inside <div>, there's a checkbox <input> and a <span>.
## 2.2 Processing form submission

Just like @GetMapping handles GET requests, you can use @PostMapping to handle POST requests. For handling taco design submissions, add the processDesign() method in the following listing to DesignTacoController.

```java
@PostMapping
public String processDesign(Taco design) { // Save the taco design... 
// We'll do this in chapter 3 
    log.info("Processing design: " + design);
    return "redirect:/orders/current"; 
}
```

When the form is submitted, the fields in the form are bound to properties of a Taco object (name and ingredients) that’s passed as a parameter into processDesign(). From there, the processDesign() method can do whatever it wants with the Taco object.
```html
   <input type="text" th:field="*{name}"/>
```
If you look back at the form in listing 2.3, you’ll see several checkbox elements, all with the name ingredients, and a text input element named name. Those fields in the form correspond directly to the ingredients and name properties of the Taco class. The Name field on the form only needs to capture a simple textual value. Thus
the name property of Taco is of type String. The ingredients check boxes also have textual values, but because zero or many of them may be selected, the ingredients property that they’re bound to is a List<String> that will capture each of the chosen ingredients.

## 2.3 Validating form input

### 2.3.1 Declaring validation rules

- Declare validation rules on the class that is to be validated: specifically, the Taco class.
- Specify that validation should be performed in the controller methods that require validation: specifically, the DesignTacoController’s processDesign() method and OrderController’s processOrder() method.
- Modify the form views to display validation errors

### 2.3.2 Performing validation at form binding
The @Valid annotation tells Spring MVC to perform validation on the submitted Taco object after it’s bound to the submitted form data and before the processDesign() method is called. 

### 2.3.3 Displaying validation errors
Thymeleaf offers convenient access to the Errors object via the fields property and with its th:errors attribute

## 2.4 Working with view controllers
- They’re all annotated with @Controller to indicate that they’re controller classes that should be automatically discovered by Spring component scanning and instantiated as beans in the Spring application context.
- All but HomeController are annotated with @RequestMapping at the class level to define a baseline request pattern that the controller will handle.
- They all have one or more methods that are annotated with @GetMapping or @PostMapping to provide specifics on which methods should handle which kinds of requests.

```java
@Configuration
public class WebConfig implements WebMvcConfigurer { 
    @Override
    public void addViewControllers(ViewControllerRegistry registry) { 
        registry.addViewController("/").setViewName("home");
    } 
}
```

## 2.5 Choosing a view template library
![](https://i.imgur.com/plK2L3n.png)

### 2.5.1 Caching templates
For example, to disable Thymeleaf caching, add the following line in application.properties:
spring.thymeleaf.cache=false

![](https://i.imgur.com/2cRWVsq.png)

## Summary
- Spring offers a powerful web framework called Spring MVC that can be used to develop the web frontend for a Spring application.
- Spring MVC is annotation-based, enabling the declaration of request-handling methods with annotations such as @RequestMapping, @GetMapping, and @PostMapping.
- Most request-handling methods conclude by returning the logical name of a view, such as a Thymeleaf template, to which the request (along with any model data) is forwarded.
- Spring MVC supports validation through the Java Bean Validation API and implementations of the Validation API such as Hibernate Validator.
- View controllers can be used to handle HTTP GET requests for which no model data or processing is required.
- In addition to Thymeleaf, Spring supports a variety of view options, including FreeMarker, Groovy Templates, and Mustache.

## Error Correction
Listing 2.4, processDesign(Taco design), rather than (Design design).