# Weather Application
```java title="WeatherJpaApplication.java"
package com.weather.jpa;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

//Fill your code here
@SpringBootApplication
public class WeatherJpaApplication {

    public static void main(String[] args) {
		SpringApplication.run(WeatherJpaApplication.class, args);
	}

}

```
## Controller
```java title="WeatherController.java"
package com.weather.jpa.controller;


import java.util.List;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.MediaType;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import com.weather.jpa.domain.WeatherReport;
import com.weather.jpa.service.WeatherService;

//Fill your code here
@RestController
public class WeatherController {
    
	//Fill your code here
	@Autowired
	WeatherService weather;
	@GetMapping("/weatherReport")
	public List<WeatherReport> getData() {
		//Fill your code here
		return this.weather.getData();
	}
	
	//Fill your code here
	@PostMapping("/weatherReport")
	public WeatherReport addCases(@RequestBody WeatherReport cases) {
		//Fill your code here
		return this.weather.addCases(cases);
	}

	//Fill your code here
	@PutMapping("/weatherReport")
	public WeatherReport updateCases(@RequestBody WeatherReport cases) {
		//Fill your code here
		return this.weather.updateCases(cases);
	}
	
	//Fill your code here
	@GetMapping("/weatherReport/{id}")
	public WeatherReport view(@PathVariable Long id) {
		//Fill your code here
		return this.weather.view(id);
	}
	
	//Fill your code here
	@DeleteMapping("/weatherReport/{id}")
	public Boolean deleteCases(@PathVariable Long id) {
        //Fill your code here
		return this.weather.deleteCases(id);
	}
	
}

```
## Service
```java title="WeatherService.java"
package com.weather.jpa.service;

import java.util.List;
import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import com.weather.jpa.domain.WeatherReport;
import com.weather.jpa.repository.WeatherRepository;

//Fill your code here
@Service
public class WeatherService {
//Fill your code here
	@Autowired
	WeatherRepository weather;

	public List<WeatherReport> getData() {
		// Fill your code here
		return  this.weather.findAll();

	}

	public WeatherReport addCases(WeatherReport cases) {

		return this.weather.save(cases);

	}

	public WeatherReport updateCases(WeatherReport cases) {
		// Fill your code here
		return this.weather.save(cases);

	}

	public WeatherReport view(Long id) {
		// Fill your code here
		return this.weather.getById(id);

	}

	public Boolean deleteCases(Long id) {
		// Fill your code here
		this.weather.deleteById(id);
		return true;

	}

}
```
## Repository
```java title="WeatherRepository.java"
package com.weather.jpa.repository;

import java.util.List;
import org.springframework.stereotype.Repository;
import com.weather.jpa.domain.WeatherReport;

import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.CrudRepository;

//Fill your code here
public interface WeatherRepository extends CrudRepository<WeatherReport, Long>{
	public List<WeatherReport> findAll();
	
	@Query("select w from WeatherReport w where w.id=?1")
	WeatherReport getById(Long id);
}

```
## Domain
```java title="WeatherReport.java"
package com.weather.jpa.domain;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;
//Fill your code here
@Entity
@Table(name="weather_report")
public class WeatherReport {

    //Fill your code here
	@Id
	@GeneratedValue(strategy= GenerationType.AUTO)
    private Long id;
	//Fill your code here
	@Column(name="city")
	private String city;
	//Fill your code here
	@Column(name="min_temperature")
	private Double minTemperature;
	//Fill your code here
	@Column(name="max_temperature")
	private Double maxTemperature;
	
	public WeatherReport() {}

	public WeatherReport(Long id, String city, Double minTemperature, Double maxTemperature) {
		super();
		this.id = id;
		this.city = city;
		this.minTemperature = minTemperature;
		this.maxTemperature = maxTemperature;
	}

	public Long getId() {
		return id;
	}

	public void setId(Long id) {
		this.id = id;
	}

	public String getCity() {
		return city;
	}

	public void setCity(String city) {
		this.city = city;
	}

	public Double getMinTemperature() {
		return minTemperature;
	}

	public void setMinTemperature(Double minTemperature) {
		this.minTemperature = minTemperature;
	}

	public Double getMaxTemperature() {
		return maxTemperature;
	}

	public void setMaxTemperature(Double maxTemperature) {
		this.maxTemperature = maxTemperature;
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
