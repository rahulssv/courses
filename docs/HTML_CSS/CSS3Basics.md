# CSS3 Basics
## iDesign

    CSS styling - color
    Sean and Roger have joined the WebMakers company as interns. As they are beginners in the field, they were guided to get hands-on exposure about HTML and CSS concepts. The major client of their company was the Pink frag Event Organizer Company. The Company provides the leading event management services for birthday, wedding, corporate events and business conference.

    After their internship period, Sean and Reon's first task was to create a sample webpage for Pink frag Organizer Company. They initially used the basic black font-color for the home page which was not much appealing. Sean and Roger wants to find out the suitable font colors for the webpage but they are not so confident of implementing it.

    Let us explain them the usage of color attribute by creating a webpage using color attribute in CSS.
    Hints : color attribute 
    It is used to change the color of the any element in which the styling is used. 
    Syntax :   `<h1 style="color:blue;">This is a Blue Heading</h1> `

    Content :
    H1 - Pink Frag Event Organizer
    HR
    H2 - Service Description
    P - We are indulged in offering a Promotional Event Management. These services are provided by our team of professionals as per the requirement of the client. These services are highly praised for their features like sophisticated technology, effective results and reliability. We offer these services in a definite time frame and at affordable rates.
    HR
    H2 - Features
    H5 - Customized services
    H5 - On-time completion
    H5 - Execution in tandem with clients demand
    HR
    H2 - About Us
    p- Pink Frag Event is a reputed organization, which has come into being in 2009, as a Sole Proprietorship Firm, with a sole aim of achieving the trust and support of large customers. We have indulged our all endeavors towards offering trustworthy Wedding Event Management, Promotional Event Management, Birthday Party Management and many more. All our services are reliable and offered keeping the exact customers’ preferences and choice in mind. To offer these services, we have hired specialized professionals, who are capable of understanding as well as accomplishing the specific customers’ desires. `<br />` We have adopted modern technology, to cope up with the challenges of industry. We keep all quality parameters in mind, so that we cannot make any compromise in terms of the excellence of products.
    HR
    H2 - Contact Us
    H3 - Address
    p - 14/509A,Sterlin Street,Nungambakkam
    Chennai - 600034.
    H3 - Mobile
    p - Manager-9596645125
    H3 - Landline
    p - 0422-2727272
    H3 - EMail
    p - pinkfragevent123@gmail.com   pinkfragOfficial@gmail.com

    Constraints :
    There must be one h1 tag with color '#356ecc' .
    There must be four h2 tags with color '#f9b222'.
    All tags should have seperate style attribute with color specification.

    Note :
    Content of the page should be present as shown in the screenshot.
    Kindly refer the content which is given as a part of description.

    Sample Screenshot 1:



    Sample Screenshot 2:

```html title="index.html"
<!DOCTYPE html>
<html>
    <head>
        <title>My First Website</title>
    </head>
    <body>
        <h1 style="color:#356ecc ;">Pink Frag Event Organizer</h1>
        <hr>
        <h2 style="color:#f9b222 ;">Service Description</h2>
        <p>We are indulged in offering a Promotional Event Management. 
            These services are provided by our team of professionals as 
            per the requirement of the client. 
            These services are highly praised for their features like 
            sophisticated technology, effective results and reliability. We offer 
            these services in a definite time frame and at affordable rates.
        </p>
        <hr>
        <h2 style="color:#f9b222 ;"> Features</h2>
        <h5>Customized services</h5>
        <h5>On-time completion</h5>
        <h5>Execution in tandem with clients demand</h5>
        <hr>
        <h2 style="color:#f9b222 ;">About Us</h2>
        <p> Pink Frag Event is a reputed organization, 
            which has come into being in 2009, as a Sole Proprietorship
            Firm, with a sole aim of achieving the trust and support of 
            large customers. We have indulged our all endeavors towards 
            offering trustworthy Wedding Event Management, Promotional
            Event Management, Birthday Party Management and many more. 
            All our services are reliable and offered keeping the exact 
            customers preferences and choice in mind. To offer these 
            services, we have hired specialized professionals, who are 
            capable of understanding as well as accomplishing the specific 
            customers desires.<br />
            We have adopted modern technology, 
            to cope up with the challenges of industry. We keep all quality 
            parameters in mind, so that we cannot make any compromise in 
            terms of the excellence of products. </p>
        <hr>
        <h2 style="color:#f9b222 ;">Contact Us</h2>
        <h3>Address</h3>
        <p>14/509A,Sterlin Street,Nungambakkam
        Chennai - 600034.</p>
        <h3>Mobile</h3>
        <p>Manager-9596645125</p>
        <h3>Landline</h3>
        <p>0422-2727272</p>
        <h3>EMail</h3>
        <p>pinkfragevent123@gmail.com   pinkfragOfficial@gmail.com
        </p>
    </body>
</html>

```
## iAssess
    CSS - Internal styling by id


    Design a webpage using Internal styling by id as shown in the screenshot.

    Sample Screenshot :



    Constraints :



    Additional Constraints :

    The webpage design shall be of internal style.
    The content is given in the template itself.
    The colors shall be the same as given in the constraints.
    Use the id attribute for styling the webpage.

    h1 titles are in pink color(#F835C0)
    h2 titles are in red color(#ff0000)
    h3 titles are in green color(#15D365)
    h5 titles are in violet color( #9F41F5)

    Note :

    Content of the page should be present as shown in the screenshot.
    Kindly refer to the content which is given as a part of the description.

    Template Code :

    Click here to download the template code.

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
#h1Tag{
    color: #F835C0;
}
#h2Tag{
    color:#ff0000;
}
#h3Tag{
    color: #15D365;
}
#h5Tag{
    color:  #9F41F5;
}
```