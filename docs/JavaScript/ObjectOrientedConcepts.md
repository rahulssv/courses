# Object Oriented Concepts
## iDesign
### 1
    Check Name Length using ES5

    Check the given user name length using Javascript class using ES5.

    Problem Description:
    1) Read input file ‘input.txt’
    2) Create class named as User.
    3) Inside the class create the argument as user name.
    4) Now create getter for name.
    5) Create the function checkNameLength() inside the class.
    6) Inside the function check the length of the user name.
    7) If the user name length is greater than 4 then, print the name as it is. Else print the message ‘Name is too short’.
    6) Create object for the class using new Classname() and pass the input to the constructor.
    7) And call the object method, using object.methodName() to print the output.

    Input and Output Format:

    Refer to sample input and output.

    Input is user name.

    Output is user name.(If the length is greater than 4), Else  ‘Name is too short’.

    Input:

    Harina

    Output:

    Harina

    Input:

    Jim

    Output:

    Name is too short
```js title="app.js"
var fs = require('fs');
var input=fs.readFileSync('input.txt').toString().trim().split('\n');
//fill your code
var value=String(input)
class User {
    constructor(name) {
        this._name = name;
    }

    get name() {
        return this._name;
    }

    checkNameLength() {
        if (this._name.length > 4) {
    
            console.log(this._name);
        } else {
            console.log('Name is too short');
        }
    }
}
var user=new User(value)
user.checkNameLength();
```
```txt title="input.txt"
Harina
```
### 2
    Prime or Composite using ES6

    Write a program to check the given number is prime or composite.

    Problem Description:
    1) Read a number from file ‘input.txt’
    2) In display.js check and print, the given number is prime or composite.
    3) In display.js exports the function/class name.  ( Example : exports.className = className; )
    4) In app.js import the function/class name. ( Example: {className} = require(‘file path'); )
    5) From app.js call the function/class to print the message.

    Input and Output Format:

    Refer to sample input and output.

    Input is a number.

    The output is the statement.

    Input:

    23

    Output:

    Prime Number

    Input:

    26

    Output:

    Composite Number

    Input:

    1

    Output:

    Neither Prime nor Composite
```js title="app.js"

//fill your code
const {value} = require ('./display.js')
var fs = require('fs');
var data = fs.readFileSync('input.txt');
var intval=parseInt(data)
console.log(value(intval))
```
```js title="display.js"

let value=(data)=>{
    if(data<=1){
        return "Neither Prime nor Composite"
    }
for(let i=2;i<=Math.sqrt(data);i++){
    if(data%i===0){
        return "Composite Number"
    }
    
}
return "Prime Number"
}
exports.value=value
```
```txt title="input.txt"
23
```
## iAssess
### 1
    Print Employee Details using ES5

    Print employee details using javascript class using ES5.

    Problem Description:
    1) Read input file ‘input.txt’
    2) Create a class named as Employee.
    3) Inside the class create arguments employee name,dept and DOJ.
    4) Now create the method as displayEmployee() and inside the method print the employee details.
    5) Create object for the class using new Classname() and pass the input to the constructor.
    6) And call the object method, using object.methodName() to print the employee details.

    Input and Output Format:

    Refer to sample input and output.

    Input and output is employee details.

    Input:

    John
    HR
    23-8-1997

    Output:

    Name : John
    Department : HR
    DOJ : 23-8-1997
