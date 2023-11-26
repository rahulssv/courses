# Spring MVC

```xml title="pom.xml"
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.psl</groupId>
  <artifactId>mvc</artifactId>
  <packaging>war</packaging>
  <version>0.0.1-SNAPSHOT</version>
  <name>mvc Maven Webapp</name>
  <url>http://maven.apache.org</url>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
    <dependency> 
		<groupId>org.springframework</groupId> 
		<artifactId>spring-webmvc</artifactId> 
		<version>5.3.25</version> 
	</dependency> 
	<dependency> 
		<groupId>javax.servlet</groupId> 
		<artifactId>jstl</artifactId> 
		<version>1.2</version> 
	</dependency> 
  </dependencies>
  <build>
    <finalName>mvc</finalName>
  </build>
</project>

```
## Java
```java title="App.java"
package com.psl;

public class App {

}

```
```java title="BookController.java"
package com.psl.controller.book;

import java.util.Collection; 
import org.springframework.beans.factory.annotation.Autowired; 
import org.springframework.context.ApplicationContext; 
import org.springframework.stereotype.Controller; 
import org.springframework.web.bind.annotation.RequestMapping; 
import org.springframework.web.bind.annotation.RequestMethod; 
import org.springframework.web.bind.annotation.RequestParam; 
import org.springframework.web.servlet.ModelAndView; 
import com.psl.dao.book.BookRepository; 
import com.psl.model.book.Book; 
@Controller
public class BookController { 
@Autowired
private ApplicationContext appContext; 
@RequestMapping(value = "books", method = RequestMethod.GET) 
public ModelAndView allBooks() { 
 ModelAndView mav = new ModelAndView(); 
 BookRepository bookRepo = 
 appContext.getBean("bookRepo", BookRepository.class); 
 Collection<Book> allBooks = bookRepo.getRepository().values(); 
 mav.addObject("books", allBooks); 
 mav.setViewName("books"); 
 return mav; 
 } 
@RequestMapping(value = "addbook", method = RequestMethod.POST) 
public ModelAndView allBooks( 
 @RequestParam("accessionNumber") String accNo, 
 @RequestParam("title") String title, 
 @RequestParam("price") double price) { 
 ModelAndView mav = new ModelAndView(); 
 Book book = new Book(accNo, title, price); 
 BookRepository bookRepo = 
 appContext.getBean("bookRepo", BookRepository.class); 
 bookRepo.getRepository().put(accNo, book); 
 mav.addObject("book", book); 
 mav.setViewName("booksadded"); 
 return mav; 
 } 
}
```
```java title="BookRepository.java"
package com.psl.dao.book;
import java.util.HashMap; 
import java.util.Map; 
import java.util.Map.Entry; 
import org.springframework.stereotype.Component; 
import com.psl.model.book.Book; 
@Component
public class BookRepository { 

private Map<String, Book> repository = new HashMap<String, Book>(); 
public BookRepository() { 
 repository.put("333",new Book("333","1984", 456.78 )); 
 repository.put("222",new Book("222","Lila", 123.45 )); 
 repository.put("111",new Book("111","Animal Farm", 234.56 )); 
 } 
public Map<String, Book> getRepository() { 
 return repository; 
 } 
public void setRepository(Map<String, Book> repository) { 
 this.repository = repository; 
 } 
@Override
public String toString() { 
 StringBuilder builder = new StringBuilder(); 
 builder.append("BookRepository ["); 
 for (Entry<String, Book> entry : repository.entrySet()) { 
 builder.append("("); 
 builder.append(entry.getValue()); 
 builder.append(")"); 
 } 
 builder.append("]"); 
 return builder.toString(); 
 } 


}
```
```java title="Book.java"
package com.psl.model.book;

public class Book {
	private String title;
	private String accessionNumber;
	private double price;
	public String getTitle() {
		return title;
	}

	public void setTitle(String title) {
		this.title = title;
	}

	public String getAccessionNumber() {
		return accessionNumber;
	}

	public void setAccessionNumber(String accessionNumber) {
		this.accessionNumber = accessionNumber;
	}

	public double getPrice() {
		return price;
	}

	public void setPrice(double price) {
		this.price = price;
	}

	

	public Book() {
	}

	public Book(String accessionNumber, String title, double price) {
		super();
		this.accessionNumber = accessionNumber;
		this.title = title;
		this.price = price;
	}

	@Override
	public String toString() {
		StringBuilder builder = new StringBuilder();
		builder.append("Book [title=");
		builder.append(title);
		builder.append(", accessionNumber=");
		builder.append(accessionNumber);
		builder.append(", price=");
		builder.append(price);
		builder.append("]");
		return builder.toString();
	}
}

```
## WebApp
```jsp title="index.jsp"
<html>
<body>
<h2>Hello World!</h2>
</body>
</html>

```
### WEB-INF
```xml title="dispatcher-servlet.xml"
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:p="http://www.springframework.org/schema/p"
	xmlns:c="http://www.springframework.org/schema/c"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
 http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/context
 http://www.springframework.org/schema/context/spring-context.xsd"
	default-init-method="init" default-destroy-method="destroy"
	default-lazy-init="true">
	<context:component-scan
		base-package="com.psl.controller.book" />
	<bean
		class="org.springframework.web.servlet.view.InternalResourceViewResolver"
		id="viewResolver">
		<property name="prefix" value="/WEB-INF/views/book/"></property>
		<property name="suffix" value=".jsp"></property>

	</bean>
	<bean name="bookRepo"
		class="com.psl.dao.book.BookRepository" />


</beans>
```
```xml title="web.xml"
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>
  <servlet>
	  <servlet-name>dispatcher</servlet-name>
	  <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
	  
  </servlet>
  <servlet-mapping>
	  <servlet-name>dispatcher</servlet-name>
	  <url-pattern>/</url-pattern>
  </servlet-mapping>
</web-app> 


```
#### views\book
```jsp title="books.jsp"
<%@page import="java.util.List"%>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<%@ page import="com.psl.model.book.Book"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@ page isELIgnored="false"%>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<form method="post" action="addbook">
		<h1>BUY BOOKS HERE</h1>
		<table>
			<tr>
				<td>
					<table>
						<tr>
							<td>Acc. No.</td>
							<td><input type="text" id="accessionNumber"
								name="accessionNumber"></td>
						</tr>
						<tr>
							<td>Title</td>
							<td><input type="text" id="title" name="title"></td>
						</tr>
						<tr>
							<td>Price</td>
							<td><input type="text" id="price" name="price"></td>
						</tr>
						<tr>
							<td></td>
							<td><input type="submit"></td>
						</tr>
					</table>
		</table>
		</td>
		</tr>
		<tr>
			<td>
				<table border="1" align="right">
					<tr>
						<th>Acc No</th>
						<th>Title</th>
						<th>Price</th>
					</tr>
					<c:forEach var="book" items="${books}">
						<tr>
							<td>${book.accessionNumber}</td>
							<td>${book.title}</td>
							<td>${book.price}</td>
						</tr>
					</c:forEach>
				</table>
			</td>
		</tr>
		</table>
	</form>
</body>
</html>
```
```jsp title="booksaddeded.jsp"
<%@page import="java.util.List"%>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<%@ page import="com.psl.model.book.Book"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@ page isELIgnored="false"%>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<h1>BUY BOOKS HERE</h1>
	<form action="books">
		<table>
			<tr>
				<td>
					<table border="1" align="right">
						<tr>
							<th>Acc No</th>
							<th>Title</th>
							<th>Price</th>
						</tr>
						<tr>
							<td>${book.accessionNumber}</td>
							<td>${book.title}</td>
							<td>${book.price}</td>
						</tr>
						<tr>
							<td></td>
							<td></td>
							<td><input type="submit" value=Allbooks�></td>
						</tr>
					</table>
				</td>
			</tr>
		</table>
	</form>
</body>
</html>
```