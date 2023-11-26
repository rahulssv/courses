# Assessment
## Simple Billing App
```html title="index.html"
<!DOCTYPE html>
<html>
	<head>
	<meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Event Management</title>
	<script src="script.js"></script>
	;
	</head>
	<body>

	<!---Fill Code Here-->
	<center>
		<div id="eventForm">
			<table>
					
				<thead><h2>Event Management</h2></thead>
				<tr>
				<td>Event Name</td><td> <input type="text" name="name" id="name"><br></td>
				</tr>
				<tr>
					<td>Venue </td><td> <input type="text" name="venue" id="venue"><br></td>
				</tr>
				<tr>
					<td>Date  </td><td><input type="text" name="date" id="date" placeholder="dd/mm/yyy"><br></td>
				</tr>
				<tr>
					<td>Cost/day </td><td> <input type="number" name="price" id="price"><br></td>
				</tr>
				<tr>
					<td>Number of Days Needed </td><td> <input type="number" name="count" id="count"><br></td>
				</tr>
				
				<tr>
					<td></td>
					<td>
						<button type="submit" id="addEvent" onclick="addEvent()">Add Event</button><br>
						
					</td>
					
				</tr>
			</table>
		</div>
		<div id="result">		
			
			<table border=1 id="resultTable">
				
				<tbody>

				</tbody>
			</table>		
		</div>
		
	</center>
	


	</body>
</html>


```
```js title="script.js"
const events = [];
function addEvent() {
    var table = document.getElementById("resultTable");
    table.innerHTML='';
  var name = document.getElementById("name").value;
  var venue = document.getElementById("venue").value;
  var date = document.getElementById("date").value;
  var price = document.getElementById("price").value;
  var count = document.getElementById("count").value;
  var dateParts = date.split("/");
  date = dateParts[2] + "-" + dateParts[1] + "-" + dateParts[0];
  var totalCost = parseInt(count, 10) * parseInt(price, 10);

  events.push({
    name: name,
    venue: venue,
    date: date,
    totalCost: totalCost,
  });

  display();
}
function display() {
  var result = document.getElementById("result");
  //result.style.display = "inline";
  if (events.length > 0) {
    
    var table = document.getElementById("resultTable");
    
    
    for (var index =0; index < events.length; index++) {
        if(index==0){
            var row = document.createElement("tr");
            var nameCell = document.createElement("th");
            var venueCell = document.createElement("th");
            var dateCell = document.createElement("th");
            var totalCostCell = document.createElement("th");
            var cancelCell = document.createElement("th");
        
            nameCell.appendChild(document.createTextNode("Event Name"));
            venueCell.appendChild(document.createTextNode("Venue"));
            dateCell.appendChild(document.createTextNode("Date"));
            totalCostCell.appendChild(document.createTextNode("Total Cost"));
            cancelCell.appendChild(document.createTextNode("Cancel Event"));
        
            row.appendChild(nameCell);
            row.appendChild(venueCell);
            row.appendChild(dateCell);
            row.appendChild(totalCostCell);
            row.appendChild(cancelCell);
            table.appendChild(row);



        }
      var element = events[index];
      var row = document.createElement("tr");
      var nameCell = document.createElement("td");
      var venueCell = document.createElement("td");
      var dateCell = document.createElement("td");
      var totalCostCell = document.createElement("td");
      var cancelCell = document.createElement("td");

      nameCell.appendChild(document.createTextNode(element.name));
      venueCell.appendChild(document.createTextNode(element.venue));
      dateCell.appendChild(document.createTextNode(element.date));
      totalCostCell.appendChild(document.createTextNode(element.totalCost));
      var a = document.createElement("a");
      var i = index.toString();
      a.setAttribute("id", "link" + i);
      a.setAttribute("href", "#");
      a.setAttribute("onclick", "deleteElement(" + i + ")");
      a.innerHTML = "Cancel";
      cancelCell.appendChild(a);

      row.appendChild(nameCell);
      row.appendChild(venueCell);
      row.appendChild(dateCell);
      row.appendChild(totalCostCell);
      row.appendChild(cancelCell);
      table.appendChild(row);
    }
  } else {
    //result.style.display = "inline";
    result.innerHTML = "No Events available";
  }
}
function deleteElement(i) {

  events.splice(i, 1);
  var table = document.getElementById("resultTable");
    table.innerHTML='';
  display();
}

```
## Student Details Search
```html title="index.html"
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <link  rel="stylesheet"href="style.css">
        <title>Student Details</title>
    </head>
<body>      
   
<h3>Student Details Search</h3>
<input type="text" id="studentname" placeholder="Enter Student Name">
<button id="search" onclick="display()">Search</button>
<div id="result"></div>
<!-- Fill your code -->

<script>


    // Fill your code
    function display() {
        var xhttp = new XMLHttpRequest();
        xhttp.onreadystatechange = function () {
          if (this.readyState == 4 && this.status == 200) {
            var students = JSON.parse(this.responseText);
            var div = document.getElementById("result");
            

            for (let i = 0; i < students.length; i++) {
                if(students[i].name ==(document.getElementById("studentname").value)){
                var nameCell = document.createElement("ul");
              var cgpaCell = document.createElement("ul");
              var ageCell = document.createElement("ul");
              var departmentCell = document.createElement("ul");
              var batchCell = document.createElement("ul");

              nameCell.appendChild(document.createTextNode("Name :" +students[i].name));
              cgpaCell.appendChild(document.createTextNode("CGPA :" +students[i].cgpa));
              ageCell.appendChild(document.createTextNode("Age :" +students[i].age));
              departmentCell.appendChild(document.createTextNode("Department :" +students[i].department));
              batchCell.appendChild(document.createTextNode("Batch :" +students[i].batch));

              div.appendChild(nameCell);
              div.appendChild(cgpaCell);
              div.appendChild(ageCell);
              div.appendChild(departmentCell);
              div.appendChild(batchCell);
                }

              
            }
          }
        };
        xhttp.open("GET", "StudentDetails.json", true);
        xhttp.send();
      }

</script>
</body>
</html>


```

