# Spring MVC - Form

```xml title="pom.xml"
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.psl</groupId>
	<artifactId>mvcform</artifactId>
	<packaging>war</packaging>
	<version>0.0.1-SNAPSHOT</version>
	<name>mvcform Maven Webapp</name>
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
		<finalName>mvcform</finalName>
	</build>
</project>

```
## Java
```java title="App.java"
package com.psl;

public class App {

}

```
```java title="FormController.java"
package com.psl.controller;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

import com.psl.model.Student;
@Controller
public class FormController {
	@RequestMapping(path = "/form", method = RequestMethod.GET) 
	public String addStudent() {
		System.out.println("form called");
		return "form";
	}
	@RequestMapping(path = "/data", method = RequestMethod.POST) 
	public String displayStudent(@ModelAttribute("student") Student student, Model model) {
		System.out.println("display data called" +student);
		return "data";
	}
	@RequestMapping("/student") 
	public String student() {
		System.out.println("display data called");
		return "student";
	}
}

```

```java title="Student.java"
package com.psl.model;

public class Student {
private String name;
private String email;
private String password;
public Student() {
	super();
	// TODO Auto-generated constructor stub
}
public Student(String name, String email, String password) {
	this.name = name;
	this.email = email;
	this.password = password;
}
public String getName() {
	return name;
}
public void setName(String name) {
	this.name = name;
}
public String getEmail() {
	return email;
}
public void setEmail(String email) {
	this.email = email;
}
public String getPassword() {
	return password;
}
public void setPassword(String password) {
	this.password = password;
}
@Override
public String toString() {
	StringBuilder builder = new StringBuilder();
	builder.append("Student [name=");
	builder.append(name);
	builder.append(", email=");
	builder.append(email);
	builder.append(", password=");
	builder.append(password);
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
```xml title="form-servlet.xml"
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:p="http://www.springframework.org/schema/p"
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xmlns:c="http://www.springframework.org/schema/c"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
 http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/context
 http://www.springframework.org/schema/context/spring-context.xsd
 http://www.springframework.org/schema/mvc
 http://www.springframework.org/schema/mvc/spring-mvc.xsd"
	default-init-method="init" default-destroy-method="destroy"
	default-lazy-init="true">
	<context:component-scan
		base-package="com.psl.controller" />
	<mvc:resources location="/WEB-INF/resources/" mapping="/resources/**"/>
	<bean
		class="org.springframework.web.servlet.view.InternalResourceViewResolver"
		id="viewResolver">
		<property name="prefix" value="/WEB-INF/views/"></property>
		<property name="suffix" value=".jsp"></property>

	</bean>
	


</beans>
```
```xml title="web.xml"
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>
  <servlet>
	  <servlet-name>form</servlet-name>
	  <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
	  
  </servlet>
  <servlet-mapping>
	  <servlet-name>form</servlet-name>
	  <url-pattern>/</url-pattern>
  </servlet-mapping>
</web-app>

```
#### views\book
```jsp title="data.jsp"
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@ page isELignored="false"  %>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
 <h1>this is ${student.name}  </h1>
</body>
</html>
```
```jsp title="form.jsp"
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Student Registration Form</title>
<link rel="stylesheet"
	href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css"
	integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO"
	crossorigin="anonymous">
<link href="<c:url value="/resources/css/register.css"/>">
</head>
<body>
	<div class="d-flex align-items-center light-blue-gradient"
		style="height: 100vh;">
		<div class="container">
			<div class="d-flex justify-content-center">
				<div class="col-md-6">
					<div class="card rounded-0 shadow">
						<div class="card-body">
							<h3>Student Registration Form</h3>
							<form action="data" method="post">
								<div class="form-group">
									<label for="exampleInputEmail1">Enter Student's Name</label> <input
										name="name" type="text" class="form-control"
										id="exampleInputEmail1" aria-describedby="emailHelp"
										placeholder="Enter full name">
								</div>
								<div class="form-group">
									<label for="exampleInputEmail1">Email address:</label> <input
										name="email " type="email" class="form-control"
										id="exampleInputEmail1" aria-describedby="emailHelp"
										placeholder="Enter email"> <small id="emailHelp"
										class="form-text text-muted">We'll never share your
										email with anyone else.</small>
								</div>

								<div class="form-group">
									<label for="exampleInputPassword1">Password: </label> <input
										type="password" class="form-control"
										id="exampleInputPassword1" placeholder="Password">
								</div>


								<button type="submit" class="btn btn-primary">Submit</button>
							</form>
						</div>
					</div>
				</div>
			</div>

		</div>
</body>
</html>
```
```jsp title="student.jsp"
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
<h1>hi Rahul here </h1> 
</body>
</html>
```