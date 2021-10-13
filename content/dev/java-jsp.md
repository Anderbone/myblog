+++ 
date = "2020-10-03"
title = "JSP and Servlets"
tags = ["servlets", "jsp", "database" ]
toc = true
+++


Based on [udemy course](https://www.udemy.com/course/jsp-tutorial/)
# JSP
## Basic concept

JSP: similar to html page, with some Java code. It's processed on the server, results of Java code included in HTML returned to browser
- jsp expression``` <%= new java.util.Date() %> ```
  - Obj, <%= new String("hello").toUpperCase() %>
  - number, <%= 25*4 %>
  - boolean, <%= 5>6 %>
- jsp scriptlet ```<% some Java %>```  out.println() to print. Minimisze the use here.
- jsp declaration ``` <%! variable or method declaration%>```
    ```java
   <% String lower(String data){
      return data.toLowerCase();
      }%>
    ```
- call Java class from JSP 
```java
<%@ page import="com.hello" %>
```
![](https://i.imgur.com/GtBsbsR.png)
- include files
```java
<jsp:include page="header.html"/>
```

- form/radio/checkbox
action:response.jsp, this is where we response the input form. Use ${param.firstName} in response page to output/match the input name in form.

## Session object
created once for user's browser session, unique for this user. Keep track of user's actions.
- add data to session object
```java
List<String> items = new ArrayList<>();
session.SetAttribute("myTodoList", items);
...
List<String> myStuff = (List<String>) session.getAttribute("myTodoList);

```
- commonly used: isNew, getID, invalidate, setMaxInactiveInterval(long mills)

- cookies
  1. form, submit name favoriteLanguage
  2. response.jsp, ```String favL = request.getParameter("favoriteLanguage")```
  3. ```Cookie theCookie = new Cookie("myapp.ck", favL)  theCookie.setMaxAge```
  4. ```response.addCookie(theCookie)``` Notice this step, send cookie to *browser*, with response.
  5. homepage, ```Cookie[] cookies = resquest.getCookies();```
  6. for loop, ```tempCk.getName().equals("myapp.ck")```, get tempCk.getValue()

## JSTL, jsp standard tag library
- Choose
```html
<c:choose>, <c:when test=>,<c:otherwise>
```
- if
```html
<c:if test="${not tempStudent.goldCustomer}">
```
- forEach/forTokens
```html
pageContext.setAttribute("myStudents",data);
<c:forEach var="tempStu" items="${myStudnets}">
${ tempStu.firstName }
</c:forEach>
```
- function
```html
<c:set var="data" value="haha" />
Length of ${data}: ${fn: length(data)}
```
- I18N/Formatting
![](https://i.imgur.com/bmJZ7be.png)

# Servlets
## Basics
- Java class that processed on the server
- Java class generates HTML that is returned to browser
- can read HTML form data, use cookies and sessions etc.
- At a high level, simialr to JSPs
```java
@WebServlet("/funny")
public class HelloWorldServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public HelloWorldServlet() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

		// Step 1: set the content type
		response.setContentType("text/html");
		
		// Step 2: get the printwriter
		PrintWriter out = response.getWriter();
		
		// Step 3: generate HTML content
		out.println("<html><body>");
		
		out.println("<h2>Hello World</h2>");
		out.println("<hr>");
		out.println("Time on the server is: " + new java.util.Date());
		
		out.println("</body></html>");
	}   
	
	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		doGet(request, response);
	}

}

```
- form action="StudentServlet", method="GET". doGet method then use request.getParameter("firstName") to get the form data. 
- in doGet, ```response.setContentType("text/html")```
- ```PrintWriter out = response.getWriter.getWriter()```
- ```out.println("<html><body>")```

## Get/Post difference
- GET: url?field=1?... good for debug, bookmark/email. limitation on data length.
- Post: won't see in url. No limitations on data length. can send binary data.

## Servlet with JSP
### Servlet can call JSP using a request dispatcher
- ```RequestDispatcher dispatcher = request.getRequestDispatcher("/view_student.jsp");```
- Forward to JSP
- ```dispatcher.forward(request, response);```

### Sending data to JSP
![](https://i.imgur.com/K6ieDeE.png)

# Database
## tomcat config
- Define connection pool in context.xml
- in java world, see Datasource, think of connection pool.
- maxIdle="5", no user in our system, at least 5 connections available 
- maxWait="10000", waiting 10 seconds.

## MVC
- resource injection with Servlets
![](https://i.imgur.com/UdLhHOd.png)




