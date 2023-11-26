# JDBC
```java title="oracle.properties"
db.url = jdbc:oracle:thin:@localhost:1521:xe
db.username = root
db.password = student
```
```java title="DBConnection.java"
import java.sql.*;
import java.util.ResourceBundle;
public class DBConnection {
	public static Connection getConnection() throws ClassNotFoundException, SQLException {        
        ResourceBundle rb = ResourceBundle.getBundle("oracle");
        String url = rb.getString("db.url");
        String username = rb.getString("db.username");
        String password = rb.getString("db.password");
        //fill your code here

        Connection con = null;

        try {
            Class.forName("oracle.jdbc.driver.OracleDriver");
            con = DriverManager.getConnection(url, username, password);
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return con;
    }
}
```
## 1
**`Select Statement `**

Write a program to retrieve all the records present in the Book table and display those records in the specified format using the SELECT select.

Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names and method names should be the same as specified in the problem statement.

 

Create a class named Book with the following private attributes/variables.

Data type	Variable
Integer	id
String	title
String	category
String	author
Double	price
Include appropriate getters and setters.
Include default and parameterized constructors in the order public Book(Integer id, String title, String category, String author, Double price)

 

Create a class BookdDAO with the following method.

Method Name	Description
ArrayList<Book> listBooks()	This method is used to list the all the books in the database.
 

Create a class DBConnection with following method.

Method	Description
public static Connection getConnection()	This method is used to connect the java application with oracle database. Here register the JDBC driver for the application, configure the database properties(fetch from oracle.properties) and return the connection object.
 

Create a class Main with main method. In the method, create instances of the above classes and test the above classes.

Use the below format to print the details in table :
System.out.format("%-5s %-20s %-20s %-10s %s\n","Id","Title","Category","Author","Price");

 

oracle.properties :

db.url = jdbc:oracle:thin:@localhost:1521:xe
db.username = root
db.password = student

Use the below code to retrieve the connection details from oracle.properties to establish connection

ResourceBundle rb = ResourceBundle.getBundle("oracle");
String url = rb.getString("db.url");
String user = rb.getString("db.username");
String pass = rb.getString("db.password");

Table Properties:

create table book(
id number(10) not null,
title VARCHAR2(45) not null,
category VARCHAR2(45) not null,
author VARCHAR2(45) not null,
price binary_double not null,
primary key(id));  

Download the oracle jar file in the below link.
Oracle jar

Sample Input and Output:

List of Books
Id       Title          Category       Author      Price
1        Vampire Dairy  Fiction       Chetan      150.0
2        Harry potter   Witchcraft    Rowling     450.0
```java title="oraclescript.sql"
begin
   execute immediate 'drop table travel_class';
exception
   when others then null;
end;
/

create table travel_class(
id number(10) not null,
name VARCHAR2(45) not null,
description CLOB not null,
primary key(id)
);

insert into travel_class(id,name,description) values (1,'First Class','Limited Seats and Luxurious.');
insert into travel_class(id,name,description) values (2,'Business Class','Intermediate level of service between economy class and first class.');
insert into travel_class(id,name,description) values (3,'Premium Economy Class','Positioning in price, comfort, and amenities, this travel class is leveled between economy class and business class.');
insert into travel_class(id,name,description) values (4,'Economy Class','Lowest travel class of seating in air travel.');


```
```java title="Main.java"
import java.util.ArrayList;
import java.sql.*;

public class Main {
    public static void main(String[] args) {
        try {
            ArrayList<Book> books = new BookDAO().listBooks();

            System.out.println("List of Books");
            System.out.format("%-5s %-20s %-20s %-10s %s\n","Id","Title","Category","Author","Price");

            for (Book book : books) {
                System.out.format("%-5s %-20s %-20s %-10s %s\n",
                        book.getId(), book.getTitle(), book.getCategory(), book.getAuthor(), book.getPrice());
            }
        } 
        catch (SQLException e) {
            System.out.println("Error: " + e.getMessage());
        }
        catch (ClassNotFoundException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
    }
}


```
```java title="Book.java"
public class Book {
	Integer id;
	String title;
	String category;
	String author;
	Double price;
	public Book() {
		super();
		// TODO Auto-generated constructor stub
	}
	public Book(Integer id, String title, String category, String author, Double price) {
		super();
		this.id = id;
		this.title = title;
		this.category = category;
		this.author = author;
		this.price = price;
	}
	public Integer getId() {
		return id;
	}
	public void setId(Integer id) {
		this.id = id;
	}
	public String getTitle() {
		return title;
	}
	public void setTitle(String title) {
		this.title = title;
	}
	public String getCategory() {
		return category;
	}
	public void setCategory(String category) {
		this.category = category;
	}
	public String getAuthor() {
		return author;
	}
	public void setAuthor(String author) {
		this.author = author;
	}
	public Double getPrice() {
		return price;
	}
	public void setPrice(Double price) {
		this.price = price;
	}
	
}

```
```java title="BookDAO.java"
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;

public class BookDAO {
	public ArrayList<Book> listBooks() throws ClassNotFoundException, SQLException{
    	ArrayList<Book> bookList = new ArrayList<Book>();
    	//fill your code here

		 try {
            Connection conn = DBConnection.getConnection();
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM book");

            while (rs.next()) {
                Book book = new Book(rs.getInt("id"), rs.getString("title"),
                        rs.getString("category"), rs.getString("author"), rs.getDouble("price"));
                bookList.add(book);
            }

            rs.close();
            stmt.close();
            conn.close();
        } catch (ClassNotFoundException e) {
            System.out.println("Error: " + e.getMessage());
        } catch (SQLException e) {
            System.out.println("Error: " + e.getMessage());
        }

		return bookList;
    }
}


```



