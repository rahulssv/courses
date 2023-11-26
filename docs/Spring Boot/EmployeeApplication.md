# Employee Application

```java title="Application.java"
package com.psl;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}

}


```
## Controller
```java title="springController.java"
package com.psl.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.psl.entity.Employee;
import com.psl.service.EmployeeServiceImpl;

import io.swagger.v3.oas.annotations.Hidden;

@RestController
public class springController {
	@Autowired
	EmployeeServiceImpl empService;
	public springController() {
		// TODO Auto-generated constructor stub

	}
	@PostMapping("/employee")
	@Hidden
	public Employee addEmployee(@RequestBody Employee e) {
		return empService.addEmployee(e);
	}
	@GetMapping("/employee/{id}")
	public Employee getEmployeeById(@PathVariable int id) {
		return empService.getEmployeeById(id);
	}
	@GetMapping("/employee")
	public List<Employee> getAllEmployee(@RequestBody Employee e) {
		return empService.getAllEmployee(e);
	}
	@PutMapping("/employee")
	public Employee updateEmployee(@RequestBody Employee e) {
		return empService.updateEmployee(e);
	}
	@DeleteMapping("/employee/{id}")
	public void deleteEmployee(@PathVariable int id) {
		empService.deleteEmployee(id);
	}
	@GetMapping("/employee/name/{name}")
	public List<Employee> getEmployeeByName(@PathVariable String name) {
		// TODO Auto-generated method stub
		return empService.getEmployeeByName(name);
	}

	@GetMapping("/employee/tech/{name}")
	public List<Employee> getEmployeeByNameAndTech(@PathVariable String name, @RequestParam String tech) {
		// TODO Auto-generated method stub
		return empService.getEmployeeByNameAndTech(name, tech);
	}
}

```
## Service
```java title="EmployeeService.java"
package com.psl.service;

import java.util.List;

import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestBody;

import com.psl.entity.Employee;

public interface EmployeeService {
	 public Employee addEmployee(Employee e);
	 public Employee getEmployeeById(int id);
	 public List<Employee> getEmployeeByName(String name);
	 public List<Employee> getEmployeeByNameAndTech(String name, String Tech);
	 public List<Employee> getAllEmployee(Employee e);
	 public Employee updateEmployee(Employee e);
	 public void deleteEmployee(int id);
}

```
```java title="EmployeeServiceImpl.java"
package com.psl.service;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.psl.entity.Employee;
import com.psl.repository.EmployeeRepository;

@Service
public class EmployeeServiceImpl implements EmployeeService {
	@Autowired
	EmployeeRepository repo;
	public EmployeeServiceImpl() {
		// TODO Auto-generated constructor stub
	}

	@Override
	public Employee addEmployee(Employee e) {
		// TODO Auto-generated method stub
		return repo.save(e);
	}

	@Override
	public Employee getEmployeeById(int id) {
		// TODO Auto-generated method stub
		return repo.findById(id).get();
	}

	@Override
	public List<Employee> getAllEmployee(Employee e) {
		// TODO Auto-generated method stub
		return (List<Employee>) repo.findAll();
	}

	@Override
	public Employee updateEmployee(Employee e) {
		// TODO Auto-generated method stub
		return repo.save(e);
	}

	@Override
	public void deleteEmployee(int id) {
		// TODO Auto-generated method stub
		repo.deleteById(id);		
	}

	@Override
	public List<Employee> getEmployeeByName(String name) {
		// TODO Auto-generated method stub
		return repo.findEmployeeByName(name);
	}

	@Override
	public List<Employee> getEmployeeByNameAndTech(String name, String tech) {
		// TODO Auto-generated method stub
		return repo.findEmployeeByNameAndTechJpql(name, tech);
	}

}


```
## Repository
```java title="EmployeeRepository.java"
package com.psl.repository;

import java.util.List;

import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.CrudRepository;
import org.springframework.data.repository.query.Param;

import com.psl.entity.Employee;

public interface EmployeeRepository extends CrudRepository<Employee, Integer> {
	@Query("Select e from Employee e where e.name=?1")
	List<Employee> findEmployeeByNameJpql(String name);
	@Query(value="Select * from employee where name=?1", nativeQuery=true )
	List<Employee> findEmployeeByName(String name);
	@Query("Select e from Employee e where e.name=:name" )
	List<Employee> findEmployeeByNameParam(@Param("name")String name);
	
	@Query("Select e from Employee e where e.name=?1 and e.tech=?2")
	List<Employee> findEmployeeByNameAndTechJpql(String name, String tech);
	@Query(value="Select * from employee where name=?1 and tech=?2", nativeQuery=true )
	List<Employee> findEmployeeByNameAndTech(String name, String tech);
	@Query(value="Select * from employee where name=:name and tech=:tech", nativeQuery=true )
	List<Employee> findEmployeeByNameAndTechParam(@Param("name")String name,@Param("tech") String tech);

}

```
## Domain
```java title="Employee.java"
package com.psl.entity;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class Employee {
	@Id
	@GeneratedValue(strategy = GenerationType.AUTO)
	private int id;
	private String name;
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getTech() {
		return tech;
	}
	public void setTech(String tech) {
		this.tech = tech;
	}
	public Employee(int id, String name, String tech) {
		super();
		this.id = id;
		this.name = name;
		this.tech = tech;
	}
	private String tech;
	public Employee() {
		// TODO Auto-generated constructor stub
	}

}

```
## Resorces
```py title="application.properties"
#Don't remove the content below
#####DB_CONFIG_START#####
spring.datasource.url = jdbc:mysql://localhost:3306/empDatabase
spring.datasource.username = springuser
spring.datasource.password = password
#####DB_CONFIG_END#####
#Don't remove the content above
spring.datasource.driver-class-name = com.mysql.jdbc.Driver
spring.jpa.database-platform = org.hibernate.dialect.MySQL5Dialect
spring.jpa.generate-ddl = true
spring.jpa.hibernate.ddl-auto = update
server.port = 8090

```
