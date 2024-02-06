# Object Oriented Programming
## 1
    The class Department has been created with the following attributes,
    Attribute	Datatype
    departmentName	String
    staff	Staff

    The class Staff has been created with the following attributes,
    Attribute 	Datatype
    staffName	String
    designation	String

    Include the following method in the Department class,
    Method 	Description
    public displayStaff()	This method displays "staffName is working in the departmentName department as designation".

    Create a driver class Main, in the main method get the inputs from user, create the objects and call the methods.

    Input and Output format:
    Refer to sample Input and Output for formatting specifications.

    Sample Input and Output:
    [All text in bold corresponds to the input and rest corresponds to the output]

    Enter the name of the staff:
    Jane
    Enter the staff designation:
    Associate Professor
    Enter the department name:
    Physics
    Jane is working in the Physics department as Associate Professor

```java title="Main.java"
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner input= new Scanner(System.in);
        Department department = new Department();
        System.out.println("Enter the name of the staff:");
        department.staff.staffName=input.nextLine();
        System.out.println("Enter the staff designation:");
        department.staff.designation=input.nextLine();
        System.out.println("Enter the department name:");
        department.departmentName=input.nextLine();
        department.displayStaff();
        input.close();
    }
}

```
```java title="Staff.java"

public class Staff {
    String staffName;
    String designation;
}

```
```java title="Department.java"
/**
 * Department
 */
public class Department {

    String departmentName;
    Staff staff= new Staff() ;
    public void displayStaff() {
        System.out.println(staff.staffName +" is working in the "+departmentName+" department as "+staff.designation);
    }
}
```
## 2
    Bank Account
    Inheritance in Java is same as that of inheritance in real Life. A class which inherits another class obtains all the latter's attributes and methods. The former is called Child class whilst the latter is called Parent class. This phenomenon would be very promising in applications dealing with multiple classes that are constituted by similar or more likely same attributes. You 'll get to know the importance of inheritance from the following problem. All type of accounts in a bank have common attributes which can be inherited from an Account class.

    The class Account has been created with the following protected attributes,

    Attributes	Datatype
    accName	String
    accNo	String
    bankName	String
    Include appropriate getters and setters.


    Include the following protected methods.

    Method	Description
    public void display()	This protected method displays the account details
    

    Create a class CurrentAccount with following private attributes which extends Account class

    Attributes	Datatype
    tinNumber	String
    Create default constructor and a parameterized constructor with arguments in order CurrentAccount(String accName,String accNo,String bankName,String tinNumber).
    Include appropriate getters and setters.


    Include the following public methods.

    Method	Description
    public void display()	This method calls the super class display().
    This public method displays the TIN number.
    Call this method with the reference of base class.
    

    Create a class SavingsAccount with following private attributes which extends Account class

    Attributes	Datatype
    orgName	String
    Create default constructor and a parameterized constructor with arguments in order SavingsAccount(String accName,String accNo,String bankName,String orgName).
    Include appropriate getters and setters.


    Include the following public methods.

    Method	Description
    public void display()	This method calls the super class display().
    This public method displays the Organisation Name.
    Call this method with the reference of base class.
    

    Create a driver class named Main to test the above class.

    Note:
    Strictly adhere to the Object-Oriented Specifications given in the problem statement.All class names, attribute names and method names should be the same as specified in the problem statement.

    Input Format:
    The first input corresponds to choose current or savings account
    The next line consists of account name,account number,bank name,org name or tin number (according to chosen account type)

    Output Format
    The output consists of account details  and TIN number or Organisation name
    Refer sample output for formatting specifications.

    Sample Input/Output-1:
    Choose Account Type
    1.Savings Account
    2.Current Account
    1
    Enter Account details in comma separated(Account Name,Account Number,Bank Name,Organisation Name)
    Morsh,033808020000879,Baroda,Amphisoft
    Account Name:Morsh
    Account Number:033808020000879
    Bank Name:Baroda
    Organisation Name:Amphisoft

    Sample Input/Output-2:
    Choose Account Type
    1.Savings Account
    2.Current Account
    2
    Enter Account details in comma separated(Account Name,Account Number,Bank Name,TIN Number)
    Krish,131231451,ICICI,798902
    Account Name:Krish
    Account Number:131231451
    Bank Name:ICICI
    TIN Number:798902

