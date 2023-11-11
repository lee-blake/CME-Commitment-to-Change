# Feature Navigation as a User
*** 
### Requirements and Assumptions
1. **__The development environment must be setup and running before attempting to use the application__**
    - See [Development.md](Development.md) for steps on how to do this.
2. The server is running - either with `python manage.py runserver` as detailed 
[here](Development.md#testing-the-environment-and-app) or with a full deployment as detailed [here](Deployment.md)
3. URLs point to the local machine on port 8000 - otherwise replace 
`localhost:8000` with the appropriate address.

***

## Opening the Application
- The CME Commitment to Change App is accessed through a local internet browser.
1. Open a web browser (Microsoft Edge, Firefox, Chrome...)
2. In the address bar, type in `http://localhost:8000/`
3. Currently, this welcome page will redirect to the login page.

**All preceding addresses will begin with `http://localhost:8000` for this specific environment setup**

  
## Registering a Clinician Profile
- This page is used to create new clinician user profiles.
- Address for this page: `/app/register/clinician/`
1. Navigate to the clinician registration webpage. This can be done from the 
login page by clicking "Click here to register" and then "Clinician account".
2. Fill out the fields for username, email, password, and password verification.
3. Select 'Submit'.
   - **If you are redirected back to this page, either an invalid email was used, 
    the password was not strong enough, or the passwords did not match. Error 
    text in the page should inform you of the specifics.**
3. If your clinician account was successful in its creation, it will redirect you to the
   login page.

## Registering a Provider Profile
- This page is used to create new provider user profiles.
- Address for this page: `/app/register/provider/`
1. Navigate to the provider registration webpage. This can be done from the 
login page by clicking "Click here to register" and then "Provider account".
2. Fill out the fields for username, email, password, and password verification.
3. Select 'Submit'.
   - **If you are redirected back to this page, either an invalid email was used, 
    the password was not strong enough, or the passwords did not match. Error 
    text in the page should inform you of the specifics.**
3. If your provider account was successful in its creation, it will redirect you to the
   login page.


## Logging In (Clinician & Provider Profiles)
- This page is used for logging into an already registered clinician  or provider profile.
- Address for this page: `/accounts/login/`
1. Fill out the fields with the username and password that you used when creating a profile.
![sign_in](<../Auxiliary Files/Images/User_Images/sign_in.PNG>)
2. Press the 'log in' button located underneath these fields.
3. If you were successfully logged in, you will be redirected to the commitment
dashboard (for clinician accounts) or course dashboard (for provider accounts).
4. If you were not successful, you will directed to enter a correct user name and password.


## Logging Out (Clinician & Provider Profiles)
- This button is used to log out the currently logged-in user.
- Must be logged in.
- Address for this page: `/accounts/logout/`
1. While logged-in to the application, find the navigation bar at the top of the screen.
2. There should be a *Logged in as 'USERNAME'* title followed by a *Log Out* button. Press this button.
![log_out-button.PNG](<../Auxiliary Files/Images/User_Images/log_out_button.PNG>)
3. After pressing *Logout*, you will be brought to the logout confirmation page.
4. If this was a mistake, you can log back in using the *Log In* button.


## Navigating to the Commitment Dashboard (Clinician Profile)
- This button is used to navigate to the logged-in user's commitment dashboard.
- Must be logged-in
- Address for this page: `/app/dashboard/` or `/app/dashboard/clinician/`
1. Locate the navigation bar at the top of the screen
2. There should be a *Dashboard* text that can be clicked. Click this text.
3. This opens the dashboard.


## Creating A Commitment (Clinician Profile)
- This button is used to create a new commitment.
- Must be logged in.
- Address for this page: `/app/commitment/make/`
1. While logged-in to the application, find the navigation bar at the top of the screen.
2. There should be a *Create a Commitment* text that can be clicked. Click this text.
3. This opens the commitment creation page. Fill out the title, description, and deadline fields
   and press the *Submit* button underneath the deadline field.


## Viewing a Commitment from the Dashboard (Clinician Profile)
- Must be logged in to navigate from your dashboard.
- Address for this page: `/app/commitment/<Commitment ID Number>/view/`
1. Locate the navigation bar and go to the commitment dashboard.
2. Locate a commitment in the *In-Progress*, *Expired*, *Past Due*, or *Discontinued* boxes.
3. Click on the text of the commitment.

## Sharing a Commitment page for viewing (Clinician Profile)
- Note: Currently, since there is no domain name registered, the link will need
to change `localhost:8000` to `<your ip address>:8000` to be viewable from 
another machine.
- Address for this page: `/app/commitment/<Commitment ID Number>/view/`
1. View one of your owned commitments with the instructions above
2. Copy and paste the URL in the browser
3. Share with others. They will be able to see the details of the commitment but
not alter it.

## Editing A Commitment (Clinician Profile)
- This option is used to edit an existing commitment.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Locate a commitment in the *In-Progress*, *Expired*, or *Discontinued* boxes 
on the dashboard.
2. Click on the commitment that you want to edit and open its view page.
3. Below the commitment details, there should be a box labeled *Edit*. Click this box.
4. This brings you to the commitment edit page. Make your edits in these fields.
5. Below the commitment edit details, press the submit button to save your changes.


## Completing A Commitment (Clinician Profile)
- This button is used to mark a commitment complete.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *In-Progress* or *Past Due* boxes on the dashboard.
3. To the right of the title of the commitment, click on the box that says *Complete*.
4. The commitment should move from whichever box it was in, into the *Completed* box, 
   and it will be marked as complete.


## Deleting A Commitment (Clinician Profile)
- This button is used to delete a commitment.
- Must be logged-in.
Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *In-Progress*, *Expired*, *Discontinued*, or *Complete* boxes on the dashboard.
3. Open the edit view for the commitment by clicking on it.
4. Below the commitment details, there should be a button titled *Delete*. Click that button.
5. This will bring you to a page that asks if you are sure you want to delete. You will press
   the delete button located under this text titled *Delete*.


## Discontinuing a Commitment (Clinician Profile)
- This button is used to mark a commitment as discontinued indefinitely but not
completed.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *In-Progress* or *Past-Due* boxes.
3. To the right of the title of the commitment, click on the box that says *Discontinue*.
4. The commitment should move from whichever box it was in, into the *Discontinued* box
   and it will be marked as discontinued.


## Reopening Discontinued Commitments (Clinician Profile)
- This button is used to reactive a discontinued commitment.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *Discontinued* box.
3. To the right of the title of the commitment, click on the box that says *Reopen*.
4. The commitment should move from whichever box it was in, into the *In-Progress* box,
   and it will be marked as discontinued.

## Joining a Course (Clinician Profile)
- This procedure is used to join a course created by a provider.
- Must be logged in.
1. Obtain an invite link from a provider.
2. Click the link or paste it into your browser.
3. If prompted, log in.
4. You will automatically be enrolled in the course and be taken to that 
course's page.

## Viewing a Course (Clinician Profile)
- This page displays the details of a course you are enrolled in.
- Must be logged in.
- Must be a member of the course.
- Address for this page: `/app/course/<Course id>/view/`
1. Navigate to the Commitment Dashboard.
2. Locate the "My Courses" section.
3. Clink the link with the name of the course you want to view.

## Associating a Commitment with a Course (Clinician Profile)
- Commitments may be optionally associated with a course.
- Must be logged in.
- Must be a member of the course.
- Addresses for this page: `/app/commitment/make/` and 
`/app/commitment/<commitment id>/edit/`
1. Association may be done while making or editing a commitment. Navigate to 
the respective page depending on whether or not your commitment already exists.
2. In the form, locate the "Associate Course" dropdown menu.
3. In that dropdown menu, select the name of the desired course to associate with.
4. Complete the make/edit process for a commitment as usual.

## Disassociating a Commitment with a Course (Clinician profile)
- If a commitment is associated in error, this can be reversed.
- Must be logged in.
- Must be a member of the course to reassociate.
- Address for this page: `/app/commitment/<commitment id>/edit/`
1. Edit the commitment.
2. In the "Associated Course" dropdown menu, select "-----" to remove any course
association or the correct course if an incorrect course was selected.
3. Complete the edit process as usual.

 


## Navigating to the Course Dashboard (Provider Profile)
- These instructions detail how to get back to the Course Dashboard that most 
porovider instructions will reference.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. When logging in as a provider, you will generally be automatically redirected
to the dashboard.
2. If you are on another page, you can click "Dashboard" in the navigation bar 
at the top of the current page.
3. If you prefer, you can instead manually type the url `/app/dashboard` after the address discussed in [Opening the Application](#opening-the-application).


## Creating a Course (Provider Profile)
- This page is used to create a course that you can then invite clinicians to join.
- Must be logged-in.
- Address for this page: `/app/course/create/`
1. Click "Create Course" in the navigation bar at the top.
2. Fill out the title and description of the course.
3. When you click submit, you will be taken to the course's view page.

## Viewing a Course (Provider Profile)
- This page shows the details for a course.
- Must be logged-in.
- Address for this page: `/app/course/<Course id>/view/`
1. Navigate to the Course Dashboard.
2. Locate the link with the name of the course you want to view.
3. Click the link.

## Inviting Clinicians to a Course via a link (Provider Profile)
- This covers inviting clinciians to a course by sharing a link.
- Must be logged-in.
- Address for this page: `/app/course/<Course id>/view/`
1. Navigate to the View Course page for the course.
2. Locate the section with "Share this link to invite students"
3. Copy that link in its entirety.
4. Distribute the link to the clinicians you want to invite to the course.
5. When they go to the link, they will be prompted to log in and automatically
join the course.
