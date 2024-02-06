# Language Fundamentals
## 1
	ROBOT

	

	Think that you are a scientist and you have invented a Humanoid Robo.



	You want to introduce your Robo in a public meeting.




	You need to feed the information that the Robo has to speak in the public meeting.So feed the basic information into the Robo using a program.

	NOTE: The basic information includes the name of the Robo, creator, purpose of creation, Memory space of the Robo and its speed.

	Input and Output Format:

	Input consists of name (char array), creator (char array), purpose (char array), memory space (int), speed (float) and the output format is to display all the details in correct order. Refer sample input and output for further details.

	[All text in bold corresponds to input and the rest corresponds to output]

	Sample Input and output:

	Enter the Name :

	Chitti

	Enter the Creator Name :

	Dr.Vasegran

	Enter the Purpose :

	militaryservice

	Memory Space :

	22

	Speed :

	1.1

	My Details :

	I am the Robot named Chitti.

	I was created by Dr.Vasegran.

	I am created for the purpose of militaryservice.

	My memory space is around 22Gb and my speed is 1.1Tb

```java title="Main.java"
import java.util.Scanner;
public class Main{
    public static void main(String[] args) {
		//fill your code here
		Scanner s = new  Scanner(System.in);
		String  name;
		String creator;
		String purpose;
		int ms;
		float speed;
		System.out.println("Enter the Name :"); 
		name = s.nextLine();
		System.out.println("Enter the Creator Name :"); 
		creator = s.nextLine();
		System.out.println("Enter the Purpose :"); 
		purpose = s.nextLine();
		System.out.println("Memory Space :"); 
		ms = s.nextInt();
		System.out.println("Speed :"); 
		speed = s.nextFloat();
		System.out.println("My Details : " ); 
		System.out.println("I am the Robot named " + name+"." ); 
		System.out.println("I was created by " + creator+"."); 
		System.out.println("I am created for the purpose of  "+ purpose+"."); 
		System.out.println("My memory space is around "+ ms+"GB and my speed is " + speed +"Tb."); 
	}

}
```
## 2
	CALCULATE GRADE

	Write a program that accepts the marks in 3 subjects of a student , calculates the average mark of the student and prints the student's grade. If the average mark is greater than or equal to 90, then the grade is 'A'. If the average mark is 80 and between 80 and 90, then the grade is 'B'. If the average mark is  70 and between 70 and 80, then the grade is 'C'. If the average mark is  60 and between 60 and 70, then the grade is 'D'. If the average mark is 50 and between 50 and 60, then the grade is 'E'. If the average mark is less than 50, then the grade is 'F'.

	Input Format:

	Input consists of 3 lines. Each line consists of an integer.

	Output Format:

	Output consists of a single line. Refer sample output for the format.

	Sample Input 1 :

	45

	45

	45

	Sample Output 1 :

	The grade is F

	Sample Input 2:

	91

	95

	100

	Sample Output 2:

	The grade is A

```java title="Main.java"
import java.util.*;
public class Main {

	public static void main(String[] args) {
		//fill your code here
		Scanner s =new Scanner(System.in);
		int x[]= new int[3];
		int sum=0;
		for(int i=0;i<3;i++){
		x[i]=s.nextInt();
		sum=sum + x[i]; 
		}
    int avg=sum/3;
	if(avg>=90){
		System.out.println("The grade is A");
	}
	else if(avg>=80 && avg<90 ){
		System.out.println("The grade is B");
	}
	else if(avg>=70 && avg<80 ){
		System.out.println("The grade is C");
	}
	else if(avg>=60 && avg<700 ){
		System.out.println("The grade is D");
	}
	else if(avg>=50 && avg<60 ){
		System.out.println("The grade is E");
	}
	else if( avg<50 ){
		System.out.println("The grade is F");
	}
	}

}
```
## 3
	EarthQuake11

	Mr. Ram is a very rich businessman and he  lost his family in the Gujarat Earthquake. He lost interest in his business after the tragic incident and he decided to serve the society. He started an NGO named after his only son Santosh to help the earth-quake victims. Santosh Helpline will provide a compensation to all earth quake survivors.

	The compensation amount given to the survivors is not fixed and it depends on the intensity of the earthquake.

	The expression Richter magnitude scale refers to a number of ways to assign a single number to quantify the energy contained in an earthquake.

	

	Earthquake Magnitude Scale

	Magnitude

	Type

	2.4 or less

	Micro

	2.5 to 5.4

	Light

	5.5 to 6.0

	Moderate

	6.1 to 6.9

	Strong

	7.0 to 7.9

	Major

	8.0 or greater

	Great

	Please help Ram to decide the intensity of the earthquake.

	

	Input Format:

	Input consists of a single floating point number which corresponds to the earthquake's ritcher magnitude scale.

	

	Ouput Format:

	Output consists of the string “Micro” or “Light” or “Moderate” or “Strong” or “Major” or Great”

	Refer sample input and output for further formatting specifications.

	[All text in bold corresponds to input and the rest corresponds to output]

	Sample Input and Output 1:

	Richter Magnitude:

	5.7

	Moderate

	

	Sample Input and Output 2:

	Richter Magnitude:

	5

	Light

 
