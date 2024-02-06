# Collections And Maps
## 1
    **`contains() & indexOf() methods in ArrayList`**
    Write a program to get the hall details and store in the ArrayList and search the hall and display it's position details.

    Get hall names in the Main class and store it an ArrayList.

    Input format:
    The first line of input is an integer which corresponds to the number ‘n’ of halls.
    The n lines of input are the string which corresponds to the hall name.
    The last line of input is the string which corresponds to the hall name to be searched.

    Output format:
    The output is the hall position.
    It is the position at which the hall is present in the list starting from 0.
    If the hall to be searched is not present in the list, then print "[Hall name] hall is not found"
    Refer to sample Input and Output for formatting specifications.

    [All Texts in bold corresponds to the input and rest are output]
    Sample Input and Output 1:

    Enter the number of halls:
    3
    Enter the Hall Name 1
    SPK
    Enter the Hall Name 2
    DFG
    Enter the Hall Name 3
    TRE
    Enter the hall name to be searched:
    DFG
    DFG hall is found in the list at position 1

    Sample Input/Output 2:

    Enter the number of halls:
    3
    Enter the Hall Name 1
    SPJ
    Enter the Hall Name 2
    RWE
    Enter the Hall Name 3
    HFG
    Enter the hall name to be searched:
    SPK
    SPK hall is not found

```java title="Main.java"
import java.util.ArrayList;
import java.util.Scanner;

/**
 * Main
 */
public class Main {

    public static void main(String[] args) {
        Scanner input= new Scanner(System.in);
        System.out.println("Enter the number of halls:");
        int numberOfHalls=input.nextInt();
        String hallName;
        ArrayList<String> halls=new ArrayList<String>();
        for (int i = 0; i < numberOfHalls; i++) {
            System.out.println("Enter the Hall Name "+(i+1));
            hallName=input.next();
           // hallName+=input.nextLine();
            halls.add(hallName);
        }
        System.out.println("Enter the hall name to be searched:");
        String searchHallName=input.next();
        //searchHallName+=input.nextLine();
        try {
            if(halls.contains(searchHallName)){
                System.out.println(searchHallName+" hall is found in the list at position "+(halls.indexOf(searchHallName)));
            }
            else{
                System.out.println(searchHallName+" hall is not found");
            }
        } catch (Exception e) {
            // TODO: handle exception
            
        }
        
        input.close();
    }
}
```
## 2
**`Email Search`**
 
    In your application let’s dive deep into Set and explore its inbuilt functions. In this problem experiment with containsAll() method. Write a program to search all the email addresses which are given as CSV format.

    Create a Main class. Obtain email addresses from the user and add them to a Set. At last, get a String that has multiple email addresses in CSV format. Print "Email addresses are present" if all email addresses are present in the Set, else print "Email addresses are not present".

    Input and Output format:
    Refer to sample Input and Output for formatting specifications.

    Note: All Texts in bold corresponds to the input and rest are output

    Sample Input and Output 1:
    Enter Email address
    Merry@gmail.com
    Do you want to Continue?(yes/no)
    yes
    Enter Email address
    Peter@yahoo.com
    Do you want to Continue?(yes/no)
    yes
    Enter Email address
    Christian@hotmail.com
    Do you want to Continue?(yes/no)
    yes
    Enter Email address
    Merry@gmail.com
    Do you want to Continue?(yes/no)
    no
    Enter the email addresses to be searched separated by comma
    Merry@gmail.com,Peter@yahoo.com
    Email addresses are present


    Sample Input and Output 2:
    Enter Email address
    Manikandan@yahoo.com
    Do you want to Continue?(yes/no)
    yes
    Enter Email address
    bala@google.co.in
    Do you want to Continue?(yes/no)
    no
    Enter the email addresses to be searched separated by comma
    bala@google.co.in,jeryy@gmail.com
    Email addresses are not present

