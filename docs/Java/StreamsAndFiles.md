# Streams and Files
## 1
    File handling introduction

    File handling is an important technique that you need to accustom to it. File reading and writing are types of handling. Let's practice file reading for now. There is a Class called FileReader that will help us with file reading. You'll be provided with a file that contains the data in CSV format. Using FileReader, read the file and parse the data contained in it to below specified format.

    Provided "input.csv" which have User details. Read all the user information stored in CSV format and create a user object by parsing the line. Add all the user objects to the ArrayList. At last, display the user list.

    Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names and method names should be the same as specified in the problem statement.

    Create a class called User with following private attributes

    Attributes	Datatype
    name	String
    email	String
    username	String
    password	String

    Include getters and setters.
    Create a default constructor and parameterized constructor.
    Format for the parameterized constructor is User(String name, String email, String username, String password)

    Create UserBO class with following methods

    Method 	Description
    public List<User> readFromFile(BufferedReader br)	This method accepts the BufferedReader object as input and parses the data
    in the file to User objects and adds them to a list. Finally, it returns the list of User objects.
    public void display(List<User> list)	This method accepts a list of User objects and displays the user details by iterating the list.
    Use "%-15s %-20s %-15s %s\n" to print the details.

    Create a driver class called Main. If the List of Users is empty print "The list is empty" in the main method. Else display the user detail by calling the display method.

    Note : Use BufferedReader br=new BufferedReader(new FileReader("input.csv")) for file reading.

    Input format:
    Read the input from the "input.csv" file which contains the user details.

    Output format:
    Use "%-15s %-20s %-15s %s\n" to print statements for the heading of the details in the Main method.

    Sample Input: (input.csv)




    Sample Output :

    Name            Email                Username        Password
    Ram             ram@gmail.com        ram             ram123
    krish           krish@gmail.com     krish           abc

```java title="input.csv"
Ram,ram@gmail.com,ram,ram123
krish,krish@gmail.com,krish,abc
```
```java title="Main.java"
import java.io.BufferedReader;
import java.io.FileReader;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        try{
            BufferedReader br=new BufferedReader(new FileReader("input.csv"));
            UserBO user=new UserBO();
            ArrayList<User> userData=user.readFromFile(br);
            if(userData.isEmpty()){
                System.out.println("The list is empty");
            }
            else{
                user.display(userData);
            }
        }
        catch(Exception e){
            System.out.println("File Not Found");
        }
    }
    
    

}

```
```java title="User.java"
/**
 * User
 */
public class User {

    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    private String email;
    public String getEmail() {
        return email;
    }
    public void setEmail(String email) {
        this.email = email;
    }
    private String username;
    public String getUsername() {
        return username;
    }
    public void setUsername(String username) {
        this.username = username;
    }
    private String password;

    public String getPassword() {
        return password;
    }
    public void setPassword(String password) {
        this.password = password;
    }
    public User(){

    }
    public User(String name, String email, String username, String password){
        this.name=name;
        this.email=email;
        this.username=username;
        this.password=password;
    }

}
```
```java title="UserBO.java"
import java.io.BufferedReader;
import java.util.ArrayList;
import java.util.Formatter;

public class UserBO {
    public ArrayList<User> readFromFile (BufferedReader br){
        ArrayList<User> user= new ArrayList<User>();
        try{
            
                    String row;
                    while((row=br.readLine())!=null){
                        String[] userData= row.split(",");
                        user.add(new User(userData[0],userData[1],userData[2],userData[3]));
                    }
            
        }catch(Exception e){
            System.out.println("Exception");
        }
        return user;
        
    }
    public void display(ArrayList<User> list){
        Formatter formatter=new Formatter();
        formatter.format("%-15s %-20s %-15s %s\n","Name","Email","Username","Password");
        
        for (int i = 0; i < list.size(); i++) {
            formatter.format("%-15s %-20s %-15s %s\n",list.get(i).getName(),list.get(i).getEmail(),list.get(i).getUsername(),list.get(i).getPassword());
    
        }
        System.out.print(formatter);
    }
}

```
## 2
    File Writing
    The file we write can be of several formats. But for now, we are just going to write a CSV text file, in which all the fields are separated by comma delimiter. Use FileWriter and BufferedWriter to write the data to a file.

    As a first thing, we are gonna create a file that contains the record of all the users registered. So write a program that can write all the user details from the console into a file "output.csv".

    Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names and method names should be the same as specified in the problem statement.

    Create a class User with the following attributes, 

    Attribute	Data type
    name	String
    mobileNumber	String
    username	String
    password	String
    
    Create a class UserBO with the following methods,

    Method	Description
    public static void writeFile(ArrayList<User> userList, BufferedWriter bw)	This method gets a list of the user as argument and
    writes all the user details in the list into a file

    Create a driver class Main and use the main method to get the details from the user.

    Input format:
    The first line of input consists of an integer that corresponds to the number of users.
    The next n line of input consists of user details in  the CSV format (name, mobileNumber, username, password)
    Refer to sample Input for other further details.

    Output format:
    Write the user details in the output.csv file.
    Refer to sample Output for other further details.

    Sample Input:
    [All Texts in bold corresponds to the input and rest are output]

    Enter the number of users:
    3
    Enter the details of user :1
    Jane,1234,jane,jane
    Enter the details of user :2
    John,5678,john,john
    Enter the details of user :3
    Jill,1357,jill,jill

    

    Sample Output: (output.csv)

