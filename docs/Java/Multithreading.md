# Multi-threading
## 1
Article count
 
Multithreading is a Java feature that allows concurrent execution of two or more parts of a program for maximum utilization of CPU. Each part of such a program is called a thread. The threads are light-weight processes within a process.

Let's have a quick look at the way threads work in Java. For multi-threading to work, the class that will be invoked as a thread should extend the Thread class. You may wonder, what is the use of multi-threading. Let's understand it by the following exercise. Given 'n' number of lines of text, you have to find the total number of articles present in the given lines. while obtaining inputs from the user, the Main method has the full control of the execution.

The time is wasted in input gathering, which can be invaluable for large computing applications, has to be utilized properly. Hence a thread is invoked when a line is obtained and the articles are counted while the input for the subsequent lines is obtained from the user. Thus threading can increase efficiency and time constraints.

Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names and method names should be the same as specified in the problem statement.

Create a class called Article which extends the Thread class with the following private attributes.

Attributes	Datatype
line	String
count	Integer
 
Include appropriate getters and setters.
Generate default and parameterized constructors. The format for the parameterized constructor is Article(String line)

The Article class includes the following methods

Method 	Description
void run()	This method counts the number of articles in a given line and stores the value in the count variable.

Create a driver class called Main. In the Main method, invoke 'n' threads for 'n' lines of input and compute the total count of the articles in the given lines.

Input and Output format:
Refer to sample Input and Output for formatting specifications.

[All text in bold corresponds to the input and rest corresponds to the output]
Sample Input and Output:

Enter the number of lines
3
Enter line 1
An article is a word used to modify a noun, which is a person, place, object, or idea.
Enter line 2
Technically, an article is an adjective, which is any word that modifies a noun.
Enter line 3
There are two different types of articles.
There are 7 articles in the given input
```java title="Main.java"
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input= new Scanner(System.in);
        String line;
        Integer count=0;
        System.out.println("Enter the number of lines");
        int numberOfLines=input.nextInt();
        Article[] thread= new Article[numberOfLines];
        for (int i = 0; i < numberOfLines; i++) {
            System.out.println("Enter line "+(i+1));
            line="";
            line=input.next();
            line+=input.nextLine();
            thread[i]=new Article(line);
            thread[i].run();
            count+=thread[i].getCount();
             
        }
        
        
        System.out.println("There are "+count+" articles in the given input");
        input.close();
    }
}

```
```java title="Article.java"
//import java.util.StringTokenizer;

/**
 * Article
 */
public class Article extends Thread  {

    private String line;
    private Integer count=0;
    public void run(){
        try{//StringTokenizer token =new StringTokenizer(line);
           /*  while(token.hasMoreTokens()){
                if(token.nextToken().equals("The")||token.nextToken().equals("the")||token.nextToken().equals("A")||token.nextToken().equals("a")||token.nextToken().equals("An")||token.nextToken().equals("an")){
                    count++;
                }
            }*/
            String[] token=line.split("\\s");
            for (int i = 0; i < token.length; i++) {
                if(token[i].equals("The")||token[i].equals("the")||token[i].equals("A")||token[i].equals("a")||token[i].equals("An")||token[i].equals("an")){
                    count++;
                    //System.out.println(Thread.currentThread().getName());
                }
            }
        }
        catch(Exception e){
            System.out.println("Exception is caught");
        }   
        //Thread.yield();   
    }
    public Article(){

    }
    public Article(String line){
        this.line=line;
    }
    public Integer getCount(){
        return count;
    }
}
```
## 2
City Count

Now we are gonna use threading in a small part of our application. The users can be from any city. So get the user details in the console and count the number of users from each city.

Strictly adhere to the Object-Oriented specifications given in the problem statement. All class names, attribute names and method names should be the same as specified in the problem statement.

Create a class User with the following private attributes
Attributes	Datatype
name	String
mobileNumber	String
city	String
state	String
 
Include appropriate getters and setters
Create Default and Parameterized Constructor as User(String name, String mobileNumber, String city, String state) for the class.

Create a class CityCount extends Thread with the following private attribute,

Attributes	Datatype
city	String
count	Integer
userList	List<User>
Call a thread class for each city and count the number of users in that city.

Create constructor as public CityCount(String city, ArrayList<User> userList) and create appropriate getters and setters.

When creating CityCount object initialize count as zero.
Create a driver class Main and use the main method.

