# Fundamental Classes
## 1
    Using contains() and trim() method
    
    Sunil has finished most of his application for the fair, it's time to focus on minor details that went wrong during a test run of his application in this module. Accidentally some gibberish text with leading and trailing got copied to the clipboard and got pasted in some of the text documents. But, still. He has the gibberish text with him, he can manually load each document, and find the text and delete it. Think it will take ages, no he can think of a time saver. He can use his programming skills, he can load each document in a program and find in which files the text got copied. Even though, he feels difficult to identify it. So let him.

    write a program to find whether the gibberish text is present in the string. Assume text of the document is given as the input to the program.

    Create a driver class called Main. In the Main method, obtain the inputs from the console and prompt whether the gibberish text is present in the main text.

    Problem Constraints:

    Use contains() and trim()

    Input and Output format:
    The first line of the input consists of the text of the document.
    The second line of the input consists of a string that has to be found in the given text.

    Note: All text in bold corresponds to the input and rest corresponds to the output.

    Sample Input and output 1:

    Enter the text from the document
    One fine morning, a minister from Emperor Akbar's court had gathered in the assembly hall. He informed the Emperor that all his valuables had been stolen by a thief the previous night.
    Enter the string to be found in the data
        stolen   
    String is found in the document

    Sample Input and output 2:

    Enter the text from the document
    One fine morning, a minister from Emperor Akbar's court had gathered in the assembly hall. He informed the Emperor that all his valuables had been stolen by a thief the previous night.
    Enter the string to be found in the data
        Birbal
    String is not found in the document
```java title="Main.java"
import java.util.Scanner;

/**
 * Main
 */
public class Main {

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.println("Enter the text from the document");
        String text= input.next();
        text+= input.nextLine();
        System.out.println("Enter the string to be found in the data");
        String string= input.next();
        string.trim();
        if(text.contains(string)){
            System.out.println("String is found in the document");
        }
        else{
            System.out.println("String is not found in the document");
        }
        input.close();
    }
}
```
## 2
    String Builder
    StringBuilder class is used to create mutable (modifiable) string. StringBuilders are used when the String has to be modified constantly. We recently observed that the availability of items for the stall is hard to know. So we are gonna program that requirement here. Get the availability of the items from the vendors. They are providing the list separated by "$". So use string builder and display the details of the items along with their availability. The list provided by vendors only have the available numbers of the item. We don't want that, so just display whether the item is available or not.

    Create a class Item with following private attributes

    Attributes	Datatype
    name	String
    type	String
    cost	Integer
    availableQuantity	Integer
    Include appropriate getters and setters
    Create default constructor and a parameterized constructor with arguments in order Item(String name, String type, Integer cost, Integer availableQuantity).

    Create a driver class named Main to test the above class.

    Note:
    Strictly adhere to the Object-Oriented Specifications given in the problem statement.All class names, attribute names and method names should be the same as specified in the problem statement.

    Input Format:
    The first line input corresponds to the number of items 'n'.
    The next 'n' line of inputs corresponds to the item details in the format of `(Item Name$Item Type$Item Cost$Item Availability)`.
    Refer sample input for formatting specifications.

    Output Format:
    The output consists Item details in the CSV format.If the available quantity of the item is 0 then make it as "Not Available" else "Available".
    Refer sample output for formatting specifications.

    Sample Input/Output-1:
    Enter the number of items:
    3
    Enter the item details in the format`(Item Name$Item Type$Item Cost$Item Availability)`
    `Wallets$Leather$1200$10
    Notebooks$Papers$200$0
    Headphones$Electronics$800$3`
    Items:
    Wallets,Leather,1200,Available
    Notebooks,Papers,200,Not Available
    Headphones,Electronics,800,Available
```java title="Main.java"
import java.util.ArrayList;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input =new Scanner(System.in).useDelimiter("\\s*[$\\n]\\s*");
        System.out.println("Enter the number of items:");
        int numberOfItems=input.nextInt();
        ArrayList<Item> item= new ArrayList<Item>();
        System.out.println("Enter the item details in the format(Item Name$Item Type$Item Cost$Item Availability)");
        for (int i = 0; i < numberOfItems; i++) {
            item.add(new Item(input.next(),input.next(),input.nextInt(),input.nextInt()));
        }
        System.out.println("Items:");
        
        
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
        input.close();
    }
}

```
```java title="Item.java"


public class Item {
    private String name;
    private String type;
    private Integer cost;
    private Integer availableQuantity;
    public String checkAvailable(){
        if(this.availableQuantity==0){
            return "Not Available";
        }
        else{
            return "Available";
        }
    }
    public Item(){

    }
    public Item(String name, String type, Integer cost, Integer availableQuantity){
        this.name=name;
        this.type=type;
        this.cost=cost;
        this.availableQuantity=availableQuantity;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getType() {
        return type;
    }
    public void setType(String type) {
        this.type = type;
    }
    public Integer getCost() {
        return cost;
    }
    public void setCost(Integer cost) {
        this.cost = cost;
    }
    public Integer getAvailableQuantity() {
        return availableQuantity;
    }
    public void setAvailableQuantity(Integer availableQuantity) {
        this.availableQuantity = availableQuantity;
    }
}

```
## 3
    Date Formats

    So far, we have got the dates from the user in MM-dd-yyyy format. but in some reports, we want them in some other formats. So write a program to convert the dates gotten from the user into different formats.

    Create a driver class named Main and do all manipulation in the main method.

    Input Format:
    The first line input corresponds to the date that is to be processed in various date formats.
    Refer sample input for formatting specifications.

    Output Format:
    The output consists of date in the format of ("EEE, MMM d, yy" , "dd.MM.yyyy" , "dd/MM/yyyy").
    Refer sample output for formatting specifications.

    Sample Input/Output-1:
    Enter the date to be formatted:(MM-dd-yyyy)
    10-20-1996
    Date Format with EEE, MMM d, yy : Sun, Oct 20, 96
    Date Format with dd.MM.yyyy : 20.10.1996
    Date Format with dd dd/MM/yyyy : 20/10/1996
