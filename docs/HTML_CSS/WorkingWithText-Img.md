# Working with Text Img
## iDesign
    CSS - background repeat-x
    Being in the family of Webnotch Technologies, Sandra is very much interested in contributing her efforts for the betterment of the company. She has been waiting for the right time for showcasing her talent in web designing. Sandra has been assigned the task of redoing the web page created for their major client Pink Frag Event Organizer. Her superior gave her a prototype for the blog and the contents to be displayed in it.

    The blog contained the facts about the company and was decorated with a background image relating to the nature of the company's services. She thought of bringing something innovative about the site. She surfed various websites about the alignment of the background image in different ways and found out the usage of background repeat-x property in CSS as it will fill the image only in the horizontal axis.

    She has requested you to help her by finding out the implementations of this property.Hence create a web page using the background repeat-x property in CSS.

    Hints : background-repeat The background-repeat property sets how a background image will be repeated. By default, a background-image is repeated both vertically and horizontally. repeat-xThe background image is repeated only horizontallySyntax :    
    background-repeat: repeat|repeat-x|repeat-y|no-repeat|initial|inherit; 

    Content :
    h1 - Pink Frag Event Organizer
    hr
    h2 - Service Description
    p - We are indulged in offering a Promotional Event Management. These services are provided by our team of professionals as per the requirement of the client. These services are highly praised for their features like sophisticated technology, effective results and reliability. We offer these services in a definite time frame and at affordable rates.
    hr
    h2 - Features
    h5 - Customized services
    h5 - On-time completion
    h5 - Execution in tandem with clients demand
    hr
    h2 - About Us
    p - Pink Frag Event is a reputed organization, which has come into being in 2009, as a Sole Proprietorship Firm, with a sole aim of achieving the trust and support of large customers. We have indulged our all endeavors towards offering trustworthy Wedding Event Management, Promotional Event Management, Birthday Party Management and many more. All our services are reliable and offered keeping the exact customers’ preferences and choice in mind. To offer these services, we have hired specialized professionals, who are capable of understanding as well as accomplishing the specific customers’ desires. <br /> We have adopted modern technology, to cope up with the challenges of the industry. We keep all quality parameters in mind, so that we cannot make any compromise in terms of the excellence of products.
    hr
    h2 - Contact Us
    h3 - Address
    p - 14/509A,Sterlin Street,Nungambakkam
    Chennai - 600034.
    h3 - Mobile
    p - Manager-9596645125
    h3 - Landline
    p - 0422-2727272
    h3 - EMail
    p - pinkfragevent123@gmail.com   pinkfragOfficial@gmail.com

    Constraints :
    body tag with ' Background Repeat - repeat-x '  should be used in the html page .
    background image - Event.png


    Note :
    Web page should be displayed as shown in the screenshot.
    Kindly refer the content which is given as a part of the description.

    Sample Screenshot 1 :
    Without applying the Background Repeat - repeat-x property,


    Sample Screenshot 2 :
    After applying the Background Repeat - repeat-x property,

