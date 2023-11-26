# Scope Games 
Scope Games- 1
Note: Strictly adhere to the object-oriented specifications given as a part of the problem statement.
Follow the naming conventions as mentioned.  Create separate classes in separate files.
Vimal is learning about bean scopes. He decides to create an application that asks the number of owners to create and the number of events to create. When the owner or event is created, print the message "...Creating an owner..." or "...Creating an event..."
Let us help him
 
Class Event has been created with the follwing attributes/variables
Data Type	Variable
int				id
String	eventName
Owner	eventOrganiser
 
Appropriate getters, setters and parametrized constructor has been created for you.
Include a default argument constructor to print out "...Creating an event..."
 
Class Owner has been created with the following attributes/variables
Data Type	Variable
String	name
String	password
 
Appropriate getters, setters and parametrized constructor has been created for you.
Include a default argument constructor to print out "...Creating an owner..."
 
Create an applicationContext.xml file and mention the required scopes
 
 
 
Hint:
Include these following lines to prevent logging :
Logger log = Logger.getLogger("org.hibernate");
log.setLevel(Level.OFF);
System.setProperty("org.apache.commons.logging.Log", "org.apache.commons.logging.impl.NoOpLog");
 
In the main method get the number of owners , events , ownerdetails and eventdetails and set them. Pass the owner object to the
eventOrganiser attribute , based on user's choice.
(Refer sample input and output for the details).
Jars for spring are available in this link – Spring Jars
 
Input and Output Format     
Refer sample input and output for formatting specifications.     
All text in bold corresponds to the input and the rest corresponds to output.     


Sample Input and Output :    
 
Enter the number of owners you want to create
2
...Creating an owner...
Enter the Name and Password of the Owner
Cersei
cersei312
...Creating an owner...
Enter the Name and Password of the Owner
Jaime
jaime1234
Enter the number of events you want to create
2
...Creating a new event...
Enter the  Event name
Red wedding
Select any option from the list and enter the number
1)Cersei
2)Jaime
Enter the choice
1
...Creating a new event...
Enter the  Event name
Duel
Select any option from the list and enter the number
1)Cersei
2)Jaime
Enter the choice
2
...Listing events...
1)Red wedding - Cersei
2)Duel - Jaime
 
```xml title="pom.xml"
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

	<groupId>com</groupId>
	<artifactId>scopeGames</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>pci</name>
	<url>http://maven.apache.org</url>

	<properties>
		<java.version>1.8</java.version>
	</properties>

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.4.2.RELEASE</version>
	</parent>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<!-- https://mvnrepository.com/artifact/org.json/json -->
	   <dependency>
    		<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
			<!--<scope>provided</scope> -->
		</dependency>
        <dependency>
    		<groupId>org.easymock</groupId>
			<artifactId>easymock</artifactId>
			<version>3.1</version>
			<scope>test</scope>
		</dependency>
        <dependency>
    		<groupId>com.google.code.gson</groupId>
			<artifactId>gson</artifactId>
		</dependency>

		<dependency>
		    <groupId>org.json</groupId>
		    <artifactId>json</artifactId>
		</dependency>

		<dependency>
			<groupId>org.apache.httpcomponents</groupId>
			<artifactId>httpclient</artifactId>
		</dependency>
		<dependency>
    		<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.12</version>
		</dependency>
		<dependency>
		    <groupId>org.springframework</groupId>
		    <artifactId>spring-test</artifactId>
		    <version>4.0.5.RELEASE</version>
		    <scope>test</scope>
		</dependency>
		 <dependency>
		 	<groupId>org.springframework.boot</groupId>
  			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
        <dependency>
    		<groupId>org.springframework</groupId>
			<artifactId>spring-test</artifactId>
			<scope>test</scope>
		</dependency>
        <dependency>
    	    <groupId>org.seleniumhq.selenium</groupId>
		    <artifactId>selenium-java</artifactId>
		</dependency>
        
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>

```
```java title="Main.java"



import com.spring.*;
import java.util.ArrayList;

import java.util.logging.Level;
import java.util.logging.Logger;
import java.util.Scanner;

import org.springframework.context.support.ClassPathXmlApplicationContext;


public class Main {

	public static void main(String[] args) {
		Logger log = Logger.getLogger("org.hibernate");
		log.setLevel(Level.OFF);
		System.setProperty("org.apache.commons.logging.Log", "org.apache.commons.logging.impl.NoOpLog");
		Scanner input=new Scanner(System.in).useDelimiter("\\s*[\\n]\\s*");
		ClassPathXmlApplicationContext context=new ClassPathXmlApplicationContext("applicationContext.xml");
	
		System.out.println("Enter the number of owners you want to create");
		int numberOfOwners=input.nextInt();
		ArrayList<Owner> addOwner=new ArrayList<>();
		for(int i=1;i<=numberOfOwners;i++) {
			
			Owner owner= new Owner();
			
			System.out.println("Enter the Name and Password of the Owner");
			String name=input.next();
			String password=input.next();
			
			
			owner.setName(name);
			owner.setPassword(password);
			addOwner.add(owner);
			
		}
	
		System.out.println("Enter the number of events you want to create");
		int numberOfEvents=input.nextInt();
		ArrayList<Event> addEvent=new ArrayList<>();
		for(int j=1;j<=numberOfEvents;j++) {
	
			Event event=new Event();
			System.out.println("Enter the  Event name");
			String Ename=input.next();
			System.out.println("Select any option from the list and enter the number");

			int k=1;
			for(Owner own:addOwner) {
				System.out.println(k+")"+(own).getName());
				k++;
			}
			System.out.println("Enter the choice");
			int choice=input.nextInt();
			event.setId(j);
			event.setEventName(Ename);
			event.setEventOrganiser(addOwner.get(choice-1));
			addEvent.add(event);
		}
		
		
		System.out.println("...Listing events...");
		for(Event eventt:addEvent) {
			System.out.println((eventt).getId() +")"+(eventt).getEventName()+" - "+(eventt).getEventOrganiser().getName());

		}

		
		input.close();
		
	}
	
	

}

```
## Entities
```java title="Event.java"
package com.spring;

public class Event {

	int id;
	String eventName;
	Owner eventOrganiser;

	public Event() {
		System.out.println("...Creating a new event...");
	}

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

	public Owner getEventOrganiser() {
		return eventOrganiser;
	}

	public void setEventOrganiser(Owner eventOrganiser) {
		this.eventOrganiser = eventOrganiser;
	}

	public void display() {

	}

	public void setProperties(String eventName) {
		this.setEventName(eventName);

	}

}

```
```java title="Owner.java"
package com.spring;

public class Owner {
	public Owner() {
		System.out.println("...Creating an owner...");
	}
	public Owner(String name, String password) {
		this.name = name;
		this.password = password;
	}

	String name;
	String password;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getPassword() {
		return password;
	}

	public void setPassword(String password) {
		this.password = password;
	}

}

```
## Resources
```xml title="applicationContext.xml"
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans 
    http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- No bean definitions needed here since they will be created dynamically -->
  <bean class="com.spring.Owner">
	  
  </bean>
  <bean class="com.spring.Event">
	  
  </bean>
</beans>
```