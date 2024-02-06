# HTML-DOM
## iDesign
### 1
    Changing property using Javascript

    

    Design an HTML page as shown in the screenshot and apply the style using the Javascript function.

    Property marginTop
    Set the top margin of a <div> element.
    Syntax :
    document.getElementById("myDiv").style.marginTop = "50px"; 
    Property border
    Add a border to a <div> element.
    Syntax :
    document.getElementById("myDiv").style.border= "1px solid"; 

    Sample Screenshot :



    Constraints:

    The outer div should have a border and the inner div should have margin-top property



    Additional Constraints :

    The file name shall be index.html.
    Have two div's, one inside the other.
    The outer div shall have id "outerDiv" and apply border property in the script.
    The inner div shall have id "innerDiv" and apply marginTop property in the script.
    Change the properties inside the apply() function.
    Load the function apply() on body onload attribute.

    Note :

    Content of the page should be present as shown in the screenshot.

    Content :

    A wedding planner is a professional who assists with the design, planning and management of a client's wedding. Weddings are significant events in people's lives and as such, couples are often willing to spend considerable amount of money to ensure that their weddings are well-organized. Wedding planners are often used by couples who work long hours and have little spare time available for sourcing and managing wedding venues and wedding suppliers.

    Template Code :

    Click here to download the template code.
```html title="index.html"
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body onload="apply()">
    <div id="outerDiv">
        <div id="innerDiv">
            <p>
A wedding planner is a professional who assists with the design, planning and management of a client's wedding. Weddings are significant events in people's lives and as such, couples are often willing to spend considerable amount of money to ensure that their weddings are well-organized. Wedding planners are often used by couples who work long hours and have little spare time available for sourcing and managing wedding venues and wedding suppliers.

            </p>
        </div>
    </div>
    <script>
        function apply(){
            document.getElementById("outerDiv").style.border= "1px solid"; 
        document.getElementById("innerDiv").style.marginTop = "100px"; 
        }
   
    </script>
</body>
</html>
```
### 2

    JS - Credit card validation


    Design an HTML page to perform phone number and credit card validation using javascript as shown in the screenshot.

    Sample Screenshot 1:



    Sample Screenshot 2 :

    If the phone number contains anything other than digits it must print 'Phone number must contain only digits' in the div with id 'phoneNumber_Warning'.



    Sample Screenshot 3 :

    If the card number contains other than digits it must print 'Card number must contain only digits' in the div with id 'cardNumber_Warning'.



    Sample Screenshot 4 :



    Sample Screenshot 5 :

    If the Phone number does not contain 10 digits it must print 'Phone Number must be 10 digits' in the div with id 'phoneNumber_Warning'.



    Sample Screenshot 6 :

    If the card number does not contain 16 digits it must print 'Card Number must be 16 digits' in the div with id 'cardNumber_Warning'. 



    Sample Screenshot 7 :

    If both phone and card numbers are validated, then print 'Details stored in database' in the div with id 'success'



    Note :

    Content of the page should be present as shown in the screenshot.

    Template Code :

    Click here to download the template code.
