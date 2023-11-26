# Exception Handling
## 1
NumberFormatException
Let’s learn a common type of exception which you would have come across already. When you use BufferedReader to read input you need to parse String it into various datatype like Integer, Double. For example, If you try to parse a String ("abc") into Integer, it throws NumberFormatException. So let's try to handle this NumberFormat exception.

In our application, while acquiring attributes for classes like ItemType, this exception may occur. So try to handle it in this program.

Create a class ItemType with the following attribute,
Attributes	Data type
name	String
deposit	Double
costPerDay	Double

Add appropriate getter/setter, default and parameterized constructor. public ItemType(String name, Double deposit, Double costPerDay).

Override toString() and print the details as in the specified format.

Create a Main class and test the above class. Display "The details of the item type are:" in the main method. Handle the NumberFormatException in the Main Class.

Input and Output format:
Refer to sample Input and Output for formatting specifications.

[All Texts in bold corresponds to the input and rest are output]

Sample Input and Output 1:

Enter the Item type details:
Enter the name:
Electronics
Enter the deposit:
1000
Enter the cost per day:
100
The details of the item type are:
Name:Electronics
Deposit:1000.0
Cost Per Day:100.0

Sample Input and Output 2:

Enter the Item type details:
Enter the name:
Electronics
Enter the deposit:
One thousand
java.lang.NumberFormatException: For input string: "One thousand"
```java title="Main.java"
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input=new Scanner(System.in);
        String name;
        Double deposit;
        Double cost;
        try{
        System.out.println("Enter the Item type details:\nEnter the name:");
        name=input.next();
        name+=input.nextLine();
        System.out.println("Enter the deposit:");
        deposit=Double.parseDouble(input.nextLine());
        System.out.println("Enter the cost per day:");
        cost=Double.parseDouble(input.nextLine());
        ItemType item=new ItemType(name,deposit,cost);
        System.out.println("The details of the item type are:");
        System.out.println(item.toString());
        input.close();
        }
        catch(NumberFormatException e){
            System.out.println(e);
        }
        
        
    }
}

```
```java title="ItemType.java"
/**
 * ItemType
 */
public class ItemType {

    String name;
    Double deposit;
    Double costPerDay;
    public String toString(){
        return "Name:"+this.name+"\nDeposit:"+this.deposit+"\nCost Per Day:"+this.costPerDay;
    }
    public ItemType(){

    }
    public ItemType(String name, Double deposit, Double costPerDay){
        this.name=name;
        this.deposit=deposit;
        this.costPerDay=costPerDay;
    }
}
```
## 2
ArrayIndexOutOfBoundsException

The next prominent exception which you will see is ArrayIndexOutOfBoundsException. It occurs when the program tries to access the array beyond its size. As we know arrays have fixed size. So when you try to use array beyond its size it throws this exception. Let's try to handle this exception.

Handling this exception will also prove to be good for our application. For example, if there are only 100 seats in the event and the user tries to book the 105th seat, it will throw this exception. So you must handle it to do a specific job.

Create an array of size 100 and assume it as seat array. Get the tickets to be booked from the user and handle any exception that occurs in Main Class. At last display all the tickets booked.

Input and Output format:
The first line of input consists of an integer which corresponds to the number of seats to be booked.
The next n lines of input consist of the integer which corresponds to the seat number.
Refer to sample Input and Output for formatting specifications.

Note: All Texts in bold corresponds to the input and rest are output.

Sample Input and Output 1:

Enter the number of seats to be booked:
5
Enter the seat number 1
23
Enter the seat number 2
42
Enter the seat number 3
65
Enter the seat number 4
81
Enter the seat number 5
100
The seats booked are:
23
42
65
81
100

Sample Input and Output 2:

Enter the number of seats to be booked:
4
Enter the seat number 1
12
Enter the seat number 2
101
java.lang.ArrayIndexOutOfBoundsException: 100
```java title="Main.java"
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input= new Scanner(System.in);
        System.out.println("Enter the number of seats to be booked:");
        int numberOfSeats = input.nextInt();
        int[] arr= new int[100];
        try{
            for (int i = 0; i < numberOfSeats; i++) {
                System.out.println("Enter the seat number "+(i+1));
                int seatNumber=input.nextInt();
                arr[seatNumber-1]=1;
            }
            System.out.println("The seats booked are:");
        for (int i = 0; i < arr.length; i++) {
            if(arr[i]==1){
                System.out.println(i+1);
            }
        }
        input.close();
        }
        catch(ArrayIndexOutOfBoundsException e){
            System.out.println(e);
        }
        
    }
}

```
## 3
Duplicate mobile number exception
 