```json title="StudentDetails.json"
[
    {
    "name": "Jhon",
    "cgpa":"6.7",
    "age": 20,
    "department": "CSE",
    "batch":"2022"
    },

    {
    "name": "Smith",
    "cgpa":"7.7",
    "age": 21,
    "department": "EEE",
    "batch":"2021"
    },

    {
    "name": "Alex",
    "cgpa":"8.7",
    "age": 22,
    "department": "MECH",
    "batch":"2020"
    },

    {
    "name": "Jack",
    "cgpa":"10.7",
    "age": 24,
    "department": "ECE",
    "batch":"2018"
    },

    {
    "name": "James",
    "cgpa":"9.7",
    "age": 23,
    "department": "CIVIL",  
    "batch":"2019"
    },

    {
    "name": "Tom",
    "cgpa":"7.6",
    "age": 25,
    "department": "CSE",
    "batch":"2017"
    },

    {
    "name": "Harry",
    "cgpa":"8.6",
    "age": 26,
    "department": "EEE",
    "batch":"2016"
    },

    {
    "name": "Ron",
    "cgpa":"9.6",
    "age": 27,
    "department": "MECH",
    "batch":"2015"
    },

    {
    "name": "Hermione",
    "cgpa":"10.6",
    "age": 28,
    "department": "ECE",
    "batch":"2014"
    },

    {
    "name": "Draco",
    "cgpa":"9.5",
    "age": 29,
    "department": "CIVIL",  
    "batch":"2013"
    },

    {
    "name": "Voldemort",
    "cgpa":"8.5",
    "age": 30,
    "department": "CSE",
    "batch":"2012"
    }   
]
```
```css title="style.css"
body{
    font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    font-size: 20px;
    line-height: 1.5;
    margin: 0;
    padding: 0;
    text-align: center;
}
#result{
    text-align: left;
    margin: 0 auto;
    margin-top: 30px;
    width: 25%;
    border-radius: 10px;

}
#studentname{
    font-weight: bold;
    margin-bottom: 10px;
    padding: auto;
    width: 200px;
    height: 20px;
    border-radius: 5px;
    border: 2px solid rgb(215, 211, 211);
    
}
ul{
    list-style-type: none;
    margin-bottom: 10px;
    margin-left: 30px;
    text-align: left;
}
h3{
    margin-bottom: 20px;
    font-size: 25px;
}


```