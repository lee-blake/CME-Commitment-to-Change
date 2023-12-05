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

**All preceding addresses will begin with `http://localhost:8000/` for this specific environment setup**


&nbsp;
&nbsp;
&nbsp;

---
# General Instructions and Tips
---
## Info icons
- Look for the info icons throughout the applike the one shown below:
  
![Info Icon](<../Auxiliary Files/Images/User_Images/info-icon.png>)

- You can click on these info icons if you need help or tips for how to use the application effectively. Once clicked, a dialogue box like the one below will show with added information.

![Info Popup](<../Auxiliary Files/Images/User_Images/info-popup.png>)

---
&nbsp;
&nbsp;
&nbsp;
# Provider Instructions
---
## Account Registration:
---
### Registering for a Provider Account
- This page is used to create new provider user profiles.
- Address for this page: `/app/register/provider/`

1. Navigate to the provider registration webpage. This can be done from the 
login page by clicking "Click here to register" and then "Provider account".

![Account Type](<../Auxiliary Files/Images/User_Images/register_account_type.PNG>)

2. Fill out the fields for username, email, password, password verification, and for Institution Name.

![Register Account](<../Auxiliary Files/Images/User_Images/register_provider.png>)

- Please note that you can reveal the password as you type it by clicking on the eye icon in the password field.

![Register Show Password](<../Auxiliary Files/Images/User_Images/show_password.png>)


3. Select 'Submit'.
   - **If you are redirected back to this page, either an invalid email was used, 
    the password was not strong enough, or the passwords did not match. Error 
    text in the page should inform you of the specifics.**
4. If your provider account was successful in its creation, you will see this page.

![Success](<../Auxiliary Files/Images/User_Images/successful_registration.PNG>)

### Logging In as a Provider
- This page is used for logging into an already registered clinician  or provider profile.
- Address for this page: `/accounts/login/`
1. Fill out the fields with the username and password that you used when creating a profile.

![sign_in](<../Auxiliary Files/Images/User_Images/sign_in.PNG>)

- Please note that you can reveal the password as you type it by clicking on the eye icon in the password field.

![Login Show Password](<../Auxiliary Files/Images/User_Images/sign_in_show_password.png>)

2. Press the 'log in' button located underneath these fields.
3. If you were successfully logged in, you will be redirected to the commitment
dashboard (for clinician accounts) or course dashboard (for provider accounts).

4. If you were not successful, you will be directed to enter a correct username and password.


### Logging Out as a Provider
- This button is used to log out the currently logged-in user.
- Must be logged in.
- Address for this page: `/accounts/logout/`
1. While logged-in to the application, find the navigation bar at the top of the screen.
2. There should be a *Logged in as 'USERNAME'* title followed by a *Log Out* button. Press this button.

![log_out-button.PNG](<../Auxiliary Files/Images/User_Images/log_out_button.PNG>)

3. After pressing *Logout*, you will be brought to the logout confirmation page.

![logout_success.PNG](<../Auxiliary Files/Images/User_Images/logout_success.png>)

4. If this was a mistake, you can log back in using the *Log In* button.

---
## Dashboard:
---
### Navigating to the Provider Dashboard
- These instructions detail how to get back to the Course Dashboard that most 
provider instructions will reference.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. When logging in as a provider, you will generally be automatically redirected
to the dashboard.
2. If you are on another page, you can click "Dashboard" in the navigation bar 
at the top of the current page.

![Provider Dashboard](<../Auxiliary Files/Images/User_Images/provider_dashboard.png>)

