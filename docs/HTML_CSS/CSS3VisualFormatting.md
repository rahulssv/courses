# CSS3 Visual Formatting
## iDesign
    Contact Me - Responsive

    Julie is a topper in her college, She is a nerd who just talks about the stuffs in the book, but she does not have a good knowledge on the technical side. She can clear all the interviews as she is brilliant in aptitude and conveying things to people, but she has a concern in getting her resume created. She wants to get through the interview process by creating a resume that stands out among the other candidates who competes with her in the interview. She decides to create a resume, so she comes across our website.

    Our resume-writing walks her through the entire process, from header to footer and section by section. We’ll make sure Julie will convince the employer that Julie is the perfect candidate.Lets help her out in creating the webpage with layouts that she is waiting for.

    She has created the contact me page , but the page is not responsive.Help her in designing the responsive Contact me page

    Constraints

    Responsive style should be present inside the style tag inside the index.html file
    To make page responsive
    @media should have  max-width-1024px for monitor
    CSS property value  should be  width-100%;

      @media should have  max-width-991px for tablet
    CSS property value  should be  width-85%;      

    @media should have  max-width-768px for mobile phones
    CSS property value  should be  width-70%;       
    In the mobile view ,it should display only the icons  in the li tags inside the nav tag id navbar(Refer screenshot 2)
    Use   display- none property
    In the index.html page 
    Add meta tag  with name -viewport,content-width=device-width,initial-scale=1,shrink-to-fit=no
    Note: 

    Refer the sample screenshot to create the web page.

    Adhere to the specifications given in the screenshot 3 ,4. 

    Sample Screenshot 1:


    Sample Screenshot 2:


    Sample Screenshot 3:


    Sample Screenshot 4:

