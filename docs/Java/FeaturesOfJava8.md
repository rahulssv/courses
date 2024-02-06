# Features of Java 8
## 1
    Write a program to get Expenses details and Salary detail from the user, add it to the list, map all expense and calculate sum of all expenses using reduce from Java Streams and check for the following conditions.

    If the total expenses go above salary amount, then display the message "Expenses exceeds Salary"
    If the total expenses are less than or equal to the salary amount, then display the remaining amount as "Savings amount will be Rs<..>".
    Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names, and method names should be the same as specified in the problem statement.

    

    Create a class named Expenses with the following private attributes/variables.

    Data type	Variable
    String	expenseType
    Double	cost
    Include appropriate getters and setters.
    Include default and parameterized constructors

    expenseType include food, rent, shopping, groceries, ebBill(electricity bill)

    Create a class Main with the main method. In the method, get Expenses details from the user and also salary from the user, add it to the list, map the expense cost, and get sum using reduce method.

    

    Sample Input and Output 1:

    Enter expense for food
    800
    Enter expense for rent
    1800
    Enter expense for shopping
    2000
    Enter expense for groceries
    1500
    Enter expense for electricity
    1500
    Enter salary
    10000
    Savings amount will be Rs.2400.0

    Sample Input and Output 2:

    Enter expense for food
    4000
    Enter expense for rent
    7500
    Enter expense for shopping
    6000
    Enter expense for groceries
    5800
    Enter expense for electricity
    3000
    Enter salary
    25000
    Expenses exceeds Salary
```java title="Main.java"
import java.util.ArrayList;
import java.util.Scanner;
import java.text.DecimalFormat;

public class Main {
    public static void main(String[] args) {
        Scanner input=new Scanner(System.in);
        ArrayList<Expenses> expense=new ArrayList<>();
        System.out.println("Enter expense for food");
        expense.add(new Expenses("Food",input.nextDouble()));
        System.out.println("Enter expense for rent");
        expense.add(new Expenses("Rent",input.nextDouble()));
        System.out.println("Enter expense for shopping");
        expense.add(new Expenses("Shopping",input.nextDouble()));
        System.out.println("Enter expense for groceries");
        expense.add(new Expenses("Groceries",input.nextDouble()));
        System.out.println("Enter expense for electricity");
        expense.add(new Expenses("Electricity",input.nextDouble()));
        System.out.println("Enter salary");
        Double salary=input.nextDouble();
        Double cost=0.0;
        DecimalFormat decimal=new DecimalFormat("0.0");
        for (int i = 0; i < expense.size(); i++) {
            cost+=expense.get(i).getCost();
        }
        if(cost<=salary){
            System.out.println("Savings amount will be Rs." +decimal.format(salary-cost));
        }
        else{
            System.out.println("Expenses exceeds Salary");
        }
        input.close();

    }
}

```
```java title="Expenses.java"
/**
 * Expenses
 */
public class Expenses {

    private String expenseType;
    public String getExpenseType() {
        return expenseType;
    }
    public void setExpenseType(String expenseType) {
        this.expenseType = expenseType;
    }
    private Double cost;
    public Double getCost() {
        return cost;
    }
    public void setCost(Double cost) {
        this.cost = cost;
    }
    public Expenses(){
        
    }
    public Expenses(String expenseType,Double cost){
        this.expenseType=expenseType;
        this.cost=cost;
    }

}
```
## 2
    Event List
    The event details we have got are in a comma-separated format. But suddenly there is a need for the details in a different format. So get details in csv format and change comma into '|'. Write a program to get event details separated by a comma and change it into a format in which the details are separated by Pipe.

    Create a class Event with the following private attributes

    Attributes	Datatype
    eventName	String
    organiserName	String
    eventCost	Double
    Include appropriate getters and setters.
    Create default constructor and a parameterized constructor with arguments in order Event(String eventName, String organiserName, Double eventCost).


    Include the following public methods in the Event class

    Method	Description
    void display(List<Event> eventList)	This method takes event list as parameter and iterates
    over the list using Lambda Expression
    and displays the event details.

    Create a driver class Main to access the above class.

    Input Format:
    The first line of input corresponds to the number of events 'n'.
    The next 'n' line of inputs corresponds to the event details in the CSV format of (Event Name,Organiser Name,Event Cost).
    Refer to sample input for formatting specifications.

    Output Format:
    The output consists of event details separated by "|".
    Refer to sample output for formatting specifications.


    [All text in bold corresponds to input and rest corresponds to output]
    Sample Input and Output-1:

    Enter the number of events
    2
    Enter event details in CSV(Event Name,Organiser Name,Event Cost)
    Jaqulos,Einstein,1230000
    Hip Hop,Wright Brothers,300000
    Jaqulos|Einstein|1230000.0
    Hip Hop|Wright Brothers|300000.0