```html title="index.html"
<!DOCTYPE html>
<html>
    <head>
        <title>My First Website</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <link rel="stylesheet" href="styles.css" type="text/css">

    </head>
    <body>
        <img src="Event.png" alt="" backgro>
        <h1 id="h1Tag">Pink Frag Event Organizer</h1>  
        <hr>
        <h2 id="h2Tag">Service Description</h2>
        <p>We are indulged in offering a Promotional Event Management. 
            These services are provided by our team of professionals as 
            per the requirement of the client. 
            These services are highly praised for their features like 
            sophisticated technology, effective results and reliability. We offer 
            these services in a definite time frame and at affordable rates.
        </p>
        <hr>
        <h2 id="h2Tag"> Features</h2>
        <h5 id="h5Tag">Customized services</h5>
        <h5 id="h5Tag">On-time completion</h5>
        <h5 id="h5Tag">Execution in tandem with clients demand</h5>
        <hr>
        <h2 id="h2Tag">About Us</h2>
        <p> Pink Frag Event is a reputed organization, 
            which has come into being in 2009, as a Sole Proprietorship
            Firm, with a sole aim of achieving the trust and support of 
            large customers. We have indulged our all endeavors towards 
            offering trustworthy Wedding Event Management, Promotional
            Event Management, Birthday Party Management and many more. 
            All our services are reliable and offered keeping the exact 
            customers’ preferences and choice in mind. To offer these 
            services, we have hired specialized professionals, who are 
            capable of understanding as well as accomplishing the specific 
            customers’ desires. We have adopted modern technology, 
            to cope up with the challenges of industry. We keep all quality 
            parameters in mind, so that we cannot make any compromise in 
            terms of the excellence of products. </p>
        <hr>
        <h2 id="h2Tag">Contact Us</h2>
        <h3 id="h3Tag">Address</h3>
        <p>14/509A,Sterlin Street,Nungambakkam
        Chennai - 600034.</p>
        <h3 id="h3Tag">Mobile</h3>
        <p>Manager-9596645125</p>
        <h3 id="h3Tag">Landline</h3>
        <p>0422-2727272</p>
        <h3 id="h3Tag">EMail</h3>
        <p>pinkfragevent123@gmail.com   pinkfragOfficial@gmail.com
        </p>
    </body>
</html>

```
```css title="styles.css"
body{
    background-image: url("Event.png");
    background-repeat: repeat-x ;
}
```
## iAssess
    CSS - Striped Tables without class

    Nova, a web designer at Fusion Events has created a webpage for the upcoming Events that the company has signed for this year. She tested the webpage after completing it, but she noticed that all the rows in the event schedule were of the same color. To improve the visual appearance of the page, Nova decided to give two different colors for the odd and even rows in the event schedule.

    Let us help Nova to create the webpage displaying the events schedule using the nth-child() property.
    Hints : table-header-group   The :nth-child(n) selector matches every element that is the nth child, regardless of type,parent type.
    Odd and even are keywords that can be used to match child elements whose index is odd or even (theindex of the first child is 1).Syntax :   tagname:nth-child(odd) {
    CSS declarations
    }
    Example:   
    p:nth-child(odd) 
    {   
    color:pink;
    }

    Content :
    Name	Venue	Start Time	End Time
    Corporate Events	RVS Hall, 3rd Floor	4.5.2018 9.00AM	4.5.2018 12.00AM
    Wedding Planning	Sri Plus Thirumana Mahal	1.1.2019 7.00AM	1.1.2019 9.00AM
    Product Launches	RVS Hall, 2nd Floor	4.5.2018 2.00PM	4.5.2018 5.00PM
    Seminor on Cloud Computing	Vivekanandha Auditorium	18.12.2018 8.30AM	18.12.2018 1.00PM
    Heavenly Fashion	Bath Record Office	21.3.2018 5.00PM	21.3.2018 8.00PM
    Gala Dinners	City Tower, Hall No 2	12.1.2018 7.00 PM	12.1.2018 10.00 PM
    Award Ceremony	Hindustan Auditorium	11.11.2018 9.00 AM	11.11.2018 5.00 PM


    Constraints :
    The file name should be index.html.
    Apply styling properties without using the class or id attribute.
    The background color must be given for nth element in the table.
    The background color for even rows must be '#e0f0e9'.
    The background color for odd rows must be '#b3edcf'.

    Note :
    The webpage should be displayed as shown in the screenshot.
    Kindly refer the content which is given as a part of description.

    Sample Screenshot 1:



    Sample Screenshot 2:


```html title="index.html"
<!DOCTYPE html>
<html>
<head>
<style>
/*Fill you text here*/
tr:nth-child(odd){
background-color: #b3edcf;
}
tr:nth-child(even){
background-color: #e0f0e9;
}
</style>
</head>
<body>
<center>
  <h1>Event Schedule</h1>
  <div>          
		<table>
		<tr ><th>Name</th><th>Venue</th><th>Start Time</th><th>End Time</th></tr>
		<tr><td>Corporate Events</td><td>RVS Hall, 3rd Floor</td><td>4.5.2018 9.00AM</td><td>4.5.2018 12.00AM</td></tr>
		<tr><td>Wedding Planning</td><td>Sri Plus Thirumana Mahal</td><td>1.1.2019 7.00AM</td><td>1.1.2019 9.00AM</td></tr>
		<tr><td>Product Launches</td><td>RVS Hall, 2nd Floor</td><td>4.5.2018 2.00PM</td><td>4.5.2018 5.00PM</td></tr>
		<tr><td>Seminor on Cloud Computing</td><td>Vivekanandha Auditorium</td><td>18.12.2018 8.30AM</td><td>18.12.2018 1.00PM</td></tr>
		<tr><td>Heavenly Fashion</td><td>Bath Record Office</td><td>21.3.2018 5.00PM</td><td>21.3.2018 8.00PM</td></tr>
		<tr><td>Gala Dinners</td><td>City Tower, Hall No 2</td><td>12.1.2018 7.00 PM</td><td>12.1.2018 10.00 PM</td></tr>
		<tr><td>Award Ceremony</td><td>Hindustan Auditorium</td><td>11.11.2018 9.00 AM</td><td>11.11.2018 5.00 PM</td></tr>
		</table>
  </div>
</center>
</body>
</html>

```