```java title="Main.java"
import java.util.*;
import java.text.*;
public class Main{
    public static void main(String args[]){
        // fill the code
     Scanner s =new Scanner(System.in);
	 System.out.println("Richter Magnitude:");
	float avg= s.nextFloat();

	if(avg<=2.4){
		System.out.println("Micro");
	}
	else if(avg>=2.5 && avg<=5.4 ){
		System.out.println("Light");
	}
	else if(avg>=5.5 && avg<=6.0 ){
		System.out.println("Moderate");
	}
	else if(avg>=6.1 && avg<=6.9 ){
		System.out.println("Strong");
	}
	else if(avg>=7.0 && avg<=7.9 ){
		System.out.println("Major");
	}
	else if( avg>=8.0 ){
		System.out.println("Great");
	}
    }
}


```
## 4
	LIST OF PRIME NUMBERS

	

	To speed up his composition of generating unpredictable rhythms, A.R.Rahman wants the list of prime numbers available in a range of numbers.

	Can you help him out?

	Write a program to print all prime numbers in the interval [a,b] (a and b, both inclusive).

	Use a minimum of one for loop and one while loop


	Input Format:

	Input consists of 2 integers which correspond to a and b. Assume that a is always less than or equal to b.

	

	Output Format:

	Refer sample output for details.

	

	Sample Input 1:
	2
	15

	Sample Output 1:
	2 3 5 7 11 13

```java title="Main.java"
import java.util.*;
import java.lang.Math;
public class Main {

	public static void main(String[] args) {
		//fill your code here
		Scanner s = new Scanner(System.in);
		int a=s.nextInt();
		int b=s.nextInt();
	
		boolean flag=false;
		int i=a;
		while(i<=b){
			
			if(i>=2){
				flag=true;
			}
		
				for(int j=2;j<i;j++){
				if(i % j == 0 ){
					flag=false;
					break;
				}
			}
			
			if(flag==true){
				System.out.print(i+" ");
			}
			i++;
		}
	}

}
 
```
## iAssess
### 1
	Largest of three numbers using Ternary Operator

	Write a program to find greatest of three numbers , using Ternary Operator.

	Input Format:
	The input consists of 3 integers.
	Output Format:
	Output should display the greatest of the 3 numbers.  

	Refer sample input and output for formatting specifications.
	[All text in bold corresponds to input and the rest corresponds to output] 


	Sample Input and Output 1:
	Enter the numbers :
	5
	8
	2
	8 is the greatest number

	Sample Input and Output 2:
	Enter the numbers :
	44
	16
	23
	44 is the greatest number

```java title="Main.java"
public class Main {
    
}

```
### 2
	Reverse of a number

	

	Write a program to reverse the digits of a number.

	

	Input format :

	Input consists of an integer value.

	Output format :

	Output consists of the reverse of the given number.

	[ Refer Sample Input and Output for further details ]
	[ All text of bold corresponds to Input and the rest output]

	Sample Input and Output 1 :
	Enter the number :
	5642
	Reverse of the number is 2465

	Sample Input and Output 2 :

	Enter the number :
	144
	Reverse of the number is 441

```java title="Main.java"
public class Main {
    
}

```