```html title="index.html"
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="form-data">
        <h3>Phone Number & Card Validation</h3>
        <form action="" id="form-validation" >
            <div id="PhoneNumber_Warning" style="-webkit-text-fill-color: red;"></div>
            <label for="phone-number">Enter your Phone Number :</label>
            <input type="text" id="phone-number" name="phone-number" onkeydown="checkPhone()" required>
            
            <br>
            <label for="card-number">Enter your Card Number :</label>
            <input type="text" id="card-number" name="card-number" onkeydown="checkCard()" required>
            <div id="CardNumber_Warning" style="-webkit-text-fill-color: red;"></div>
            <br>
            <button type="submit" id="validate">Validate</button>
            <br>
            <div id="success" style="-webkit-text-fill-color: green;"></div>

        </form>
    </div>
    <script>
        document.getElementById("form-data").style.border="1px solid"
        function checkPhone(){
            const phone=/^\d*$/;
            const phoneData=document.getElementById("phone-number").value;
            if(!phone.test(phoneData)){
                document.getElementById("PhoneNumber_Warning").innerHTML="Phone number must contains only digits"
            }
        }
        function checkCard(){
            const card=/^\d*$/;
            const cardData=document.getElementById("card-number").value;
            if(!card.test(cardData)){
                document.getElementById("CardNumber_Warning").innerHTML="Card number must contains only digits"
            }
        }
        function validate(event){
            event.preventDefault();
            const phoneNumber= document.getElementById("phone-number").value;
            const cardNumber= document.getElementById("card-number").value;
            flag=true;

            //const phoneNumberRegex=/^\d{10}$/
            if (phoneNumber.length!=10) {
                document.getElementById("PhoneNumber_Warning").innerHTML="Phone Number must be 10 digits";
                
                    flag=false;
            }
            //const cardNumberRegex=/^\d{16}$/
            if (cardNumber.length!=16) {
                document.getElementById("CardNumber_Warning").innerHTML="Card Number must be 16 digits";
               flag=false
            }
            if(flag){
                document.getElementById("success").innerHTML="Details stored in database"
            }
               
            
            
        }
        const form =document.getElementById("form-validation")
        form.addEventListener("submit",validate)
    </script>
</body>
</html>
```
### 3
    `JS - Oninput Event
    "Eventious" is one of the most popular online application being used by the people of all age groups as it would include knowledgeable games. They have planned to launch a new game that would display the content simultaneously when the user types the values in the specific field. This game would estimate the speed of the contents being typed in the content box.

    As the developers of Eventious are busy in playing support roles for the existing games, the technnical team has assigned you the task of creating the web-app for repeating the contents in the text area using oninput events in javascript.
    Hints : The oninput event occurs when an element gets user input.
    This event occurs when the value of an `<input> or <textarea>` element is changed.Syntax :`<element oninput="myScript">`

    Content :
    h3 - Oninput Event
    Have one `<div>` element with id 'result'
    Have a `<textarea> `field with id 'myContent' and oninput attribute value 'displayContent()'
    Display the whole content inside the `<center>` tag.
    Include the following functions/methods in the script.
    Function Name	Description
    displayContent()	This method is used to display the content of textarea in the resulting `<div> `element while the user types and clears the content.

    Constraints:
    File name should be 'index.html'.
    Enter the content in the textarea with id 'myContent'.
    The content of textarea must be displayed inside the div element with id 'result' while the user types and clears the content.

    Note :
    Content of the page should be present as shown in the screenshot.
    Kindly refer the content which is given as a part of description.

    Sample Screenshot 1 :



    Sample Screenshot 2 :
    On entering the contents in textarea , it should be displayed in the result div as mentioned below,



    Sample Screenshot 3 :



    Sample Screenshot 4 :
    On clearing the content in textarea , the change should be reflected in the result div.`

```html title="index.html"
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div style="border: 1px solid;">
        <center>
        <h3>Oninput Event</h3>
        <br>
        <textarea name="myContent" id="myContent" cols="30" rows="10" oninput="displayContent()"></textarea>
        <div id="result"></div>
        </center>
        
        
    </div>
    <script>
        function displayContent(){
            var x = document.getElementById("myContent").value;
            document.getElementById("result").innerHTML="Typed text is : "+x;
        }
    </script>
</body>
</html>
```
## iAssess
### 1
    JS - Grade
    Maple Educational Institutions has conducted an Entrance Examination to select prospective students for admissions of the upcoming academic year. The students who have cleared the entrance exam with 50% and above i.e more than 'E' grade are considered for the post-admission process, where other students have to re-appear for the examinations.


    The Institution Management decided to announce the exam results with the grade obtained by each of the students on their official website and has approached you for help.  Create a webpage which will get the marks as input from the students and display the grade obtained by them.
    Hints : if/else statementUse if to specify a block of code to be executed, if a specified condition is true. 
    Use else to specify a block of code to be executed, if the same condition is false. Syntax :    
    if (condition) {
    // if the condition is true block of code to be executed 
    } else {
    // if fails else part gets executed
    }

    Constraints :
    The Html page must contain a h1 tag.
    The name and id of the text field should be "mark".
    The name of the button should be "submit".
    onclick attribute should have the value "myFunction()".
    Grade sheet is as mentioned below.
    S.No	Marks	Grade
    1	100	A+
    2	90 - 99	A
    3	80 - 89	B
    4	70 - 79	C
    5	60 - 69	D
    6	50 - 59	E
    7	below 50	RA

    The grade of the student must be displayed inside the div element with id "result".

    Note :
    Content of the page should be present as shown in the screenshot.
    Kindly refer the content which is given as a part of description.

    Sample Screenshot 1 :



    Sample Screenshot 2 :



    Sample Screenshot 3 :




    Sample Screenshot 4 :



    Sample Screenshot 5 :



    Sample Screenshot 6 :



    Sample Screenshot 7 :



    Sample Screenshot 8 :