```java title="Main.java"
import java.util.ArrayList;
import java.util.Scanner;


public class Main {
    public static void main(String[] args) {
        Scanner input= new Scanner(System.in);//.useDelimiter("\\s*[,\\n]\\s*");
        System.out.println("Enter the number of events");
        int numberOfEvents= input.nextInt();
        System.out.println("Enter event details in CSV(Event Name,Organiser Name,Event Cost)");
        ArrayList<Event> events=new ArrayList<Event>();
        for (int i = 0; i < numberOfEvents; i++) {
            String eventDetail=input.next();
            eventDetail+=input.nextLine();
            String[] details= eventDetail.split(",");
            events.add(new Event(details[0],details[1],Double.parseDouble(details[2])));
        }
        
       Event.display(events);
       
        input.close();
    }
}

```
```java title="Event.java"
import java.util.ArrayList;

public class Event {
    private String eventName;
    public String getEventName() {
        return eventName;
    }
    public void setEventName(String eventName) {
        this.eventName = eventName;
    }
    private String organiserName;
    public String getOrganiserName() {
        return organiserName;
    }
    public void setOrganiserName(String organiserName) {
        this.organiserName = organiserName;
    }
    private Double eventCost;
    public Double getEventCost() {
        return eventCost;
    }
    public void setEventCost(Double eventCost) {
        this.eventCost = eventCost;
    }
    static void display(ArrayList<Event> eventList){
        eventList.forEach(t ->{
            System.out.println(t.getEventName()+"|"+t.getOrganiserName()+"|"+t.getEventCost());
        } );
    }
    public Event(){
        
    }
    public Event(String eventName,String organiserName,Double eventCost){
        this.eventName=eventName;
        this.organiserName=organiserName;
        this.eventCost=eventCost;

    }
}

```
## iAssess
    Write a program to get Ticket Booking details from the user, add it to the list, sort the list by price, and display it using sorted and forEach from Java Streams.

    Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names, and method names should be the same as specified in the problem statement.

    

    Create a class named TicketBooking with the following private attributes/variables.

    Data type	Variable
    String	customerName 
    Integer	noOfTickets
    Double	price
    Include appropriate getters and setters.
    Include default and parameterized constructors
    Include toString function

    

    Create a class Main with the main method. In the method, get TicketBooking details from the user, add it to the list, sort the list by price, and display it.

    Use the below format to print the details in table :

    System.out.format("%-10s %-15s %-15s\n", "Customer", "No Of Tickets", "Price");

    

    Sample Input and Output:

    Enter number of bookings
    3
    Enter customer name
    Ravi
    Enter number of tickets
    4
    Enter the price
    320
    Enter customer name
    Collin
    Enter number of tickets
    2
    Enter the price
    210
    Enter customer name
    Mohan
    Enter number of tickets
    1
    Enter the price
    160
    Customer   No Of Tickets   Price          
    Mohan      1               160.0          
    Collin     2               210.0          
    Ravi       4               320.0
```java title="Main.java"
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input=new Scanner(System.in);
        System.out.println("Enter number of bookings");
        Integer numberOfBookings=input.nextInt();
        ArrayList<TicketBooking> ticket=new ArrayList<>();
        for (int i = 0; i < numberOfBookings; i++) {
        System.out.println("Enter customer name");
        String customerName=input.next();
        System.out.println("Enter number of tickets");
        Integer numberOfTickets=input.nextInt();
        System.out.println("Enter the price");
        Double price=input.nextDouble();
        ticket.add(new TicketBooking(customerName, numberOfTickets, price));
        }
        //Collections.sort(ticket);
        Collections.sort(ticket, Comparator.comparing(TicketBooking::getPrice));
        System.out.format("%-10s %-15s %-15s\n", "Customer", "No Of Tickets", "Price");
        for (int i = 0; i < numberOfBookings; i++) {
            System.out.format("%-10s %-15s %-15s\n", ticket.get(i).getCustomerName(), ticket.get(i).getNoOfTickets(), ticket.get(i).getPrice());
        }

    }
}

```
```java title="TicketBooking.java"
import java.util.Comparator;

public class TicketBooking {
    private String customerName ;
    private Integer noOfTickets ;
    private Double price ;
    public String getCustomerName() {
        return customerName;
    }
    public void setCustomerName(String customerName) {
        this.customerName = customerName;
    }
    public Integer getNoOfTickets() {
        return noOfTickets;
    }
    public void setNoOfTickets(Integer noOfTickets) {
        this.noOfTickets = noOfTickets;
    }
    public Double getPrice() {
        return price;
    }
    public void setPrice(Double price) {
        this.price = price;
    }
    public TicketBooking(String customerName, Integer noOfTickets, Double price) {
        this.customerName = customerName;
        this.noOfTickets = noOfTickets;
        this.price = price;
    }
    public String toString(){
        return "";
    }
}

```


