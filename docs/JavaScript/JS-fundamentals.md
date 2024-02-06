# JS-Fundamentals
## iDesign
    Eligible Voter

    A voting age is a minimum age established by law that a person must attain before they become eligible to vote in public election. Allow the person if his/her age is greater than or equal to 18 using function.

    Problem Description:
    1) Read input file ‘input.txt’.
    2) Check the constraint inside the function checkAge().
    3) Display the message for the voters based on the constraint.


    Input and Output Format:

    Refer to sample input and output.

    Input is the age of the person.

    Output is the message for voters.(Allowed/Not Allowed)

    Input:

    25

    Output:

    Allowed

    Input:

    7

    Output:
    Not Allowed
```js title="app.js"
var fs = require('fs');
var input = fs.readFileSync('input.txt').toString();
//fill your code
var age=parseInt(input)
if(checkAge(age)){
    console.log("Allowed")
}
else{
    console.log("Not Allowed")
}
function checkAge(age){
if(age>=18){
return true;
}
}
```
```txt title="input.txt"
65
```
## iAssess
### 1
    String Palindrome

    Write a JavaScript console program to read the input file and check whether the given string is palindrome or not.

    Input and Output Format:

    Refer sample input and output for formatting specifications.

    Input is a string.

    Output displays whether the given string is palindrome or not. (case insensitive)

    Note: Input should be read from input.txt

    The spaces should be removed before checking.

    Input 1:

    Taco cat

    Output 1:

    Taco cat is a palindrome

    Input 2:

    A gross creature

    Output 2:

    A gross creature is not a palindrome
```js title="app.js"
var fs = require('fs');
var input1 = fs.readFileSync('input.txt').toString();
//fill your code
var input=input1.trim().toLowerCase().replace(/\s/g, "");
function checkPalindrome(input){
    let length=input.length
    for(var i=0;i<length/2;i++){
        if(input[i]!==input[length-1-i]){
            return input1+" is not a palindrome"
        }
    }
    return input1+" is a palindrome"
}
var value=checkPalindrome(input)
console.log(value)

```
```txt title="input.txt"
Taco cat
```
### 2
    Find Factorial

    Write a program using the Arrow function to find the factorial of a given number.

    Input and Output :

    Below input is the format of the file input.txt.
    Input consists of an integer.
    Output is an integer.

    Sample Input :

    5

    Sample Output :

    120
```js title="app.js"
var fs=require('fs');
var input=fs.readFileSync('input.txt').toString().trim();

//Fill your code here
var value=(input)=>{
    var factorial=input
    for (let index = 1; index < input; index++) {
        factorial=factorial*index
        
    }

    return factorial
}
console.log(value(input))

```