```html title="index.html"
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div style="border: 1px solid;">
        <center>
            <h1>Grade Sheet</h1>
            <br>
            Marks <input type="text" name="mark" id="mark">
            <br>
            <button type="button" name="submit" onclick="myFunction()">Submit</button>
            <div id="result"></div>
        </center>
    </div>
    <script>
        function myFunction(){
            const marks=document.getElementById("mark").value;
            if (marks==100) {
                document.getElementById("result").style.color="green";
                document.getElementById("result").innerHTML="Grade obtained by the student is : A+"
            }
            else{
                if(marks<100&&marks>=90){
                document.getElementById("result").style.color="green";
                document.getElementById("result").innerHTML="Grade obtained by the student is : A"
            }else{
                if(marks<90&&marks>=80){
                document.getElementById("result").style.color="green";
                document.getElementById("result").innerHTML="Grade obtained by the student is : B"
            }
            else{
                if(marks<80&&marks>=70){
                document.getElementById("result").style.color="green";
                document.getElementById("result").innerHTML="Grade obtained by the student is : C"
            }
            else{
                if(marks<70&&marks>=60){
                document.getElementById("result").style.color="green";
                document.getElementById("result").innerHTML="Grade obtained by the student is : D"
            }

            else{
                if(marks<60&&marks>=50){
                document.getElementById("result").style.color="green";
                document.getElementById("result").innerHTML="Grade obtained by the student is : E"
            }
            else{
                if(marks<50){
                document.getElementById("result").style.color="red";
                document.getElementById("result").innerHTML="Grade obtained by the student is : RA"
            }
            }
            }
            }
            }
            }
            }
            
        }
    </script>
</body>
</html>
```
### 2
    JS - Increase width and height
    Nowadays, pictures play an important role in strengthening the communication and marketing efforts in all levels of publishing the organization. Recently Lee, the techno-assistant of "Pink Frag Event Organization" got a feedback regarding the images being uploaded in their official website couldnt be clearly understood, as the resolution was not upto the level.

    Hence, Lee has assigned you the task of making the images to be zoomed in i.e, the width and heigth of the images should be increased on every double click on the image using the javascript functions.

    Hints :  Width and height Property  The width property sets or returns the width an element. The height property sets or returns the height of an element. The width and height property has effect only on block-level elements or on elements with absolute / fixed position.  Syntax :   object.style.width (for width) and object.style.height (for height) where object = document.getElementById("#id");


    Content :
    h1 - Increase width and height of div
    div id="myDiv" width="400px" height="200px" ondblclick="addSize()"
    h3 - Pink frag Event Organization
    Our events team handles all your requirements from conceptualization to execution, leaving you free to focus completely on achieving your objectives.With proper planning and logistics management and the ability to activate requisite resources, we have undertaken a wide variety of projects.

    Constraints:
    The file name should be index.html.
    Create a div with id "myDiv" and the content as mentioned above.
    Increase the width and the height of the div by "10px" on every double click.

    Note :
    Content of the page should be present as shown in the screenshot.
    Kindly refer the content which is given as a part of description.

    Sample Screenshot 1 :



    Sample Screenshot 2 :
    For the first doubleClick(),


    Sample Screenshot 3 :
    For the sixth doubleClick(),

```html title="index.html"
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <center>
        <div style="border: 1px solid;">
            <h1>Increase width and height of div</h1>
            <div id="myDiv" ondblclick="addSize()" style=" height: 200px;width: 400px;">
                <h3>Pink frag Event Organization</h3>
                Our events team handles all your requirements from conceptualization to execution, leaving you free to focus completely on achieving your objectives.With proper planning and logistics management and the ability to activate requisite resources, we have undertaken a wide variety of projects.
    
            </div>
        </div>
    </center>
    
    <script>
        function addSize(){
            
            var currentWidth = document.getElementById('myDiv').offsetWidth;

  
  document.getElementById('myDiv').style.width = (currentWidth +10) + "px";
  var currentHeight = document.getElementById('myDiv').offsetHeight;
 
  
  document.getElementById('myDiv').style.height = (currentHeight + 10) + "px";
        }
    </script>
</body>
</html>
```