## 2
Update details of Travel Classes

Write a java program to update the details of Travel class available in the database and display the list of travel class details in the descending order of names using JDBC drivers.

[Note:  Strictly adhere to the object-oriented specifications given as a part of the problem statement. Follow the naming conventions as mentioned. Create separate classes in separate files.]

Create a class TravelClass with the following attributes.

Data Type	Variable Name
String	name
String	description
Include appropirate getters, setters, default and parameterized constructors for the above class

Create a class TravelClassDAO with a following method

Method name	Description
ArrayList<TravelClass> listAllTravelClassess()	This method retrieves the list of travel classes available in the database in the descending order of the travel class name and returns the same.
void updateDetail(String name, String description)	This method update the given description into the database for the given travel class name.

Create a class DBConnection with following method.

Method	Description
public static Connection getConnection()	This method is used to connect the java application with oracle database. Here register the JDBC driver for the application, configure the database properties(fetch from oracle.properties) and return the connection object.

Create a class Main with main method and call the methods of TravelClassDAO and display the list as shown in the main method.

Use the below format to print the details in table :
System.out.format("%-25s %s\n","Name","Description");

oracle.properties :

db.url = jdbc:oracle:thin:@localhost:1521:xe
db.username = root
db.password = student

Use the below code to retrieve the connection details from oracle.properties to establish connection

ResourceBundle rb = ResourceBundle.getBundle("oracle");
String url = rb.getString("db.url");
String user = rb.getString("db.username");
String pass = rb.getString("db.password");

Table Properties:

create table travel_class(
id number(10) not null,
name VARCHAR2(45) not null,
description CLOB not null,
primary key(id)
);


Download the oracle jar file in the below link.
Oracle jar

Sample Input and Output:
Enter the name of TravelClass :
Economy Class
Enter the description to update :
Lowest travel class of seating in flight travel.
Updated List of Travel Classes
Name                      Description                   
Premium Economy Class     Positioning in price, comfort, and amenities, this travel class is leveled between economy class and business class.
Economy Class             Lowest travel class of seating in flight travel.
Business Class            Intermediate level of service between economy class and first class.

```java title="Main.java"
import java.io.*;
import java.sql.SQLException;
import java.util.ArrayList;


public class Main {
    public static void main(String args[]) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        System.out.println("Enter the name of TravelClass :");
        String name = br.readLine();
        System.out.println("Enter the description to update :");
        String description = br.readLine();
        //fill your code here

        // create a new instance of TravelClassDAO
        TravelClassDAO travelClassDAO = new TravelClassDAO();

        // call the updateDetail method to update the description of a travel class
        travelClassDAO.updateDetail(name, description);

        // call the listAllTravelClassess method to retrieve the list of travel classes
        ArrayList<TravelClass> travelClasses = travelClassDAO.listAllTravelClassess();

        // display the list of travel classes in descending order of names
        System.out.println("Updated List of Travel Classes");
        System.out.format("%-25s %s\n", "Name", "Description");
        for (TravelClass travelClass : travelClasses) {
            System.out.format("%-25s %s\n", travelClass.getName(), travelClass.getDescription());
        }
    }
}


```

