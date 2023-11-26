# Covid Application

```java title="CovidApplication.java"
package com.covid.jpa;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class CovidApplication {

    public static void main(String[] args) {
		SpringApplication.run(CovidApplication.class, args);
	}

}

```
## Controller
```java title="WeatherController.java"
package com.covid.jpa.controller;


import java.util.List;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.MediaType;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import com.covid.jpa.domain.CovidCases;
import com.covid.jpa.service.CovidService;


//Fill your code here
@RestController
@RequestMapping("/covid")
public class CovidController
{

    //Fill your code here
	@Autowired
	CovidService covid;
	
	@GetMapping("/cases")
    public List<CovidCases> fetchAll() {
        //Fill your code here
		return this.covid.findAll();

    }

    //Fill your code here
	@PostMapping("/cases")
    public CovidCases addCases(@RequestBody CovidCases cases) {
        //Fill your code here
    	return this.covid.addCases(cases);

    }

    //Fill your code here
	@PutMapping("/cases")
    public CovidCases updateCases(@RequestBody CovidCases cases) {
        //Fill your code here
    	return this.covid.save(cases);

    }

    //Fill your code here
	@GetMapping("/cases/{id}")
    public CovidCases findById(@PathVariable Long id) {
        //Fill your code here
    	return this.covid.findById(id);

    }

    //Fill your code here
	@DeleteMapping("/cases/{id}")
    public Boolean deleteCases(@PathVariable Long id) {
         //Fill your code here
    	return this.covid.deleteById(id);
    }

}

```
## Service
```java title="WeatherService.java"
package com.covid.jpa.service;

 
import java.util.List;
 
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import com.covid.jpa.domain.CovidCases;
import com.covid.jpa.repository.CovidRepository;


//Fill your code here
@Service
public class CovidService
{
    //Fill your code here
	@Autowired
	CovidRepository covidRepo;
    
    public List<CovidCases> findAll() {
        //Fill your code here
    	return this.covidRepo.findAll();

    }

    public CovidCases addCases(CovidCases cases) {
        //Fill your code here
    	return this.covidRepo.save(cases);
    }

    public CovidCases save(CovidCases cases) {
        //Fill your code here
    	return this.covidRepo.save(cases);
    }

    public CovidCases findById(Long id) {
        //Fill your code here
    	return this.covidRepo.getById(id);
    }

    public Boolean deleteById(Long id) {

        //Fill your code here
    	 this.covidRepo.deleteById(id);
    	 return true;

    }


}

```
## Repository
```java title="WeatherRepository.java"
package com.covid.jpa.repository;

import java.util.List;
import org.springframework.stereotype.Repository;
import com.covid.jpa.domain.CovidCases;

import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.CrudRepository;

//Fill your code here
public interface CovidRepository extends CrudRepository<CovidCases, Long>{
	public List<CovidCases> findAll();
	
	@Query("select w from CovidCases w where w.id=?1")
	CovidCases getById(Long id);
	
}
```
## Domain
```java title="WeatherReport.java"
package com.covid.jpa.domain;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

//Fill your code here
@Entity
@Table(name="covid_cases")
public class CovidCases {

    //Fill your code here
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY) 
    private Long id;
	
	//Fill your code here
	@Column(name="country")
	private String country;
	
	//Fill your code here
	@Column(name="active_count")
	private Long activeCount;
	
	//Fill your code here
	@Column(name="discharged_cases")
	private Long dischargedCases;
	
	public CovidCases() {}

	public CovidCases(Long id,String country, Long activeCount, Long dischargedCases) {
		super();
		this.id = id;
		this.country = country;
		this.activeCount = activeCount;
		this.dischargedCases = dischargedCases;
	}

		public CovidCases(String country, Long activeCount, Long dischargedCases) {
		this.country = country;
		this.activeCount = activeCount;
		this.dischargedCases = dischargedCases;
	}

	public Long getId() {
		return id;
	}

	public void setId(Long id) {
		this.id = id;
	}

	public String getCountry() {
		return country;
	}

	public void setCountry(String country) {
		this.country = country;
	}

	public Long getActiveCount() {
		return activeCount;
	}

	public void setActiveCount(Long activeCount) {
		this.activeCount = activeCount;
	}

	public Long getDischargedCases() {
		return dischargedCases;
	}

	public void setDischargedCases(Long dischargedCases) {
		this.dischargedCases = dischargedCases;
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
