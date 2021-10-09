# Live Project

### For two weeks towards the end of my Tech Academy Bootcamp, I worked in a Team Sprint developing a project using ASP .NET MVC and Entity Framework and utilizing the Aglie/Scrum Methodology. The project I worked on is an interactive website for managing the content and productions for a theater/acting company. I was expected to complete at least 2 User Stories and attend 10 daily Stand-Up meetings, as well as participate in Code Retrospectives at the end. This provided some real-world experience and practice using clean version control and Azure DevOps.

### Below are descriptions of the stories I worked on, along with code snippets and screen shots.


## User Story 1 - Create and Style Contact Page
### *Description: Create a new View in the Home View folder called Contact.cshtml.  Create a form that takes the User's first and last name, Email address, subject, and message.  The form doesn't need to be operational.  To the right of the form have an option for users to Donate and Volunteer.*

Here is the code I wrote:

 ```@*---Header Text---*@
  <h2 class="cms-contact--contactText">CONTACT US</h2>
  <h3 class="cms-contact--headerText"> GET IN TOUCH</h3>
  <hr class="cms-contact--textUnderline" />

  @*---Contact Form---*@
  <div class="row">
    <div class="col-7">
      <form class="cms-contact--formContainer">
        <div class="cms-contact--nameContainer">
          <label for="FirstAndLastName" required>First and Last Name *</label>
          <input type="text" class="form-control input-lg">
        </div>
        <div class="cms-contact--emailContainer">
          <label for="Email" required>Email Address *</label>
          <input type="email" class="form-control input-lg">
        </div>
        <div class="cms-contact--subjectContainer">
          <label for="Subject" required>Subject *</label>
          <input type="text" class="form-control input-lg">
        </div>
        <div class="cms-contact--messageContainer">
          <label for="message" required>Message *</label>
          <textarea class="form-control input-lg" rows="8"></textarea>
        </div>
        <div>
          <button type="submit" class="cms-contact--SubmitButton">Submit</button>
        </div>
      </form>
    </div>
   @*---Donate and Volunteer section---*@
    <div class="col-4">
      <div class="cms-contact--donateContainer">
        <h3> DONATE</h3>
        <p class="cms-contact--donateText">
          We've got a Patreon account!
          Help support live theatre in Portland, OR. by becoming a Patron today!
        </p>
        <button type="submit" class="cms-contact--DonateButton">Donate</button>
        <div class="cms-contact--volunteerContainer">
          <h3>VOLUNTEER</h3>
          <p class="cms-contact--volunteerText">Contact us to learn more about volunteering in the theatre.</p>
          <button type="submit" class="cms-contact--VolunteerButton">Volunteer</button>
        </div>
      </div>
    </div>
  </div>
  ```
  
Here is the finished result:


