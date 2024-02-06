# AJAX
## iDesign
  Ajax – JSON Retrieval and updating JSON data

  Write a javascript code to display and update the Student details using JSON data.

  UI Constraints:   

  The file name should be index.html
  Get the details from the JSON data and display them in the table.
  Retrieve the table data from JSON during body onload and the function name should be display( ).
  Have a heading text 'Student Details' inside the 'h2' tag.
  The JSON file name should be Students.json
  After providing inputs and clicking the Update button, the Student table data should be updated.
  Kindly give the id’s and class names as per the constraints and screenshot.
  Use XMLHttpRequest to make Ajax call.
  Note :

  The content of the page should be present as shown in the screenshot.
  If you are using createElement() in the table, then use createTextNode() instead of innerText.
  Use ‘var’ instead of ‘let’ in the variable declaration.

  Sample Screenshot 1:



  Sample Screenshot 2:



  Sample Screenshot 3: (Provide the inputs to update)



  Sample Screenshot 4: (After the Email for the first Student)

```html title="index.html"
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    
    <title>Document</title>
    <style>
      table,
      th,
      td {
        border: 1px solid black;
        border-collapse: collapse;
        padding: 5px;
      }
    </style>
  </head>

  <body onload="display()">
    <center>
      <div style="border: 1px solid; padding: 5px" >
        <h2>Student Details</h2>
        <table id="student-table">
          
        </table>
        <br />
        Student Id : <input type="text" id="id" /><br /><br />
        Field Type :
        <select name="field" id="fieldType">
          <option value="name">Name</option>
          <option value="DOB">DOB</option>
          <option value="mobileNumber">Mobile Number</option>
          <option value="email">Email</option>
          <option value="address">Address</option>
          <option value="DOJ">DOJ</option>
          <option value="department">Department</option>
          <option value="mark">Mark</option></select
        ><br /><br />
        Field Value : <input type="text" id="fieldValue" /><br /><br />
        <button id="update" onclick="update()">UPDATE</button>
      </div>
    </center>
    <script>
      function display() {
        var xhttp = new XMLHttpRequest();
        xhttp.onreadystatechange = function () {
          if (this.readyState == 4 && this.status == 200) {
            var students = JSON.parse(this.responseText);
            var table = document.getElementById("student-table");
            var row = document.createElement("tr");
              var idCell = document.createElement("th");
              var nameCell = document.createElement("th");
              var dobCell = document.createElement("th");
              var mobileCell = document.createElement("th");
              var emailCell = document.createElement("th");
              var addressCell = document.createElement("th");
              var dojCell = document.createElement("th");
              var departmentCell = document.createElement("th");
              var markCell = document.createElement("th");

             
              idCell.appendChild(document.createTextNode("Id"));
              nameCell.appendChild(document.createTextNode("Name"));
              dobCell.appendChild(document.createTextNode("DOB"));
              mobileCell.appendChild(
              document.createTextNode("Mobile Number")
            );
            emailCell.appendChild(document.createTextNode("Email"));
            addressCell.appendChild(document.createTextNode("Address"));
            dojCell.appendChild(document.createTextNode("DOJ"));
            departmentCell.appendChild(document.createTextNode("Department"));
            markCell.appendChild(document.createTextNode("Mark"));

              row.appendChild(idCell);
              row.appendChild(nameCell);
              row.appendChild(dobCell);
              row.appendChild(mobileCell);
              row.appendChild(emailCell);
              row.appendChild(addressCell);
              row.appendChild(dojCell);
              row.appendChild(departmentCell);
              row.appendChild(markCell);
              table.appendChild(row);

            for (let i = 0; i < students.length; i++) {
              var row = document.createElement("tr");
              var idCell = document.createElement("td");
              var nameCell = document.createElement("td");
              var dobCell = document.createElement("td");
              var mobileCell = document.createElement("td");
              var emailCell = document.createElement("td");
              var addressCell = document.createElement("td");
              var dojCell = document.createElement("td");
              var departmentCell = document.createElement("td");
              var markCell = document.createElement("td");

              idCell.appendChild(document.createTextNode(students[i].id));
              nameCell.appendChild(document.createTextNode(students[i].name));
              dobCell.appendChild(document.createTextNode(students[i].DOB));
              mobileCell.appendChild(
                document.createTextNode(students[i].mobileNumber)
              );
              emailCell.appendChild(document.createTextNode(students[i].email));
              addressCell.appendChild(
                document.createTextNode(students[i].address)
              );
              dojCell.appendChild(document.createTextNode(students[i].DOJ));
              departmentCell.appendChild(
                document.createTextNode(students[i].department)
              );
              markCell.appendChild(document.createTextNode(students[i].mark));

              row.appendChild(idCell);
              row.appendChild(nameCell);
              row.appendChild(dobCell);
              row.appendChild(mobileCell);
              row.appendChild(emailCell);
              row.appendChild(addressCell);
              row.appendChild(dojCell);
              row.appendChild(departmentCell);
              row.appendChild(markCell);

              table.appendChild(row);
            }
          }
        };
        xhttp.open("GET", "Students.json", true);
        xhttp.send();
      }
      
      function update() {
        let id = document.getElementById("id").value;
        let fieldType = document.getElementById("fieldType").value;
        let fieldValue = document.getElementById("fieldValue").value;
        var table = document.getElementById("student-table");
        //var row = table.rows[id];
        var row = table.rows[id];

        let cellIndex = 0;

        console.log(fieldType);
        console.log(row);

        if (fieldType == "name") {
          cellIndex = 1;
        } else if (fieldType == "dob") {
          cellIndex = 2;
        } else if (fieldType == "mobileNumber") {
          cellIndex = 3;
        } else if (fieldType == "email") {
          cellIndex = 4;
        } else if (fieldType == "address") {
          cellIndex = 5;
        } else if (fieldType == "doj") {
          cellIndex = 6;
        } else if (fieldType == "department") {
          cellIndex = 7;
        } else {
          cellIndex = 8;
        }

        
          var cell = row.cells[cellIndex];
          cell.innerHTML = fieldValue;
          //console.log(cell);
        
      }
      
    </script>
  </body>
</html>

```
```json title="Students.json"
[
    {
    "id":"1",
    "name":"John",
    "DOB":"09-15-1998",
    "mobileNumber":"9967543421",
    "email":"john@email.com",
    "address":"Chennai",
    "DOJ" : "06-01-2016",
    "department" : "CSE",
    "mark" : "100"
    },
    {
    "id":"2",
    "name":"Liya",
    "DOB":"12-15-1997",
    "mobileNumber":"8978321211",
    "email":"liya@email.com",
    "address":"Coimbatore",
    "DOJ" : "06-01-2016",
    "department" : "ECE",
    "mark" : "78"
    },
    {
    "id":"3",
    "name":"Rio",
    "DOB":"10-20-1998",
    "mobileNumber":"9078342122",
    "email":"rio@email.com",
    "address":"Madurai",
    "DOJ" : "06-20-2016",
    "department" : "CSE",
    "mark" : "90"
    },
    {
    "id":"4",
    "name":"Priya",
    "DOB":"01-01-1998",
    "mobileNumber":"9965348304",
    "email":"priya@email.com",
    "address":"Coimbatore",
    "DOJ" : "06-20-2016",
    "department" : "CIVIL",
    "mark" : "95"
    },
    {
    "id":"5",
    "name":"Amy",
    "DOB":"11-23-1997",
    "mobileNumber":"9880153455",
    "email":"amy@email.com",
    "address":"Chennai",
    "DOJ" : "07-01-2016",
    "department" : "CSE",
    "mark" : "50"
    }
    ]
```
## iAssess
  Ajax – JSON Retrieval and JSON Conversion

  Design a webpage that will get the JSON details from a file and display it in a table. Then, display the Input fields to convert the particular booklist into a JSON format.

  Problem specification:

  The file name should be index.html.
  Get the details from the JSON data and display them in the table.
  Then displays the table data in the object notation format.
  UI Constraints :
  Retrieve the table data from JSON during body onload and the function name should be loadJson( ).
  Have a heading text 'Book List' inside the 'h1' tag.
  The JSON file name should be booklist.json
  Have a div tag with id “booklist”. And display the result table inside the div with id 'booklist'.
  Parse the JSON elements and display them in tabular form as shown in the screenshot.
  Have a button with id “convertToJSON” . While on clicking, the JSON format of entered book details should be displayed inside the div tag with id ‘jsonData’.
  Kindly give the id’s and class names as per the constraints and screenshot.
  Use XMLHttpRequest to make Ajax call.
  Note :

  The content of the page should be present as shown in the screenshot.
  If you are using createElement() in the table, then use createTextNode() instead of innerText.
  Use ‘var’ instead of ‘let’ in the variable declaration.

  Sample Screenshot 1:



  Sample Screenshot 2 :

```html title="index.html"
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body onload="loadJson()">
    <center>
      <h1>Book List</h1>
      <div id="booklist">
        <table id="listTable">
            <tbody>
                <tr>
                    <th>Book Name</th>
                    <th>Author Name</th>
                    <th>Price</th>
                    
                </tr>
            </tbody>
        </table>
      </div>
      <div class="formData">
        Book Name :<input type="text" id="name" /><br /><br />

        <div class="fields">
          Author name :<input type="text" id="price" /><br /><br />
        </div>
        Book Price :<input type="text" id="availableQuantity" /><br /><br />
      </div>
      <button id="convertToJSON" onclick="tojson()">Convert To JSON</button>
      <div id="jsonData"></div>
    </center>
  </body>
  <script>
    function loadJson() {
      const xhr = new XMLHttpRequest();
      xhr.open("GET", "booklist.json", true);
      xhr.onreadystatechange = function () {
        if (this.readyState == 4 && this.status == 200) {
          var object = JSON.parse(this.responseText);
          var div = document.getElementById("booklist");
          var table= document.getElementById("listTable")
          var tbody=table.getElementsByTagName("tbody")[0];

          for (let index = 0; index < object.length; index++) {
            const element = object[index];
            var row = document.createElement("tr");
            var bookCell = document.createElement("td");
            var authorCell = document.createElement("td");
            var priceCell = document.createElement("td");

            bookCell.appendChild(document.createTextNode(element.bookname));
            authorCell.appendChild(document.createTextNode(element.authorname));
            priceCell.appendChild(document.createTextNode(element.price));

            row.appendChild(bookCell);
            row.appendChild(authorCell);
            row.appendChild(priceCell);
            tbody.appendChild(row);
          }
        }
      };
      xhr.send();
    }
    function tojson() {
      var json = document.getElementById("jsonData");
      const xhr = new XMLHttpRequest();
      xhr.open("GET", "booklist.json", true);
      xhr.onreadystatechange = function () {
        if (this.readyState == 4 && this.status == 200) {
            var name=document.getElementById("name").value;
            var author=document.getElementById("price").value;
            var price=document.getElementById("availableQuantity").value;
            
          var object = JSON.parse(this.responseText);
          var jsonObject={}
          for (let index = 0; index <object.length; index++) {
            const element = object[index];
            if(element.bookname==name){
                jsonObject.bookname=name;
            }
            if(element.authorname==author){
                jsonObject.authorname=author;
            }
            if(element.price==price){
                jsonObject.price=price;
            }
          }
          json.innerHTML=JSON.stringify(jsonObject);
        }
      };
      xhr.send();
    }
  </script>
</html>

```
```css tiitle="style.css"
h1 {
    text-align: center;
    padding-top: 50px;
  }
  
  .btn {
    text-align: center;
  }
  
  #booklist {
    display: flex;
    justify-content: center;
  }
  
  table {
    border: 1px solid black;
    margin: 15px;
    border-collapse: collapse;
  }
  
  tr:first-child {
    background-color: lightblue;
  }
  
  tr:nth-child(even) {
    background-color: #f2f2f2;
  }
  
  th {
    border-bottom: 1px solid black;
    text-align: left;
    padding: 15px !important;
  }
  
  td {
    padding: 15px;
  }
  
  #getBooklist {
    padding: 10px;
  }
  
  .formData {
    text-align: center;
  }
  
  .fields {
    padding: 15px;
  }
  
  #convertToJSON {
    margin-top: 15px;
    padding: 10px;
    border: 1px solid black;
    border-radius: 5px;
    background-color: lightblue;
  }
  
  #jsonData {
    margin-top: 15px;
  }
  
  input {
      border-radius: 5px;
      padding: 7px;
      border: 1px solid gray;
  }
```
```json title="booklist.json"
[
    {
    "bookname":"Farm House",
    "authorname":"George Orwell",
    "price":"$10"
    },
    {
    "bookname":"Good Times, Bad Times",
    "authorname":"Harold Evans",
    "price":"$20"
    },
    {
    "bookname":"A Journey",
    "authorname":"Tony Blair",
    "price":"$50"
    },
    {
    "bookname":"The Jungle Book",
    "authorname":"Rudyard Kipling",
    "price":"$30"
    },
    {
    "bookname":"Oliver Twist",
    "authorname":"Charles Dickens",
    "price":"$40"
    }
    ]
```