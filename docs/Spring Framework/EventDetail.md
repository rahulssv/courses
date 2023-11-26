# Event Detail Application


```xml title="pom.xml"
   <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.spring</groupId>
	<artifactId>eventDetail</artifactId>
	<packaging>war</packaging>
	<version>0.0.1-SNAPSHOT</version>	
	<url>http://maven.apache.org</url>
	<properties>
		<failOnMissingWebXml>false</failOnMissingWebXml>
		<spring.version>5.1.0.RELEASE</spring.version>
		<hibernate.version>5.2.17.Final</hibernate.version>
		<hibernate.validator>5.4.1.Final</hibernate.validator>
		<c3p0.version>0.9.5.2</c3p0.version>
		<jstl.version>1.2.1</jstl.version>
		<tld.version>1.1.2</tld.version>
		<servlets.version>3.1.0</servlets.version>
		<jsp.version>2.3.1</jsp.version>
		<log4j.version>1.2.17</log4j.version>
	</properties>
	<dependencies>

		<!-- Spring MVC Dependency -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc</artifactId>
			<version>${spring.version}</version>
			<exclusions>
				<exclusion>
					<groupId>commons-logging</groupId>
					<artifactId>commons-logging</artifactId>
				</exclusion>
			</exclusions>
		</dependency>

		<!-- Spring ORM -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-orm</artifactId>
			<version>${spring.version}</version>
		</dependency>

		<dependency>
			<groupId>org.hibernate</groupId>
			<artifactId>hibernate-entitymanager</artifactId>
			<version>${hibernate.version}</version>
		</dependency>

		<!-- Hibernate Validator -->
		<dependency>
			<groupId>org.hibernate</groupId>
			<artifactId>hibernate-validator</artifactId>
			<version>${hibernate.validator}</version>
		</dependency>

		<!-- https://mvnrepository.com/artifact/org.springframework.data/spring-data-jpa -->
		<dependency>
			<groupId>org.springframework.data</groupId>
			<artifactId>spring-data-jpa</artifactId>
			<version>2.1.0.RELEASE</version>
		</dependency>

		<!-- JSTL Dependency -->
		<dependency>
			<groupId>javax.servlet.jsp.jstl</groupId>
			<artifactId>javax.servlet.jsp.jstl-api</artifactId>
			<version>${jstl.version}</version>
		</dependency>

		<dependency>
			<groupId>taglibs</groupId>
			<artifactId>standard</artifactId>
			<version>${tld.version}</version>
		</dependency>

		<!-- Servlet Dependency -->
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>javax.servlet-api</artifactId>
			<version>${servlets.version}</version>
			<scope>provided</scope>
		</dependency>

		<!-- JSP Dependency -->
		<dependency>
			<groupId>javax.servlet.jsp</groupId>
			<artifactId>javax.servlet.jsp-api</artifactId>
			<version>${jsp.version}</version>
			<scope>provided</scope>
		</dependency>

		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>5.1.47</version>
		</dependency>

		<!-- logging -->
		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>jcl-over-slf4j</artifactId>
			<version>1.7.20</version>
		</dependency>
		<dependency>
			<groupId>ch.qos.logback</groupId>
			<artifactId>logback-classic</artifactId>
			<version>1.1.7</version>
		</dependency>

		<dependency>
			<groupId>org.apache.tomcat.maven</groupId>
			<artifactId>tomcat7-maven-plugin</artifactId>
			<version>2.2</version>
			<scope>provided</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-war-plugin</artifactId>
				<version>2.3</version>
				<configuration>
					<warSourceDirectory>src/main/webapp</warSourceDirectory>
				</configuration>
			</plugin>

			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>3.1</version>
				<configuration>
					<source>1.8</source>
					<target>1.8</target>
				</configuration>
			</plugin>
			<plugin>
				<groupId>org.apache.tomcat.maven</groupId>
				<artifactId>tomcat7-maven-plugin</artifactId>
				<version>2.2</version>

				<configuration>
					<path>/</path>
				</configuration>
			</plugin>
		</plugins>
	</build>
</project>

```
```java title="Main.java"

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.logging.Level;
import java.util.logging.Logger;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import com.spring.dao.EventDAO;
import com.spring.entity.Event;
import com.spring.service.EventService;
import java.util.Scanner;

public class Main {

	public static void main(String[] args) throws NumberFormatException, IOException {
		Logger log = Logger.getLogger("org.hibernate");
		log.setLevel(Level.OFF);
		System.setProperty("org.apache.commons.logging.Log", "org.apache.commons.logging.impl.NoOpLog");
		Scanner input = new Scanner(System.in).useDelimiter("\\s*[\\n]\\s*");
		// BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
		// Fill your code here
		ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
		EventDAO enentservice = context.getBean("eventDAO", EventDAO.class);
		System.out.println("Before inserting");
		System.out.printf("%-15s%-15s%-15s%-15s%-15s%-15s\n", "Id", "Event Name", "Organiser Name", "Organiser Number","Hall Name","Location");
		for (Event event : enentservice.getAllEvents()) {
			System.out.printf("%-15s%-15s%-15s%-15s%-15s%-15s\n", event.getId(), event.getEventName(), event.getOrganiser(), event.getOrganiserNumber(),event.getHallName(),event.getLocation());

		}
		System.out.println("Enter the id of the Event :");
		int id = input.nextInt();
		try {
			Event event1 = enentservice.getEventById(id);
			event1.getId();
			System.out.println("Invalid id");
			System.exit(0);
		}catch(Exception e) {


			System.out.println("Enter the name of the Event : ");
			String eventName = input.next();
			System.out.println("Enter the Organiser name :");
			String organiserName = input.next();
			System.out.println("Enter the organiser number :");
			String organiserNumber = input.next();
			System.out.println("Enter the Hall name :");
			String hallName = input.next();
			System.out.println("Enter the location :");
			String location = input.next();
			enentservice.createEvent(id, eventName, organiserName, organiserNumber, hallName, location);
			System.out.println("Value inserted successfully");
			System.out.println("After insertion");
			System.out.printf("%-15s%-15s%-15s%-15s%-15s%-15s\n", "Id", "Event Name", "Organiser Name", "Organiser Number","Hall Name","Location");
			for (Event event : enentservice.getAllEvents()) {
				System.out.printf("%-15s%-15s%-15s%-15s%-15s%-15s\n", event.getId(), event.getEventName(), event.getOrganiser(), event.getOrganiserNumber(),event.getHallName(),event.getLocation());

			}
			// }
			// else {
			// System.out.println("Invalid id");
			// }

			System.exit(0);

			
		}
		
		
	}
}
```
## Configuration
```xml title="applicationContext.xml"
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="
           http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans-3.1.xsd
           http://www.springframework.org/schema/context
           http://www.springframework.org/schema/context/spring-context-3.1.xsd">
           
<context:annotation-config/>
<context:component-scan base-package="com.spring"/>
<context:property-placeholder location="classpath:oracle.properties"/>	

<!-- 
<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">  
<property name="driverClassName" value="oracle.jdbc.driver.OracleDriver" />  
<property name="url" value="${db.url}" />  
<property name="username" value="${db.username}" />  
<property name="password" value="${db.password}" />  
</bean>  
 -->  
<bean class="org.springframework.jdbc.datasource.DriverManagerDataSource" id="dataSource">
		<property name="driverClassName" value="com.mysql.jdbc.Driver"/>
		<property name="url" value="jdbc:mysql://localhost:3306/jdbc"/>
		<property name="username" value="root"/>
		<property name="password" value="root"/>
	</bean>

<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">  
<property name="dataSource" ref="dataSource"></property>  
</bean>

<bean id="eventDAO" class="com.spring.dao.EventDAO">
<property name="template" ref="jdbcTemplate"/></bean>
</beans>   
```
## Service
```java title="EventService.java"
package com.spring.service;
import com.spring.dao.EventDAO;
import com.spring.entity.*;
import java.sql.ResultSet;
import java.sql.Types;
import java.sql.SQLException;
import java.util.List;

import javax.sql.DataSource;
import org.springframework.dao.DuplicateKeyException;
import org.springframework.dao.EmptyResultDataAccessException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.ResultSetExtractor;
import org.springframework.jdbc.core.RowMapper;
import org.springframework.stereotype.Service;
//Fill your code here
@Service
public class EventService {
		@Autowired
    	EventDAO eventdao;
        public EventService(EventDAO eventdao) {
			super();
			this.eventdao = eventdao;
		}
		//Fill your code here
        
	public EventService() {
			super();
			// TODO Auto-generated constructor stub
		}
	public List<Event> getAllEvents(){
		//fill your code
		
        return this.eventdao.getAllEvents();
		 
    }
    public Event getEventById(int id){
    	  //Fill your code here
    	return this.eventdao.getEventById(id);
    }
    
	public void createEvent(int id,String eventName,String organiser,String organiserNumber,String hallName, String location) {
	  
	    //Fill your code here
        this.eventdao.createEvent(id, eventName, organiser, organiserNumber, hallName, location);

	}           
    }

```
## DAO
```java title="EventDAO.java"
package com.spring.dao;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import com.spring.entity.Event;
import java.sql.ResultSet;
import java.sql.Types;
import java.sql.SQLException;
import java.util.List;
import javax.sql.DataSource;

import org.springframework.dao.DataAccessException;
import org.springframework.dao.DuplicateKeyException;
import org.springframework.dao.EmptyResultDataAccessException;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.ResultSetExtractor;
import org.springframework.jdbc.core.RowMapper;
import org.springframework.stereotype.Component;
import org.springframework.stereotype.Repository;
//Fill your code here

public class EventDAO {
    
    //Fill your code here
	JdbcTemplate template;

	public JdbcTemplate getTemplate() {
		return template;
	}

	public void setTemplate(JdbcTemplate template) {
		this.template = template;
	}

	public EventDAO(JdbcTemplate template) {
		super();
		this.template = template;
	}

	public EventDAO() {
		super();
		// TODO Auto-generated constructor stub
	}
  
	public List<Event> getAllEvents(){
		//fill your code
		String query="select * from event";
		return this.template.query(query, new RowMapper<Event>() {

			@Override
			public Event mapRow(ResultSet rs, int rowNum) throws SQLException {
				// TODO Auto-generated method stub
				Event event=new Event();
				event.setId(rs.getInt("id"));
				event.setEventName(rs.getString("event_name"));
				event.setOrganiser(rs.getString("organiser"));
				event.setOrganiserNumber(rs.getString("organiser_number"));
				event.setHallName(rs.getString("hall_name"));
				event.setLocation(rs.getString("location"));
				return event;
			}
			
		});
		 
    }
    
    public Event getEventById(int id){
    	  //Fill your code here
    	String query="select * from event where id="+id;
    	return this.template.query(query, new ResultSetExtractor<Event>() {

			@Override
			public Event extractData(ResultSet rs) throws SQLException, DataAccessException {
				// TODO Auto-generated method stub
				if(rs.next()) {
					Event event=new Event();
					event.setId(rs.getInt("id"));
					event.setEventName(rs.getString("event_name"));
					event.setOrganiserNumber(rs.getString("organiser_number"));
					event.setOrganiserNumber("organiser_number");
					event.setHallName(rs.getString("hall_name"));
					event.setLocation(rs.getString("location"));
					return event;
				}
				return null;
			}
    		
    	});
        
        
    }
    
	public void createEvent(int id,String eventName,String organiser,String organiserNumber,String hallName, String location) {
		String query="INSERT INTO event (id, event_name, organiser, organiser_number, hall_name, location) VALUES (?,?,?,?,?,?)";
	    //Fill your code here
		 this.template.update(query,id,eventName,organiser,organiserNumber,hallName,location);

	}           
    }
/*
 * 
 * public List<Event> getAllEvents(){
		//fill your code
		String query="select * from event";
		return this.template.query(query, new RowMapperImpl());
		 
    }
    
    public Event getEventById(int id){
    	  //Fill your code here
    	String query="select * from event where id=?";
    	return (Event) this.template.queryForObject(query, new RowMapperImpl(), id);
        
        
    }
    
	public void createEvent(int id,String eventName,String organiser,String organiserNumber,String hallName, String location) {
		String query="INSERT INTO event (id, event_name, organiser, organiser_number, hall_name, location) VALUES (?,?,?,?,?,?)";
	    //Fill your code here
		 this.template.update(query,id,eventName,organiser,organiserNumber,hallName,location);

	}  
 * 
 * 
 * 
 * 
 * 
 * */

```
## Entity
```java title="Event.java"
package com.spring.entity;


public class Event {

    private int id;
    private String eventName;
    private String organiser;
    private String organiserNumber;
    private String hallName;
    private String location;
    
    public int getId() {
    	return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getEventName() {
		return eventName;
	}
	public void setEventName(String eventName) {
		this.eventName = eventName;
	}
	public String getOrganiser() {
		return organiser;
	}
	public void setOrganiser(String organiser) {
		this.organiser = organiser;
	}
	public String getOrganiserNumber() {
		return organiserNumber;
	}
	public void setOrganiserNumber(String organiserNumber) {
		this.organiserNumber = organiserNumber;
	}
	public String getHallName() {
		return hallName;
	}
	public void setHallName(String hallName) {
		this.hallName = hallName;
	}

	public String getLocation() {
		return location;
	}
	public void setLocation(String location) {
		this.location = location;
	}


	public Event() {}
	
	public Event(int id,String eventName,String organiser,String organiserNumber,String hallName, String location) {
	   this.id = id;
	   this.eventName = eventName;
        this.organiser = organiser;
        this.organiserNumber = organiserNumber;
        this.hallName = hallName;
	   this.location = location;
		
	}

}

```
## Resources
```py title="oracle.properties"
db.url = jdbc:oracle:thin:@localhost:1521:xe
db.username = root
db.password = student

```
```sql title="queries.sql"
Begin
   execute immediate 'Drop table event';
EXCEPTION
   WHEN OTHERS THEN NULL;
END;
/

create table event(id number(19) primary key,event_name varchar2(255),organiser varchar2(255),organiser_number varchar2(255),hall_name varchar2(255),location varchar2(255), primary key(id));

-- Generate ID using sequence and trigger
drop sequence event_seq;
create sequence event_seq start with 1 increment by 1;

create or replace trigger event_seq_tr
 before insert on event for each row
 when (new.id is null)
begin
 select event_seq.nextval into :new.id from dual;
end;
/

INSERT INTO event (id, event_name, organiser, organiser_number, hall_name, location) VALUES (1,'Birthday Party','Robert','7894561230', 'RR Hall', 'Washington');
INSERT INTO event (id, event_name, organiser, organiser_number, hall_name, location) VALUES (2,'Sports Ceremony','William','7894567890', 'KK Mahal','San Fransisco');
INSERT INTO event (id, event_name, organiser, organiser_number, hall_name, location) VALUES (3,'Home Fest','Jessy','968520147', 'Golden Mahal', 'Chicago');
INSERT INTO event (id, event_name, organiser, organiser_number, hall_name, location) VALUES (4,'Wedding Event','Peter','8523697410', 'PKR Mahal', 'New York');
INSERT INTO event (id, event_name, organiser, organiser_number, hall_name, location) VALUES (5,'Roto Fest','Stuart','9874563201', 'Hills Party Hall', 'Paris');

```