# Class Packaging
## 1
`toString() and getClass() - Illustration`

    The toString() method returns a textual representation of an object. A basic implementation is already included in java.lang.Object and so because all objects inherit from java.lang.Object it is guaranteed that every object in Java has this method. Overriding the method is always a good idea.

    getClass() method defined in the Object class returns the class Type of an object. getClass() method cannot be overridden.

    

    Create a class named Product with the following private member variables.

    id of type Long

    productName of type String

    supplierName of type String

    Include appropriate getters and setters.

    Include a 3-argument constructor and a default constructor.

    

    Override the toString() method defined in the Object class. Display the details of the product in this method as shown in the sample output.

    

    Create another class and write a main method to test the above class. Invoke the getClass() method from main.

    

    Input and Output Format:

    

    Refer sample input and output for formatting specifications.

    All text in bold corresponds to input and the rest corresponds to output.

    

    Sample Input and Output :

    Enter the product id

    1

    Enter the product name

    Printer

    Enter the supplier name

    HP

    1 : Printer : HP

    Invoking getClass() method : class Product

```java title="Main.java"
import java.util.*;
public class Main {

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
    System.out.println("Enter the product id");
    Long id= input.nextLong();
    System.out.println("Enter the product name"); 
    String product2=input.next();
    product2+=input.nextLine();
    System.out.println("Enter the supplier name");  
    String supplier=input.next();
    supplier+=input.nextLine();
    Product product1=new Product(id,product2,supplier);
    System.out.println(product1.toString()); 
    System.out.print("Invoking getClass() method:"); 
    System.out.println(product1.getClass()); 
    input.close();
    }
}
```
```java title="Product.java"
public class Product {
    private Long id ;
    private String productName ;
    private String supplierName ;
    public String toString() {
                return this.id +" : "+ this.productName+" : "+this.supplierName;
    }
    Product(){

    }
    Product(Long id, String productName ,String supplierName){
        this.id =id;
        this.productName=productName;
        this.supplierName=supplierName;
    }
}
```

## iAssess
### 1
`Clone Method`

    One method to quickly copy the primitive data members of an object is by invoking the clone method. The clone method allocates new memory for all primitive data types, but maintains the same reference to members representing it as objects of other classes. Lets try a very simple clone invocation for a customer object.

    Write a program to get the Customer name, id , country and complaint from the user. If the name entered is an empty string, it is assumed that the complaint is raised by the previous customer. In such cases omit the customer's id and country, use the "clone()" method to create a copy of the previous customer object and get the complaint from the user.

    Cretate a class called Customer with the following member variables
    Data Type	Variable Name
    String	name
    String	id
    String	country
    Include a default constructor.
    Include a 3 argument constructor.
    1st argument name
    2nd argument id
    3rd argument country


    Create a class called Complaint with the following member variables
    Data Type	Variable Name
    String	complaint
    Customer	customer

    Methods in Complaint class
    Method Name	Return Type	Function
    display()	void	display the complaint detail
    Include a default constructor.
    Include a 2 argument constructor.
    1st argument complaint
    2nd argument customer
    
    
    Note :
    Strictly adhere to the object oriented specifications given as a part of the problem statement.
    Use the same class names and member variable names.

    Assume: that the Maximum number of complaints as 100.

    Sample Input and Output :

    Enter the customer name
    Hubbib
    Enter the id
    006
    Enter the country
    AF
    Enter the complaint
    Late service
    Add another complaint ??
    yes
    Enter the customer name
    Abin
    Enter the id
    080
    Enter the country
    KLN
    Enter the complaint
    Improper response
    Add another complaint ??
    yes
    Enter the customer name

    Same customer
    Enter the complaint
    Bad Quality
    Add another complaint ??
    no

    Complaint Details
    Name : Hubbib ID : 006 Country : AF Complaint : Late service
    Name : Abin ID : 080 Country : KLN Complaint : Improper response
    Name : Abin ID : 080 Country : KLN Complaint : Bad Quality


```java title="Main.java"
import java.util.*;
public class Main {
    public static void main(String[] args) throws CloneNotSupportedException {
      //  try {
            Scanner input= new Scanner(System.in);
        String name;
        String id;
        String country;
        String complaint;
        String choice;
        //Customer customer;
        ArrayList<Complaint> complaints=new ArrayList<Complaint>();
        Stack<Customer> customers=new Stack<Customer>();
    do{
        System.out.println("Enter the customer name");
        name = input.next();
        name += input.nextLine();
        
        //if(name==null){
          // customer=ArrayComplaint.get(ArrayComplaint.size()-1).customer;
        //}
        //else{
        if(!name.isEmpty()){
            System.out.println("Enter the id");
            id= input.next();
            System.out.println("Enter the country");
            country= input.next();
            country+= input.nextLine();
            customers.add(new Customer(name,id,country));
            System.out.println("Enter the complaint");
                complaint= input.next();
                complaint+= input.nextLine();
                complaints.add(new Complaint(complaint,customers.get(complaints.size()-1)));
            
        }
        else{
            if(!complaints.isEmpty()){
                System.out.println("Enter the complaint");
                complaint= input.next();
                complaint+= input.nextLine();
                complaints.add((Complaint)complaints.get(complaints.size()-1).clone());
                complaints.get(complaints.size()-1).complaint=complaint;
                
            }
        
        }
        
        //}
        
        System.out.println("Add another complaint ??");
        choice= input.next();
        

        
    }while(choice.equals("yes"));
    System.out.println("Complaint Details");
        for(int i=0;i<complaints.size();i++){
            complaints.get(i).display();
        }
        input.close();
        //} catch (Exception e) {
            // TODO: handle exception
        //}
        
    
    }
}
```

```java title="Customer.java"
/**
 * Customer
 */
public class Customer{

    String name;
    String id;
    String country;
    Customer(){

    }
    Customer(String name,String id,String country){
        this.name=name;
        this.id=id;
        this.country=country;
    }
    
}
```
```java title="Complaint.java"
public class Complaint  implements Cloneable {
    String complaint;
    Customer customer= new Customer();
    public void display() {
        System.out.println("Name : "+customer.name+" ID : "+customer.id+" Country : "+customer.country+" Complaint : "+complaint);
    }
    Complaint(){

    }
    Complaint(String complaint,Customer customer){
        this.complaint=complaint;
        this.customer=customer;
    }
    public Object clone()throws CloneNotSupportedException{  
        return super.clone();  
        } 
}

```