```java title="Main.java"
import java.util.HashSet;
import java.util.Scanner;
import java.util.Set;

public class Main {
    public static void main(String[] args) {
        Scanner input= new Scanner(System.in);
        String choice;
        Set<String> emails =new HashSet<>();
        do {
            System.out.println("Enter Email address");
            String email=input.next();
            emails.add(email);
            System.out.println("Do you want to Continue?(yes/no)");
            choice=input.next();

        } while (choice.equals("yes"));  
        System.out.println("Enter the email addresses to be searched separated by comma");
        String emailString=input.next();
        String[] emailSeparated=emailString.split(",");
        Set<String> emailSearched=new HashSet<>();
        for (int i = 0; i < emailSeparated.length; i++) {
            emailSearched.add(emailSeparated[i]);
        }
        if(emails.containsAll(emailSearched)){
            System.out.println("Email addresses are present");
        }
        else{
            System.out.println("Email addresses are not present");
        }
        input.close();
    }
}

```
## 3
**`City map`**
 

    Let's spice up things by creating a Multimap. `Map<City,List<Address>>` with City name as key and List of address that corresponds to the City as value. Given list of Addresses as input create a map with the above specification. Obtain a city name as input from the user and display the addresses with the city name as that of the given city by fetching the list of addresses from the map.

    Create a class called Address with the following private attributes.

    

    Attributes	Datatype
    addressLine1	String
    addressLine2	String
    city	String
    state	String
    pincode	Integer
    

    Include appropriate getters and setters.
    Include default and parameterized constructor for the class.
    Format for the Parameterized Constructor Address(String addressLine1, String addressLine2, String city,String state, Integer pincode)

    Create a driver class called Main. In the Main method, obtain address details from the input and create the map of above specification. Obtain a city as a search term and display the address that has the given city. If no such address is present, Print "Searched city not found".

    Note: 
    [Strictly adhere to the Object-Oriented Specifications given in the problem statement.
    All class names, attribute names and method names should be the same as specified in the problem statement.]

    Input format:

    First line corresponds to number of address details
    Next n lines consists of n address details in CSV format
    n+1th  line consists of city input

    Output format:

    Address details are displayed in tabular format.(Use "%-15s %-15s %-15s %-15s %s\n" for formatting Address details.)

    [All text in bold corresponds to the input and rest corresponds to the output]
    Sample Input/Output:

    Enter the number of address
    4
    Enter the address 1 detail
    22nd lane,RR nagar,Chennai,Tamil nadu,600028
    Enter the address 2 detail
    3rd street,KRK nagar,Visak,Andhrapradesh,745601
    Enter the address 3 detail
    1/45 8th street,KK nagar,Chennai,Tamil nadu,600021
    Enter the address 4 detail
    5/15 7th lane,RK nagar,Madurai,Tamil nadu,625001
    Enter the city to be searched
    Chennai
    Line 1          Line 2          City            State           Pincode
    22nd lane       RRnagar        Chennai         Tamilnadu      600028
    1/45 8th street KKnagar        Chennai         Tamilnadu      600021

 
```java title="Main.java"
import java.util.ArrayList;
import java.util.Formatter;
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input= new Scanner(System.in);
        
        Map<String,ArrayList<Address>> map=new HashMap<>();
        System.out.println("Enter the number of address");
        int numberOfAddresses=input.nextInt();
        String address;
        ArrayList<Address> addressList=new ArrayList<Address>();
        for (int i = 0; i < numberOfAddresses; i++) {
            System.out.println("Enter the address "+(i+1)+" detail");
            address=input.next();
            address+=input.nextLine();
            String[] addressSplit=address.split(",");
            
            if(!map.containsKey(addressSplit[2])){
                addressList.add(new Address(addressSplit[0],addressSplit[1],addressSplit[2],addressSplit[3],Integer.parseInt(addressSplit[4])));
                map.put(addressSplit[2], addressList);
            }
            else{
                map.get(addressSplit[2]).add(new Address(addressSplit[0],addressSplit[1],addressSplit[2],addressSplit[3],Integer.parseInt(addressSplit[4])));
            }
            
        }
        System.out.println("Enter the city to be searched");
        String city=input.next();
        if(map.containsKey(city)){
            Formatter formatter= new Formatter();
            formatter.format("%-15s %-15s %-15s %-15s %s\n","Line 1","Line 2","City","State","Pincode");
            
            for (int index = 0; index < map.get(city).size(); index++) {
                if(city.equals(map.get(city).get(index).getCity())){
                    formatter.format("%-15s %-15s %-15s %-15s %s\n",map.get(city).get(index).getAddressLine1(),map.get(city).get(index).getAddressLine2(),map.get(city).get(index).getCity(),map.get(city).get(index).getState(),map.get(city).get(index).getPincode());
                }
                
            }
            System.out.println(formatter);
            formatter.close();
        }
        else{
            System.out.println("Searched city not found");
        }
        input.close();
    }
}

```
```java title="Address.java"
public class Address {
    private String addressLine1;
    public String getAddressLine1() {
        return addressLine1;
    }
    public void setAddressLine1(String addressLine1) {
        this.addressLine1 = addressLine1;
    }
    private String addressLine2;
    public String getAddressLine2() {
        return addressLine2;
    }
    public void setAddressLine2(String addressLine2) {
        this.addressLine2 = addressLine2;
    }
    private String city;
    public String getCity() {
        return city;
    }
    public void setCity(String city) {
        this.city = city;
    }
    private String state;
    public String getState() {
        return state;
    }
    public void setState(String state) {
        this.state = state;
    }
    private Integer pincode;
    public Integer getPincode() {
        return pincode;
    }
    public void setPincode(Integer pincode) {
        this.pincode = pincode;
    }
    public Address(){
        
    }
    public Address(String addressLine1, String addressLine2, String city,String state, Integer pincode){
        this.addressLine1=addressLine1;
        this.addressLine2=addressLine2;
        this.city=city;
        this.state=state;
        this.pincode=pincode;
    }
}

```
## iAssess

