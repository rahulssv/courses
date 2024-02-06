# Forms
## iDesign
    Forms - Registration form


    Design an HTML page for the registration form as shown in the screenshot.

    Hints :Tag `<select>`
    The `<select> `element is used to create a drop-down list. The `<option>` tags inside the `<select>` element define the available options in the list.
    Syntax :
    `<select> <option value="xxx"> xxx </option> <option value="yyy"> yyy </option> </select>`

    Sample Screenshot 1:



    Sample Screenshot 2 :



    Sample Screenshot 3 :



    Constraints :

    Have two pages named index.html and display.php.
    Refer screenshot for name and value specification of fields
    Display the entered details in display.php page.

    Note :

    Content of the page should be present as shown in the screenshot.
    Kindly refer to the content which is given as a part of the description.

    Content :

    Design a simple registration form with values
    h1 - Registration form
    Use ‘textarea’ element for the address field.

    TextField value

    name

    type

    Name                   

    name

    text

    Username

    userName

    text

    Password

    password

    password

    Re-enter Password

    re-EnterPassword

    password

    Address

    address

    textarea(element)

    Gender

    gender

    radio

    District Name

    districtName

    select

    Events

    events[]

    checkbox

    Register

    register

    submit


    Create a form with the above fields.
    display.php is provided in the template code.
    Design the HTML page using form and form action should be 'display.php' and the method should be 'POST'

    Template Code :

    Click here to download the template code.

```php title="display.php"
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
<center>
<h1>User Details</h1>
<?php
$name = $_POST['name'];
$username = $_POST['userName'];
$address = $_POST['address'];
$gender = $_POST['gender'];
$district = $_POST['districtName'];
$event[] =  array();
$event[] = $_POST['events'];
//print_r($event);
?>
<table>
	<tr>
		<td><?php echo "Name" ?></td>
		<td><?php echo ":" ?></td>
		<td><?php echo $name ?></td>
	</tr>
	<tr>
		<td><?php echo "User name" ?></td>
		<td><?php echo ":" ?></td>
		<td><?php echo $username ?></td>
	</tr>
	<tr>
		<td><?php echo "Address" ?></td>
		<td><?php echo ":" ?></td>
		<td><?php echo $address ?></td>
	</tr>
	<tr>
		<td><?php echo "Gender" ?></td>
		<td><?php echo ":" ?></td>
		<td><?php echo $gender ?></td>
	</tr>
	<tr>
		<td><?php echo "District" ?></td>
		<td><?php echo ":" ?></td>
		<td><?php echo $district ?></td>
	</tr>
	<tr>
		<td><?php echo "Events" ?></td>
		<td><?php echo ":" ?></td>
		<td>
			<?php foreach ($event[1] as $key =>$value): ?>
				<?php if($key< count($event[1])-1){
				  echo $value.", "; }
				  else { echo $value; } ?>
			<?php endforeach ?>	
		</td>
	</tr>
	</table>

</center>
</body>
</html>
```
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
    <form action="display.php" method="post">
        
            
            
            
            <table>
                
                <thead><h1>Registration form</h1></thead>
                <tr>
                <td>Name</td><td>: <input type="text" name="name" id="name"><br></td>
                </tr>
                <tr>
                    <td>Username </td><td>: <input type="text" name="userName" id="userName"><br></td>
                </tr>
                <tr>
                    <td>Password  </td><td>: <input type="password" name="password" id="password"><br></td>
                </tr>
                <tr>
                    <td>Re-enter Password </td><td>: <input type="password" name="re-EnterPassword" id="re-EnterPassword"><br></td>
                </tr>
                <tr>
                    <td>Address </td><td>: <textarea name="address" id="address" ></textarea><br></td>
                </tr>
                <tr>
                    <td>Gender </td><td>: <input type="radio" name="gender" id="gender" value="male">Male<input type="radio" name="gender" id="gender" value="female">Female <br></td>
                </tr>
                <tr>
                    <td>District Name  </td><td>: <select name="districtName" id="districtName"> <option value="New York">New York</option><option value="Coimbatore">Coimbatore</option></select><br></td>
                </tr>
                <tr>
                    <td>Events </td><td>: <input type="checkbox" name="events[]" id="events[]" value="wedding">Wedding <input type="checkbox" name="events[]" id="events[]"value="corporate">Corporate <input type="checkbox" name="events[]" id="events[]"value="social">Social<br></td>
                </tr>
                <tr>
                    <td></td>
                    <td>
                        <button type="submit" name="register">Register</button><br>
                        
                    </td>
                    
                </tr>
            </table>
    </form>