```java title="output.csv"
Jane,1234,jane,jane
John,5678,john,john
Jill,1357,jill,jill

```
```java title="Main.java"

import java.io.BufferedWriter;
import java.io.FileWriter;
import java.util.ArrayList;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        try{
            Scanner input= new Scanner(System.in).useDelimiter("\\s*[,\\n]\\s*");
            FileWriter writer = new FileWriter("output.csv");
            BufferedWriter bw=new BufferedWriter(writer);
            
            ArrayList<User> userData=new ArrayList<User>();
            System.out.println("Enter the number of users:");
            int numberOfUsers=input.nextInt();
            for (int index = 0; index < numberOfUsers; index++) {
                System.out.println("Enter the details of user :"+(index+1));
                userData.add(new User(input.next(),input.next(),input.next(),input.next()));
            }
            UserBO.writeFile(userData, bw);
            input.close();
        }
        catch(Exception e){
            System.out.println("File Not Found");
        }
    }
    
    

}

```
```java title="User.java"
/**
 * User
 */
public class User {

    private String name;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    private String email;
    public String getEmail() {
        return email;
    }
    public void setEmail(String email) {
        this.email = email;
    }
    private String username;
    public String getUsername() {
        return username;
    }
    public void setUsername(String username) {
        this.username = username;
    }
    private String password;

    public String getPassword() {
        return password;
    }
    public void setPassword(String password) {
        this.password = password;
    }
    public User(){

    }
    public User(String name, String email, String username, String password){
        this.name=name;
        this.email=email;
        this.username=username;
        this.password=password;
    }

}
```
```java title="UserBO.java"

import java.io.BufferedWriter;
import java.io.IOException;
import java.util.ArrayList;


public class UserBO {
        public static void writeFile(ArrayList<User> userList, BufferedWriter bw){
            try {
            for (int i = 0; i < userList.size(); i++) {
                /* String data=userList.get(i).getName()+","+userList.get(i).getEmail()+","+userList.get(i).getUsername()+","+userList.get(i).getPassword()+"\n";
                   */
                bw.write(userList.get(i).getName());
                    bw.write(",");
                    bw.write(userList.get(i).getEmail());
                    bw.write(",");
                    bw.write(userList.get(i).getUsername());
                    bw.write(",");
                    bw.write(userList.get(i).getPassword());
                    bw.write("\n");
                    
                   /* bw.write(data);*/
                                    
                
                
            }
            
                bw.close();
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
            
        }
}

```
## 3
    Read and Write
    In our application, we are gonna read the contents of a file and write it into another file with some conditions. There can be many events for the same organization or owner. But we want only one event for every owner available. So we are gonna read the event details from the file "input.txt" and then write the event details into "output.txt" but after removal of duplicate entries.

    Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names and method names should be the same as specified in the problem statement.

    Create a class Event with the following private attributes

    Attributes	Datatype
    eventName	String
    attendeesCount	Integer
    ownerName	String
    Include appropriate getters and setters
    Create default constructor and a parameterized constructor with arguments in order Event(String eventName, Integer attendeesCount, String ownerName).

    Create a class EventBO to access the above class. Include the following public methods.

    Method	Description
    public List<Event> readFromFile(BufferedReader br)	This method accepts the BufferedReader object as input and parses the data in the file to Event objects
    and then adds them to a list. Finally, it returns the list of Event objects.
    void writeFile(List<Event> eventList,FileWriter fr)	This method takes event list and file writer as the arguments and writes into "output.txt" with
    the removal of duplicate event details (i.e) an event having the same owner name.
    

    Create a driver class named Main which reads data from console and to test the above class.

    Input:
    Read the contents[event details] from the file "input.txt".

    Output:
    Write the contents[event details] with the removal of duplicate events into the "output.txt".

    Sample Input: (input.txt)




    Sample Output: (output.txt)