```java title="oraclescript.sql"
begin
   execute immediate 'drop table travel_class';
exception
   when others then null;
end;
/

create table travel_class(
id number(10) not null,
name VARCHAR2(45) not null,
description CLOB not null,
primary key(id)
);

insert into travel_class(id,name,description) values (1,'First Class','Limited Seats and Luxurious.');
insert into travel_class(id,name,description) values (2,'Business Class','Intermediate level of service between economy class and first class.');
insert into travel_class(id,name,description) values (3,'Premium Economy Class','Positioning in price, comfort, and amenities, this travel class is leveled between economy class and business class.');
insert into travel_class(id,name,description) values (4,'Economy Class','Lowest travel class of seating in air travel.');


```
```java title=""
public class TravelClass {
    String name,description;

    public TravelClass() {
    }

    public TravelClass(String name, String description) {
        this.name = name;
        this.description = description;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }
    
}

```
```java title="TravelClassDAO"
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.List;

public class TravelClassDAO {
    ArrayList<TravelClass> listAllTravelClassess() throws ClassNotFoundException, SQLException {
        
        ArrayList<TravelClass> travelClassList= new ArrayList<TravelClass>();

        //fill your code here

          Connection con = null;
        PreparedStatement ps = null;
        ResultSet rs = null;
        try {
            con = DBConnection.getConnection();
            String query = "SELECT * FROM travel_class ORDER BY name DESC";
            ps = con.prepareStatement(query);
            rs = ps.executeQuery();
            while (rs.next()) {
                TravelClass travelClass = new TravelClass();
                travelClass.setName(rs.getString("name"));
                travelClass.setDescription(rs.getString("description"));
                travelClassList.add(travelClass);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (rs != null)
                    rs.close();
                if (ps != null)
                    ps.close();
                if (con != null)
                    con.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        return travelClassList;
    }
    public void updateDetail(String name, String description) throws ClassNotFoundException, SQLException {
    	//fill your code here
          Connection con = null;
        PreparedStatement ps = null;
        try {
            con = DBConnection.getConnection();
            String query = "UPDATE travel_class SET description = ? WHERE name = ?";
            ps = con.prepareStatement(query);
            ps.setString(1, description);
            ps.setString(2, name);
            ps.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (ps != null)
                    ps.close();
                if (con != null)
                    con.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}


```
## 3
Insert new Airport
Write a program to insert the airport data and display the list of airport details by retrieving data from the database.

[Note:  Strictly adhere to the object-oriented specifications given as a part of the problem statement. Follow the naming conventions as mentioned. Create separate classes in separate files.]

The class Airport has been created with the following attributes.

Data type	Variable name
String	iataAirportCode
String	name
String	city
String	country
The appropriate getters, setters, default and parameterized constructors for the above class have been already included for you.

The class AirportDAO has been created with the following methods.

Method name	Description
ArrayList<Airport> listAirport()	This method will return the list of airports sorted in ascending order based on iataAirportCode in the database
void insertAirport(Airport airportIns)	This method will insert the new airport into the database
 

The class DBConnection has been created with the following method.

Method	Description
public static Connection getConnection()	This method is used to connect the java application with oracle database. Here register the JDBC driver for the application, configure the database properties(fetch from oracle.properties) and return the connection object.

Create a class Main with main method. In the method, create instances of the above classes and test the above classes.

Use the below format to print the details in table :
System.out.format("%-10s %-40s %-10s %s\n","IATA Code","Name","City","Country");

 

oracle.properties :

db.url = jdbc:oracle:thin:@localhost:1521:xe
db.username = root
db.password = student

The below code has already been implemented to retrieve the connection details from oracle.properties to establish connection.

ResourceBundle rb = ResourceBundle.getBundle("oracle");
String url = rb.getString("db.url");
String user = rb.getString("db.username");
String pass = rb.getString("db.password");

Table Properties:

create table airport(
id number(10) GENERATED ALWAYS AS IDENTITY not null,
iata_airport_code VARCHAR2(45) not null,
name VARCHAR2(45) not null,
city VARCHAR2(45) not null,
country_name VARCHAR2(45) not null,
primary key(id));


Download the oracle jar file in the below link.
Oracle jar

Sample Input and Output:
Enter the Airport Code :
MDZ
Enter the Airport name :
Francisco Gabriell International Airport
Enter the City :
Mendoza
Enter the Country name :
Arizona
IATA Code  Name                                     City       Country
BNE        Brisbane Airport                         Brisbane   Australia
COK        Cochin International Airport             Cochin     India
MDZ        Francisco Gabriell International Airport Mendoza    Arizona
SXR        Srinagar International Airport           Srinagar   India
```java title="Main.java"
import java.io.*;
import java.util.ArrayList;

public class Main {
    public static void main(String args[]) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String countryName,airportCode,airportName,city;
        System.out.println("Enter the Airport Code :");
        airportCode = br.readLine();
        System.out.println("Enter the Airport name :");
        airportName = br.readLine();
        System.out.println("Enter the City :");
        city = br.readLine();
	System.out.println("Enter the Country name :");
        countryName = br.readLine();
        
        //fill your code
    AirportDAO dao = new AirportDAO();
        Airport airport = new Airport();

        // Insert a new airport
        airport.setIataAirportCode(airportCode);
        airport.setName(airportName);
        airport.setCity(city);
        airport.setCountry(countryName);
        dao.insertAirport(airport);

        // Retrieve the list of airports and display them in a table format
        ArrayList<Airport> airportList = dao.listAirport();
        System.out.format("%-10s %-40s %-10s %s\n", "IATA Code", "Name", "City", "Country");
        for (Airport a : airportList) {
            System.out.format("%-10s %-40s %-10s %s\n", a.getIataAirportCode(), a.getName(), a.getCity(), a.getCountry());
        }
        
    }
}


```
```java title="Airport.java"
public class Airport {
	String iataAirportCode,name,city,country;

	public Airport() {
		super();
		// TODO Auto-generated constructor stub
	}

	public Airport(String iataAirportCode, String name, String city, String country) {
		super();
		this.iataAirportCode = iataAirportCode;
		this.name = name;
		this.city = city;
		this.country = country;
	}

	public String getIataAirportCode() {
		return iataAirportCode;
	}

	public void setIataAirportCode(String iataAirportCode) {
		this.iataAirportCode = iataAirportCode;
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

	public String getCountry() {
		return country;
	}

	public void setCountry(String country) {
		this.country = country;
	}
    
    
    
}
```
```java title="AirportDAO.java"
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;


public class AirportDAO {
    public void insertAirport(Airport airportIns) throws ClassNotFoundException, SQLException{
        
        //fill your code
         Connection con = null;
        PreparedStatement ps = null;
        try {
            con = DBConnection.getConnection();
            ps = con.prepareStatement("INSERT INTO airport (iata_airport_code, name, city, country_name) VALUES (?, ?, ?, ?)");
            ps.setString(1, airportIns.getIataAirportCode());
            ps.setString(2, airportIns.getName());
            ps.setString(3, airportIns.getCity());
            ps.setString(4, airportIns.getCountry());
            ps.executeUpdate();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (ps != null)
                    ps.close();
                if (con != null)
                    con.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
    public ArrayList<Airport> listAirport() throws ClassNotFoundException, SQLException{
        
        //fill your code

        ArrayList<Airport> airportList = new ArrayList<>();
        Connection con = null;
        PreparedStatement ps = null;
        ResultSet rs = null;
        try {
            con = DBConnection.getConnection();
            ps = con.prepareStatement("SELECT * FROM airport ORDER BY iata_airport_code");
            rs = ps.executeQuery();
            while (rs.next()) {
                String iataAirportCode = rs.getString("iata_airport_code");
                String name = rs.getString("name");
                String city = rs.getString("city");
                String country = rs.getString("country_name");
                Airport airport = new Airport(iataAirportCode, name, city, country);
                airportList.add(airport);
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (rs != null)
                    rs.close();
                if (ps != null)
                    ps.close();
                if (con != null)
                    con.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        return airportList;
    }
}

```
## iAssess
User-Delete