### 1
    User Search
    In your application, it is time to experiment with a Set of user-defined Objects. Just like List of objects, Set of objects is also relatively simple.
    Consider a Set of bank users. The set contains users who are inactive as well. The bank wants to retain only the Users who are active given a list of active users.

    Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names and method names should be the same as specified in the problem statement.

    Create a User class with the following private attributes

    Attributes	Datatype
    username	String
    bankname	String
    Include appropriate getters and setters.
    Create default constructor and a parameterized constructor with arguments in order User(String username, String bankname).

    Note:
    Override equals method to compare the username, to improve the comparison of username use hashCode method to check the strings are same.
    Override the Comparable interface to sort Users in Alphabetical order of Username.

    In the Main class, Create a Set of user objects from the user input. Now obtain input in CSV format, create User objects and add to a List but with null values in bankName. Now Use retainAll() to remove elements in Set that are not in the present in the List.

    Input and output format:
    Refer to sample Input and Output for formatting specifications.

    Sample Input and Output 1:
    [All Texts in bold corresponds to the input and rest are output]

    Enter number of users:
    3
    Enter details of user1
    Username:
    Rikhra
    Bank name:
    Bank of Baroda
    Enter details of user2
    Username:
    Krish
    Bank name:
    Lakshmi vilas Bank
    Enter details of user3
    Username:
    Saroja
    Bank name:
    Karur vysya Bank
    Enter username(Expire in one month) seperated by comma
    Saroja,Anil,Krish
    Users going to expire within a month
    User 1
    User Name = Krish
    Bank Name = Lakshmi vilas Bank
    User 2
    User Name = Saroja
    Bank Name = Karur vysya Bank