```java title="Main.java"
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner input= new Scanner(System.in);
        System.out.println("Choose Account Type\n1.Savings Account\n2.Current Account");
        int choice = input.nextInt();
        switch (choice) {
            case 1:
                
                System.out.println("Enter Account details in comma separated(Account Name,Account Number,Bank Name,Organisation Name)");
                Account savings= new SavingsAccount(input.useDelimiter("[,]").next(),input.useDelimiter("[,]").next(),input.useDelimiter("[,]").next(),input.useDelimiter("[,\\n]").next());
                savings.display();
                break;
            case 2:
                System.out.println("Enter Account details in comma separated(Account Name,Account Number,Bank Name,TIN Number)");
                Account current= new CurrentAccount(input.useDelimiter("[,]").next(),input.useDelimiter("[,]").next(),input.useDelimiter("[,]").next(),input.useDelimiter("[,\\n]").next());
                current.display();
                break;
            default:
                break;
        }
        input.close();
    }
}

```
```java title="Account.java"
/**
 * Account
 */
public class Account {

    protected String accName;
    protected String accNo;
    protected String bankName;
    protected void display() {
        
    }
}

```
```java title="SavingsAccount.java"
public class SavingsAccount extends Account {
    private String orgName;
    public SavingsAccount(){

    }
    public SavingsAccount(String accName,String accNo,String bankName,String orgName){
        this.accName= accName;
        this.accNo= accNo;
        this.bankName=bankName;
        this.orgName= orgName;
    }
    public void display(){
        System.out.println("Account Name:"+accName);
        System.out.println("Account Number:"+accNo);
        System.out.println("Bank Name:"+bankName);
        System.out.println("Organisation Name:"+orgName);
    }
}

```
```java title="CurrentAccount.java"
public class CurrentAccount extends Account {
    private String tinNumber;
    public CurrentAccount(){

    }
    public CurrentAccount(String accName,String accNo,String bankName,String tinNumber){
        this.accName= accName;
        this.accNo= accNo;
        this.bankName=bankName;
        this.tinNumber= tinNumber;
    }
    public void display(){
        System.out.println("Account Name:"+accName);
        System.out.println("Account Number:"+accNo);
        System.out.println("Bank Name:"+bankName);
        System.out.println("TIN Number:"+tinNumber);
    }
}

```
## 3
    Abstract Class - FundTransfer

    Let's try an application like a fund transfer for our larger application. So, in fund transfer, there are 3 types of NEFT/IMPS/RGTS. We can create an abstract class FundTransfer. And extend it in the child classes. Create an abstract method transfer and implement it in all the child classes.

    Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names and method names should be the same as specified in the problem statement.

    Create an abstract class FundTransfer with following private attributes,

    Attributes	Datatype
    accountNumber	String
    balance	Double
    
    Include the following methods in the class FundTransfer.

    Method	Description
    Boolean validate(Double transfer)	To check if the accountNumber is 10 digits, the transfer amount is non-negative and less than balance.
    If all cases are satisfied then return true, if not return false
    Boolean transfer(Double transfer)	It is an abstract method with no definition

    Create a class NEFTTransfer which extends FundTransfer.

    Include the following method in the class NEFTTransfer.

    Method	Description
    Boolean transfer(Double transfer)	To check whether the transfer amount+5% of the transfer amount is less than balance.
    If then subtracts transfer amount and 5% service charge from balance and return true, if not return false

    Create a class IMPSTransfer which extends FundTransfer.

    Include the following method in the class IMPSTransfer.

    Method	Description
    Boolean transfer(Double transfer)	To check whether transfer amount+2% of transfer amount is less than balance.
    If then subtracts transfer amount and 2% service charge from balance and return true, if not return false.

    Create a class RTGSTransfer which extends FundTransfer.

    Include the following method in the class RTGSTransfer.

    Method	Description
    Boolean transfer(Double transfer)	To check whether the transfer amount is greater than Rs.10000.
    If then subtracts transfer amount from balance and return true, if not return false.
    
    Include appropriate getters/setters, constructors with super() to create objects. Write a driver class Main to test them.

    Input format:
    Refer to sample Input and Output for the details and for the formatting specifications.

    Output format:
    Print “Transfer occurred successfully” in the main method. If the transfer function returns true.
    Print "Account number or transfer amount seems to be wrong" in the main method. If validate function returns false.
    Print "Transfer could not be made" in the main method. If the transfer function returns false.
    Refer to sample Input and Output for formatting specifications.

    Note: All Texts in bold corresponds to the input and rest are output

    Sample Input and Output 1:

    Enter your account number:
    1234567890
    Enter the balance of the account:
    10000
    Enter the type of transfer to be made:
    1.NEFT
    2.IMPS
    3.RTGS
    1
    Enter the amount to be transferred:
    2000
    Transfer occurred successfully
    Remaining balance is 7900.0

    Sample Input and Output 2:

    Enter your account number:
    1111111
    Enter the balance of the account:
    10000
    Enter the type of transfer to be made:
    1.NEFT
    2.IMPS
    3.RTGS
    2
    Enter the amount to be transferred:
    1000
    Account number or transfer amount seems to be wrong

    Sample Input and Output 3:

    Enter your account number:
    1234567890
    Enter the balance of the account:
    50000
    Enter the type of transfer to be made:
    1.NEFT
    2.IMPS
    3.RTGS
    3
    Enter the amount to be transferred:
    7500
    Transfer could not be made

    
