# Layout
## iDesign
  BestBuy Electronix  has been one of the  premier electronic appliances and good dealership company with branches spread across multiple states. They have most comprehensive ranges of branded products for sale in the market. A lot of their stock has been driven by customer demand. They are experts at sourcing exactly what the client needs and offering at the best affordable price. Customer satisfaction is their primary goal and they are always looking to please their clients. So they decided to design a webpage for the company.

  Help the team to design an attractive webpage for the BestBuy Electronix.

  Constraints :
  The main file name should be “index.html”.
  Write css codes in css/app.css file.
  Images should be in images folder.
  Icons will be loaded from css/icon.css folder.
  Design the page using basics styles mentioned below.
  img tag should have src attribute as ‘fastrack.jpg’

  div with class product-card should have following styles

      width: 35%;
      position: relative;
      padding: 20px 20px 40px 20px;
      background-color: #fff;
      box-shadow: 0 0px 10px #e4e4e4;
      border-radius: 5px;
      overflow: hidden;
  figure tag with class image should have following styles

  width: 220px;
  height: 220px;
  overflow: hidden;
  text-align: center;
  display: block;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 20px;
  div with class star-group should have following styles

  margin-top:10px;
  display: inline-block;
  background-color: #F5821F;
  padding: 2px 10px;
  display: inline-block;
  border-radius: 5px;
  div with class product-name should have following styles

  margin-top:10px;
  div with class product-name should have following styles

  font-size : 12px
  HTML Constraints :
  All the tags marked in the screenshots should be present in the html page.

  Sample Screenshot 1:


  Sample Screenshot 2:

```html title="index.html"
<!DOCTYPE html>
<html lang="en">

<head>
    <title>Retail Project | Product Details</title>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <link href="css/icon.css" rel="stylesheet">
    <link href="css/app.css" rel="stylesheet">
</head>
<body>
    <div class="top-wrapper">
        <div class="logo-wrapper">
            <img src="images/logo.png">
        </div>
        <div class="menu-bar">
            <div class="search-bar">
                <input type="text" class="form-control" placeholder="Search for Products">
                <span class="icon icon-search"></span>
            </div>
            <div class="action-lists">
                <ul>
                    <li class="alert"><a href="#"><span class="icon icon-alert"></span></a></li>
                    <li class="cart"><a href="#"><span class="icon icon-cart"></span></a></li>
                    <li class="wishlist"><a href="#"><span class="icon icon-wishlist"></span></a></li>
                    <li class="user">
                        <a href="#">
                            <span class="user-name">Aaron</span>
                        </a>
                    </li>
                </ul>
            </div>           
        </div>
    </div>   

    <div class="main-wrapper">
       <!-- Fill your code  -->
       <div class="product-card">
        <figure class="image">
            <img src="images/fastrack.jpg" alt="">
        </figure>
        <div>

            <div class="star-group">
                4 <span class="icon icon-star"></span>
            </div>
            <span class="price">
                $299
            </span> 
            
        </div>
        
        <div>
            <p class="product-name">Fastrack Reflex Activity Tracker </p>
            <p class="small-text">Redesigned from scratch and completely revised</p>
        </div>
        
        <center><div>
            <a id="wishlist" href="#" ><span class="icon icon-wishlist"></span> WISHLIST</a>
            <a id="add-to-cart" href="#" >ADD TO CART</a>
        </div>
        </center>
        
            
            
       </div>
    </div>
	<footer>
	  <p>Posted by: Hege Refsnes</p>
	  <p>Contact information: <a href="mailto:hege@bestbuy.com">hege@bestbuy.com</a></p>
	</footer>
</body>
</html>

```
## iAssess
  Lists - horizontal menu
  Britto, the Chief Executive Officer of the "Boomerang Solutions" is an entrepreneur by profession but a web designer by passion. During his leisure time, he used to re-create his favorite site in the Internet using HTML. In the recent times, he got attracted to the official website of the "Pink Frag Event Organizers" company and started trying the design using a sample content.

  He understood all the concepts used in the website except the Horizontal menu containing links. Hence, he is in need of your help for creating a webpage using float property.

  Hints :float propertyThe float property specifies how an element should float. It is used to get block elements to slide next to each other.Syntax :   
  float: none|left|right|initial|inherit;

  Content :
  h3 - Pink Frag Event Organizer
  p tag - We are indulged in offering a Promotional Event Management.These services are provided by our team of professionals as per the requirement of the client. These services are highly praised for their features like sophisticated technology, effective results and reliability. We offer these services in a definite time frame and at affordable rates.
  Pink Frag Event is a reputed organization,which has come into being in 2009, as a Sole Proprietorship Firm, with a sole aim of achieving the trust and support of large customers. We have indulged our all endeavors towards offering trustworthy Wedding Event Management, Promotional Event Management, Birthday Party Management and many more.To offer these services, we have hired specialized professionals, who are capable of understanding as well as accomplishing the specific customers' desires.

  Constraints :
  Design the html page as given in the sample screenshot1.
  Use ul tag for designing the menu.
  each 'li' tag style should have float : 'left' property.
  There must be 4 'a' tags inside the html page.
  Refer the screenshots for html specifications.
  The href attribute for 'a' tag is "#".

  The 'ul' tag should have the following style property,
      list-style-type - none
      background-color - #87CEEB
      padding -10px 0
      overflow - hidden

  Initially, 'a' tag should have the following style property,
      background-color - #87CEEB
      color - #000000
      width - 20px
      border - 1px solid #808080
      padding - 15px
      text-align - center
      text-decoration - none

  While hovering the 'a' tags, change the style property as below
      background-color- #4169E1
      color - #FFFFFF
      width - 20px
      border - 1px solid #808080
      padding - 15px
      text-align - center
      text-decoration - none

  The Content in the tags should be the same as given in the problem content.

  Note :
  Content of the page should be present as shown in the screenshot.
  Kindly refer the content which is given as a part of description.

  Sample Screenshot 1 :



  Sample Screenshot 2 :



  Sample Screenshot 3 :



  Sample Screenshot 4 :



  Sample Screenshot 5 :



  Sample Screenshot 6 :