The users who enter into 20 Ideas for Vision 2020 must be active and must keep posting their ideas.If the administrator finds out that the user is not active the admin can delete the user record from the table. Help the admin to delete the user record from the table.

[Note:  Strictly adhere to the object-oriented specifications given as a part of the problem statement. Follow the naming conventions as mentioned. Create separate classes in separate files.]

Create a User with following private attributes.
Data Type	Variable
Integer	id
String	name
String	email
String	password
Integer	age
String	role
Date	createdDate
String	status
Include appropriate getters, setters, default and parameterized constructors for the above class.


Create a class UserDAO with following methods

Method Name	Method Description
ArrayList<User> listUsers()	This method returns the list of users available in the database
void deleteUser(Integer id)	This method will delete the user from the database using the given id

Create a class DBConnection with following method
Method	Description
public static Connection getConnection()	This method is used to connect the java application with oracle database. Here register the JDBC driver for the application,configure the database properties(fetch from oracle.properties) and return the connection object.

Create a class Main with main method and call the methods of UserDAO and display the list as shown.


Output Format:
Use Java Format Specifier to display the user details
 System.out.format("%-15s %-15s %-15s %-15s %-15s %-15s %-15s %s\n","Id","Name","Email","Password","Age","Role","CreatedDate","Status");


Table Properties:

create table "user"(
id number(10) GENERATED ALWAYS AS IDENTITY not null,
name varchar2(50) not null,
email varchar2(50) not null,
password varchar2(50) not null,
age number(10) not null,
role varchar2(50) not null,
created_date date not null,
status varchar2(50) not null,
primary key(id));

 

oracle.properties :

db.url = jdbc:oracle:thin:@localhost:1521:xe
db.username = root
db.password = student

Use the below code to retrieve the connection details from oracle.properties to establish connection

ResourceBundle rb = ResourceBundle.getBundle("oracle");
String url = rb.getString("db.url");
String user = rb.getString("db.username");
String pass = rb.getString("db.password");

 
Download the oracle jar file in the below link.
Oracle jar

Sample Input and Output
[All text in bold are input and the remaining are output]