```js title="app.js"
var fs = require('fs');
var input=fs.readFileSync('input.txt').toString().trim().split('\n');
//fill your code
var name=String(input[0])
var dept=String(input[1])
var doj=String(input[2])

class Employee{
    constructor(name,dept,doj){
        this.name=name
        this.dept=dept
        this.doj=doj
    }
    displayEmployee(){
        console.log("Name : "+this.name)
         console.log("Department : "+this.dept)
          console.log("DOJ : "+this.doj)
    }
}
var emp1=new Employee(name,dept,doj)
emp1.displayEmployee()
```
```txt title="input.txt"
John
HR
23-8-1997
```
### 2
    Area and Perimeter using ES6

    Write a program to find the area and perimeter of extended classes from the parent class.

    Problem Description :

    1) Read input file ‘input.txt’
    2) Create a class named as Shape using the keyword class.
    3) Inside the class create constructor with argument name.
    3) Create a method calculatePerimeter() and calculateArea in the parent class Shape.
    4) Create three child classes Circle, Square, and Triangle.
    5) Each class should have a constructor which invokes name from the parent class:
        Constructor of Circle should have arguments for name and radius
        Constructor of Square should have arguments for name and side
        Constructor of Triangle should have arguments for name, side1, side2, side3, side4, base and height.
    6) Create methods in each class to display the measurements.    

        displayCircleMeasurments() in class Circle
        displaySquareMeasurments() in class Square
        displayTriangleMeasurments() in class Triangle
    7) Each display method should invoke the methods in the parent class

        calculateArea()
        calculatePerimeter()
    Note :

    calculateArea() and calculatePerimeter() are the methods written inside Parent class Shape. It should be invoked from the child classes with the super keyword.

    Input and Output Format :

    Refer to sample input and output.
    Input consists of n lines. Each line consists of a comma-separated values of the name of the shape and required sides of the corresponding shape
    Output should display the calculated area and perimeter of all the three shapes.

    Sample Input :

    Circle,11
    Square,4
    Triangle,3,4,5,4,6    

    Sample Output :

    Perimeter of a Circle: 69.08
    Area of a Circle: 379.94
    Perimeter of a Square: 16
    Area of a Square: 16
    Perimeter of a Triangle: 12
    Area of a Triangle: 12


```js title="app.js"
var fs = require('fs');
var input=fs.readFileSync('input.txt').toString().trim().split('\n');
//fill your code
var circle=input[0].split(',')
var square=input[1].split(',')
var triangle=input[2].split(',')
class Shape{
    
    constructor(side1,side2){
        this.side1=side1
        this.side2=side2
    }
    calculatePerimeter(side1){
           return  side1
    }
    calculateArea(side1,side2){
        return side1*side2
    }
}
var cName=String(circle[0])
var  cRadius=parseInt(circle[1])
class Circle extends Shape{
constructor(cName,cRadius){
    super()
    this.cName=cName
    this.cRadius=cRadius
}
displayCircleMeasurments(){
console.log("Perimeter of a "+this.cName+": "+2*3.14*super.calculatePerimeter(this.cRadius))
console.log("Area of a "+this.cName+": "+3.14*super.calculateArea(this.cRadius,this.cRadius))

}
}
var sName=String(square[0])
var  sSide=parseInt(square[1])
class Square extends Shape{
    constructor(sName,sSide){
        super()
    this.sName=sName
    this.sSide=sSide
}
displaySquareMeasurments(){
console.log("Perimeter of a "+this.sName+": "+4*super.calculatePerimeter(this.sSide))
console.log("Area of a "+this.sName+": "+super.calculateArea(this.sSide,this.sSide))

}
}
var tName=String(triangle[0])
var  side1=parseInt(triangle[1])
var  side2=parseInt(triangle[2])
var  side3=parseInt(triangle[3])
var  base=parseInt(triangle[4])
var  height=parseInt(triangle[5])
class Triangle extends Shape{
 
    constructor(tName,side1,side2,side3,base,height){
        super()
    this.tName=tName
    this.side1=side1
    this.side2=side2
    this.side3=side3
   // this.side4=this.side4
    this.base=base
    this.height=height
    this.sum=this.side1+this.side2+ this.side3
}

displayTriangleMeasurments(){

console.log("Perimeter of a "+this.tName+": "+super.calculatePerimeter(this.sum))
console.log("Area of a "+this.tName+": "+0.5*super.calculateArea(this.base,this.height))
}
}
var circle1=new Circle(cName,cRadius)
var square1=new Square(sName,sSide)
var triangle1=new Triangle(tName,side1,side2,side3,base,height)

circle1.displayCircleMeasurments();
square1.displaySquareMeasurments();
triangle1.displayTriangleMeasurments();
```
```txt title="input.txt"
Circle,11
Square,4
Triangle,3,4,5,4,6 
```