```java title="Main.java"
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // create set of users
        Set<User> users = new HashSet<>();

        // take user input for number of users
        System.out.println("Enter number of users:");
        int n = sc.nextInt();
         sc.nextLine(); // consume newline character

        // take user input for each user and add to set
        for (int i = 1; i <= n; i++) {
            System.out.println("Enter details of user" + i);
            System.out.println("Username:");
            String username = sc.nextLine();
            System.out.println("Bank name:");
            String bankname = sc.nextLine();
            User user = new User(username, bankname);
            users.add(user);
        }

        // create list of active users from CSV input
        System.out.println("Enter username(Expire in one month) seperated by comma");
        String[] activeUsernames = sc.next().split(",");
        List<User> activeUsers = new ArrayList<>();
        for (String username : activeUsernames) {
            User user = new User(username.trim(), null);
            activeUsers.add(user);
        }

        // remove inactive users from set using retainAll method
        users.retainAll(activeUsers);

        // sort users by username
        List<User> sortedUsers = new ArrayList<>(users);
        Collections.sort(sortedUsers);

        // print active users
        System.out.println("Users going to expire within a month");
        for (int i = 0; i < sortedUsers.size(); i++) {
            User user = sortedUsers.get(i);
            System.out.println("User " + (i+1));
            System.out.println("User Name = " + user.getUsername());
            System.out.println("Bank Name = " + user.getBankname());
        }

        sc.close();
    }
}



```
```java title="User.java"
import java.util.*;

public class User implements Comparable<User> {
	private String username;
	private String bankname;
	
	public User(){
	}

	public User(String username, String bankname) {
		super();
		this.username = username;
		this.bankname = bankname;
	}

	public String getUsername() {
		return username;
	}

	public void setUsername(String username) {
		this.username = username;
	}

	public String getBankname() {
		return bankname;
	}

	public void setBankname(String bankname) {
		this.bankname = bankname;
	}
	
	//fill the code here

	@Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        User user = (User) o;
        return Objects.equals(username, user.username);
    }

    @Override
    public int hashCode() {
        return Objects.hash(username);
    }

	@Override
    public int compareTo(User o) {
        return this.username.compareTo(o.getUsername());
    }
}


```
### 2
    List removeRange() and addAll()
    We have a lot of ArrayList methods. Let’s see a few of the important ones namely removeRange() and addAll(). You will be provided with a template function that returns ArrayList of User objects.

    Write a program to get the User in the CSV format and display the details as specified in the Sample Input and Output.

    Strictly adhere to the object Oriented specifications given in the problem statement. All class names, attribute names and method names should be the same as specified in the problem statement.

    Create a class named User class with the following private attributes.

    Attributes	Datatype
    name	String
    contactNumber	String
    userName	String
    email	String
    Include getters and setters for the above attributes and the default and parameterized constructors.
    Format for the parameterized constructor is
    User(String name, String contactNumber, String userName, String email)

    Include the following method in the User class.

    Method 	Description
    void display()	This method prints the details of the User object. 

    Create a class named UserBO which extends ArrayList.

    Include the following methods in the class UserBO.

    Method 	Description
    void removeUser(int n1,int n2)	This method accepts from and to index to delete the objects from the n1 index and to the n2 index.
    Use removeRange() method.
    static UserBO getList()	This method returns an UserBO object that contains pre-coded object values in an ArrayList.

    Create a driver class called Main. In the Main method, obtain inputs from the console. Create an object for UserBO and add the User objects to it. For displaying, Iterate through the ArrayList and call the display() method of User class.

    Input format:
    The first line of input is an integer which corresponds to the number 'n' of user details to be added.
    The next 'n' line input consists of the user details in the CSV format [name, contact number, username, email].
    Then the last line of inputs consists of two integers that correspond to the from and to index.

    Output format:
    Use System.out.printf("%-20s%-20s%-20s%-20s") for displaying the User details.
    Refer to sample Input and Output for formatting specifications.

    Sample Input and Output:
    [All text in bold corresponds to the input and rest corresponds to output]

    Enter the number of User details to be added
    1
    Enter the user 1 detail in csv format
    Ram ganesh,9874587457,Ram,ramg@abc.in
    Name                Contact Number      Username            Email               
    mohan Raja          9874563210          mohan               mohan@abc.in        
    arjun Ravi          4324237             arjun               arjun@abc.in        
    Arun kumar          9845671230          arun                arun@abc.in         
    prakash raj         7548921445          prakash             raj@abc.in          
    Ram ganesh          9874587457          Ram                 ramg@abc.in         
    Enter the range to be removed from array list
    1
    3
    Name                Contact Number      Username            Email               
    mohan Raja          9874563210          mohan               mohan@abc.in        
    prakash raj         7548921445          prakash             raj@abc.in          
    Ram ganesh          9874587457          Ram                 ramg@abc.in

