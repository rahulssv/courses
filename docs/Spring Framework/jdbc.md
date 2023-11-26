# JDBC

```xml title="pom.xml"
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.psl</groupId>
	<artifactId>jdbc</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>com.psl</name>
	<url>http://maven.apache.org</url>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	</properties>

	<dependencies>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>3.8.1</version>
			<scope>test</scope>
		</dependency>
		<!-- https://mvnrepository.com/artifact/org.springframework/spring-core -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-core</artifactId>
			<version>5.3.25</version>
		</dependency>
		<!--
		https://mvnrepository.com/artifact/org.springframework/spring-context -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context</artifactId>
			<version>5.3.25</version>
		</dependency>
		<dependency>
			<groupId>javax.annotation</groupId>
			<artifactId>javax.annotation-api</artifactId>
			<version>1.3.2</version>
		</dependency>
		<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-jdbc</artifactId>
			<version>5.3.25</version>
		</dependency>
		<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
		<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>8.0.28</version>
		</dependency>


	</dependencies>
</project>

```
```java title="Config.java"
package com.springjdbc;

import javax.sql.DataSource;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.datasource.DriverManagerDataSource;

import com.springjdbc.dao.StudentDao;
import com.springjdbc.dao.StudentDaoImpl;

@Configuration
class Config {
	@Bean("ds")
	public DataSource getDataSource() {
		 DriverManagerDataSource ds=new DriverManagerDataSource();
		 ds.setDriverClassName("com.mysql.jdbc.Driver");
		 ds.setUrl("jdbc:mysql://localhost:3306/jdbc");
		 ds.setUsername("root");
		 ds.setPassword("root");
	return ds;
	}
	@Bean("template")
	public JdbcTemplate getTemplate() {
		return new JdbcTemplate(getDataSource());
	}
	@Bean("studentDao")
	public StudentDao getStudentDao() {
		StudentDaoImpl sdi=new StudentDaoImpl();
		sdi.setTemplate(getTemplate());
		return sdi;
	}
	

}

```
```java title="App.java"
package com.springjdbc;
import java.util.List;
import java.util.Scanner;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import com.springjdbc.dao.StudentDao;
import com.springjdbc.entities.Student;

/**
 * Hello world!
 *
 */
public class App {
	public static void main(String[] args) {
		Scanner input = new Scanner(System.in).useDelimiter("\\s*[\\n]\\s*");
		/*
		 * ClassPathXmlApplicationContext context = new
		 * ClassPathXmlApplicationContext("Config.xml");
		 */
		AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(Config.class);
		StudentDao studentDao = context.getBean("studentDao", StudentDao.class);

		boolean flag = true;
		while (true) {
			System.out.println("Student Data Database");
			System.out.println("1. Insert student data in database");
			System.out.println("2. Delete student data in database");
			System.out.println("3. Update student data in database");
			System.out.println("4. Display student data in database by studentId");
			System.out.println("5. Display all student data in database");
			System.out.println("6. Exit");
			System.out.print("Enter your choice: ");
			int choice = input.nextInt();
			switch (choice) {
			case 1:
				Student studentInsert = new Student();
				System.out.print("\nEnter student's Id: ");
				int idInsert = input.nextInt();
				studentInsert.setId(idInsert);
				System.out.print("\nEnter student's name: ");
				String nameInsert = input.next();
				studentInsert.setName(nameInsert);
				System.out.print("\nEnter student's city: ");
				String cityInsert = input.next();
				studentInsert.setCity(cityInsert);
				int rInsert = studentDao.insert(studentInsert);
				System.out.println("\nData inserted succesfully " + rInsert);
				break;
			case 2:
				System.out.print("\nEnter student's Id: ");
				int idDelete = input.nextInt();
				int rDelete = studentDao.delete(idDelete);
				System.out.println("\nData deleted succesfully " + rDelete);
				break;
			case 3:
				Student studentUpdate = new Student();
				System.out.print("\nEnter student's Id: ");
				int idUpdate = input.nextInt();
				studentUpdate.setId(idUpdate);
				System.out.print("\nEnter student's name: ");
				String nameUpdate = input.next();
				studentUpdate.setName(nameUpdate);
				System.out.print("\nEnter student's city: ");
				String cityUpdate = input.next();
				studentUpdate.setCity(cityUpdate);
				int rUpdate = studentDao.update(studentUpdate);
				System.out.println("\nData Updated succesfully " + rUpdate);
				break;
			case 4:
				System.out.print("\nEnter student's Id: ");
				int idSelect = input.nextInt();
				Student studentSelect = studentDao.selectId(idSelect);
				System.out.println(studentSelect);
				break;
			case 5:
				List<Student> studentSelectall = studentDao.selectall();
				for (Student stud : studentSelectall) {
					System.out.println(stud);
				}
				break;
			case 6:
				flag = true;
				break;
			default:
				System.out.println("Invalid choie. Please enter the correct choice!");
				break;

			}
//			if (flag==true) {
//				break;
//			}

		}

		//System.out.println("Thank you for using our software!");
		/*
		 * studentDao.update(student.getId()); studentDao.selectId(student.getId());
		 * studentDao.selectall();
		 */
	}
}

```
## Configuration
```xml title="Config.xml"
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:p="http://www.springframework.org/schema/p"
	xmlns:util="http://www.springframework.org/schema/util"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd
    http://www.springframework.org/schema/tx
    http://www.springframework.org/schema/tx/spring-tx.xsd
    http://www.springframework.org/schema/util
    http://www.springframework.org/schema/util/spring-util.xsd
    ">
    <bean class="org.springframework.jdbc.datasource.DriverManagerDataSource" id="ds">
		<property name="driverClassName" value="com.mysql.jdbc.Driver"/>
		<property name="url" value="jdbc:mysql://localhost:3306/jdbc"/>
		<property name="username" value="root"/>
		<property name="password" value="root"/>
	</bean>
	<bean class="org.springframework.jdbc.core.JdbcTemplate" name="jdbc">
		<property name="dataSource" ref="ds"/>
	</bean>
    <bean class="com.springjdbc.dao.StudentDaoImpl" id="studentDao">
		<property name="template" ref="jdbc"/>
	</bean>

 </beans>
```
## DAO
```java title="StudentDao.java"
package com.springjdbc.dao;

import java.util.List;

import com.springjdbc.entities.Student;

public interface StudentDao {
public int insert(Student student);
public int update(Student student);
public int delete(int id);
public Student selectId(int id);
public List<Student> selectall();
}

```
```java title="StudentDaoImpl.java"
package com.springjdbc.dao;

import com.springjdbc.entities.Student;
import com.springjdbc.dao.RowMapperImpl;

import java.util.List;

import org.springframework.jdbc.core.JdbcTemplate;

public class StudentDaoImpl implements StudentDao {
	
	JdbcTemplate template;
	public JdbcTemplate getTemplate() {
		return template;
	}

	public void setTemplate(JdbcTemplate template) {
		this.template = template;
	}

	public int insert(Student student) {
		// TODO Auto-generated method stub
		String query="insert into student values(?,?,?)";
		return this.template.update(query,student.getId(),student.getName(),student.getCity());
		
	}

	public int delete(int id) {
		
		String query="delete from student where Id=?";
		return this.template.update(query,id);
	}

	public int update(Student student) {
		String query="update student set name=? ,city=? where Id=?";
		return this.template.update(query,student.getName(),student.getCity(),student.getId());
	}

	public Student selectId(int id) {
		String query="select * from student where Id=?";
		return this.template.queryForObject(query, new RowMapperImpl(),id);
	}

	public List<Student> selectall() {
		String query="select * from student";
		return this.template.query(query, new RowMapperImpl());
	}

}

```
```java title="RowMapperImpl.java"
package com.springjdbc.dao;
import java.sql.ResultSet;
import java.sql.SQLException;
import com.springjdbc.entities.Student;
import org.springframework.jdbc.core.RowMapper;
public class RowMapperImpl implements RowMapper {

	public Student mapRow(ResultSet rs, int rowNum) throws SQLException {
		// TODO Auto-generated method stub
		Student student=new Student();
		student.setId(rs.getInt(1));
		student.setName(rs.getString(2));
		student.setCity(rs.getString(3));
		return student;
	}

}

```
## Entities
```java title="Student.java"
package com.springjdbc.entities;

public class Student {
 private int Id;
 private String name;
 private String city;
public Student() {
	super();
	// TODO Auto-generated constructor stub
}
public Student(int id, String name, String city) {
	super();
	Id = id;
	this.name = name;
	this.city = city;
}
public int getId() {
	return Id;
}
public void setId(int id) {
	Id = id;
}
public String getName() {
	return name;
}
public void setName(String name) {
	this.name = name;
}
public String getCity() {
	return city;
}
public void setCity(String city) {
	this.city = city;
}
@Override
public String toString() {
	StringBuilder builder = new StringBuilder();
	builder.append("Student [Id=");
	builder.append(Id);
	builder.append(", name=");
	builder.append(name);
	builder.append(", city=");
	builder.append(city);
	builder.append("]");
	return builder.toString();
}
 
}

```