```html title="index.html"
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <!--Fill Code here-->
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <style>
        @media (max-width: 1024px) {
        body .main .detail-holder .form-group {
        width: 100%;
      }
      nav ul li a{
        width: 100%;
      }
    }
  
    /* Styles for tablet */
    @media (max-width: 991px) {
        body .main .detail-holder .form-group {
        width: 85%;
      }
      nav ul li a{
        width: 85%;
      }
    }
    @media (max-width: 768px) {
        body .main .detail-holder .form-group{
        width: 70%;
      }
  
      /* Hide text and only show icons */
      nav ul li a {
        display: none;
      }
  
    }
      .container li a {
        background-color: white;
        display: block;
        color: #000000;
        font-size: .75em;
        text-align: center;
        padding: 1em;
        text-decoration: none;
      }
      .container li a:hover {
        background-color: green;

        color: white;
        font-size: 0.75em;
        padding: auto;
        text-align: center;
        text-decoration: none;
      }
      .container{
        display: flex;
        list-style-type: none;
        margin: 0;
  padding: 0;
  width: 100%;
  justify-content: space-between;
      }
     
      .container li{
        width: calc(100%/4);
      }
      .icon {
        font-size: 0.7em;
      }
      nav ul li a img {
        width: 1em;
        height: 1em;
        margin-right: 1em;
      }
      body {
        background-color: #ececec;
      }
      .main {
        background-color: white;

        display: flex;
        width: 50%;
        margin-left: 20em;
        margin-right: 20em;
      }
      .detail-holder {
        margin-left: 2em;
        margin-right: 2em;
        padding-top: 2em;
        padding-bottom: 2em;
      }
      .form-group {
        display:inline-block;
        
        padding: 1em 1em 1em 1em;
      }
      .form-group #message{
        width: 100%;
        height: auto;
      }
      #submit {
        text-align: center;
        text-decoration: none;
      }
      #navbar{
        width: 100%;
        background-color: white;
      }
    </style>
  </head>

  <body>
    <header>
      <!--Fill code here-->
      <nav id="navbar">
        <ul class="container">
          <li>
            <a href="#"><img src="usericon.png" alt="" />ABOUT ME</a>
          </li>
          <li>
            <a href="#"><img src="icon-2.png" alt="" />RESUME</a>
          </li>
          <li>
            <a href="#"><img src="icon-3.png" alt="" />PORTFOLIO</a>
          </li>
          <li>
            <a href="#"><img src="icon-4.png" alt="" />CONTACT ME</a>
          </li>
        </ul>
      </nav>
    </header>
    <br />
    <br />

    <div class="main">
      <div class="detail-holder">
        <h3>CONTACT ME</h3>
        <hr />
        <div>
          <div class="form-group">
            <label for="firstname">First Name</label><br />
            <input type="text" id="firstname" />
          </div>
          <div class="form-group">
            <label for="lastname">Last Name</label><br />
            <input type="text" id="lastname" />
          </div>
          <div class="form-group">
            <label for="dob">Date Of Birth</label><br />
            <input type="date" name="dob" id="dob" />
          </div>
          <div class="form-group">
            <label for="email">Email</label><br />
            <input type="email" name="email" id="email" />
          </div>
          <div class="form-group">
            <label for="mobile">Mobile</label><br />
            <input type="number" name="mobile" id="mobile" maxlength="10" />
          </div>
          <div class="form-group">
            <label for="reason">Reason</label><br />
            <select name="reason" id="reason">
              <option value="business">Business</option>
              <option value="home">Home</option>
            </select>
          </div>
          <div class="form-group">
            <label for="gender">Gender</label><br />
            <input type="radio" name="gender" id="male" value="male" />Male
            <input
              type="radio"
              name="gender"
              id="female"
              value="female"
            />Female
          </div>
          <div class="form-group">
            <label for="pmoc">Preferred Mode Of Communication</label><br />
            <input
              type="checkbox"
              name="pmoc"
              id="mobile"
              value="mobile"
            />Mobile
            <input type="checkbox" name="pmoc" id="email" value="email" />Email
          </div>
          <div class="form-group">
            <label for="message">Message</label><br />
            <textarea name="message" id="message" ></textarea>
          </div>
          <div>
            <center>
              <button type="submit" id="submit">Submit</button>
            </center>
          </div>
        </div>
      </div>
    </div>
  </body>
</html>

```
## iAssess
    HTML - Transition Property
    "Pink Frag Event Organizer" are conducting an online contest for choosing the Best website of the year. The topic for the contest is to develop an innovative webpage for a Wedding Event. Shiyas has registered for the contest and started developing a web page with the contents related to the Wedding Event. He planned to create something new and started surfing about transition property in CSS, as it is capable of producing a transition effect in the image on hovering.

    Being a beginner in designing the websites, he needs your help to finish the web page for the contest by using the transition property in CSS.
    Hints :  overflow property  The CSS overflow property controls what happens to content that is too big to fit into an area. hidden - The overflow is clipped, and the rest of the content will be invisible Syntax :    overflow: visible|hidden|scroll|auto|initial|inherit;   Transition property CSS transitions allows you to change property values smoothly (from one value to another), over a given duration. The transition-timing-function property specifies the speed curve of the transition effect. ease - specifies a transition effect with a slow start, then fast, then end slowly (this is default) Syntax :    transition-property: none|all|property|initial|inherit;  width property The width property sets the width of an element. Syntax :    width: auto|value|initial|inherit;
    Refer the below gif for designing the web page. 
    http://app.e-box.co.in/uploads/TransitionProperty.gif

    Content :
    h2 - Wedding Event
    img tag with src="image.jpg" class="image"
    A wedding is a ceremony where two people or a couple are united in marriage. Wedding traditions and customs vary greatly between cultures, ethnic groups, religions, countries, and social classes. Most wedding ceremonies involve an exchange of marriage vows by the couple, presentation of a gift (offering, ring(s), symbolic item, flowers, money), and a public proclamation of marriage by an authority figure or celebrant. Special wedding garments are often worn, and the ceremony is sometimes followed by a wedding reception. Music, poetry, prayers or readings from religious texts or literature are also commonly incorporated into the ceremony.

    Constraints :
    The html page must contain the text Wedding Event inside `<h2>` tag.
    Div element with id "container" must be present and must have the below CSS properties
    position - relative
    Img tag with src "image.jpg" attribute must be present.
    Div element with id "overlay" must be present and must have the below CSS properties
    overflow - hidden
    transition:1s ease
    width:0px
    position - absolute

    height - 100%
    Text must be used which is given in the content.

    Div element with id "text" must be present and must have the below CSS properties
    text-align - justify
    transform - translate(-270px, -100px)
    position - absolute
    Text must be used which is given in the content.

    Note :
    The web page should be displayed as shown in the screenshot.
    Kindly refer the content which is given as a part of description
    Kindly don't change the template only make the changes in index.html file.

    Sample Screenshot 1:



    Sample Screenshot 2:

```html title="index.html"
<!DOCTYPE html>
<html>
  <head>
    <title>Wedding Event</title>
    <style>
		h2{
			text-align: center;
		}
      #container {
        position: relative;
      }
      
      .image {
        width: 50%;
        height: auto;
      }
      
      #overlay {
        overflow: hidden;
        width: 0;
        position: absolute;
        height: 100%;
		transition: 1s ease;
      }
      
      #overlay:hover {
        width: 50%;
		
		
      }
      
      #text {
        text-align: justify;
        transform: translate(-270px, -100px);
        position: absolute;
      }
	  #overlay:hover #text {
        width: 50%;
		
		
      }
    </style>
  </head>
  <body>
    <h2>Wedding Event</h2>
    <div id="container">
      <img src="image.jpg" class="image">
      <div id="overlay">
        <div id="text">
          A wedding is a ceremony where two people or a couple are united in marriage. Wedding traditions and customs vary greatly between cultures, ethnic groups, religions, countries, and social classes. Most wedding ceremonies involve an exchange of marriage vows by the couple, presentation of a gift (offering, ring(s), symbolic item, flowers, money), and a public proclamation of marriage by an authority figure or celebrant. Special wedding garments are often worn, and the ceremony is sometimes followed by a wedding reception. Music, poetry, prayers or readings from religious texts or literature are also commonly incorporated into the ceremony.
        </div>
      </div>
    </div>
  </body>
</html>

```