Before the Delete
Id              Name            Email           Password        Age             Role            CreatedDate     Status         
1               Asha            ash@a.com       as123           18              user            2015-10-13      Approved       
2               Rahul           rh@a.com        rh@123          15              user            2015-10-14      Approved       
3               Ravi            rv@a.com        rv@98           20              user            2015-10-14      pending        
Enter the Id :
1
After the Delete
Id              Name            Email           Password        Age             Role            CreatedDate     Status         
2               Rahul           rh@a.com        rh@123          15              user            2015-10-14      Approved       
3               Ravi            rv@a.com        rv@98           20              user            2015-10-14      pending
```java title="Main.java"
import java.util.*;
import java.io.*;
import java.sql.SQLException;
import java.text.SimpleDateFormat;

public class Main{
    
    public static void main(String [] args) throws Exception{
        //fill your code here
        try {
            Scanner input= new Scanner(System.in);
            ArrayList<User> users = new UserDAO().listUsers();

            System.out.println("Before the Delete");
            System.out.format("%-15s %-15s %-15s %-15s %-15s %-15s %-15s %s\n","Id","Name","Email","Password","Age","Role","CreatedDate","Status");

            for (User user : users) {
                System.out.format("%-15s %-15s %-15s %-15s %-15s %-15s %-15s %s\n",user.getId(),user.getName(),user.getEmail(),user.getPassword(),user.getAge(),user.getRole(),user.getCreatedDate(),user.getStatus());
            }
            /* */
            System.out.println("Enter the Id :");
            Integer id=input.nextInt();
            UserDAO user1=new UserDAO();
            user1.deleteUser(id);
            System.out.println("After the Delete");
            System.out.format("%-15s %-15s %-15s %-15s %-15s %-15s %-15s %s\n","Id","Name","Email","Password","Age","Role","CreatedDate","Status");
            ArrayList<User> usersAfterDelete = new UserDAO().listUsers();
            for (User user : usersAfterDelete) {
                System.out.format("%-15s %-15s %-15s %-15s %-15s %-15s %-15s %s\n",user.getId(),user.getName(),user.getEmail(),user.getPassword(),user.getAge(),user.getRole(),user.getCreatedDate(),user.getStatus());
            }


        } 
        catch (SQLException e) {
            System.out.println("Error: " + e.getMessage());
        }
        catch (ClassNotFoundException e) {
            System.out.println("Error: " + e.getMessage());
        }
        
    }

}
```
```java title="User.java"
import java.util.Date;

public class User {
	Integer id;
	String name;
	String email;
	String password;
	Integer age;
	String role;
	Date createdDate;
	String status;
	
	public User() {
		super();
		// TODO Auto-generated constructor stub
	}

	public User(Integer id, String name, String email, String password, Integer age, String role, Date createdDate,
			String status) {
		super();
		this.id = id;
		this.name = name;
		this.email = email;
		this.password = password;
		this.age = age;
		this.role = role;
		this.createdDate = createdDate;
		this.status = status;
	}

	public Integer getId() {
		return id;
	}

	public void setId(Integer id) {
		this.id = id;
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

	public Integer getAge() {
		return age;
	}

	public void setAge(Integer age) {
		this.age = age;
	}

	public String getRole() {
		return role;
	}

	public void setRole(String role) {
		this.role = role;
	}

	public Date getCreatedDate() {
		return createdDate;
	}

	public void setCreatedDate(Date createdDate) {
		this.createdDate = createdDate;
	}

	public String getStatus() {
		return status;
	}

	public void setStatus(String status) {
		this.status = status;
	}
	
}
```
```java title="UserDAO.java"

import java.util.ArrayList;
import java.util.Date;
import java.util.List;
import java.sql.*;
public class UserDAO{

    public ArrayList<User> listUsers() throws Exception{
    	ArrayList<User> userList = new ArrayList<User>();
    	//fill your code here
        

        Connection con = null;
        PreparedStatement ps = null;
        ResultSet rs = null;
        try {
            con = DBConnection.getConnection();
            String query ="SELECT * FROM \"user\"" ;
            ps = con.prepareStatement(query);
            rs = ps.executeQuery();
            while (rs.next()) {
                User user = new User(rs.getInt("id"),rs.getString("name"),rs.getString("email"),rs.getString("password"),rs.getInt("age"),rs.getString("role"),rs.getDate("created_date"),rs.getString("status"));
                userList.add(user);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (rs != null)
                    rs.close();
                if (ps != null)
                    ps.close();
                if (con != null)
                    con.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }



		return userList;
    }
    public void deleteUser(Integer id) throws Exception{
    	//fill your code here
        Connection con = null;
        PreparedStatement ps = null;
        try {
            con = DBConnection.getConnection();
            String query = "DELETE from \"user\" WHERE id = ?  ";
            ps = con.prepareStatement(query);
            ps.setInt(1, id);
            ps.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            try {
                if (ps != null)
                    ps.close();
                if (con != null)
                    con.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
    
}
```
```java title="user_delete.sql"
begin
   execute immediate 'drop table "user"';
exception
   when others then null;
end;
/

create table "user"(
id number(10) not null,
name varchar2(50) not null,
email varchar2(50) not null,
password varchar2(50) not null,
age number(10) not null,
role varchar2(50) not null,
created_date date not null,
status varchar2(50) not null,
primary key(id));

insert into "user"(id, name,email,password,age,role,created_date,status) values(1,'Asha','ash@a.com','as123',18,'user',TO_DATE('2015-10-13','YYYY-MM-DD'),'Approved');
insert into "user"(id, name,email,password,age,role,created_date,status) values(2,'Rahul','rh@a.com','rh@123',15,'user',TO_DATE('2015-10-14','YYYY-MM-DD'),'Approved');
insert into "user"(id, name,email,password,age,role,created_date,status) values(3,'Ravi','rv@a.com','rv@98',20,'user',TO_DATE('2015-10-14','YYYY-MM-DD'),'pending');
insert into "user"(id, name,email,password,age,role,created_date,status) values(4,'Pavi','pv@a.com','pv@98',20,'user',TO_DATE('2015-11-14','YYYY-MM-DD'),'pending');
insert into "user"(id, name,email,password,age,role,created_date,status) values(5,'Devi','dv@a.com','dv@98',20,'user',TO_DATE('2015-09-07','YYYY-MM-DD'),'pending');

```