```html title="index.html"
<!DOCTYPE html>
<html>
  <head>
    <style>
      ul {
        /* Enter your text here! */
        list-style-type: none;
        background-color: #87ceeb;
        padding: 10px 0;
        overflow: hidden;
      }
      li {
        /* Enter your text here! */
        float: left;
      }
      a {
        /* Enter your text here! */
        background-color: #87ceeb;
        color: #000000;
        width: 20px;
        border: 1px solid #808080;
        padding: 15px;
        text-align: center;
        text-decoration: none;
      }
      a:hover {
        /* Enter your text here! */
        background-color: #4169e1;
        color: #ffffff;
        width: 20px;
        border: 1px solid #808080;
        padding: 15px;
        text-align: center;
        text-decoration: none;
      }
    </style>
  </head>
  <body>
    <ul>
      <li><a href="#" id="home">Home</a></li>
      <li><a href="#" id="news">News</a></li>
      <li><a href="#" id="contact">Contact</a></li>
      <li><a href="#" id="about">About</a></li>
    </ul>
    <h3>Pink Frag Event Organizer</h3>
    <p>
      We are indulged in offering a Promotional Event Management.These services
      are provided by our team of professionals as per the requirement of the
      client. These services are highly praised for their features like
      sophisticated technology, effective results and reliability. We offer
      these services in a definite time frame and at affordable rates.
    </p>
    <p>
      Pink Frag Event is a reputed organization,which has come into being in
      2009, as a Sole Proprietorship Firm, with a sole aim of achieving the
      trust and support of large customers. We have indulged our all endeavors
      towards offering trustworthy Wedding Event Management, Promotional Event
      Management, Birthday Party Management and many more.To offer these
      services, we have hired specialized professionals, who are capable of
      understanding as well as accomplishing the specific customers' desires.
    </p>
  </body>
</html>

```