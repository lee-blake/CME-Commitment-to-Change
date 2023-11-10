# Feature Navigation as a User
***
### **__The development environment must be setup and running before attempting to use the application__**
See [Development.md](Development.md) for steps on how to do this.
***

## Opening the Application
- The CME Commitment to Change App is accessed through a local internet browser.
1. Open a web browser (Microsoft Edge, Firefox, Chrome...)
2. In the address bar, type in `http://localhost:8000/app/register/clinician/`
3. This will take you to the first page which is the clinician user register page.
   ![localhost](<../Auxiliary Files/Images/User_Images/localhost.PNG>)

**All preceding addresses will begin with `http://localhost:8000` for this specific environment setup**

  
## Registering a Clinician Profile
- This page is used to create new clinician user profiles.
- Address for this page: `/app/register/clinician/`
1. Fill out the fields for username, email, password, and password verification.
2. Select 'Submit'.
   - **If you are redirected to this page, either an invalid email was used, the password
   was not strong enough, or the passwords did not match.**
3. If your clinician account was successful in its creation, it will redirect you to the
   login page.


## Logging In (Clinician Profile)
- This page is used for logging into an already registered clinician profile.
- Address for this page: `/accounts/login/`
1. Fill out the fields with the username and password that you used when creating a profile.
![sign_in](<../Auxiliary Files/Images/User_Images/sign_in.PNG>)
2. Press the 'log in' button located underneath these fields.
3. If you were successfully logged in, you will be redirected to the commitment dashboard.
4. If you were not successful, you will directed to enter a correct user name and password.


## Logging Out (Clinician Profile)
- This button is used to log out the currently logged-in user.
- Must be logged in.
- Address for this page: `/accounts/logout/`
1. While logged-in to the application, find the navigation bar at the top of the screen.
2. There should be a *Logged in as 'USERNAME'* title followed by a *Log Out* button. Press this button.
![log_out-button.PNG](<../Auxiliary Files/Images/User_Images/log_out_button.PNG>)
3. After pressing *Logout*, you will be brought to the logout confirmation page.
4. If this was a mistake, you can log back in using the *Log In* button.


## Navigating to the Commitment Dashboard
- This button is used to navigate to the logged-in user's commitment dashboard.
- Must be logged-in
- Address for this page: `/app/dashboard/
1. Locate the navigation bar at the top of the screen
2. There should be a *Dashboard* text that can be clicked. Click this text.
3. This opens the dashboard.


## Creating A Commitment
- This button is used to create a new commitment.
- Must be logged in.
- Address for this page: `/app/commitment/make/`
1. While logged-in to the application, find the navigation bar at the top of the screen.
2. There should be a *Create a Commitment* text that can be clicked. Click this text.
3. This opens the commitment creation page. Fill out the title, description, and deadline fields
   and press the *Submit* button underneath the deadline field.


## Viewing a Commitment
- This button is used to create a new commitment.
- Must be logged in.
- Address for this page: `/app/commitment/"Commitment ID Number"/view/`
1. Locate the navigation bar and go to the commitment dashboard.
2. Locate a commitment in the *In-Progress*, *Expired*, *Past Due*, or *Discontinued* boxes.
3. Click on the text of the commitment.


## Editing A Commitment
- This option is used to edit an existing commitment.
- Must be logged-in.
- Address for this page: `/app/commitment/"Commitment ID Number"/edit/?`
1. Locate a commitment in the *In-Progress*, *Expired*, or *Discontinued* boxes.
2. Click on the commitment that you want to edit and open its view page.
3. Below the commitment details, there should be a box labeled *Edit*. Click this box.
4. This brings you to the commitment edit page. Make your edits in these fields.
5. Below the commitment edit details, press the submit button to save your changes.


## Completing A Commitment
- This button is used to mark a commitment complete.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *In-Progress*, *Past Due*, or *Discontinued* boxes.
3. To the right of the title of the commitment, click on the box that says *Complete*.
4. The commitment should move from whichever box it was in, into the *Completed* box, 
   and it will be marked as complete.


## Deleting A Commitment
- This button is used to mark a commitment complete.
- Must be logged-in.
Address for this page: `/app/commitment/"Commitment ID Number"/delete/?`
1. Navigate to the dashboard.
2. Locate a commitment in the *In-Progress*, *Expired*, *Discontinued*, or *Complete* boxes.
3. Open the edit view for the commitment by clicking on it.
4. Below the commitment details, there should be a button titled *Delete*. Click that button.
5. This will bring you to a page that asks if you are sure you want to delete. You will press
   the delete button located under this text titled *Delete*.


## Discontinuing a Commitment
- This button is used to mark a commitment complete.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *In-Progress* or *Past-Due* boxes.
3. To the right of the title of the commitment, click on the box that says *Discontinue*.
4. The commitment should move from whichever box it was in, into the *Discontinued* box
   and it will be marked as discontinued.


## Reopening Discontinued Commitments
- This button is used to mark a commitment complete.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *Discontinued* box.
3. To the right of the title of the commitment, click on the box that says *Reopen*.
4. The commitment should move from whichever box it was in, into the *In-Progress* box,
   and it will be marked as discontinued.




