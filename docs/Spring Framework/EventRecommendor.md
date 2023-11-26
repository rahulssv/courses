# Event Recommendor Application
Event Recommendor
[Note:  Strictly adhere to the object-oriented specifications given as a part of the problem statement.
Follow the naming conventions as mentioned.  Create separate classes in separate files.]  
 
Just as Vimal completed his work, his friend Ruby comes up with another idea. She tells him to create an event recommendor. The event recommendor, gets the budget the user can spend on entertainment and recommends the event based on that.
 
Can you assist Vimal in this?
 
Class Event has been created with the following attributes/variables
DataType	Variable
String	eventName
String	eventOrganiser
Double	fare
 
Appropriate getters, setters and parametrized constructor has been created for you.
 
The above class also contains the following methods
Method	Description
display()	This methids displays the details of that particular event.

Class EventList has been created with the following attribute/varible
DataType	Variable
ArrayList<Event>	eventMenu

The class contains the following methods to implement
Method	Description
public void insert(Event event) 	Inserts the event object in the eventMenu arrayList
public ArrayList<String> recommendfor(Double budget)	
This method creates a string of the format <name_of_the_event>-<numbe_of_tickets>. Then the string is added to returned arrayList.
For eg., Puppet Show-2
 
Create an applicationContext.xml file with the following beans
id=event1
eventName=Magic Show
eventOrganiser=Vadivel
fare=650
 
id=event2
eventName=Puppet Show
eventOrganiser=Maggie
fare=250
 
id=event3
eventName=Standup Comedy
eventOrganiser=Arun
fare=500
 
Hint :
To prevent logging info, include these lines in your Main 
Logger log = Logger.getLogger("org.hibernate");
log.setLevel(Level.OFF);
System.setProperty("org.apache.commons.logging.Log", "org.apache.commons.logging.impl.NoOpLog");
 
In the main method, create get the references for the event objects and insert them into the eventMenu of EventList class.
Get the budget from the user.Using the EventList object call the recommendfor(Double budget) method. Iterate through the recommendation strings and print the same.

Jars for spring are available in this link – Spring Jars
Input and Output Format   
Refer sample input and output for formatting specifications.   
All text in bold corresponds to the input and the rest corresponds to output.   

Sample Input and Output 1:  

Enter your Budget
100
No Shows available

Sample Input and Output 2:
Enter your Budget
1000
Magic Show-1
Puppet Show-4
Standup Comedy-2

```xml title="pom.xml"
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

	<groupId>com</groupId>
	<artifactId>eventRecommendor</artifactId>
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
import java.util.ArrayList;
import java.util.logging.Level;
import java.util.logging.Logger;
import java.util.Scanner;

import org.springframework.beans.BeansException;

import org.springframework.context.support.ClassPathXmlApplicationContext;

import com.spring.Event;
import com.spring.EventList;

public class Main {

	public static void main(String[] args) {
		Logger log = Logger.getLogger("org.hibernate");
		log.setLevel(Level.OFF);
		System.setProperty("org.apache.commons.logging.Log", "org.apache.commons.logging.impl.NoOpLog");
	
		ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
			EventList list= new EventList();
			list.insert(context.getBean("event1",Event.class));
			list.insert(context.getBean("event2",Event.class));
			list.insert(context.getBean("event3",Event.class));
			
			System.out.println("Enter your Budget");
			Scanner input = new Scanner(System.in);
				double budget = input.nextDouble();
				ArrayList<String> recommendfor=list.recommendfor(budget);
			
				if(recommendfor.size()==0) {
					System.out.println("No Shows available");
				}
				else {
					for(String recommend:recommendfor) {
						System.out.println(recommend);
					}
				}
				input.close();
		
	}

}
```
## Configuration
```xml title="applicationContext.xml"
<!DOCTYPE beans PUBLIC "-//SPRING//DTD BEAN 2.0//EN"
        "http://www.springframework.org/dtd/spring-beans-2.0.dtd">

<beans>
	
	<bean id="event1" class="com.spring.Event">
                <property name="eventName" value="Magic Show"/>
                <property name="eventOrganiser" value="Vadivel"/>
                <property name="fare" value="650"/>
        </bean>
        <bean id="event2" class="com.spring.Event">
                <property name="eventName" value="Puppet Show"/>
                <property name="eventOrganiser" value="Maggie"/>
                <property name="fare" value="250"/>
        </bean>
        <bean id="event3" class="com.spring.Event">
                <property name="eventName" value="Standup Comedy"/>
                <property name="eventOrganiser" value="Arun"/>
                <property name="fare" value="500"/>
        </bean>
</beans>

```
## Model
```java title="Event.java"
package com.spring;

public class Event {
	String eventName;
	String eventOrganiser;
	Double fare;
	public Event() {
		
	}
	public Event(String eventName, String eventOrganiser, Double fare) {
		this.eventName = eventName;
		this.eventOrganiser = eventOrganiser;
		this.fare = fare;
	}
	public String getEventName() {
		return eventName;
	}
	public void setEventName(String eventName) {
		this.eventName = eventName;
	}
	public String getEventOrganiser() {
		return eventOrganiser;
	}
	public void setEventOrganiser(String eventOrganiser) {
		this.eventOrganiser = eventOrganiser;
	}
	public Double getFare() {
		return fare;
	}
	public void setFare(Double fare) {
		this.fare = fare;
	}
	public void display() {
		//Fill your code here
	}
	
}

```
```java title="EventList.java"
package com.spring;

import java.util.ArrayList;

public class EventList {

	public ArrayList<Event> eventMenu = new ArrayList<>();
	public EventList() {
		
	}
	public EventList(ArrayList<Event> eventMenu) {
		this.eventMenu = eventMenu;
	}
	public void insert(Event event) {
		//Fill your code here
		this.eventMenu.add(event);
	}
	public ArrayList<String> recommendfor(Double budget){
		//Fill your code here
		ArrayList<String> recommendfor=new ArrayList<>();
		int numberOfTickets=0;
		for(Event element: eventMenu) {
			numberOfTickets=(int)(budget/element.getFare());
			if(numberOfTickets>0)
				recommendfor.add(element.getEventName()+"-"+numberOfTickets);
			
		}
	
		return recommendfor;
	}
	

}

```