Input and Output format:
Refer to Sample Input and Output for other further details and format of the output.

[All Texts in bold corresponds to the input and rest are output]
Sample Input and Output 1:

Enter the number of users:
5
Enter the details of user 1
John,123456,Banglore,Karnataka
Enter the details of user 2
Jane,23456,Hyderabad,Telungana
Enter the details of user 3
Jim,56789,Chennai,Tamil Nadu
Enter the details of user 4
June,45678,Chennai,Tamil Nadu
Enter the details of user 5
James,13579,Banglore,Karnataka
Enter the number of cities:
3
Enter the name of city 1
Chennai
Enter the name of city 2
Banglore
Enter the name of city 3
Hyderabad
Chennai--2
Banglore--2
Hyderabad--1
```java title="Main.java"
import java.util.ArrayList;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
       
        Scanner input= new Scanner(System.in).useDelimiter("\\s*[,\\n]\\s*");
        System.out.println("Enter the number of users:");
        ArrayList<User> user=new ArrayList<User>();
        int numberOfUsers=input.nextInt();

        for (int i = 0; i < numberOfUsers; i++) {
            System.out.println("Enter the details of user "+(i+1));
            user.add(new User(input.next(),input.next(),input.next(),input.next()));
        }
        try{
        System.out.println("Enter the number of cities:");
        ArrayList<CityCount> cityCount=new ArrayList<CityCount>();
        int numberOfcities=input.nextInt();
        for (int i = 0; i < numberOfcities; i++) {
            System.out.println("Enter the name of city "+(i+1));
            String city=input.next();
            //city+=input.nextLine();
            cityCount.add(new CityCount(city,user));
            cityCount.get(i).run();
        }
        
        for (int i = 0; i < cityCount.size(); i++) {
            System.out.println(cityCount.get(i).getCity()+"--"+cityCount.get(i).getCount());
            
        }
        input.close();
    }
    catch(Exception e){
        System.out.println("Exception is caught");
    }
    }
}

```
```java title="User.java"
public class User {
    private String name;
    private String mobileNumber;
    private String city;
    private String state;
    public User(){

    }
    public User(String name, String mobileNumber, String city, String state){
        this.name=name;
        this.mobileNumber=mobileNumber;
        this.city=city;
        this.state=state;
    }
    public String getCity(){
        return this.city;
    }
}

```
```java title="CityCount.java"
import java.util.ArrayList;

public class CityCount extends Thread{
    private String city;
    private Integer count=0;
    private ArrayList<User> userList=new ArrayList<User>();
    public void run(){
        
            for (int index = 0; index < userList.size(); index++) {
                if(this.city.equals(userList.get(index).getCity())){
                    count++;
                }
            }
        
        
    }
    public CityCount(){

    }
    public CityCount(String city, ArrayList<User> userList){
        this.city=city;
        this.userList=userList;
    }
    public Integer getCount(){
        return this.count;
    }
    public String getCity(){
        return this.city;
    }
}

```
## iAssess
Character Frequency - Multiple Threads

Your English literature friend is very happy with the code you gave him. Now for his research, he used your application to find character frequency in many novels. For larger novels, the application takes a lot of time for computation. So he called you on a fine Sunday to discuss this with you. He wanted to know whether you can improve the speed of the application.

You decided to modify the application by using multiple threads to reduce the computation time. For this, accept the number of counters or threads at the beginning of the problem and get the string for each counter or thread. Create a thread by extending the Thread class and take the user entered string as input. Each thread calculates the character frequency for the word assigned to that thread. All the counts are stored locally in the thread and once all the threads are completed print the character frequency for each of the threads.

Create a class Main.

Input and Output format:
Refer to sample Input and Output for formatting specifications.

Sample input and output:
[All Texts in bold corresponds to the input and rest are output]

Enter Number of Counters :
2
Enter text for counter 1 :
FrequencyCounter
Enter text for counter 2 :
JavaTheCompleteReference
Counter 1 Result :
C:1 F:1 c:1 e:3 n:2 o:1 q:1 r:2 t:1 u:2 y:1
Counter 2 Result :
C:1 J:1 R:1 T:1 a:2 c:1 e:7 f:1 h:1 l:1 m:1 n:1 o:1 p:1 r:1 t:1 v:1
```java title="Main.java"
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

```
```java title="Counter.java"


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