```java title="Main.java"
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner input= new Scanner(System.in);
        System.out.println("Enter your account number:");
        String accNo = input.nextLine();
        System.out.println("Enter the balance of the account:");
        Double accBal= input.nextDouble();
        System.out.println("Enter the type of transfer to be made:\n1.NEFT\n2.IMPS\n3.RTGS");
        int choice = input.nextInt();
        Double amount;
        switch (choice) {
            case 1:
                System.out.println("Enter the amount to be transferred:");
                amount=input.nextDouble();
                FundTransfer neft =new NEFTTransfer(accNo,accBal);
                if(neft.validate(amount)){
                    if(neft.transfer(amount)){
                    System.out.println("Transfer occurred successfully");
                    System.out.println("Remaining balance is "+neft.getBalance());
                    }
                    else{
                        System.out.println("Transfer could not be made");
                    }
                }
                else{
                    System.out.println("Account number or transfer amount seems to be wrong");
                }
                break;
            case 2:
                System.out.println("Enter the amount to be transferred:");
                amount=input.nextDouble();
                FundTransfer imps =new IMPSTransfer(accNo,accBal);
                if(imps.validate(amount)){
                    if(imps.transfer(amount)){
                    System.out.println("Transfer occurred successfully");
                    System.out.println("Remaining balance is "+imps.getBalance());
                    }
                    else{
                        System.out.println("Transfer could not be made");
                    }
                }
                else{
                    System.out.println("Account number or transfer amount seems to be wrong");
                }
                break;
            case 3:
                System.out.println("Enter the amount to be transferred:"); 
                amount=input.nextDouble();
                FundTransfer rtgs =new RTGSTransfer(accNo,accBal);  
                if(rtgs.validate(amount)){
                    if(rtgs.transfer(amount)){
                    System.out.println("Transfer occurred successfully");
                    System.out.println("Remaining balance is "+rtgs.getBalance());
                    }
                    else{
                        System.out.println("Transfer could not be made");
                    }
                }
                else{
                    System.out.println("Account number or transfer amount seems to be wrong");
                }
                break;
            default:
                break;
        }
        input.close();
    }
}

```
```java title="FundTransfer.java"
public abstract class FundTransfer {
    private String accountNumber;
    private Double balance;
    public Boolean validate(Double transfer){
        if(accountNumber.length()>10||accountNumber.length()<10 || transfer<0 || transfer >= balance){
            
            return false;
        }
        else {
            
            return true;
        }
    }
    public abstract Boolean transfer(Double transfer);
    
    public void setAccount(String accountNumber){
        this.accountNumber=accountNumber;
    }
    public void setBalance(Double balance){
        this.balance=balance;
        
    }
    public Double getBalance(){
        return balance;
    }


}

```
```java title="IMPSTransfer.java"
/**
 * IMPSTransfer
 */
public class IMPSTransfer extends FundTransfer{

    public Boolean transfer(Double transfer){
        
            if((transfer +(0.02*transfer))<super.getBalance() ){
                super.setBalance(super.getBalance()-transfer-0.02*transfer);
            return true;
            }
            
            else{
                return false;
            }        
    }
    public IMPSTransfer(String accNo,Double accBal){
        super.setAccount(accNo);
        super.setBalance(accBal);
    }
}
```
```java title="NEFTTransfer.java"
public class NEFTTransfer  extends FundTransfer {
    public Boolean transfer(Double transfer){
            if((transfer +(0.05*transfer))<super.getBalance() ){
                super.setBalance(super.getBalance()-transfer-0.05*transfer);
            return true;
            }
            
            else{
                return false;
            }
    }
    
    public NEFTTransfer(String accNo,Double accBal){
        super.setAccount(accNo);
        super.setBalance(accBal);
    }

}

```
```java title="RTGSTransfer.java"
public class RTGSTransfer extends FundTransfer {
    public Boolean transfer(Double transfer){
            if(transfer>10000 ){
                super.setBalance(super.getBalance()-transfer);
            return true;
            }
            else{
                
                return false;
            }
    }
    public RTGSTransfer(String accNo,Double accBal){
        super.setAccount(accNo);
        super.setBalance(accBal);
    }
}

```
## iAssess
### 1
    super() method

    So far you have learned about the basics of inheritance and created 2 child classes for a parent class and displayed the details. Now let's go for simple manipulation along with superclass. This will be needed in our application as some class share common attributes so they can be grouped as child classes of some superclass.

    To try this let's create a parent class Event with following attributes,
    Attributes	Datatype
    name	String
    detail	String
    type	String
    ownerName	String
    costPerDay	Double

    Then create child class Exhibition that extends Event with the following attribute,
    Attributes	Datatype
    noOfStall	Integer

    And create another child class StageEvent that extends Event with the following attribute,
    Attributes	Datatype
    noOfSeats	Integer

    Add suitable constructor (with super() if necessary) and getters/setters for the classes.

    Get the starting and ending date of the event from the user and calculate the total cost for the event. Then calculate GST for the event according to the event type.

    GST is 5% for Exhibition and 15% for StageEvent.

    Input format:
    The first line of input is an integer which corresponds to the choice of event.
    The second line of input is the details of the event in the CSV format
    (name, detail, type, owner name,costPerDay,noOfStall)  for the Exhibition.  
    (name, detail, type, owner name,costPerDay,noOfSeats)  for the stage event.
    The next line is the starting date of the event.
    The last line of the input is the ending date of the event.

    Output format:
    The output is the GST to be paid for the event.
    Refer to sample input/output for other further details and format of the output.

    [All Texts in bold corresponds to the input and rest are output]
    Sample Input/Output 1:

    Enter your choice:
    1.Exhibition event
    2.Stage event
    1
    Enter the details of exhibition:
    Science Fair,Exciting experiments,Fair,John,10000.00,10
    Enter the starting date of the event:
    03-01-2018
    Enter the ending date of the event:
    06-01-2018
    The GST to be paid is Rs.1500.0

    Sample Input/Output 2:

    Enter your choice:
    1.Exhibition event
    2.Stage event
    2
    Enter the details of stage event:
    Movie Award Function,Awards for all category,Award function,Joe,100000,10000
    Enter the starting date of the event:
    07-01-2018
    Enter the ending date of the event:
    09-01-2018
    The GST to be paid is Rs.30000.0