</body>
</html>
```
## iAssess
    Forms - maxlength
    D5 educational website which provides useful tutorials for all types of learners, has planned to maintain the database of the students and teachers who are benefited by them. The database stores information like user's name, username, password, mobile number and address. On validating the details enrolled by the users, they found many invalid entries like 12-digit mobile number, address with unwanted landmarks, etc.

    For eliminating such entries, the creative team of D5 educational institution has appointed you to create the website which would limit the input from the user as required. Hence, create a website with input fields following certain constraints like the mobile number field must not hold more than 10 digits and the address field should not hold more than 200 characters.
    Hints :  maxlength attribute  The maxlength attribute specifies the maximum number of characters allowed in the `<input> element. Syntax :    <input maxlength="number"> `

    Content :
    Design a html page with simple registration form
    h1 - Registration form 
    TextField value	name	textfield/textarea/button
    Name	name	textfield
    Username	username	textfield
    Password	password	textfield
    MobileNumber	mobilenumber	textfield
    Address	address	textarea
    Register	register	button

    Have the above textfields and a button.
    Set max attribute for the fields mobilenumber(10) and address(200).
    display.php is provided in the template code.
    Fill your code in index.html.

    Constraints :
    Have two pages called index.html and display.php
    Design the html page using form with action as 'display.php' and method as 'POST'
    The max attribute must be given for the mentioned fields.
    Use the names and the values as given in the screenshot.

    Note :
    Content of the page should be present as shown in the screenshot.
    Kindly refer to the content which is given as a part of the description.

    Sample Screenshot 1:



    Sample Screenshot 2:



    Sample Screenshot 3:



    Sample Screenshot 4 :

    display.php

```php title="display.php"
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
<center>
<?php
$name = $_POST['name'];
$username = $_POST['userName'];
$mobileNumber = $_POST['mobilenumber'];
$address = $_POST['address'];
echo "<table><tr>Name : ".$name."</tr>";
echo "<tr>User name : ".$username."</tr>";
echo "<tr>MobileNumber : ".$mobileNumber."</tr>";
echo "<tr>Address : ".$address."</tr></table>";
?>
</center>
</body>
</html>

```
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
    <form action="display.php" method="post">
        
            
            
            
            <table>
                
                <thead><h1>Registration form</h1></thead>
                <tr>
                <td>Name</td><td>: <input type="text" name="name" id="name"><br></td>
                </tr>
                <tr>
                    <td>Username </td><td>: <input type="text" name="username" id="username"><br></td>
                </tr>
                <tr>
                    <td>Password  </td><td>: <input type="password" name="password" id="password"><br></td>
                </tr>
                <tr>
                    <td>
                        Mobile Number
                    </td>
                    <td>
                        : <input type="number" name="mobilenumber" id="mobilenumber" value="MobileNumber" maxlength="10">
                    </td>
                </tr>
                <tr>
                    <td>Address </td><td>: <textarea name="address" id="address" maxlength="200"></textarea><br></td>
                </tr>
                
                <tr>
                    <td></td>
                    <td>
                        <button type="submit" name="register">Register</button><br>
                        
                    </td>
                    
                </tr>
            </table>
    </form>
</body>
</html>
```