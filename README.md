# Live Project

### For two weeks towards the end of my Tech Academy Bootcamp, I worked in a Team Sprint developing a project using ASP .NET MVC and Entity Framework and utilizing the Aglie/Scrum Methodology. The project I worked on is an interactive website for managing the content and productions for a theater/acting company. I was expected to complete at least 2 User Stories and attend 10 daily Stand-Up meetings, as well as participate in Code Retrospectives at the end. This provided some real-world experience and practice using clean version control and Azure DevOps.

### Below are descriptions of the stories I worked on, along with code snippets and screen shots.


## First User Story- Create and Style Contact Page
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

<img width="452" alt="UserStoryResult1" src="https://user-images.githubusercontent.com/84823575/136641834-a0df97a4-82ba-4be4-a069-d17de567981d.png">

## Second User Story- History Manager User Part 1: Create User
### *Description: Create a manager ApplicationUser for the Rental area.  This history manager will act as an admin for the RentalHistory area and is responsible for keeping track of the history of returned rentals. Add these properties to the HistoryManager class: (RestrictedUsers: int) and (RentalReplacementRequests: int)*

Here is what I wrote:

```
    public class HistoryManager : ApplicationUser
    {
        //This RestrictedUsers property represents the number of Users that
        //this manager has blocked from renting from the theatre again
        public int RestrictedUsers { get; set; }

        //The RentalReplacementRequests represent the number of Rentals that
        //need to be replaced due to damage.
        public int RentalReplacementRequests { get; set; }
```
This created columns in the database:

<img width="147" alt="UserStory1ColumnsInSQL" src="https://user-images.githubusercontent.com/84823575/136642118-b5924d26-077a-43b7-b4e9-0a7f1d31fc0b.png">

## 3rd User Story - History Manager User Part 2: Seed HistoryManager
### *Description: To test out the new HistoryManager class, create a seed method for HistoryManager.  Seeding the database entails creating an instance of HistoryManager and saving it to the database before the page is loaded so that we have access to the HistoryManager for testing purposes.*

Here is what I wrote for the HistoryManager.cs file:

```
        //Seeding the database
        //creating a method:
        public static void SeedHistoryManager()
        {
            //creating an instance of HistoryManager, saves to DB before page loads
            ApplicationDbContext dbContext = new ApplicationDbContext();

            if (dbContext.HistoryManagers.Count()==0)
            {
                //create a new object of type HistoryManager
                HistoryManager historyManager = new HistoryManager
                {
                    //assign values to properties inherited from ApplicationUser/Identity
                    UserName = "Admin",
                    Email = "Admin@example.com",
                    RestrictedUsers = 1,
                    RentalReplacementRequests = 1,
                };
                dbContext.HistoryManagers.Add(historyManager);
                dbContext.SaveChanges();
```

Here is what I wrote for the Startup.cs file:

```            //call the seed method
            HistoryManager.SeedHistoryManager();
            RolesManager.CreateNewRole();
        }
           
    }
    public class RolesManager
    {
        public static void CreateNewRole()
        {
            //connection to the dB
            ApplicationDbContext dbContext = new ApplicationDbContext();

            //instantiate objects - user manager and role manager
            var roleManager = new RoleManager<IdentityRole>(new RoleStore<IdentityRole>(dbContext));
            var userManager = new UserManager<ApplicationUser>(new UserStore<ApplicationUser>(dbContext));

            //check if the role "HistoryManager" alrady exists. If not, create role
            if (!roleManager.RoleExists("HistoryManager"))
            {
                //create HistoryManager Role:
                var role = new IdentityRole()
                {
                    Name = "HistoryManager"
                };
                roleManager.Create(role);

                //find admin user by email:
                var user = userManager.FindByEmail("Admin@example.com");

                //create IdentityUser Role w/the IDs of role and user:
                var userRole = new IdentityUserRole
                {
                    RoleId = role.Id,
                    UserId = user.Id
                };

                //adding the IdentityUserRole to the user
                user.Roles.Add(userRole);

```

                