```java title="Main.java"
import java.text.DecimalFormat;
import java.time.LocalDate;
import java.time.Period;
import java.time.format.DateTimeFormatter;
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        try {
            LocalDate start;
        LocalDate end;
        DateTimeFormatter dateFormat = DateTimeFormatter.ofPattern("dd-MM-yyyy");
        DecimalFormat df = new DecimalFormat("0.0");
        Period period;
        int days;
        Scanner input= new Scanner(System.in).useDelimiter("\\s*[,\\n]\\s*");
        System.out.println("Enter your choice:\n1.Exhibition event\n2.Stage event");
        int choice=input.nextInt();
        switch (choice) {
            case 1:
                System.out.println("Enter the details of exhibition:");                
                Event exhibition = new Exhibition(input.next(),input.next(),input.next(),input.next(),input.nextDouble(),input.nextInt());
                           
                System.out.println("Enter the starting date of the event:");
                start= LocalDate.parse(input.next(),dateFormat);
                System.out.println("Enter the ending date of the event:");
                end=LocalDate.parse(input.next(),dateFormat);
                period = Period.between(start,end);
                days =period.getDays();

                System.out.println("The GST to be paid is Rs."+ df.format(days*0.05*exhibition.getCostPerDay()));
                
                break;
                
            case 2:
                System.out.println("Enter the details of stage event:");
                Event stage = new StageEvent(input.next(),input.next(),input.next(),input.next(),input.nextDouble(),input.nextInt());
                System.out.println("Enter the starting date of the event:");
                start= LocalDate.parse(input.next(),dateFormat);
                System.out.println("Enter the ending date of the event:");
                end=LocalDate.parse(input.next(),dateFormat);
                period = Period.between(start,end);
                days =period.getDays();
                System.out.println("The GST to be paid is Rs."+ df.format(days*0.15*stage.getCostPerDay()));
                
                
                break;
            default:
                break;
        }
        input.close();
        } catch (Exception e) {
            // TODO: handle exception
        }
        
    }
}

```
```java title="Event.java"
/**
 * Event
 */
public class Event {

    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    private String detail;

    public String getDetail() {
        return detail;
    }

    public void setDetail(String detail) {
        this.detail = detail;
    }

    private String type;

    public String getType() {
        return type;
    }

    public void setType(String type) {
        this.type = type;
    }

    private String ownerName;

    public String getOwnerName() {
        return ownerName;
    }

    public void setOwnerName(String ownerName) {
        this.ownerName = ownerName;
    }

    private Double costPerDay;

    public Event() {
        super();
    }

    public Double getCostPerDay() {
        return costPerDay;
    }

    public void setCostPerDay(Double costPerDay) {

        this.costPerDay = costPerDay;
    }

    public Event(String name, String detail, String type, String ownerName, Double costPerDay) {
        super();
        this.name = name;
        this.detail = detail;
        this.type = type;
        this.ownerName = ownerName;
        this.costPerDay = costPerDay;
    }
}
```
```java title="Exhibition.java"
public class Exhibition extends Event{
    private Integer noOfStall;
    public Exhibition(){
        super();
    }

public Exhibition(String name, String detail, String type, String ownerName, Double costPerDay, Integer noOfStall) {
        super(name, detail, type, ownerName, costPerDay);
        this.noOfStall = noOfStall;
    }

public Integer getNoOfStall() {
    return noOfStall;
}

public void setNoOfStall(Integer noOfStall) {
    this.noOfStall = noOfStall;
}

}

```
```java title="StageEvent.java"
public class StageEvent extends Event{
    private Integer noOfSeats;
    public StageEvent(){
        super();
    }
    
    public StageEvent(String name, String detail, String type, String ownerName, Double costPerDay, Integer noOfSeats) {
        super(name, detail, type, ownerName, costPerDay);
        this.noOfSeats = noOfSeats;
    }
    
   

    public Integer getNoOfSeats() {
        return noOfSeats;
    }

    public void setNoOfSeats(Integer noOfSeats) {
        this.noOfSeats = noOfSeats;
    }
    
}

```
### 2
    Interface

    The Interface defines a rule that any classes that implement it should override all the methods. Let's implement Interface in our application. We'll start simple, by including display method in the Stall interface. Now all types of stalls that implement the interface should override the method.

    Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names and method names should be the same as specified in the problem statement.

    Create an interface Stall  with the following method

    Method          Description

    void display()  abstract method.


    Create a class GoldStall which implements Stall interface with the following private attributes

    Attribute   Datatype

    stallName   String

    cost        Integer

    ownerName   String

    tvSet       Integer

    Create default constructor and a parameterized constructor with arguments in order GoldStall(String stallName, Integer cost, String ownerName, Integer tvSet).
    Include appropriate getters and setters.

    Include the following method in the class GoldStall

    Method

    Description

    void display()

    To display the stall name, cost of the stall, owner name and the number of tv sets.


    Create a class PremiumStall which implements Stall interface with following private attributes

    Attribute   Datatype

    stallName   String

    cost        Integer

    ownerName   String

    projector   Integer

    Create default constructor and a parameterized constructor with arguments in order PremiumStall(String stallName, Integer cost, String ownerName, Integer projector).
    Include appropriate getters and setters.

    Include the following method in the class PremiumStall.

    Method          Description

    void display()  To display the stall name, cost of the stall, owner name and the number of projectors.


    Create a class ExecutiveStall which implements Stall interface with following private attributes

    Attribute   Datatype

    stallName   String

    cost        Integer

    ownerName   String

    screen      Integer

    Create default constructor and a parameterized constructor with arguments in order ExecutiveStall(String stallName, Integer cost, String ownerName, Integer screen).
    Include appropriate getters and setters.

    Include the following method in the class ExecutiveStall.

    Method          Description

    void display()  To display the stall name, cost of the stall, owner name and the number of screens.


    Create a driver class named Main to test the above class.

    Input Format:
    The first input corresponds to choose the stall type.
    The next line of input corresponds to the details of the stall in CSV format according to the stall type.

    Output Format:
    Print “Invalid Stall Type” if the user has chosen the stall type other than the given type
    Otherwise, display the details of the stall.
    Refer to sample output for formatting specifications.

    Note: All Texts in bold corresponds to the input and rest are output

    Sample Input and Output 1:

    Choose Stall Type
    1)Gold Stall
    2)Premium Stall
    3)Executive Stall
    1
    Enter Stall details in comma separated(Stall Name,Stall Cost,Owner Name,Number of TV sets)
    The Mechanic,120000,Johnson,10
    Stall Name:The Mechanic
    Cost:120000.Rs
    Owner Name:Johnson
    Number of TV sets:10

    Sample Input and Output 2:

    ChooseStall Type
    1)Gold Stall
    2)Premium Stall
    3)Executive Stall
    2
    Enter Stall details in comma separated(Stall Name,Stall Cost,Owner Name,Number of Projectors)
    Knitting plaza,300000,Zain,20
    Stall Name:Knitting plaza
    Cost:300000.Rs
    Owner Name:Zain
    Number of Projectors:20

    Sample Input Output 3:

    ChooseStall Type
    1)Gold Stall
    2)Premium Stall
    3)Executive Stall
    3
    Enter Stall details in comma separated(Stall Name,Stall Cost,Owner Name,Number of Screens)
    Fruits Hunt,10000,Uber,7
    Stall Name:Fruits Hunt
    Cost:10000.Rs
    Owner Name:Uber
    Number of Screens:7

    Sample Input Output 4:

    ChooseStall Type
    1)Gold Stall
    2)Premium Stall
    3)Executive Stall
    4
    Invalid Stall Type