```java title="Main.java"
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.util.Scanner;

public class Main {
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
}

```
## iAssess
### 1
    StringBuilder

    For more practice in StringBuilder let's try the exercise below. Given a code, try to change the code to expected format. The first 2 letters correspond to the city code, DH - Delhi MB - Mumbai KL - Kolkata. The digits following the city code correspond to the reference number. In the output code, the city code changes as given below.
    DH - DEL
    MB - MUM
    KL - KOL

    Also, need to maintain uniformity in the number of digits in the reference number be 5 digits.
    Create a driver class called Main. In the Main method, obtain the input from the console and print the formatted code.
    Note: Use StringBuilder

    [All text in bold corresponds to the input and rest corresponds to the output]
    Sample Input/Output 1:

    Enter the code
    DH1
    Formatted code
    DEL00001

    Sample Input/Output 2:

    Enter the code
    MB12345
    Formatted code
    MUB12345
```java title="Main.java"
import java.util.*;

public class Main {
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
}

```
### 2
    Date Processing --- Compare dates
    We realized that there are many events held on different dates and lasts for the different duration. And we want the count of events that are held only for one day so the arrangements of the hall can be made. Now we have a list of events with the name along with starting and ending date in CSV format. So write a program to split them and display the number of 1-day events.

    Create class Event with following private attributes

    Attributes	Datatype
    eventName	String
    startDate	Date
    endDate	Date
    Include appropriate getters and setters.
    Create default constructor and a parameterized constructor with arguments in order Event(String eventName, Date startDate, Date endDate).

    Note:
    Strictly adhere to the Object-Oriented Specifications given in the problem statement.All class names, attribute names and method names should be the same as specified in the problem statement.

    Create a driver class named Main to test the above class.

    Input Format:
    The first line input corresponds to the number of events 'n'.
    The next 'n' lines of input corresponding to the event details in CSV format(Event Name,Start Date,End Date).
    Refer sample input for formatting specifications.

    Output Format:
    The output consists of 1-day event names. If no 1-day event present, then display "No Events".
    Refer sample output for formatting specifications.

    [All text in bold corresponds to input and rest corresponds to output]
    Sample Input/Output-1:

    Enter the number of Events
    3
    Enter event details in CSV(Event Name,Start Date,End Date) Date:dd/MM/yyyy
    Reunion,28/02/2017,28/02/2017
    Party,30/06/2017,05/07/2017
    Wedding,23/10/2017,24/10/2017
    1-day Events:
    Reunion

    Sample Input/Output-2:
    Enter the number of Events
    2
    Enter event details in CSV(Event Name,Start Date,End Date) Date:dd/MM/yyyy
    Celebration,30/06/1998,31/06/1998
    Christmas Party,22/01/2000,25/02/2000
    1-day Events:
    No Events
```java title="Main.java"
import java.util.*;
import java.text.*;

public class Main {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		DateFormat dateFormat = new SimpleDateFormat("dd/MM/yyyy");

		// Read the number of events
		System.out.println("Enter the number of Events");
		int n = scanner.nextInt();
		scanner.nextLine();

		List<Event> events = new ArrayList<>();

		// Read the details of each event and create objects of the Event class
		System.out.println("Enter event details in CSV(Event Name,Start Date,End Date) Date:dd/MM/yyyy");
		for (int i = 0; i < n; i++) {
			String input = scanner.nextLine();
			String[] tokens = input.split(",");
			String eventName = tokens[0];
			Date startDate = null;
			Date endDate = null;

			try {
				startDate = dateFormat.parse(tokens[1]);
				endDate = dateFormat.parse(tokens[2]);
			} catch (ParseException e) {
				e.printStackTrace();
			}

			events.add(new Event(eventName, startDate, endDate));
		}

		// Check for 1-day events and display their names
		List<String> oneDayEvents = new ArrayList<>();
		for (Event event : events) {
			if (event.isOneDayEvent()) {
				oneDayEvents.add(event.getEventName());
			}
		}

		// Display the names of all 1-day events
		System.out.println("1-day Events:");
		if (oneDayEvents.size() == 0) {
			System.out.println("No Events");
		} else {
			for (String eventName : oneDayEvents) {
				System.out.println(eventName);
			}
		}

		scanner.close();
	}
}




```
```java title="Event.java"
import java.util.*;
import java.text.*;

class Event {
	private String eventName;
	private Date startDate;
	private Date endDate;

	// Default constructor
	public Event() {}

	// Parameterized constructor
	public Event(String eventName, Date startDate, Date endDate) {
		this.eventName = eventName;
		this.startDate = startDate;
		this.endDate = endDate;
	}

	// Getters and setters
	public String getEventName() {
		return eventName;
	}

	public void setEventName(String eventName) {
		this.eventName = eventName;
	}

	public Date getStartDate() {
		return startDate;
	}

	public void setStartDate(Date startDate) {
		this.startDate = startDate;
	}

	public Date getEndDate() {
		return endDate;
	}

	public void setEndDate(Date endDate) {
		this.endDate = endDate;
	}

	// Method to check if the event is for only one day
	public boolean isOneDayEvent() {
		return startDate.compareTo(endDate) == 0;
	}
}

```