```java title="input.txt"
Jill,1,jill
Jill,1,jill
```
```java title="output.txt"
Jill,1,jill

```
```java title="Main.java"
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.FileWriter;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        try{
            BufferedReader br=new BufferedReader(new FileReader("input.txt"));
            EventBO event=new EventBO();
            ArrayList<Event> eventData=event.readFromFile(br);
            if(eventData.isEmpty()){
                System.out.println("The list is empty");
            }
            
            
            FileWriter writer = new FileWriter("output.txt");
            event.writeFile(eventData,writer);
        }
        catch(Exception e){
            System.out.println("File Not Found");
        }
    }
    
    

}
```
```java title="Event.java"

public class Event {
    private String eventName;
    public String getEventName() {
        return eventName;
    }
    public void setEventName(String eventName) {
        this.eventName = eventName;
    }
    private Integer attendeesCount;
    public Integer getAttendeesCount() {
        return attendeesCount;
    }
    public void setAttendeesCount(Integer attendeesCount) {
        this.attendeesCount = attendeesCount;
    }
    private String ownerName;
    public String getOwnerName() {
        return ownerName;
    }
    public void setOwnerName(String ownerName) {
        this.ownerName = ownerName;
    }
    public Event(){

    }
    public Event(String eventName, Integer attendeesCount, String ownerName){
        this.eventName=eventName;
        this.attendeesCount=attendeesCount;
        this.ownerName=ownerName;
    }
    
}

```
```java title="EventBO.java"
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.HashSet;
import java.util.Set;

public class EventBO {
    public ArrayList<Event> readFromFile(BufferedReader br) {
        ArrayList<Event> event = new ArrayList<Event>();
        try {

            String row;
            while ((row = br.readLine()) != null) {
                String[] userData = row.split(",");
                event.add(new Event(userData[0], Integer.parseInt(userData[1]), userData[2]));
            }

        } catch (Exception e) {
            System.out.println("Exception");
        }
        return event;

    }

    public void writeFile(ArrayList<Event> eventList, FileWriter writer) {
        try {
            BufferedWriter bw = new BufferedWriter(writer);
            Set<String> set = new HashSet<>();
            for (int i = 0; i < eventList.size(); i++) {
                if (set.contains(eventList.get(i).getOwnerName())) {
                    continue;
                } else{
                    set.add(eventList.get(i).getOwnerName());
                    bw.write(eventList.get(i).getEventName());
                    bw.write(",");
                    bw.write(String.valueOf(eventList.get(i).getAttendeesCount()));
                    bw.write(",");
                    bw.write(eventList.get(i).getOwnerName());
                    bw.write("\n");
                }
                    
            }
            /*for (int i = 0; i < eventList.size(); i++) {
                
                 * String
                 * data=userList.get(i).getName()+","+userList.get(i).getEmail()+","+userList.
                 * get(i).getUsername()+","+userList.get(i).getPassword()+"\n";
                 
                if (eventList.lastIndexOf(eventList.get(i).getOwnerName()) == i) {
                    
                }

                // System.out.println(eventList.get(i).getAttendeesCount());
                /* bw.write(data); 
            }*/

            bw.close();
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }
}

```

## iAssess
    IO - Simple File Write
    
    Write a Java program to record the airport details into the file. Get the airport details name, cityName and countryCode from the user and write that information in a comma-separated format in a file (CSV).
    Below is the format of the output file.
    <name>,<cityName>,<countryCode>
    eg: Cochin International Airport,Cochin,IN
    Create a main class "Main.java"
    
    Input and Output Format:
    Get the airport details name, cityName and country code from the user.
    Print the airport details in the output file airport.csv
    Sample Input :
    [All text in bold corresponds to input and the rest corresponds to output]
    Enter the name of the airport
    Cochin International Airport
    Enter the city name
    Cochin
    Enter the country code
    IN

    Sample Output:


```java title="airport.csv"
Cochin International Airport,Cochin,IN
```
```java title="Main.java"
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input=new Scanner(System.in);
        System.out.println("Enter the name of the airport");
        String nameOfAirport=input.next();
        nameOfAirport+=input.nextLine();
        System.out.println("Enter the city name");
        String cityName=input.next();
        System.out.println("Enter the country code");
        String countryCode=input.next();
        FileWriter file;
        try {
            file = new FileWriter("airport.csv");
            BufferedWriter bw=new BufferedWriter(file);
            bw.write(nameOfAirport);
            bw.write(",");
            bw.write(cityName);
            bw.write(",");
            bw.write(countryCode);
            bw.close();
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        input.close();
        
        
        

    }   
}

```