Write a java program to find the duplicate mobile number using the exception handling mechanism.

Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names and method names should be the same as specified in the problem statement.

Create a Class called ContactDetail with the following private attributes.

Attributes	Datatype
mobile	String
alternateMobile	String
landLine	String
email	String
address	String
Include getters and setters.
Include default and parameterized constructors.
Format for a parameterized constructor is ContactDetail(String mobile, String alternateMobile,String landLine, String email, String address)

Override the toString() method to display the Contact details as specified.

Create a class called ContactDetailBO with following methods

Method 	Description
static void validate(String mobile,String alternateMobile)	This method throws DuplicateMobileNumber exception
if the mobile and alternateMobile are the same.
 

Create a driver class called Main. In the Main method, obtain inputs from the user. Validate the mobile and alternateMobile and display the ContactDetail if no exception occurs else handle the exception.

Pass the exception message as "Mobile number and alternate mobile number are same". If mobile and alternateMobile are the same.

Input and Output format:
Refer to sample Input and Output for formatting specifications.

Note: All text in bold corresponds to the input and rest corresponds to the output.

Sample Input and Output 1:

Enter the contact details
9874563210,9874563210,0447896541,johndoe@abc.in,22nd street kk nagar chennai
DuplicateMobileNumberException: Mobile number and alternate mobile number are same

Sample Input and Output 2:

Enter the contact details
9874563210,9876543211,0447896541,johndoe@abc.in,22nd lane RR nagar kovai
Mobile:9874563210
Alternate mobile:9876543211
LandLine:0447896541
Email:johndoe@abc.in
Address:22nd lane RR nagar kovai
```java title="Main.java"
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input= new Scanner(System.in).useDelimiter("\\s*[,\\n]\\s*");
        System.out.println("Enter the contact details");
        ContactDetail detail=new ContactDetail(input.next(),input.next(),input.next(),input.next(),input.next());
        try{
        ContactDetailBO.validate(detail.mobile, detail.alternateMobile);
        System.out.println(detail.toString()); 
        input.close();
        }
        catch(DuplicateMobileNumberException e){
            System.out.print("DuplicateMobileNumberException: ");
            System.out.print(e.getMessage());
            
        }
    }
}

```
```java title="ContactDetails.java"
public class ContactDetail {
    String mobile;
    String alternateMobile;
    String landLine;
    String email;
    String address;
    public String toString(){
        return "Mobile:"+this.mobile+"\nAlternate mobile:"+this.alternateMobile+"\nLandLine:"+this.landLine+"\nEmail:"+this.email+"\nAddress:"+this.address;
    }
    public ContactDetail(){

    }
    public ContactDetail(String mobile, String alternateMobile,String landLine, String email, String address){
        this.mobile=mobile;
        this.alternateMobile=alternateMobile;
        this.landLine=landLine;
        this.email=email;
        this.address=address;
    }

}

```
```java title="ContactDetailBO.java"


public class ContactDetailBO {
    static void validate(String mobile,String alternateMobile) throws DuplicateMobileNumberException{
        
            if(mobile.equals(alternateMobile)){
                throw new DuplicateMobileNumberException("Mobile number and alternate mobile number are same");
            }
        
        
    }
}

```
```java title="DuplicateMobileNumberException.java"


public class DuplicateMobileNumberException extends Exception {
    public DuplicateMobileNumberException(String str){
        super(str);
    }
}

```
## iAssess
### 1
Parse Exception
  
For our application, we would have obtained date inputs. If the user enters a different format other than specified, an Invalid Date Exception occurs and the program is interrupted. To avoid that, handle the exception and prompt the user to enter the right format as specified.

Create a driver class called Main. In the main method, Obtain start time and end time for stage event show, if an exception occurs, handle the exception and notify the user about the right format.

Input format:
The input consists of the start date and end date. 
The format for the date is dd-MM-yyyy-HH:mm:ss

Output format:
Refer sample Input and Output for formatting specifications 


Note: All text in bold corresponds to the input and rest corresponds to the output.

Sample Input and Output 1:

Enter the stage event start date and end date
27-01-2017-12
Input dates should be in the format 'dd-MM-yyyy-HH:mm:ss'

Sample Input and Output 2:

Enter the stage event start date and end date
27-01-2017-12:0:0
28-01-2017-12:0:0
Start date:27-01-2017-12:00:00
End date:28-01-2017-12:00:00
```java title="Main.java"
import java.text.ParseException;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) throws ParseException{
        try {
            Scanner input =new Scanner(System.in);
            LocalDateTime start;
            LocalDateTime end;
            DateTimeFormatter formatter=DateTimeFormatter.ofPattern("dd-MM-yyyy-HH:m:s");
            DateTimeFormatter formatter1=DateTimeFormatter.ofPattern("dd-MM-yyyy-HH:mm:ss");
            System.out.println("Enter the stage event start date and end date");
            start=LocalDateTime.parse(input.next(),formatter);
            end=LocalDateTime.parse(input.next(),formatter);
            System.out.println("Start date:"+start.format(formatter1));
            System.out.println("End date:"+end.format(formatter1));
            input.close();
        } catch (Exception e) {
            // TODO: handle exception
            System.out.println("Input dates should be in the format 'dd-MM-yyyy-HH:mm:ss'");
        }
        

    }
}

```
### 2
Weak password Exception
A typical requirement of a custom exception would be for validation purposes. In this exercise, Let's validate a password input. A password is said to be strong if it satisfies the following criteria
    i)  It should be a minimum of 10 characters and a maximum of 20 characters.
    ii) It should contain at least one digit.
    iii)It should contain at least one special character (non-numeric, non-alphabetic).
    iv)It should contain at least one letter.

If the password fails any one of the criteria, it is considered as weak.

Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names and method names should be the same as specified in the problem statement.

Create a class called User with the following private attributes.

Attributes	Datatype
name	String
mobile	String
username	String
password	String
 

Include getters and setters.
Include default and parameterized constructors.
Format for the parameterized constructor is User(String name, String mobile, String username, String password)
Override the toString() method to display the User detail 

Create a class called UserBO with the following methods.

Method 	Description
static void validate(User u)	This method throws WeakPasswordNumber exception if the Password is weak.
 

Create a driver class called Main. In the Main method, obtain inputs from the user. Validate the password and if there is an exception, handle the exception.

Pass the exception message as "Your password is weak".

Sample Input and Output:
Refer to sample Input and Output for formatting specifications.

Note: All text in bold corresponds to the input and rest corresponds to the output.

Sample Input and Output 1:

Enter the user details
John Doe,9876543210,john,johndoe
WeakPasswordException: Your password is weak

Sample Input and Output 2:

Enter the user details
Jane doe,9876543210,Jane,Janedoe@123
Name:Jane doe
Mobile:9876543210
Username:Jane
Password:Janedoe@123
```java title="Main.java"
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        try {
        Scanner input=new Scanner(System.in).useDelimiter("\\s*[,\\n]\\s*");
        System.out.println("Enter the user details");
        User detail=new User(input.next(),input.next(),input.next(),input.next());
        UserBO.validate(detail);
        System.out.println(detail.toString());
        input.close();
        } catch (WeakPasswordException e) {
            // TODO: handle exception
            System.out.print("WeakPasswordException: ");
           System.out.println(e.getMessage()); 
        }
        
    }
}

```
```java title="User.java"


public class User {
    private String name;
    private String mobile;
    private String username;
    private String password;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getMobile() {
        return mobile;
    }
    public void setMobile(String mobile) {
        this.mobile = mobile;
    }
    public String getUsername() {
        return username;
    }
    public void setUsername(String username) {
        this.username = username;
    }
    public String getPassword() {
        return password;
    }
    public void setPassword(String password) {
        this.password = password;
    }
    public User(String name, String mobile, String username, String password) {
        this.name = name;
        this.mobile = mobile;
        this.username = username;
        this.password = password;
    }
    public String toString(){
        return "Name:"+this.name+"\nMobile:"+this.mobile+"\nUsername:"+this.username+"\nPassword:"+this.password;
    }
}

```
```java title="UserBO.java"

public class UserBO {
    static void validate(User u) throws WeakPasswordException {
        String password=u.getPassword();
        int length=password.length();
        int digit=0;
        int special=0;
        int letter=0;
        for (int i = 0; i < length; i++) {
            if(Character.isDigit(password.charAt(i))){
                digit++;
            }
            if(Character.isLetter(password.charAt(i))){
                letter++;
            }
            if(!Character.isDigit(password.charAt(i))&&!Character.isLetter(password.charAt(i))&&!Character.isWhitespace(password.charAt(i))){
                special++;
            }
        }


        if(length>9&&length<21&&digit>0&&letter>0&&special>0){
                   
            
        }
        else{
            throw new WeakPasswordException("Your password is weak");
        }
        
    }
}

```
```java title="WeakPasswordException.java"

public class WeakPasswordException extends Exception {
    public WeakPasswordException(String s){
        super(s);

    }
}

```