```java title="Main.java"
import java.util.*;

public class Main{
    public static void main(String[] args){
		//Your code here
        Scanner scanner = new Scanner(System.in);
        System.out.println("Enter the number of User details to be added");
        int n = scanner.nextInt();
        scanner.nextLine();

        UserBO userList = new  UserBO();
        UserBO predefinedList =  UserBO.getList();

	  userList.addAll(predefinedList);

        for (int i = 1; i <= n; i++) {
            System.out.printf("Enter the user %d detail in csv format\n", i);
            String[] userDetails = scanner.nextLine().split(",");
            userList.add(new User(userDetails[0].trim(), userDetails[1].trim(), userDetails[2].trim(), userDetails[3].trim()));
        }

        System.out.printf("%-20s%-20s%-20s%-20s\n", "Name", "Contact Number", "Username", "Email");
         for (User user : userList) {
            user.display();
        }

        System.out.println("Enter the range to be removed from array list");
        int n1 = scanner.nextInt();
        int n2 = scanner.nextInt();
        scanner.close();

        userList.removeUser(n1, n2);

        System.out.printf("%-20s%-20s%-20s%-20s\n", "Name", "Contact Number", "Username", "Email");
        for (User user : userList) {
            user.display();
        }
	}
}

```
```java title="User.java"
import java.util.*;

class User {
    private String name;
    private String contactNumber;
    private String userName;
    private String email;

    public User() {}

    public User(String name, String contactNumber, String userName, String email) {
        this.name = name;
        this.contactNumber = contactNumber;
        this.userName = userName;
        this.email = email;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getContactNumber() {
        return contactNumber;
    }

    public void setContactNumber(String contactNumber) {
        this.contactNumber = contactNumber;
    }

    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public void display() {
        System.out.printf("%-20s%-20s%-20s%-20s\n", name, contactNumber, userName, email);
    }
}
```
```java title="UserBO.java"
import java.util.*;

public class UserBO extends ArrayList<User>{
    
    public static UserBO getList(){
		UserBO u=new UserBO();
		u.add(new User("mohan Raja","9874563210","mohan","mohan@abc.in"));
		u.add(new User("arjun Ravi","4324237","arjun","arjun@abc.in"));
		u.add(new User("Arun kumar","9845671230","arun","arun@abc.in"));
		u.add(new User("prakash raj","7548921445","prakash","raj@abc.in"));
		return u;
	}
    //Your code here

       public void removeUser(int n1, int n2) {
        if (n1 > n2 || n1 < 0 || n2 >= this.size()) {
            return;
        }
        this.removeRange(n1, n2);
    }
}
```
### 3
    Map of Maps
    

    In our application, we gonna implement Map of Map. The value of the map is gonna be another map. This can be helpful in making counts of linked variables. We have the Address class. The address belongs to a city and state. So if we separate addresses based on each state and city maps of maps will be useful. The first map will have the state as key with a map as value. The inner map will have the city as key and count of addresses in that city as value.

    Map<String,Map<String,Integer>> is the general format and Map<state,Map<city,count>> is the format for this problem.

    Create a driver class Main and using the main method get the details, create a map, and display the details.

    Input Format:
    The first line has the number of address n.
    The next n lines have the addresses in CSV format. (area,city,state, pincode)
    Refer to the sample Input and Output for the formatting specifications.

    Output Format:
    Output has State name in the first line and each city name along with the count of address in the city in the next lines. A new line between 2 different states.
    The order of output must be in lexicographical order for both state and city.

    [All Texts in bold corresponds to the input and rest are output]
    Sample Input/Output 1:

    Enter the number of address:
    3
    Enter the address:
    Annanagar,Madurai,Tamil Nadu,666666
    Enter the address:
    Gandhipuram,Coimbatore,Tamil Nadu,123456
    Enter the address:
    KKnagar,Madurai,Tamil Nadu,678901
    Number of entries in city/state wise:

    State:Tamil Nadu
    City:Coimbatore Count:1
    City:Madurai Count:2

    Sample Input/Output 2:

    Enter the number of address:
    5
    Enter the address:
    Annanagar,Madurai,Tamil Nadu,666666
    Enter the address:
    Gandhipuram,Coimbatore,Tamil Nadu,123456
    Enter the address:
    KKnagar,Madurai,Tamil Nadu,678901
    Enter the address:
    Marathahalli,Banglore,Karnataka,123456
    Enter the address:
    Electronic City,Banglore,Karnataka,123457
    Number of entries in city/state wise:

    State:Karnataka
    City:Banglore Count:2

    State:Tamil Nadu
    City:Coimbatore Count:1
    City:Madurai Count:2

```java title="Main.java"
import java.util.*;

public class Main {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("Enter the number of address:");
        int n = sc.nextInt();
        sc.nextLine(); // consume the newline character after reading integer input

        // create the map of maps
        Map<String, Map<String, Integer>> mapOfMaps = new TreeMap<>();

        for (int i = 0; i < n; i++) {
            System.out.println("Enter the address:");
            String[] address = sc.nextLine().split(",");

            String area = address[0];
            String city = address[1];
            String state = address[2];
            String pincode = address[3];

            // update the map of maps with the current address
            if (!mapOfMaps.containsKey(state)) {
                mapOfMaps.put(state, new TreeMap<>());
            }
            Map<String, Integer> cityMap = mapOfMaps.get(state);
            if (!cityMap.containsKey(city)) {
                cityMap.put(city, 0);
            }
            cityMap.put(city, cityMap.get(city) + 1);
        }

        // print the output
        System.out.println("Number of entries in city/state wise:\n");

        for (String state : mapOfMaps.keySet()) {
            System.out.println("State:" + state);
            Map<String, Integer> cityMap = mapOfMaps.get(state);
            for (String city : cityMap.keySet()) {
                System.out.println("City:" + city + " Count:" + cityMap.get(city));
            }
            System.out.println();
        }
    }
}

```