3. If you prefer, you can instead manually type the url `/app/dashboard` after the address discussed in [Opening the Application](#opening-the-application).

---
## Courses:
---
### Creating a Course as a Provider
- This page is used to create a course that you can then invite clinicians to join.
- Must be logged-in.
- Address for this page: `/app/course/create/`
1. Click "Create Course" in the navigation bar at the top.

![Provider Dashboard](<../Auxiliary Files/Images/User_Images/provider_create_course.png>)

3. Fill out the title and description of the course. Optionally, you can add a course identifier, a start date, and an end date.

   ![Provider Create Course](<../Auxiliary Files/Images/User_Images/create_course.png>)

4. When you click submit, you will be taken to the course's view page.

![Provider Course View](<../Auxiliary Files/Images/User_Images/provider-course-view.png>)

### Viewing a Created Course as a Provider
- This page shows the details for a course.
- Must be logged-in.
- Address for this page: `/app/course/<Course id>/view/`
1. Navigate to the Course Dashboard.
2. Locate the link with the name of the course you want to view.
3. Click the link.

![Provider view course](<../Auxiliary Files/Images/User_Images/Provider_view_course.png>)

### Inviting Clinicians to Your Course as a Provider
- This covers inviting clinicians to a course by sharing a link.
- Must be logged-in.
- Address for this page: `/app/course/<Course id>/view/`
1. Navigate to the View Course page for the course.
2. Locate the section with "Share this link to invite students"
   
![Share course link](<../Auxiliary Files/Images/User_Images/provider-share-course-link.png>)

3. Click on the "Copy to Clipboard" button, or manually copy the link.
4. Distribute the link to the clinicians you want to invite to the course.
5. When they go to the link, they will be prompted to log in and automatically
join the course.

# Clinician Instructions
---
## Account Creation:
---

### Registering for a Clinician Account
- This page is used to create new clinician user profiles.
- Address for this page: `/app/register/clinician/`
1. Navigate to the clinician registration webpage. This can be done from the 
login page by clicking "Click here to register" and then "Clinician account".

![Account Type](<../Auxiliary Files/Images/User_Images/register_account_type.PNG>)

2. Fill out the required fields for username, email, password, and password verification. Optionally, you can put in your first and last name, as well as the institution you attend.

![Register Account](<../Auxiliary Files/Images/User_Images/register_clinician.png>)

- Please note that you can reveal the password as you type it by clicking on the eye icon in the password field.
  
![Register Show Password](<../Auxiliary Files/Images/User_Images/show_password.png>)


3. Select 'Submit'.
   - **If you are redirected back to this page, either an invalid email was used, 
    the password was not strong enough, or the passwords did not match. Error 
    text in the page should inform you of the specifics.**
4. If your clinician account was successful in its creation, you will see this page.

![Success](<../Auxiliary Files/Images/User_Images/successful_registration.PNG>)



### Logging In as a Clinician
- This page is used for logging into an already registered clinician  or provider profile.
- Address for this page: `/accounts/login/`
1. Fill out the fields with the username and password that you used when creating a profile.
   
![sign_in](<../Auxiliary Files/Images/User_Images/sign_in.PNG>)

- Please note that you can reveal the password as you type it by clicking on the eye icon in the password field.

![Login Show Password](<../Auxiliary Files/Images/User_Images/sign_in_show_password.png>)

2. Press the 'log in' button located underneath these fields.
3. If you were successfully logged in, you will be redirected to the commitment
dashboard (for clinician accounts) or course dashboard (for provider accounts).

4. If you were not successful, you will be directed to enter a correct username and password.


### Logging Out as a Clinician
- This button is used to log out the currently logged-in user.
- Must be logged in.
- Address for this page: `/accounts/logout/`
1. While logged-in to the application, find the navigation bar at the top of the screen.
2. There should be a *Logged in as 'USERNAME'* title followed by a *Log Out* button. Press this button.
![log_out-button.PNG](<../Auxiliary Files/Images/User_Images/log_out_button.PNG>)

3. After pressing *Logout*, you will be brought to the logout confirmation page.
   
![logout_success.PNG](<../Auxiliary Files/Images/User_Images/logout_success.png>)

4. If this was a mistake, you can log back in using the *Log In* button.


## Dashboard:
---

### Navigating to the Clinician Dashboard 
- This button is used to navigate to the logged-in user's commitment dashboard.
- Must be logged-in
- Address for this page: `/app/dashboard/` or `/app/dashboard/clinician/`
1. Locate the navigation bar at the top of the screen
2. There should be a *Dashboard* text that can be clicked. Click this text.

![Nav Bar Dashboard](<../Auxiliary Files/Images/User_Images/clinician_nav_bar_dashboard.PNG>)

3. Alternatively, you can press the *CME Commitment to Change* text.
4. This opens the dashboard.

![Clinician Dashboard](<../Auxiliary Files/Images/User_Images/finalDashboard.png>)


### Creating A Commitment as a Clinician
- This button is used to create a new commitment.
- Must be logged in.
- Address for this page: `/app/commitment/make/`
1. While logged-in to the application, find the navigation bar at the top of the screen.
2. There should be a *Create a Commitment* text that can be clicked. Click this text.
   
![Nav Bar Create](<../Auxiliary Files/Images/User_Images/clinician_nav_bar_create_commitment.PNG>)

3. This opens the commitment creation page. Fill out the title, description, and deadline fields
   and press the *Submit* button underneath the deadline field.
   
![Commitment Create](<../Auxiliary Files/Images/User_Images/commitment_creation.PNG>)

### Completing A Commitment (Clinician Profile)
- This button is used to mark a commitment complete.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *In-Progress* or *Past Due* boxes on the dashboard.
3. Below the title of the commitment, click on the box that says *Complete*.
   
![Complete Button](<../Auxiliary Files/Images/User_Images/commitment_complete_circled.PNG>)

4. This opens the commitment creation page. Fill out the title, description, and deadline fields
   and press the *Submit* button underneath the deadline field.

![Complete Confirm Button](<../Auxiliary Files/Images/User_Images/commitment-complete-confirm.png>)\

5. The commitment should move from whichever box it was in, into the *Completed* box, 
   and it will be marked as complete.
   
![Completed Commitments](<../Auxiliary Files/Images/User_Images/commitment_complete.PNG>)


### Deleting A Commitment (Clinician Profile)
- This button is used to delete a commitment.
- Must be logged-in.
Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *In-Progress*, *Expired*, *Discontinued*, or *Complete* boxes on the dashboard.
3. Open the edit view for the commitment by clicking on it.
4. Below the commitment details, there should be a button titled *Delete*. Click that button.

![Edit Button](<../Auxiliary Files/Images/User_Images/commitment_delete_circled.PNG>)

5. This brings up a modal asking you to confirm. Click the *DELETE* button to confirm deletion.
   
![Delete Confirm](<../Auxiliary Files/Images/User_Images/commitment_delete.PNG>)


### Discontinuing a Commitment (Clinician Profile)
- This button is used to mark a commitment as discontinued indefinitely but not
completed.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *In-Progress* or *Past-Due* boxes.
3. Below the title of the commitment, click on the box that says *Discontinue*.

![Discontinue Button](<../Auxiliary Files/Images/User_Images/commitment_discontinue_circled.PNG>)

4. This brings up a modal asking you to confirm. Click the *Discontinue* button to confirm discontinuation.

![Discontinue Confirm Button](<../Auxiliary Files/Images/User_Images/commitment-discontinue-confirm.png>)

5. The commitment should move from whichever box it was in, into the *Discontinued* box,
   and it will be marked as discontinued.
   
![Discontinued](<../Auxiliary Files/Images/User_Images/commitment_discontinued.PNG>)

6. If this action was a mistake, the commitment can be reopened from here.


### Reopening Discontinued Commitments (Clinician Profile)
- This button is used to reactivate a discontinued commitment.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Navigate to the dashboard.
2. Locate a commitment in the *Discontinued* box.
3. At the bottom of the commitment, click on the box that says *Reopen*.

![reopen discontinued](<../Auxiliary Files/Images/User_Images/discontinued_Reopen.png>)

4. This brings up a modal asking you to confirm. Click the *Reopen* button to confirm.

![reopen Confirm Button](<../Auxiliary Files/Images/User_Images/confirm-reopen.png>)

5. The commitment should move from whichever box it was in, into the *In-Progress* box,
   and it will be marked as in-progress.

## Commitment Page:
---

### Navigate to a Commitment Page from the Dashboard as a Clinician
- Must be logged in to navigate from your dashboard.
- Address for this page: `/app/commitment/<Commitment ID Number>/view/`
1. Locate the navigation bar and go to the commitment dashboard.
2. Locate a commitment in the *In-Progress*, *Past Due*, or *Discontinued* boxes.
   
![View Commitment](<../Auxiliary Files/Images/User_Images/view_commitment_text.PNG>)

3. Click on the text of the commitment.

![Commitment View](<../Auxiliary Files/Images/User_Images/commitment_view.PNG>)

4. This opens the commitment view page.

### Editing A Commitment as a Clinician
- This option is used to edit an existing commitment.
- Must be logged-in.
- Address for this page: `/app/dashboard/`
1. Locate a commitment in the *In-Progress*, *Expired*, or *Discontinued* boxes 
on the dashboard.
2. Click on the commitment that you want to edit and open its view page.
3. Below the commitment details, there should be a box labeled *Edit*. Click this box.

![Edit Button](<../Auxiliary Files/Images/User_Images/commitment_edit_circled.PNG>)

4. This brings you to the commitment edit page. Make your edits in these fields.

![Edit View](<../Auxiliary Files/Images/User_Images/commitment_edit_page.PNG>)

5. Below the commitment edit details, press the submit button to save your changes.

### Sharing a Commitment Page
- Note: Currently, since there is no domain name registered, the link will need
to change `localhost:8000` to `<your ip address>:8000` to be viewable from 
another machine.
- Address for this page: `/app/commitment/<Commitment ID Number>/view/`
1. View one of your owned commitments with the instructions above
2. Copy and paste the URL in the browser.
   
![View Link](<../Auxiliary Files/Images/User_Images/commitment_view_link.PNG>)

3. Share with others. They will be able to see the details of the commitment but
not alter it.

---
## Courses:
---
### Joining a Course (Clinician Profile)
- This procedure is used to join a course created by a provider.
- Must be logged in.
- **If running the development server or Apache without SSL, change `https` to `http` in the links.**
1. Obtain an invitation link from a provider.
  - It should look something like the link in [Inviting Clinicians to a Course via a link (Provider Profile)](#inviting-clinicians-to-a-course-via-a-link-provider-profile).
3. Click the link or paste it into your browser.
4. If prompted, log in.
5. You will automatically be enrolled in the course and be taken to that course's page.

### Viewing a Course (Clinician Profile)
- This page displays the details of a course you are enrolled in.
- Must be logged in.
- Must be a member of the course.
- Address for this page: `/app/course/<Course id>/view/`
1. Navigate to the Commitment Dashboard.
2. Locate the "My Courses" section.
   
![my course view](<../Auxiliary Files/Images/User_Images/my_courses.png>)

3. Clink the link with the name of the course you want to view. This will take you to the course page.

![Course View Clinician](<../Auxiliary Files/Images/User_Images/CourseView_Clinican.png>)

### Associating a Commitment with a Course (Clinician Profile)
- Commitments may be optionally associated with a course.
- Must be logged in.
- Must be a member of the course.
- Addresses for this page: `/app/commitment/make/` and 
`/app/commitment/<commitment id>/edit/`
1. Association may be done while making or editing a commitment. Navigate to 
the respective page depending on whether your commitment already exists.
2. In the form, locate the "Associate Course" dropdown menu.
3. In that dropdown menu, select the name of the desired course to associate with.
4. Complete the make/edit process for a commitment as usual.

![Associate commitment](<../Auxiliary Files/Images/User_Images/Associate_commitment_with_course.png>)

### Disassociating a Commitment with a Course (Clinician profile)
- If a commitment is associated in error, this can be reversed.
- Must be logged in.
- Must be a member of the course to reassociate.
- Address for this page: `/app/commitment/<commitment id>/edit/`
1. Edit the commitment.
2. In the "Associated Course" dropdown menu, select "-----" to remove any course
association or the correct course if an incorrect course was selected.

![Selecting "-----"](<../Auxiliary Files/Images/User_Images/commitment_disassociate_course.PNG>)

3. Complete the edit process as usual.