```java title="Main.java"
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        
        Scanner input= new Scanner(System.in).useDelimiter("\\s*[,\\n]\\s*");
        System.out.println("Choose Stall Type\n1)Gold Stall\n2)Premium Stall\n3)Executive Stall");
        int choice=input.nextInt();
        switch (choice) {
            case 1:
                System.out.println("Enter Stall details in comma separated(Stall Name,Stall Cost,Owner Name,Number of TV sets)");                
                GoldStall gold = new GoldStall(input.next(),input.nextInt(),input.next(),input.nextInt());
                gold.display();
                break;
                
            case 2:
                System.out.println("Enter Stall details in comma separated(Stall Name,Stall Cost,Owner Name,Number of Projectors)");
                PremiumStall premium = new PremiumStall(input.next(),input.nextInt(),input.next(),input.nextInt());
                premium.display();
                
                break;
            case 3:
                System.out.println("Enter Stall details in comma separated(Stall Name,Stall Cost,Owner Name,Number of Screens)");
                ExecutiveStall executive = new ExecutiveStall(input.next(),input.nextInt(),input.next(),input.nextInt());
                executive.display();
                
                break;
            default:
            System.out.println("Invalid Stall Type");
                break;
        }
        input.close();
    }
}

```
```java title="Stall.java"
interface Stall{
       abstract void display();
}
```
```java title="ExecutiveStall.java"
/**
 * ExecutiveStall
 */
public class ExecutiveStall implements Stall {

    String stallName;
    Integer cost;
    String ownerName;
    Integer screen;
    public void display(){
        System.out.println("Stall Name:"+this.stallName);       
        System.out.println("Cost:"+ this.cost+ ".Rs");
        System.out.println("Owner Name:"+this.ownerName);
        System.out.println("Number of Screens:"+this.screen);
    }
    ExecutiveStall(){
        super();
    }
    ExecutiveStall(String stallName, Integer cost, String ownerName, Integer screen){
        super();
        this.stallName=stallName;
        this.cost=cost;
        this.ownerName=ownerName;
        this.screen=screen;
    }
}
```
```java title="GoldStall.java"
/**
 * GoldStall
 */
public class GoldStall implements Stall{

    public String stallName;
    Integer cost;
    String ownerName;
    Integer tvSet;
    public void display(){
        System.out.println("Stall Name:"+this.stallName);       
        System.out.println("Cost:"+ this.cost+ ".Rs");
        System.out.println("Owner Name:"+this.ownerName);
        System.out.println("Number of TV sets:"+this.tvSet);
    }
    GoldStall(){
        super();
    }
    GoldStall(String stallName, Integer cost, String ownerName, Integer tvSet){
        super();
        this.stallName=stallName;
        this.cost=cost;
        this.ownerName=ownerName;
        this.tvSet=tvSet;
    }
}
```
```java title="PremiumStall.java"
public class PremiumStall implements Stall{
    String stallName;
    Integer cost;
    String ownerName;
    Integer projector;
    public void display(){
        System.out.println("Stall Name:"+this.stallName);       
        System.out.println("Cost:"+ this.cost+ ".Rs");
        System.out.println("Owner Name:"+this.ownerName);
        System.out.println("Number of Projectors:"+this.projector);
    }
    PremiumStall(){
        super();
    }
    PremiumStall(String stallName, Integer cost, String ownerName, Integer projector){
        super();
        this.stallName=stallName;
        this.cost=cost;
        this.ownerName=ownerName;
        this.projector=projector;
    }
}

```