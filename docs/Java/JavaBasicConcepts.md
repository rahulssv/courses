## Class Packaging

```java
ArrayList<Complaint> complaints=new ArrayList<Complaint>();
Stack<Customer> customers=new Stack<Customer>();
```

```java
name = input.next();
name += input.nextLine();
```

```java
complaints.add((Complaint)complaints.get(complaints.size()-1).clone());
complaints.get(complaints.size()-1).complaint=complaint;
complaints.get(i).display();
```

## Collection and Maps

```java
        String hallName;
        ArrayList<String> halls=new ArrayList<String>();
        String searchHallName=input.next();
        System.out.println(searchHallName+" hall is found in the list at position "+(halls.indexOf(searchHallName)));
```

```java
String choice;
Set<String> emails =new HashSet<>();
String email=input.next();
emails.add(email);
choice.equals("yes")
String emailString=input.next();
String[] emailSeparated=emailString.split(",");
```

```java
Map<String,ArrayList<Address>> map=new HashMap<>();
ArrayList<Address> addressList=new ArrayList<Address>();
address=input.next();
address+=input.nextLine();
String[] addressSplit=address.split(",");
addressList.add(new Address(addressSplit[0],addressSplit[1],addressSplit[2],addressSplit[3],Integer.parseInt(addressSplit[4])));
map.put(addressSplit[2], addressList);
map.get(addressSplit[2]).add(new Address(addressSplit[0],addressSplit[1],addressSplit[2],addressSplit[3],Integer.parseInt(addressSplit[4])));

Formatter formatter= new Formatter();
formatter.format("%-15s %-15s %-15s %-15s %s\n","Line 1","Line 2","City","State","Pincode");
formatter.format("%-15s %-15s %-15s %-15s %s\n",map.get(city).get(index).getAddressLine1(),map.get(city).get(index).getAddressLine2(),map.get(city).get(index).getCity(),map.get(city).get(index).getState(),map.get(city).get(index).getPincode());
System.out.println(formatter);
formatter.close();
```

```java
List<User> sortedUsers = new ArrayList<>(users);
Collections.sort(sortedUsers);
```

```java
System.out.printf("%-20s%-20s%-20s%-20s\n", "Name", "Contact Number", "Username", "Email");
```

```java
Map<String, Map<String, Integer>> mapOfMaps = new TreeMap<>();
String[] address = sc.nextLine().split(",");
if (!mapOfMaps.containsKey(state)) {
    mapOfMaps.put(state, new TreeMap<>());
}
cityMap.put(city, cityMap.get(city) + 1);
for (String state : mapOfMaps.keySet()) {
    System.out.println("State:" + state);
    Map<String, Integer> cityMap = mapOfMaps.get(state);
    for (String city : cityMap.keySet()) {
        System.out.println("City:" + city + " Count:" + cityMap.get(city));
    }
    System.out.println();
}
```

## Exception Handling

```java
try{

}
catch(NumberFormatException e){
            System.out.println(e);
        }
```

```java
try{
}
catch(ArrayIndexOutOfBoundsException e){
            System.out.println(e);
        }
```

```java
try{
        ContactDetailBO.validate(detail.mobile, detail.alternateMobile);
        System.out.println(detail.toString()); 
        input.close();
}
catch(DuplicateMobileNumberException e){
    System.out.print("DuplicateMobileNumberException: ");
    System.out.print(e.getMessage());

}
public class DuplicateMobileNumberException extends Exception {
    public DuplicateMobileNumberException(String str){
        super(str);
    }
}
public class ContactDetailBO {
    static void validate(String mobile,String alternateMobile) throws DuplicateMobileNumberException{

            if(mobile.equals(alternateMobile)){
                throw new DuplicateMobileNumberException("Mobile number and alternate mobile number are same");
            }


    }
}
```

```java
try{
} catch (Exception e) {
            // TODO: handle exception
            System.out.println("Input dates should be in the format 'dd-MM-yyyy-HH:mm:ss'");
        }
```

## Features of Java 8

```java
DecimalFormat decimal=new DecimalFormat("0.0");
```

```java
Collections.sort(ticket, Comparator.comparing(TicketBooking::getPrice));
System.out.format("%-10s %-15s %-15s\n","Customer", "No Of Tickets", "Price");
for (int i = 0; i < numberOfBookings; i++) {
    System.out.format("%-10s %-15s %-15s\n", ticket.get(i).getCustomerName(), ticket.get(i).getNoOfTickets(), ticket.get(i).getPrice());
}
```

## Fundamental Classes

```java
String string= input.next();
string.trim();
if(text.contains(string)){
    System.out.println("String is found in the document");
}
```

```java
Scanner input =new Scanner(System.in).useDelimiter("\\s*[$\\n]\\s*");

for (int index = 0; index < numberOfItems; index++) {
            StringBuilder sb=new StringBuilder();
            sb.append(item.get(index).getName());
            sb.append(",");
            sb.append(item.get(index).getType());
            sb.append(",");
            sb.append(item.get(index).getCost());
            sb.append(",");
            sb.append(item.get(index).checkAvailable());

            System.out.println(sb);
}
```

```java
public static void main(String[] args) {
    Scanner input= new Scanner(System.in);
    System.out.println("Enter the date to be formatted:(MM-dd-yyyy)");
    DateTimeFormatter dateFormat0 = DateTimeFormatter.ofPattern("MM-dd-yyyy");
    LocalDate date=LocalDate.parse(input.next(),dateFormat0);
    DateTimeFormatter dateFormat1 = DateTimeFormatter.ofPattern("EEE, MMM d, yy");
    System.out.println("Date Format with EEE, MMM d, yy : "+dateFormat1.format(date));
    DateTimeFormatter dateFormat2 = DateTimeFormatter.ofPattern("dd.MM.yyyy");
    System.out.println("Date Format with dd.MM.yyyy : "+dateFormat2.format(date));
    DateTimeFormatter dateFormat3 = DateTimeFormatter.ofPattern("dd/MM/yyyy");
    System.out.println("Date Format with dd dd/MM/yyyy : "+dateFormat3.format(date));
    input.close();
   } 
```

```java
public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Enter the code");
        String code = scanner.nextLine();

        StringBuilder formattedCode = new StringBuilder(code);

        if (code.substring(0, 2).equals("DH")) {
            formattedCode.replace(0, 2,"DEL");
        } else if (code.substring(0, 2).equals("MB")) {
            formattedCode.replace(0, 2,"MUB");
        } else if (code.substring(0, 2).equals("KL")) {
            formattedCode.replace(0, 2,"KOL");
        }

        int referenceNumber = Integer.parseInt(code.substring(2));

        formattedCode.replace(3, formattedCode.length()+1, String.format("%05d", referenceNumber));

        System.out.println("Formatted code");
        System.out.println(formattedCode.toString());
    }
```

## JDBC

```java
import java.sql.*;
import java.util.ResourceBundle;
public class DBConnection {
    public static Connection getConnection() throws ClassNotFoundException, SQLException {        
        ResourceBundle rb = ResourceBundle.getBundle("oracle");
        String url = rb.getString("db.url");
        String username = rb.getString("db.username");
        String password = rb.getString("db.password");
        //fill your code here

        DriverManager.registerDriver(new oracle.jdbc.driver.OracleDriver());

        return DriverManager.getConnection(url, username, password);
    }
}
```

```java
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

## Language Fundamentals

```java

```

## Multithreading

```java
import java.util.ArrayList;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input=new Scanner(System.in);
        System.out.println("Enter Number of Counters :");
        int numberOfCounters=input.nextInt();
        String textForCounter;
        ArrayList<Counter> threads=new ArrayList<>();
        for (int i = 0; i < numberOfCounters; i++) {
            System.out.println("Enter text for counter "+(i+1)+" :");
            textForCounter=input.next();
            textForCounter+=input.nextLine();
            threads.add(new Counter(textForCounter));
            threads.get(i).run();
        }
        int[]frequency=new int[256];
        for (int i = 0; i < numberOfCounters; i++) {

            frequency=threads.get(i).getFrequency();
            System.out.println("Counter "+(i+1)+" Result :");
            for (int j = 0; j < frequency.length; j++) {
                if(frequency[j]!=0){

                    System.out.print((char)j+":"+frequency[j]+" ");
                }

            }
            System.out.println("");
        }


    }
}




public class Counter extends Thread{
    int[] frequency=new int[256];
    String counter;
    public void run(){
            for (int i = 0; i < counter.length(); i++) {
                frequency[(int)counter.charAt(i)]++;
            }
    }
    public int[] getFrequency(){
        return this.frequency;
    }
    public Counter (String counter){
        this.counter=counter;
    }

}
```

## Object Oriented Programming

```java

```

# Streams and Files

```java
BufferedReader br=new BufferedReader(new FileReader("input.csv"));
```

```java
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


