# Spring Concepts with Demo
```xml title="pom.xml"
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.psl</groupId>
  <artifactId>spring.a.didemo</artifactId>
  <version>0.0.1-SNAPSHOT</version>

  <name>spring.a.didemo</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
   
	<dependency>
   		 <groupId>org.springframework</groupId>
    		<artifactId>spring-context</artifactId>
    	<version>5.3.25</version>
	</dependency>

<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>5.3.25</version>
</dependency>

  </dependencies>

  <build>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <!-- clean lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#clean_Lifecycle -->
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- default lifecycle, jar packaging: see https://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_jar_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-jar-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
        <!-- site lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#site_Lifecycle -->
        <plugin>
          <artifactId>maven-site-plugin</artifactId>
          <version>3.7.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-project-info-reports-plugin</artifactId>
          <version>3.0.0</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

```
## Java
```java title="App_annotation.java"
package com.psl.spring.a.didemo;

import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

import com.psl.spring.a.didemo.entity.Engine;
import com.psl.spring.a.didemo.entity.Vehicle;

public class App_annotation {
	public static void main( String[] args )
    {
     ApplicationContext context= new AnnotationConfigApplicationContext(BeanConfig.class);
     Engine engine=context.getBean("extraEngine", Engine.class);
     System.out.println(engine);
     Engine commonEngine=context.getBean("commonEngine", Engine.class);
     System.out.println(commonEngine);
     Vehicle v=context.getBean("officePickup", Vehicle.class);
     System.out.println(v);
    }
}

```
```java title="App_autowire.java"
package com.psl.spring.a.didemo;

import org.springframework.beans.BeansException;
import org.springframework.context.support.ClassPathXmlApplicationContext;


import com.psl.spring.a.didemo.entity.Customer;


/**
 * Hello world!
 *
 */

public class App_autowire 
{
    public static void main( String[] args )
    {
     try (ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beanconfig_autowire.xml")) {
    	 System.out.println("Using ByName");
    	 Customer byName=context.getBean("autowireByName", Customer.class);
		 System.out.println(byName);
    	 System.out.println("Using ByType");
    	 Customer byType=context.getBean("autowireByType", Customer.class);
		 System.out.println(byType);
    	 System.out.println("Using Constructor");
    	 Customer byConstructor=context.getBean("autowireByConstructor", Customer.class);
		 System.out.println(byConstructor);
		 
	} catch (BeansException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
     
    }
}

```
```java title="App_cnamespace_inj2.java"
package com.psl.spring.a.didemo;

import org.springframework.context.support.ClassPathXmlApplicationContext;

import com.psl.spring.a.didemo.entity.Engine;
import com.psl.spring.a.didemo.entity.Vehicle;

/**
 * Hello world!
 *
 */
public class App_cnamespace_inj2 
{
    public static void main( String[] args )
    {
     ClassPathXmlApplicationContext context= new ClassPathXmlApplicationContext("beanconfig_cnamespace_inj.xml");
     Engine engine=context.getBean("powerEngine", Engine.class);
     System.out.println(engine);
     Engine commonEngine=context.getBean("commonEngine", Engine.class);
     System.out.println(commonEngine);
     Vehicle v=context.getBean("officePickup", Vehicle.class);
     System.out.println(v);
    }
}

```
```java title="App_constr_inj.java"
package com.psl.spring.a.didemo;

import org.springframework.context.support.ClassPathXmlApplicationContext;

import com.psl.spring.a.didemo.entity.Engine;
import com.psl.spring.a.didemo.entity.Vehicle;

/**
 * Hello world!
 *
 */
public class App_constr_inj 
{
    public static void main( String[] args )
    {
     ClassPathXmlApplicationContext context= new ClassPathXmlApplicationContext("beanconfig_constr_inj.xml");
     Engine engine=context.getBean("powerEngine", Engine.class);
     System.out.println(engine);
     Engine commonEngine=context.getBean("commonEngine", Engine.class);
     System.out.println(commonEngine);
     Vehicle v=context.getBean("officePickup", Vehicle.class);
     System.out.println(v);
    }
}

```
```java title="App_innerbean_inj.java"
package com.psl.spring.a.didemo;

import org.springframework.context.support.ClassPathXmlApplicationContext;

import com.psl.spring.a.didemo.entity.Engine;
import com.psl.spring.a.didemo.entity.Vehicle;

/**
 * Hello world!
 *
 */
public class App_innerbean_inj 
{
    public static void main( String[] args )
    {
     ClassPathXmlApplicationContext context= new ClassPathXmlApplicationContext("beanconfig_pnamespace_inj.xml");
     Engine engine=context.getBean("powerEngine", Engine.class);
     System.out.println(engine);
     Engine commonEngine=context.getBean("commonEngine", Engine.class);
     System.out.println(commonEngine);
     Vehicle v=context.getBean("officePickup", Vehicle.class);
     System.out.println(v);
    }
}

```
```java title="App_lifecycle.java"
package com.psl.spring.a.didemo;

import org.springframework.beans.BeansException;
import org.springframework.context.support.ClassPathXmlApplicationContext;


import com.psl.spring.a.didemo.entity.Lookupt;


/**
 * Hello world!
 *
 */

public class App_lifecycle 
{
    public static void main( String[] args )
    {
     try (ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("beanconfig_lifecycle.xml")) {
		Lookupt lookup=context.getBean("lifeCycle", Lookupt.class);
		 System.out.println(lookup);
		 //it will not call destroy() until we handle context exception 
	} catch (BeansException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
     
    }
}

```
```java title="App_pnamespace_inj.java"
package com.psl.spring.a.didemo;

import org.springframework.context.support.ClassPathXmlApplicationContext;

import com.psl.spring.a.didemo.entity.Engine;
import com.psl.spring.a.didemo.entity.Vehicle;

/**
 * Hello world!
 *
 */
public class App_pnamespace_inj 
{
    public static void main( String[] args )
    {
     ClassPathXmlApplicationContext context= new ClassPathXmlApplicationContext("beanconfig_pnamespace_inj.xml");
     Engine engine=context.getBean("powerEngine", Engine.class);
     System.out.println(engine);
     Engine commonEngine=context.getBean("commonEngine", Engine.class);
     System.out.println(commonEngine);
     Vehicle v=context.getBean("officePickup", Vehicle.class);
     System.out.println(v);
    }
}

```
```java title="App_setter_inj.java"
package com.psl.spring.a.didemo;

import org.springframework.context.support.ClassPathXmlApplicationContext;

import com.psl.spring.a.didemo.entity.Engine;
import com.psl.spring.a.didemo.entity.Vehicle;

/**
 * Hello world!
 *
 */
public class App_setter_inj 
{
    public static void main( String[] args )
    {
     ClassPathXmlApplicationContext context= new ClassPathXmlApplicationContext("beanconfig_setter_inj.xml");
     Engine engine=context.getBean("powerEngine", Engine.class);
     System.out.println(engine);
     Engine commonEngine=context.getBean("commonEngine", Engine.class);
     System.out.println(commonEngine);
     Vehicle v=context.getBean("officePickup", Vehicle.class);
     System.out.println(v);
    }
}

```
### Entity
```java title="Customer.java"
package com.psl.spring.a.didemo.entity;

public class Customer {
private Email officeEmail;
private Email perEmail;
private MobileNumber officeNumber;
public Customer() {
	System.out.println("Customer() called");
}
public Customer(Email officeEmail, MobileNumber officeNumber) {
	this.officeEmail = officeEmail;
	this.officeNumber = officeNumber;
	System.out.println("Customer(email,mobile) called");
}
public Customer(Email perEmail) {
	this.perEmail = perEmail;
	System.out.println("Customer(email) called");
}
public Email getOfficeEmail() {
	return officeEmail;
}
public void setOfficeEmail(Email officeEmail) {
	this.officeEmail = officeEmail;
}
public Email getPerEmail() {
	return perEmail;
}
public void setPerEmail(Email perEmail) {
	this.perEmail = perEmail;
}
public MobileNumber getOfficeNumber() {
	return officeNumber;
}
public void setOfficeNumber(MobileNumber officeNumber) {
	this.officeNumber = officeNumber;
}
@Override
public String toString() {
	StringBuilder builder = new StringBuilder();
	builder.append("Customer [officeEmail=");
	builder.append(officeEmail);
	builder.append(", perEmail=");
	builder.append(perEmail);
	builder.append(", officeNumber=");
	builder.append(officeNumber);
	builder.append("]");
	return builder.toString();
}

}

```
```java title="Email.java"
package com.psl.spring.a.didemo.entity;

public class Email {
private String address;
public Email() {
	
}
public Email(String address) {
	this.address = address;
}

public String getAddress() {
	return address;
}

public void setAddress(String address) {
	this.address = address;
}
public void init() {
	System.out.println("init()");
}
public void destroy() {
	System.out.println("destroy()");
}
}

```
```java title="Engine.java"
package com.psl.spring.a.didemo.entity;

public class Engine {
	private double power;
	private int cylinders;
	public Engine() {
		// TODO Auto-generated constructor stub
	}
	public Engine(double power, int cylinders) {
		this.power=power;
		this.cylinders=cylinders;
	}
	public double getPower() {
		return power;
	}
	public void setPower(double power) {
		this.power = power;
	}
	public int getCylinders() {
		return cylinders;
	}
	public void setCylinders(int cylinders) {
		this.cylinders = cylinders;
	}
	@Override
	public String toString() {
		StringBuilder builder = new StringBuilder();
		builder.append("Engine [power=");
		builder.append(power);
		builder.append(", cylinders=");
		builder.append(cylinders);
		builder.append("]");
		return builder.toString();
	}


}

```
```java title="Lookupt.java"
package com.psl.spring.a.didemo.entity;

public class Lookupt {
private String email;
public Lookupt() {
	
}
public Lookupt(String email) {
	this.email = email;
}
public String getEmail() {
	return email;
}
public void setEmail(String email) {
	this.email = email;
}
public void init() {
	System.out.println("init()");
}
public void destroy() throws Exception {
	System.out.println("destroy()");
}
public void cleanup() {
	System.out.println("cleanup()");
}
@Override
public String toString() {
	StringBuilder builder = new StringBuilder();
	builder.append("Lookupt [email=");
	builder.append(email);
	builder.append("]");
	return builder.toString();
}


}

```
```java title="MobileNumber.java"
package com.psl.spring.a.didemo.entity;

public class MobileNumber {
private String number;
public MobileNumber() {
	
	
}
public String getNumber() {
	return number;
}
public void setNumber(String number) {
	this.number = number;
}
public MobileNumber(String number) {
	this.number = number;
}
public void init() {
	System.out.println("init()");
}
public void destroy() {
	System.out.println("destroy()");
}
}

```
```java title="Vehicle.java"
package com.psl.spring.a.didemo.entity;
import org.springframework.beans.factory.annotation.*;
public class Vehicle {
	private String rtoNumber;
	private int capacity;
	@Autowired (required =false)
	private Engine engine; 
	@Autowired (required=false)
	private Engine extraEngine;
	public String getRtoNumber() {
		return rtoNumber;
	}
	public void setRtoNumber(String rtoNumber) {
		this.rtoNumber = rtoNumber;
	}
	public int getCapacity() {
		return capacity;
	}
	public void setCapacity(int capacity) {
		this.capacity = capacity;
	}
	public Engine getEngine() {
		return engine;
	}
	public void setEngine(Engine engine) {
		this.engine = engine;
	}
	/**
	 * @param rtoNumber
	 * @param capacity
	 * @param engine
	 */
	public Vehicle(String rtoNumber, int capacity, Engine engine) {
		this.rtoNumber = rtoNumber;
		this.capacity = capacity;
		this.engine = engine;
	}
	public Vehicle() {
		// TODO Auto-generated constructor stub
	}
	@Override
	public String toString() {
		StringBuilder builder = new StringBuilder();
		builder.append("Vehicle [rtoNumber=");
		builder.append(rtoNumber);
		builder.append(", capacity=");
		builder.append(capacity);
		builder.append(", engine=");
		builder.append(engine);
		builder.append("]");
		return builder.toString();
	}
	

}

```
### Config
```java title="BeanConfig.java"
package com.psl.spring.a.didemo.config;
import com.psl.spring.a.didemo.entity.*;
import org.springframework.context.annotation.*;
@Configuration
public class BeanConfig {
	@Bean
	public Vehicle vehicle() {
		Vehicle vehicle =new Vehicle();
		return vehicle;
	}
	@Bean(name="engine")
	public Engine getEngine() {
		Engine engine =new Engine(77.7,6);
		return engine;
	}
	@Bean(name="extraEngine")
	public Engine getExtraEngine() {
		Engine engine =new Engine(55.5,9);
		return engine;
	}
}

```
## Resources
```xml title="beanconfig_autowire.xml"
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
 default-init-method="init" default-destroy-method="destroy" default-lazy-init="true">


<bean id="officeEmail" class="com.psl.spring.a.didemo.entity.Email"
p:address="rahul@gmail.com"
/>
<bean id="officeNumber" class="com.psl.spring.a.didemo.entity.MobileNumber"
p:number="8788582604"
/>
<bean id="autowireByName" class="com.psl.spring.a.didemo.entity.Customer"
autowire="byName"
/>
<bean id="autowireByType" class="com.psl.spring.a.didemo.entity.Customer"
autowire="byType"
/>
<bean id="autowireByConstructor" class="com.psl.spring.a.didemo.entity.Customer"
autowire="constructor"
/>





</beans>
```
```xml title="beanconfig_cnamespace_inj.xml"
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:context="http://www.springframework.org/schema/context"
xmlns:p="http://www.springframework.org/schema/p"
xmlns:c="http://www.springframework.org/schema/c"
xsi:schemaLocation="http://www.springframework.org/schema/beans
 http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/context
 http://www.springframework.org/schema/context/spring-context.xsd">

<!-- Bean Visible ENGINE BEAN -->
<bean id="commonEngine" class="com.psl.spring.a.didemo.entity.Engine" c:power="72.5" c:cylinders="4" />
<!-- POWER ENGINE BEAN -->
<bean id="powerEngine" class="com.psl.spring.a.didemo.entity.Engine" c:power="92.5" c:cylinders="6"/>
<!-- OFFICE PICKUP WITH POWER ENGINE BEAN -->
<bean id="officePickup" class="com.psl.spring.a.didemo.entity.Vehicle" c:engine-ref="powerEngine" c:rtoNumber="MH56 AB 1111" c:capacity="3"/>
</beans>


```
```xml title="beanconfig_constr_inj.xml"
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:aop="http://www.springframework.org/schema/aop"
xmlns:context="http://www.springframework.org/schema/context"
xmlns:jee="http://www.springframework.org/schema/jee"
xsi:schemaLocation="http://www.springframework.org/schema/beans 
http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/aop 
http://www.springframework.org/schema/aop/spring-aop-4.3.xsd
 http://www.springframework.org/schema/context 
http://www.springframework.org/schema/context/spring-context-4.3.xsd
 http://www.springframework.org/schema/jee 
http://www.springframework.org/schema/jee/spring-jee-4.3.xsd">

<bean id="powerEngine" class="com.psl.spring.a.didemo.entity.Engine">
	<constructor-arg name="power" value="92.5"/>
	<constructor-arg name="cylinders" value="4"/>
</bean>
<bean id="commonEngine" class="com.psl.spring.a.didemo.entity.Engine">
	<constructor-arg name="power" value="74.5"/>
	<constructor-arg name="cylinders" value="3"/>
</bean>
<bean id="officePickup" class="com.psl.spring.a.didemo.entity.Vehicle">
	<constructor-arg ref="powerEngine"/>
	<constructor-arg name="rtoNumber" value="GA05V3259"/>
	<constructor-arg name="capacity" value="6"></constructor-arg>
	
</bean>
<bean id="commonPickup" class="com.psl.spring.a.didemo.entity.Vehicle">
	<constructor-arg ref="commonEngine"/>
	<constructor-arg name="rtoNumber" value="GA05V6426"/>
	<constructor-arg name="capacity" value="5"></constructor-arg>
	
</bean>




</beans>
```
```xml title="beanconfig_innerbean_inj.xml"
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:aop="http://www.springframework.org/schema/aop"
xmlns:context="http://www.springframework.org/schema/context"
xmlns:jee="http://www.springframework.org/schema/jee"
xsi:schemaLocation="http://www.springframework.org/schema/beans 
http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/aop 
http://www.springframework.org/schema/aop/spring-aop-4.3.xsd
 http://www.springframework.org/schema/context 
http://www.springframework.org/schema/context/spring-context-4.3.xsd
 http://www.springframework.org/schema/jee 
http://www.springframework.org/schema/jee/spring-jee-4.3.xsd">
<!-- COMMON ENGINE BEAN -->
<bean id="commonEngine" class="com.psl.spring.a.didemo.entity.Engine">
 <property name="power" value="72.5" />
 <property name="cylinders" value="4" />
</bean>
<!-- POWER ENGINE BEAN -->
<bean id="powerEngine" class="com.psl.spring.a.didemo.entity.Engine">
 <property name="power" value="92.5" />
 <property name="cylinders" value="6" />
</bean>
<!-- OFFICE PICKUP WITH POWER ENGINE BEAN -->
<bean id="officePickup" class="com.psl.spring.a.didemo.entity.Vehicle">
 <!-- PROPERTY DEFINED BY ATTRIBUTES -->
 <property name="engine">
	 <bean id="economyEngine" class="com.psl.spring.a.didemo.entity.Engine">
 <property name="power" value="32.5" />
 <property name="cylinders" value="3" />
</bean>
 </property>
 <!-- PROPERTY DEFINED BY VALUE TAG -->
 <property name="rtoNumber">
 <value>MH56 AB 1111"</value>
 </property>
 <property name="capacity" value="12" />
</bean>
<!-- COMMON PICKUP WITH COMMON ENGINE BEAN -->
<bean id="commonPickup" class="com.psl.spring.a.didemo.entity.Vehicle">
 <property name = "engine" ref="commonEngine" />
 <property name="rtoNumber" value="MH56 AB 2222" />
 <property name="capacity" value="6"></property>
</bean>
</beans>
```
```xml title="beanconfig_lifecycle.xml"
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
 default-init-method="init" default-destroy-method="destroy">


<bean id="lifeCycle" class="com.psl.spring.a.didemo.entity.Lookupt"
p:email="rahul@gmail.com"
destroy-method="cleanup"/>




</beans>
```
```xml title="beanconfig_pnamespace_inj.xml"
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:context="http://www.springframework.org/schema/context"
xmlns:p="http://www.springframework.org/schema/p"
xmlns:c="http://www.springframework.org/schema/c"
xsi:schemaLocation="http://www.springframework.org/schema/beans
 http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/context
 http://www.springframework.org/schema/context/spring-context.xsd">

<!-- Bean Visible ENGINE BEAN -->
<bean id="commonEngine" class="com.psl.spring.a.didemo.entity.Engine" p:power="72.5" p:cylinders="4" />
<!-- POWER ENGINE BEAN -->
<bean id="powerEngine" class="com.psl.spring.a.didemo.entity.Engine" p:power="92.5" p:cylinders="6"/>
<!-- OFFICE PICKUP WITH POWER ENGINE BEAN -->
<bean id="officePickup" class="com.psl.spring.a.didemo.entity.Vehicle" p:engine-ref="powerEngine" p:rtoNumber="MH56 AB 1111" p:capacity="3"/>
</beans>

```
```xml title="beanconfig_setter_inj.xml"
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:aop="http://www.springframework.org/schema/aop"
xmlns:context="http://www.springframework.org/schema/context"
xmlns:jee="http://www.springframework.org/schema/jee"
xsi:schemaLocation="http://www.springframework.org/schema/beans 
http://www.springframework.org/schema/beans/spring-beans.xsd
 http://www.springframework.org/schema/aop 
http://www.springframework.org/schema/aop/spring-aop-4.3.xsd
 http://www.springframework.org/schema/context 
http://www.springframework.org/schema/context/spring-context-4.3.xsd
 http://www.springframework.org/schema/jee 
http://www.springframework.org/schema/jee/spring-jee-4.3.xsd">
<!-- Bean Visible ENGINE BEAN -->
<bean id="commonEngine" class="com.psl.spring.a.didemo.entity.Engine">
 <property name="power" value="72.5" />
 <property name="cylinders" value="4" />
</bean>
<!-- POWER ENGINE BEAN -->
<bean id="powerEngine" class="com.psl.spring.a.didemo.entity.Engine">
 <property name="power" value="92.5" />
 <property name="cylinders" value="6" />
</bean>
<!-- OFFICE PICKUP WITH POWER ENGINE BEAN -->
<bean id="officePickup" class="com.psl.spring.a.didemo.entity.Vehicle">
 <!-- PROPERTY DEFINED BY ATTRIBUTES -->
 <property name="engine">
	 <bean id="economyEngine" class="com.psl.spring.a.didemo.entity.Engine">
 <property name="power" value="32.5" />
 <property name="cylinders" value="3" />
</bean>
 </property>
 <!-- PROPERTY DEFINED BY VALUE TAG -->
 <property name="rtoNumber">
 <value>MH56 AB 1111"</value>
 </property>
 <property name="capacity" value="12" />
</bean>
<!-- COMMON PICKUP WITH COMMON ENGINE BEAN -->
<bean id="commonPickup" class="com.psl.spring.a.didemo.entity.Vehicle">
 <property name = "engine" ref="commonEngine" />
 <property name="rtoNumber" value="MH56 AB 2222" />
 <property name="capacity" value="6"></property>
</bean>
</beans>
```